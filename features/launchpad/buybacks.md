# Automated Token Buybacks

Circuits Protocol includes a permissionless buyback-and-burn mechanism that uses accumulated trade fees to repurchase agent tokens and permanently burn them on Arc.

---

## How the Buyback Engine Works

```mermaid
graph TD
    A[Launchpad Trade Fees] --> B[Creator Treasury Pool]
    B -->|Configured buybackBps| C[buybackPoolUsdc in Contract]
    C -->|Interval Elapsed: Daily / Weekly / Monthly| D[executeBuyback(launchId)]
    D --> E[Market Buy Tokens from Curve / Uniswap]
    E --> F[Permanent Burn: 0xdead]
```

1. **Fee Accumulation**:
   * A percentage of every trade fee accumulates directly in the contract's treasury reserves.
2. **Configurable Basis Points (`buybackBps`)**:
   * Creators configure what percentage of accumulated treasury balances are deployed per buyback (from 100 bps = 1% to 10,000 bps = 100%, default **2,000 bps = 20%**).
3. **Scheduled Cadence (`BuybackInterval`)**:
   * Configured at launch: **Daily**, **Weekly**, or **Monthly**.
   * Creators can modify interval and basis points anytime via `updateBuybackConfig`.
4. **Permissionless Execution**:
   * Once `block.timestamp >= nextBuybackAt`, anyone can click **Execute Buyback** in the UI or call `executeBuyback(launchId)`.
   * The protocol indexer also runs an automated scheduler to trigger due buybacks.
5. **Permanent Token Burn**:
   * The contract market-buys tokens and sends them directly to `0x000000000000000000000000000000000000dEaD`.

---

## Checking & Triggering Buybacks in the UI

1. Open `/app/launchpad/[launchId]`.
2. View the **Buyback Module**:
   * **Pool Balance**: Current USDC waiting in the buyback pool.
   * **Buyback Rate**: Active percentage configured (`buybackBps`).
   * **Next Buyback Countdown**: Time remaining until the execution window opens.
   * **Total Burned**: Cumulative tokens burned to date.
3. When the countdown reaches zero, the **Execute Buyback** button activates for anyone to trigger.
