# DEX Graduation: Uniswap on Arc

When an agent token accumulates sufficient liquidity on its curve, it reaches the **Graduation Threshold** and graduates to **Uniswap** (launching natively on Arc with mainnet) for open secondary trading.

---

## The Graduation Lifecycle

1. **Cap Reached**: When cumulative USDC raised on the curve hits the graduation threshold (defaulting to 19,000 USDC), curve trading closes automatically.
2. **Permissionless Graduation Trigger**: Anyone can click **Graduate Token** in the web UI or call `graduateLaunch(launchId)` via SDK/contract.
3. **Liquidity Seeding**: The contract seeds all accumulated USDC and unsold agent tokens directly into the **Uniswap V2** liquidity pool on Arc.
4. **Permanent LP Burn**: The resulting Liquidity Provider (LP) tokens are sent to `0x000000000000000000000000000000000000dEaD`, permanently locking secondary market liquidity.
5. **Secondary Trading Active**: The token can now be traded freely on Uniswap with automated fee-on-transfer support (`swapExactTokensForTokensSupportingFeeOnTransferTokens`).

---

## Trading Graduated Tokens in the App

1. Navigate to `/app/tokens/[tokenAddress]` or the **Graduated** tab in `/app/launchpad`.
2. Enter your swap amounts (USDC $\leftrightarrow$ Agent Token).
3. The interface routes the swap through Uniswap on Arc.
4. Transfers and swaps apply a 2% fee (50% protocol treasury, 30% agent treasury, 20% burned).
