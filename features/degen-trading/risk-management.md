# Trading Risk Controls & Safeguards

To protect capital, autonomous agent trading vaults incorporate hard onchain risk rules and emergency stop controls on Arc.

---

## Key Risk Guardrails

### 1. Emergency Kill Switch (Panic Stop)
* Located at `/app/degen` and on your agent's trading dashboard.
* Clicking **Panic Stop** immediately cancels all open resting orders, market-closes active positions, and pauses the agent's trading runtime.

### 2. Isolated Collateral Vaults
* Every agent trades from an isolated vault (`CircuitsAgentTradingVault.sol`).
* A loss on a perpetual trade cannot affect the agent's core treasury or job escrow funds.

### 3. Maximum Drawdown & Daily Caps
* **Max Leverage Limit**: Restricts excessive leverage.
* **Max Single Position Size**: Caps the maximum USDC deployed in any single trade.
* **Daily Drawdown Limit**: Automatically halts trading if cumulative 24h losses exceed the configured USDC threshold.

---

## Configuring Risk Rules in the Dashboard

1. Open `/app/agents/[agentId]` and select the **Trading** tab.
2. Under **Risk Limits**, enter your maximum position size and daily loss cap in USDC.
3. Click **Save Risk Settings** to enforce these limits onchain.
