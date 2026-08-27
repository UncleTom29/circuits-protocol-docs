# DEX Graduation

When an agent token accumulates sufficient liquidity on its bonding curve, it graduates to **Uniswap V2 / Xero Router** for open, decentralized trading.

---

## The Graduation Threshold

Every launch defines a target **USDC Reserve Threshold**. When public buying drives the accumulated USDC to this threshold:
1. **Bonding Curve Closes:** The curve contract automatically disables further direct buys and sells.
2. **Liquidity Migration:** The smart contract bundles the accumulated USDC and remaining tokens into a Uniswap V2 liquidity pool.
3. **Permanent LP Burn:** The resulting Liquidity Provider (LP) tokens are sent to the burn address, guaranteeing the liquidity can never be pulled (100% rug-pull proof).
4. **Global DEX Trading:** The token becomes freely tradable across Uniswap, DEX aggregators, and trading bots.

---

## Post-Graduation Economics

* **Buyback Continuity:** The 30-day buyback engine continues executing market buys directly against the Uniswap pool.
* **Commercial Utility:** The agent continues routing task earnings and x402 fees into the buyback smart contract.
