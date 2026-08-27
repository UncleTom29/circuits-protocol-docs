# Why Arc?

Circuits Protocol is built natively on **Arc**, Circle's stablecoin-native Layer 1 blockchain.

Autonomous AI agents require an execution environment that is fast, deterministic, and free of multi-token currency friction. Arc provides the first blockchain architecture designed specifically for stablecoin-first autonomous commerce.

---

## 1. USDC as the Native Gas Token

The primary advantage of Arc is that **USDC is the native gas token**.

On traditional networks like Ethereum, Base, or Solana, an autonomous agent must hold two distinct assets:
1. **The settlement asset** (typically a stablecoin like USDC) to receive payments and pay for services.
2. **The native gas asset** (ETH, SOL) to pay the validator network for every state write.

This dual-asset requirement introduces severe operational friction for autonomous agents:
* An agent with $10,000 in USDC can be rendered completely unresponsive if its gas wallet drops to $0.00 in ETH.
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

## 3. Native Circle CCTP V2 Integration

Arc is integrated directly into Circle's cross-chain architecture:
* **Slippage-Free Transfers**: Circle's Cross-Chain Transfer Protocol (CCTP) burns USDC on source chains (such as Base or Ethereum) and mints native USDC directly on Arc.
* **No Wrapped Asset Risk**: Assets bridged via CCTP are canonical native USDC, eliminating the bridge exploit risks associated with third-party liquidity pool wrappers.
* **Circle Iris Tracking**: Real-time cross-chain attestation tracking provides instant verification of incoming bridge transactions.

---

## Arc Testnet Configuration

| Parameter | Value |
|---|---|
| **Network Name** | Arc Testnet |
| **Chain ID** | `5042002` |
| **Native Gas Token** | USDC |
| **RPC Endpoint** | `https://arc-testnet.drpc.org` |
| **Block Explorer** | `https://testnet.arcscan.app` |
| **USDC Contract Address** | `0x3600000000000000000000000000000000000000` |
| **CCTP TokenMessenger** | `0x8FE6B999Dc680CcFDD5Bf7EB0974218be2542DAA` |
| **CCTP MessageTransmitter** | `0xE737e5cEBEEBa77EFE34D4aa090756590b1CE275` |
| **CCTP Domain** | `26` |
