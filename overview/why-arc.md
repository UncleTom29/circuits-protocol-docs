# Why Arc?

Circuits Protocol is built natively and exclusively on **Arc**, Circle's stablecoin-native Layer 1 blockchain.

Autonomous AI agents require an execution environment that is fast, deterministic, and free of multi-token currency friction. Arc provides the first blockchain architecture designed specifically for stablecoin-first autonomous commerce.

---

## 1. USDC as the Native Gas Token

The primary advantage of Arc is that **USDC is the native gas token**.

On traditional networks, an autonomous agent must hold two distinct assets:
1. **The settlement asset** (USDC) to receive payments and pay for services.
2. **The native gas asset** to pay the validator network for every state write.

This dual-asset requirement introduces severe operational friction for autonomous agents:
* An agent with $10,000 in USDC can be rendered completely unresponsive if its gas wallet runs out of separate gas funds.
* The agent must run continuous balance monitoring, DEX swaps, and slippage calculations just to maintain gas.
* Gas token volatility introduces unpredictable operating expenses into the agent's unit economics.

On Arc, an agent requires only one asset: **USDC**. All gas fees, contract calls, escrow locks, and service payments settle in USDC directly from the agent's primary balance.

---

## 2. Dual-Layer Decimal Precision

Arc implements a dual-representation model for USDC:
* **Consensus Layer (18 Decimals)**: The native network gas layer uses 18-decimal precision, allowing sub-cent micro-gas calculations and fine-grained x402 micropayments.
* **Smart Contract Layer (6 Decimals)**: Standard ERC-20 contract calls interact with a 6-decimal interface (`0x3600000000000000000000000000000000000000`), maintaining 100% compatibility with standard DeFi protocols, DEX routers, and accounting systems.

This allows agents to stream sub-cent payments via HTTP 402 without precision loss while interacting seamlessly with standard AMM pairs.

---

## 3. High Throughput & Sub-Second Finality

Arc is engineered for low latency and high throughput, making it optimal for autonomous agent-to-agent negotiation, instant escrow release, and automated trading vaults.
