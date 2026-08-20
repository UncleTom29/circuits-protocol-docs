# Uniswap DEX

The **Uniswap Protocol** serves as the official graduation venue for all agent tokens launched through Circuits Protocol on Arc.

{% hint style="info" %}
**Mainnet & Testnet Execution**
Uniswap has officially announced support for Arc on mainnet launch. On Arc Testnet, Circuits Protocol runs a battle-tested, gas-optimized **Uniswap V2** deployment (internally referred to as Xero Protocol) under the hood until Uniswap publishes its official contract addresses when Arc launches on mainnet.
{% endhint %}

## Architecture

The integration utilizes standard, battle-tested **Uniswap V2** smart contract architecture:

1. **Factory Contract**: Responsible for deploying new liquidity pools (Pairs) for trading pairs. It tracks the registry of all active pools and enforces the standard 0.3% LP fee.
2. **Router Contract**: The router contract that executes trades, calculates optimal routing paths, and manages adding/removing liquidity safely with slippage protection and deadlines.

## The Graduation Pipeline

When a token on `ClawdHQLaunchpad` meets its USDC funding threshold, the Launchpad automatically calls the Uniswap Router.

The migration process works as follows:
1. The Launchpad takes all raised USDC and all remaining unsold AgentTokens.
2. It calls `addLiquidity` on the Router, creating a new AgentToken/USDC pair (if it doesn't exist) or adding to it.
3. The resulting LP (Liquidity Provider) tokens are minted and instantly sent to the `BURN_ADDRESS` (`0x000000000000000000000000000000000000dEaD`).
4. This permanently locks the baseline liquidity in Uniswap, guaranteeing that the token is backed and tradable on the open market without any risk of a rug-pull by the creator or the protocol admin.

## Interacting with the DEX

Developers and market makers can interact with the DEX exactly as they would with Uniswap V2 on Ethereum. The ABI and function signatures (`swapExactTokensForTokens`, `getAmountsOut`, etc.) are standard Uniswap V2 interfaces, making it seamlessly compatible with existing DeFi tooling, aggregators, and charting platforms.
