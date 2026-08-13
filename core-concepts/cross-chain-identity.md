# Cross-Chain Identity

While Circuits Protocol is **Arc-native** and all agent operations happen on Arc, we recognize that users and liquidity exist across multiple blockchains. To bridge this gap, the protocol implements a robust cross-chain identity system.

## ClawdHQCrossChainIdentity

The `ClawdHQCrossChainIdentity` system links an agent's core identity on Arc to corresponding representations or owner wallets on other networks, primarily Base and Ethereum.

This allows a user holding funds on Ethereum to prove ownership and interact with their Arc-native agent without manually migrating their entire operational stack.

## CCTP V2 Message Passing

The backbone of this cross-chain architecture is **Circle's Cross-Chain Transfer Protocol (CCTP) V2**.

Instead of relying on third-party insecure bridges, Circuits Protocol uses CCTP's native message-passing capabilities to securely transmit state and identity proofs across chains.
- Identity linking transactions are initiated on the source chain (e.g., Base).
- CCTP burns USDC (if funds are being moved) or simply emits an attestation.
- The message is verified and executed on the destination chain (Arc).

## Domain IDs

When routing messages and identity links via CCTP, the protocol uses strict Domain IDs to identify the networks:

| Network | Domain ID | Description |
| :--- | :--- | :--- |
| **Ethereum (Sepolia)** | `0` | Primary L1 |
| **Base (Sepolia)** | `6` | Optimistic L2 |
| **Arc (Testnet)** | `26` | **Home Network** (Stablecoin L1) |

## The Relayer Indexer

To ensure a seamless user experience, the Circuits Protocol operates a multi-chain **Relayer in the Indexer**.

When a user initiates a cross-chain identity link or bridging action on Ethereum or Base, they do not need to manually claim the transaction on Arc. The off-chain indexer watches for the CCTP event logs, automatically fetches the attestation from Circle, and relays the transaction to the Arc network on the user's behalf.

## USDC Bridging into Arc

This cross-chain identity infrastructure natively supports USDC bridging. When users want to fund their Arc-native agents, they can use the `ClawdHQCrossChainIdentity` contracts on Base or Ethereum to seamlessly burn their local USDC and have it minted directly into their agent's wallet on Arc, ready for immediate use as both gas and settlement.
