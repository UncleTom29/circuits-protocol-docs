# Tokenize Your Agents: Launchpad

The **Circuits Protocol Launchpad** allows you to tokenize your agents on fair-launch curves with automated DEX graduation on Arc.

---

## Fair Launch Principles

Every token launched on Circuits Protocol adheres to strict guarantees:
* **Zero Presales**: No private rounds, no team pre-allocations, and no insider allocations.
* **100% Public Supply**: 1,000,000,000 (1 Billion) tokens start entirely on the public curve.
* **Automated DEX Graduation**: When the graduation cap is reached, liquidity automatically migrates to Xero AMM with permanently locked LP tokens.
* **Scheduled Fee Buybacks**: Accumulated trading fees execute automated buybacks and burns.

---

## Token Specifications

| Parameter | Specification |
|---|---|
| **Total Supply** | 1,000,000,000 (1 Billion) tokens fixed |
| **Settlement Currency** | Native USDC on Arc (`0x3600000000000000000000000000000000000000`) |
| **Pricing Invariant** | Constant-Product Curve ($x \cdot y = k$) |
| **Fee Model** | 2% trading fee with automated buyback pool allocation |
| **Graduation Target** | Automated migration upon reaching reserve threshold |

---

## Launchpad Lifecycle

1. **[Creating a Launch](./creating-a-launch.md)**: Tokenize your agents with custom tickers, scheduled launch timestamps, and buyback frequencies.
2. **[Trading on Curve](./trading-on-curve.md)**: Instant liquidity with deterministic pricing.
3. **[Curve Mechanics](./bonding-curve.md)**: Virtual reserves and anti-snipe protection.
4. **[DEX Graduation](./graduation.md)**: Automated Xero AMM pool creation with locked LP liquidity.
5. **[Automated Buybacks](./buybacks.md)**: Permissionless buyback executions from fee pools.
