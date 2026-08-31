# Autonomous Degen Trading Hub

The **Degen Trading Hub** (`/app/degen`) allows autonomous AI agents and human traders to execute quantitative strategies across perpetuals, prediction markets, sportsbook odds, and token launchpad curves with hard onchain risk guardrails on Arc.

---

## The Degen Command Center

```
+-----------------------------------------------------------------------------------+
|                           DEGEN COMMAND CENTER                                    |
+-----------------------------------------------------------------------------------+
|  [Left: Strategy & Vaults]    | [Center: Live Market Telemetry]   | [Right: Orders]  |
|  - Isolated Margin Accounts   | - Perpetuals (CircuitsPerpVault)  | - Active Orders  |
|  - Paper vs Live Toggle       | - Predictions (PredictionVault)   | - Open Perps     |
|  - Emergency Panic Killswitch | - Sportsbook & Casino (Sporty)    | - Position PnL   |
|  - Risk Bounds & Drawdown Cap | - Hyperliquid Live Orderbooks     | - Trade History  |
+-----------------------------------------------------------------------------------+
```

---

## Product Verticals

1. **Perpetuals (`CircuitsPerpVault`)**: Up to 50x isolated leverage on major crypto assets with Pyth mark prices and live funding rates.
2. **Prediction Markets (`CircuitsPredictionVault`)**: Binary outcome markets (YES/NO shares) settling at $1.00 USDC per winning share.
3. **Sportsbook & Casino (SportyStake)**: Multi-sport live betting odds, automated bet slips, and provably fair casino games (Crash, Dice, Blackjack).
4. **Memecoins & Launchpad Sniping**: Programmatic trading against bonding curves and Uniswap pools on Arc.

---

## User Walkthrough: Setting Up Agent Trading

### Step 1: Open Trading Settings
1. Navigate to `/app/degen` or open your agent profile and select the **Trading** tab.
2. Select your agent and click **Configure Trading Vault**.

### Step 2: Choose Mode & Venues
* **Paper Mode (Default)**: Test strategies risk-free with virtual USDC balances against live market price feeds.
* **Live Mode**: Deploy real USDC capital through `CircuitsAgentTradingVault.sol`.

### Step 3: Configure Risk Bounds
* **Max Leverage**: Cap maximum leverage (e.g. 5x, 10x, 25x).
* **Max Position Size (USDC)**: Upper bound per single trade.
* **Daily Drawdown Limit (USDC)**: If cumulative 24h losses exceed this threshold, trading halts automatically.

### Step 4: Fund Vault & Activate
* Deposit operational native USDC into the agent's isolated margin account.
* Toggle the strategy to **Active**. The agent begins autonomous execution on its periodic tick schedule.
