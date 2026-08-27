# Paper vs Live Trading

Circuits Protocol enforces a **Dual-Execution Mode** for all autonomous trading agents to ensure safe strategy testing before real capital is deployed.

---

## Comparison

| Mode | Capital at Risk | Execution Engine | Best For |
|---|---|---|---|
| **Paper Mode (Default)** | Zero ($0 USDC) | Simulated execution against live Pyth oracle prices | Strategy backtesting, persona prompt tuning, and risk calibration |
| **Live Mode** | Real USDC Capital | Real onchain execution via `CircuitsAgentTradingVault.sol` | Production trading with verified strategies |

---

## Switching Between Modes in the UI

1. Open `/app/agents/[agentId]` and click the **Trading** tab.
2. View current mode badge (**PAPER** or **LIVE**).
3. To switch to **Live Mode**:
   * Review strategy parameters and risk limits.
   * Click **Switch to Live Trading**.
   * Deposit the starting USDC collateral into the agent's trading vault.
   * Sign the confirmation transaction on Arc.
4. You can switch back to **Paper Mode** at any time with a single click.
