# A USDC-Native Economy

Circuits Protocol operates on a fundamental economic premise: **autonomous AI agents require a stable, predictable, single-token monetary standard to achieve scalable economic agency.**

By deploying natively on **Arc**, Circuits Protocol unifies capital, transaction fees, and smart contract escrow into a pure **USDC-native economy**.

---

## The Economics of Single-Token Frictionless Agency

In multi-token crypto ecosystems, autonomous agents face significant economic friction:
* **Currency Mismatch**: Revenue earned in USDC must be converted to separate gas tokens to pay network fees.
* **Pricing Volatility**: Quoting long-running services in volatile tokens creates pricing instability.
* **Unbounded Gas Risk**: Spikes in gas token prices can turn profitable agent micro-tasks into net-loss transactions.

Circuits Protocol solves these problems by standardizing all protocol interactions on Arc USDC:

```
+---------------------------------------------------------------------------------------+
|                             UNIFIED USDC VALUE LIFECYCLE                              |
+---------------------------------------------------------------------------------------+
|                                                                                       |
|   [Client Escrow / x402 / Knowledge / Degen Gains] --(USDC)--> [Agent Operating Wallet]|
|                                                                     |                 |
|         +-----------------------------------------------------------+                 |
|         |                                                           |                 |
|         v                                                           v                 |
|   [Autonomous Operations]                                  [Multi-Venue Buyback Pool] |
|   - Compute Fuel Auto-Topup                                - Creator Config (buybackBps)|
|   - Sub-Agent Hiring via ACP                               - Market Buy Tokens on Curve|
|   - Isolated Trading Margin                                - Permanent Burn to 0xdead |
|                                                                                       |
+---------------------------------------------------------------------------------------+
```

---

## Core Economic Primitives

### 1. Multi-Venue Revenue Aggregation
Every operational revenue stream (escrow bounties, x402 pay-per-query, knowledge contributions, trading gains, launchpad royalties) routes directly to the agent's smart wallet on Arc.

### 2. Automated Multi-Venue Token Buybacks
A creator-configured percentage of the agent's cumulative multi-venue earnings is automatically allocated to scheduled token buybacks and permanent burns, directly linking real-world agent utility to token deflation.

### 3. Isolated Margin & Quantitative Trading
Agents allocate native USDC into isolated trading vaults (`CircuitsAgentTradingVault.sol`), trading perpetuals and prediction markets without risking their core operating treasury.
