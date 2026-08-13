# CCTP V2 Bridging

Circuits Protocol leverages Circle's **Cross-Chain Transfer Protocol (CCTP) V2** to enable seamless USDC liquidity flow into the **Arc blockchain** from other major networks like Ethereum and Base.

## Overview

Since Arc uses USDC as its native gas and settlement token, bootstrapping liquidity on the network is critical. CCTP provides a native, zero-slippage method to move USDC between chains without relying on wrapped tokens or third-party liquidity pools.

Circuits Protocol heavily relies on CCTP to allow users to fund their accounts and agents directly from their existing wallets on supported EVM chains.

## CCTP V2 Workflow

The bridging process involves a burn-and-mint mechanism coordinated between the source chain (e.g., Base Sepolia) and the destination chain (Arc Testnet).

### 1. Initiating the Transfer (Source Chain)

The user initiates a cross-chain transfer by interacting with the `TokenMessengerV2` contract on the source chain.

```solidity
// Called on the source chain
TokenMessengerV2.depositForBurn(
    amount,
    destinationDomain,
    mintRecipient,
    burnToken
)
```

- `amount`: The amount of USDC to bridge.
- `destinationDomain`: The unique Domain ID for Arc (e.g., `8` for Arc Testnet).
- `mintRecipient`: The address on Arc that will receive the USDC (formatted as `bytes32`).
- `burnToken`: The address of the native USDC contract on the source chain.

### 2. Attestation Generation (Circle Iris)

Once the transaction is confirmed on the source chain, Circle's **Iris attestation service** observes the event. After the required block confirmations are met, Iris generates a cryptographic attestation (signature) verifying that the USDC was successfully burned.

{% hint style="info" %}
In testnet environments, the attestation generation may take a few minutes depending on the source chain's finality requirements.
{% endhint %}

### 3. Minting on Arc (Destination Chain)

The attestation and the original message bytes must be submitted to the `MessageTransmitterV2` contract on Arc.

```solidity
// Called on the destination chain (Arc)
MessageTransmitterV2.receiveMessage(
    message,
    attestation
)
```

### Automated Relayer

To provide a frictionless user experience, Circuits Protocol includes an automated **CCTP Relayer** built into the indexer.

The relayer automatically monitors the Iris API for generated attestations related to protocol users. Once an attestation is available, the relayer submits the `receiveMessage` transaction on Arc on behalf of the user, fully automating the bridging process so the user simply sees their USDC balance update on Arc.

## Supported Domain IDs

| Chain | Network | Domain ID |
| :--- | :--- | :--- |
| **Ethereum** | Sepolia | `0` |
| **Base** | Sepolia | `6` |
| **Arc** | Testnet | `8` |

*(Note: Domain IDs are subject to change based on Circle's official registry).*
