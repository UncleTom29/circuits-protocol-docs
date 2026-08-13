# ClawdHQCrossChainIdentity

`ClawdHQCrossChainIdentity` enables agent owners to link their identities across different blockchain networks (Base Sepolia, Ethereum Sepolia, and Arc Testnet). It uses Circle's **CCTP V2** (Cross-Chain Transfer Protocol) message-passing primitive to attest that an agent on Chain A and an agent on Chain B are owned by the same conceptual entity.

## Trust Model & Architecture

This module does not wrap the higher-level `TokenMessengerV2` (which handles USDC value transfer). Instead, it interacts directly with `MessageTransmitterV2.sendMessage` and acts as an `IMessageHandlerV2` to pass arbitrary bytes across chains.

* **Global ID**: A unique identifier created by hashing the origin chain's CCTP domain, the local agent ID, and the owner's address: `keccak256(originDomain, originAgentId, owner)`.
* **Security**: Because the `owner` address is a pre-image of the hash, a user can only link agents on another chain if they use the *exact same wallet address* there.
* **Attestation**: The contract only accepts inbound messages if they are verified by Circle's attestation service *and* originated from an admin-configured sibling `ClawdHQCrossChainIdentity` contract on a trusted peer chain.

## Linking Flow

### 1. Origination (`registerLink`)
An agent owner calls `registerLink` on the origin chain (e.g., Base Sepolia).
* The contract generates the `globalId` and saves the owner locally.
* It broadcasts a CCTP message containing `(globalId, localDomain, localAgentId, owner)` to all configured peer chains (e.g., Ethereum Sepolia, Arc).

### 2. Attestation Relay (Off-Chain)
An off-chain relayer (part of the Circuits Protocol indexer) waits for the transaction to finalize, fetches the attestation signature from Circle's API, and submits the `handleReceiveFinalizedMessage` transaction to the sibling contracts on the destination chains.

### 3. Claiming (`claimLocalAgent`)
Once the message lands on the destination chain (e.g., Arc), the `globalId` is officially recognized as belonging to `owner`.
The owner can then call `claimLocalAgent` on Arc, passing the `globalId` and their Arc-native `localAgentId`. The contract verifies that `msg.sender` owns both the local agent and the `globalId`, securely linking the two identities.
