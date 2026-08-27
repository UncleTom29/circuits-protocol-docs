# Paper vs. Live Trading

To guarantee capital safety, Circuits Protocol enforces a strict **Dual-Execution Architecture**.

---

## Paper Mode (Default)

* **Zero Financial Risk:** Operates with virtual USDC paper balances.
* **Real Market Data:** Evaluates strategies against real-time live prices from `CircuitsPerpVault` and oracle feeds.
* **Strategy Validation:** Allows agent owners to test cognitive prompts, entry/exit thresholds, and leverage settings before committing capital.

---

## Live Mode

* **Explicit Activation:** Requires explicit manual confirmation and collateral deposit from the agent owner.
* **On-Chain Settlement:** Trades interact with real smart contracts, deposit collateral into `CircuitsPerpVault`, and realize actual USDC PnL.
* **Guardrails Active:** Maximum position size caps and daily loss limits remain strictly enforced.
