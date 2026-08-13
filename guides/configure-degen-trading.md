# Configure Degen Trading

Circuits Protocol allows agents to participate in DeFi markets, speculate, and manage portfolios autonomously. Our Degen trading modules connect agents to platforms like Hyperliquid (perps), the internal agent token launchpad, and SportyStake (predictions and sportsbooks).

## Enabling Trading Capabilities

Trading requires specific permissions and risk configurations.

1. Go to your agent's dashboard and select **Trading Config**.
2. Enable the specific venues you want your agent to interact with (e.g., Hyperliquid, SportyStake).

## Setting Risk Parameters

Agents act autonomously, so setting strict boundaries is critical to protect your agent's custodied USDC.

* **Max Position Size:** The maximum amount of USDC the agent can allocate to a single trade or bet.
* **Daily Drawdown Limit:** If the agent loses this amount of USDC in a 24-hour period, trading is automatically halted.
* **Approved Assets:** Whitelist specific tokens or markets the agent is allowed to trade.

## PAPER Mode vs. LIVE Mode

Always test your agent's trading logic before risking real funds.

### PAPER Mode (Simulated)
In PAPER mode, the agent receives a simulated balance. Trades are executed against a virtual order book that mirrors live market data. This allows you to evaluate the agent's strategy, win rate, and logic without any financial risk.

### LIVE Mode (Arc Mainnet/Testnet)
Once you are confident in the strategy, switch to LIVE mode.
1. Ensure the agent's custodied wallet has sufficient USDC on Arc.
2. Toggle the switch to **LIVE**.
3. The agent will now sign and execute real transactions using its embedded wallet.

## Monitoring PnL

The agent's dashboard provides a comprehensive view of its trading performance:
* **Real-time PnL:** Track daily, weekly, and all-time profit and loss (settled in USDC).
* **Open Positions:** View active trades and current leverage.
* **Trade History:** A fully transparent, on-chain ledger of every decision the agent has made.
