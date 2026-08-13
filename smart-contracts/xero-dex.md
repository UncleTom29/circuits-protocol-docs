# Xero DEX

The **Xero Protocol** is a decentralized exchange (DEX) deployed natively on Circle's Arc L1. It serves as the official graduation venue for all agent tokens launched through Circuits Protocol.

## Architecture

Xero is a direct, gas-optimized fork of the battle-tested **Uniswap V2** architecture. It consists of two primary smart contracts:

1. **XeroFactory**: Responsible for deploying new liquidity pools (Pairs) for trading pairs. It tracks the registry of all active pools and enforces the standard 0.3% LP fee.
2. **XeroRouter**: The router contract that executes trades, calculates optimal routing paths, and manages adding/removing liquidity safely with slippage protection and deadlines.

## The Graduation Pipeline

When a token on `ClawdHQLaunchpad` meets its USDC funding threshold, the Launchpad automatically calls the `XeroRouter`.

The migration process works as follows:
1. The Launchpad takes all raised USDC and all remaining unsold AgentTokens.
2. It calls `addLiquidity` on the `XeroRouter`, creating a new AgentToken/USDC pair (if it doesn't exist) or adding to it.
3. The resulting LP (Liquidity Provider) tokens are minted and instantly sent to the `BURN_ADDRESS` (`0x000000000000000000000000000000000000dEaD`).
4. This permanently locks the baseline liquidity in the Xero DEX, guaranteeing that the token is backed and tradable on the open market without any risk of a rug-pull by the creator or the protocol admin.

## Interacting with Xero

Developers and market makers can interact with the Xero DEX exactly as they would with Uniswap V2 on Ethereum. The ABI and function signatures (`swapExactTokensForTokens`, `getAmountsOut`, etc.) are identical, making it seamlessly compatible with existing DeFi tooling, aggregators, and charting platforms.
