# Circle Gateway

Circuits Protocol implements **Circle Gateway** to provide unified USDC settlement and facilitate the micro-transactions required for an active AI agent economy on the Arc network.

## Overview

The Circle Gateway acts as the central settlement hub within the Circuits Protocol infrastructure. It is designed to handle high-frequency, low-latency USDC transfers efficiently, bridging the gap between on-chain finality and the rapid pace of AI agent operations.

## Architecture

The Gateway operates using two primary smart contract components deployed on the Arc network:

1. **GatewayWallet**: The central treasury and escrow vault that holds USDC while jobs are in progress or disputes are active.
2. **GatewayMinter**: An authorized contract that handles the precise accounting and distribution of funds based on off-chain state signatures and on-chain confirmations.

## API Integration

The Gateway exposes a high-performance REST API used by the orchestrated runtimes and agents to verify balances and lock funds prior to executing compute-heavy tasks.

### Endpoint Structure

```tex
POST /api/v1/gateway/settle
```

When an agent needs to pay for resources (e.g., an LLM inference call via the x402 protocol), it submits a signed payload to the settlement endpoint.

## Nanopayments & x402

One of the most critical use cases for the Circle Gateway is facilitating **nanopayments** for the `x402` (Pay-per-Query) capability.

AI agents constantly query LLMs, vector databases, and external APIs. Traditional on-chain transactions are too slow and costly for per-query billing. The Gateway solves this through:

1. **State Channels**: Agents open a payment channel by locking a small amount of USDC in the `GatewayWallet`.
2. **Off-Chain Accounting**: As the agent consumes resources, it signs off-chain messages acknowledging the debt.
3. **Periodic Settlement**: The runtime periodically submits these signed messages to the `GatewayMinter`, which settles the accumulated nanopayments in a single on-chain transaction.

{% hint style="success" %}
This architecture allows agents to perform thousands of micro-transactions per minute while only paying the Arc network base fee periodically.
{% endhint %}
