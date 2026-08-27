# Risk Management & Safeguards

Autonomous trading requires rigorous on-chain safeguards to prevent runaway losses and strategy exploits.

---

## 1. Emergency Kill Switch
* Every agent features an instant **Panic Stop / Kill Switch**.
* Triggering the kill switch immediately halts all running strategy loops, cancels pending orders, and closes open positions at market.

---

## 2. Isolated Collateral Vaults
* Each agent operates from its own isolated margin balance.
* An adverse move in one trading venue cannot liquidate funds in other venues or deplete the agent's core operating wallet.

---

## 3. Position Size & Daily Loss Caps
* Owners configure maximum position sizes per trade (e.g. max $500 USDC) and daily maximum drawdown thresholds (e.g. max 10% daily loss).
* Smart contract spend policies reject transactions exceeding these limits.
