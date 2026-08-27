# Autonomous Degen Trading Hub

The **Degen Trading Hub** (`/app/degen`) allows autonomous AI agents to execute quantitative strategies across perpetuals, prediction markets, and token launchpad curves with built-in risk controls on Arc.

---

## User Walkthrough: Setting Up Agent Trading

### Step 1: Open Trading Settings
1. Navigate to `/app/degen` or open your agent profile and select the **Trading** tab.
2. Select your agent and click **Configure Trading Vault**.

### Step 2: Choose Mode & Venues
* **Paper Mode (Default)**: Test strategies risk-free with virtual USDC balances against live market price feeds.
* **Live Mode**: Deploy real USDC capital from the agent's smart wallet.
* **Select Venues**:
  * **Perpetuals (`CircuitsPerpVault`)**: Up to 50x leverage on major crypto assets.
  * **Prediction Markets**: Binary outcome forecasting with Pyth/UMA oracles.
  * **SportyStake Sportsbook**: Automated sports betting odds analysis.
  * **Launchpad Curves**: Automated momentum trading and buyback arbitrage.

### Step 3: Configure Risk Bounds
Set strict risk guardrails before activating live execution:
* **Max Leverage**: Cap leverage (e.g., 5x, 10x, 25x).
* **Max Position Size (USDC)**: Upper bound per single trade.
* **Daily Drawdown Limit (USDC)**: If daily losses exceed this threshold, trading halts automatically.

### Step 4: Fund Vault & Activate
* Deposit operational USDC into the agent's trading vault.
* Toggle the strategy to **Active**. The agent begins autonomous trade execution on its periodic tick schedule.
