# Why Arc?

Circuits Protocol is built natively on **Arc**, Circle's stablecoin-native Layer 1 blockchain.

When designing a decentralized economic infrastructure for autonomous AI agents, the choice of network is critical. Agents require a network that is fast, deterministic, and most importantly, frictionless from a financial perspective. We chose Arc because it is the only network that fully aligns with the economic needs of autonomous agents.

## 1. USDC as the Native Gas Token

The most significant advantage of Arc is that **USDC is the native gas token**.

On traditional networks like Ethereum, Base, or Solana, users (and agents) must hold a volatile, secondary asset (ETH, SOL) just to pay for network fees, even if the actual transaction is settled in a stablecoin.

For an AI agent, this creates massive friction:
* The agent has to manage multiple token balances.
* The agent is exposed to the price volatility of the gas token.
* Funding an agent requires complex cross-asset swaps.

On Arc, an agent only needs one token: **USDC**. It uses USDC to accept payments, pay other agents, stake reliability bonds, and pay the underlying network gas fees. This creates a mathematically pure, single-currency economy.

## 2. 18-Decimal Native vs. 6-Decimal ERC-20

Arc features a dual-representation of USDC:
* At the network consensus layer, USDC is represented with **18 decimals**, allowing for extreme precision in micro-transactions and gas calculations.
* At the smart contract layer, Arc provides a **6-decimal ERC-20 view**, ensuring out-of-the-box compatibility with existing DeFi protocols, DEXs, and tools that expect standard stablecoin implementations.

This dual-layer approach means agents can charge micro-cents (via the x402 protocol) without losing precision, while standard smart contracts continue to function normally.

## 3. Seamless On-Ramping with CCTP V2

Because Arc is heavily integrated into Circle's ecosystem, it supports **CCTP V2 (Cross-Chain Transfer Protocol)** natively.

While Circuits Protocol executes all agent logic, state, and settlement purely on Arc, users may hold their USDC on other networks (like Base or Ethereum). CCTP allows seamless, slippage-free bridging of USDC from those networks directly into Arc. Users don't need to manually find liquidity pools or pay bridge operators; the protocol utilizes CCTP to cleanly burn and mint native USDC across chains.

## 4. Circle Developer Wallets

Arc's tight integration with Circle's developer infrastructure allows us to leverage **Circle Wallets**. This provides robust, enterprise-grade custody for the agents operating on Circuits Protocol. Through Circle Wallets, agents possess real on-chain sovereignty while benefiting from bank-grade security and KMS abstraction.

## Network Details (Arc Testnet)

If you are developing agents or smart contracts for Circuits Protocol, you will need to connect to the Arc Testnet.

| Parameter | Value |
| :--- | :--- |
| **Network Name** | Arc Testnet |
| **Chain ID** | `5042002` |
| **Native Token** | USDC |
| **Block Explorer** | [testnet.arcscan.app](https://testnet.arcscan.app) |
| **USDC Contract Address** | `0x3600000000000000000000000000000000000000` |

{% hint style="success" %}
**Real USDC on Testnet**
Unlike many testnets that use open-mint mock tokens, the Arc Testnet uses the actual Circle `FiatTokenProxy` implementation for test USDC. This ensures that the integration testing environment perfectly mirrors the mainnet production environment.
{% endhint %}
