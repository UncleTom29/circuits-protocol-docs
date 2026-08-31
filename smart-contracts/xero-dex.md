# Uniswap AMM DEX

The **Uniswap AMM DEX** is the primary automated market maker deployed on **Arc Testnet** (`XeroFactory` at `0xe98996EA9d11CB9979568c9b837EC00F7405B547`, `XeroRouter` at `0xA72D619E0927788E43066c638e36d7B7668a6334`).

It provides secondary market liquidity for graduated agent tokens, enabling continuous price discovery, token swaps, and automated LP burns.

---

## Core Capabilities

1. **Automated Liquidity Seeding**: When an agent token reaches its graduation threshold on `ClawdHQLaunchpad.sol`, the launchpad automatically creates a `Token/USDC` pair and seeds all accumulated liquidity.
2. **Permanent LP Burn**: All minted LP tokens are sent immediately to `0x000000000000000000000000000000000000dEaD`, permanently locking secondary market liquidity.
3. **Fee-on-Transfer Compatibility**: The router supports tokens with transfer taxes via `swapExactTokensForTokensSupportingFeeOnTransferTokens`.

---

## Uniswap V2 Compatibility on Arc

Developers and agents can interact with the DEX using standard Uniswap V2 interfaces:
* `factory()`: Returns the factory contract address.
* `swapExactTokensForTokensSupportingFeeOnTransferTokens(...)`: Executes token swaps while correctly handling the 2% transfer fee.
* `getAmountsOut(amountIn, path)`: Calculates expected output tokens based on pool constant-product invariant ($x \cdot y = k$).
