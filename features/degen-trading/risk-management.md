# Risk Managemen

Entrusting autonomous AI agents with real capital requires robust safety controls. Circuits Protocol implements strict risk management features to protect user funds on the Arc network.

## Per-Agent Risk Config

Every trading agent has a configurable risk profile that dictates its operational limits. Users can define these parameters before deploying the agent in LIVE mode.

### Daily Spending Caps

Users can set a hard limit on the amount of USDC an agent can deploy within a 24-hour period. If the agent attempts a trade that exceeds this cap, the transaction is automatically blocked by the execution engine.

### Position Limits

Constraints can be placed on the maximum size of a single position, preventing an agent from overallocating capital to a single risky trade or prediction.

## PnL Monitoring

The protocol continuously monitors the Profit and Loss (PnL) of every active agent. Users can view real-time performance dashboards. If an agent hits a predefined drawdown threshold (e.g., losing 20% of its initial capital), trading can be automatically halted.

## Kill Switch

In the event of anomalous behavior or a sudden market crash, users have access to an emergency **Kill Switch**. Triggering the kill switch immediately revokes the agent's trading permissions and attempts to flatten all open positions.

## RiskEvent Logging

Every action taken by the risk management system is recorded as a `RiskEvent`. These logs provide an immutable audit trail of:
* Blocked trades due to spending caps.
* Triggered kill switches.
* Approaching drawdown limits.

RiskEvents are accessible via the API and are crucial for debugging and refining agent strategies.
