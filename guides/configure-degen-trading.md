# Configure Degen Trading

The **Degen Trading Engine** connects autonomous AI agents directly to perpetual contracts, prediction markets, and token launchpad bonding curves on Arc.

---

## Step-by-Step Configuration

### Step 1: Access the Degen Hub
1. Navigate to `/app/degen` or open `/app/agents/[agentId]` and click the **Trading** tab.
2. Select your agent from the dropdown list.

### Step 2: Select Execution Mode
* **Paper Trading**: Simulated trade execution against live orderbook and oracle feeds. Ideal for prompt tuning and backtesting.
* **Live Trading**: Real onchain trade execution using isolated margin from `CircuitsAgentTradingVault.sol`.

### Step 3: Deposit Isolated Collateral
1. Under **Margin Balance**, enter the native USDC amount to deposit into the trading vault.
2. Click **Deposit Collateral** and confirm the Arc transaction.
3. This collateral is strictly isolated from your agent's core operating treasury.

### Step 4: Configure Strategy Directives & Risk Limits
* **Strategy Directive**: Enter natural-language guidelines (e.g., *Focus on BTC/ETH trend following with tight 2% stop-losses, avoid high-volatility news events*).
* **Max Leverage**: Restrict maximum leverage (e.g. `5x`).
* **Daily Drawdown Limit**: Set maximum 24-hour loss threshold (e.g. `25 USDC`).

### Step 5: Activate Autonomous Execution
* Toggle the strategy switch to **Active**.
* During each proactive tick loop, the agent will analyze market conditions, check risk rules, and execute trades (`OPEN_PERP_POSITION`, `BUY_PREDICTION_SHARES`) via `CircuitsAgentTradingVault.sol`.
