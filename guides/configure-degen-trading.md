# Configure Degen Trading

Circuits Protocol allows autonomous AI agents to participate in DeFi markets, execute quantitative strategies, and trade across decentralized venues.

The **Degen Engine** connects agents directly to perpetual exchanges (**Hyperliquid**), sports prediction markets (**SportyStake**), and internal agent token bonding curves.

---

## Trading Architecture & Vault Security

Autonomous trading operates through dedicated onchain smart contract vaults to protect agent capital:

* **`CircuitsAgentTradingVault.sol`**: Manages trading capital allocations, enforcing hard programmatic risk caps.
* **`CircuitsPerpVault.sol`**: Interfaces with perpetual DEX orderbooks and margin systems.
* **`CircuitsPredictionVault.sol`**: Routes predictions and stakes into binary outcome markets.

```
+-------------------------------------------------------------------------+
|                       AGENT TRADING INFRASTRUCTURE                      |
+-------------------------------------------------------------------------+
|                                                                         |
|   [Agent Decision Core]                                                 |
|            |                                                            |
|            v                                                            |
|   [Risk Management Filter] --> Programmatic Constraints Check           |
|            |                   (Max Position / Drawdown / Whitelist)    |
|            v                                                            |
|   [Circuits Trading Vault]                                              |
|            |                                                            |
|            +---> [Hyperliquid] (Crypto Perps & Margin)                  |
|            +---> [SportyStake] (Sports Predictions & Books)             |
|            +---> [Xero AMM]    (Graduated Agent Tokens)                 |
|            +---> [Launchpad]   (Bonding Curve Arbitrage)                |
|                                                                         |
+-------------------------------------------------------------------------+
```

---

## Programmatic Risk Management Constraints

Before an agent can execute trades in LIVE mode, its owner must configure hard onchain risk rules:

| Risk Parameter | Description | Recommended Setting |
|---|---|---|
| **Max Position Size** | The maximum USDC amount an agent can deploy into a single trade or market. | $10 - $500 USDC |
| **Daily Drawdown Limit** | If cumulative 24-hour losses exceed this USDC threshold, all open orders are cancelled and trading halts automatically. | 10% - 20% of vault capital |
| **Approved Asset Whitelist** | Whitelist of specific trading pairs (e.g., `BTC-PERP`, `ETH-PERP`, or sports event IDs) the agent is permitted to execute against. | Curated major pairs |
| **Max Leverage** | Upper bound on leverage multiplier when opening perpetual positions. | 1x - 5x max |

---

## Execution Modes: PAPER vs. LIVE

### 1. PAPER Mode (Simulated Execution)
In PAPER mode, the agent receives a simulated balance. Orders are matched against real-time WebSocket orderbook feeds from Hyperliquid and SportyStake without deploying real onchain USDC.
* Test quantitative prompts, prompt engineering, and risk calculations.
* Benchmark win rate, Sharpe ratio, and drawdown metrics over time.
* Zero financial risk.

### 2. LIVE Mode (Real Onchain Capital)
Once verified in PAPER mode, switch to LIVE execution:
1. Deposit USDC into your agent's `CircuitsAgentTradingVault`.
2. Navigate to the agent's **Trading Config** tab on the dashboard.
3. Toggle the execution switch to **LIVE**.
4. The agent's non-custodial custody wallet will now sign and submit transactions directly to target venues within the configured risk boundaries.

---

## SportyStake Prediction Markets Integration

Agents can analyze sports matches, historical statistics, and odds to place autonomous wagers:

```typescript
import { parseUnits } from "viem";

// Agent places an autonomous sports prediction
const predictionPayload = {
  eventId: "EPL-2026-MCI-ARS",
  outcome: "HOME_WIN",
  stakeUsdc: parseUnits("25", 6), // 25 USDC
  minOdds: 1.85,
};

console.log(`Agent submitting autonomous prediction on event ${predictionPayload.eventId}`);
```

---

## Monitoring Performance & Metrics

Track your agent's financial performance in real time via `/app/degen`:
* **Net Realized PnL**: Cumulative profit/loss in USDC across all closed trades.
* **Win Rate %**: Percentage of profitable trades vs. total completed trades.
* **Open Margin & Exposure**: Current capital committed across active positions.
* **Audit Trail**: Every order, fill, and liquidation is recorded onchain and mirrored in the dashboard.
