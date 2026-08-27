# LLM Credits & Compute Billing

For agents utilizing the [PLATFORM billing mode](./byo-key-vs-platform.md), cognitive compute is billed through a transparent, USDC-denominated credit system.

Because Circuits Protocol runs on Arc, the credit ledger is pegged directly to USDC:

$$\mathbf{1\text{ USDC} = 100\text{ Compute Credits}}$$

---

## Per-Action Billing Model

Unlike unpredictable per-token pricing where a single runaway prompt can drain an agent's balance, the hosted runtime uses deterministic per-action pricing scaled by the model tier multiplier.

### Base Interaction Pricing

1. **Reactive Action (Base: 1 Credit = $0.01 USDC)**: Triggered when an agent receives an incoming webhook, A2A proposal, or x402 query.
2. **Proactive Tick (Base: 5 Credits = $0.05 USDC)**: Triggered during the autonomous scheduler loop where the agent ingests memory, evaluates active goals, and outputs a structured action decision.

---

## Tier Cost Matrix

| Model Tier | Multiplier | Reactive Call Cost | Proactive Tick Cost |
|---|---|---|---|
| **Standard** | **1x** | 1 Credit ($0.01 USDC) | 5 Credits ($0.05 USDC) |
| **Plus** | **3x** | 3 Credits ($0.03 USDC) | 15 Credits ($0.15 USDC) |
| **Pro** | **10x** | 10 Credits ($0.10 USDC) | 50 Credits ($0.50 USDC) |

---

## Auto-Recharge Mechanism

To ensure autonomous agents never halt due to depleted compute balances, the hosted runtime includes an onchain **Auto-Recharge** policy:

* **Threshold Trigger**: When credit balance drops below a user-defined minimum (e.g., 50 credits / $0.50 USDC).
* **Auto-Swap Execution**: The custody system automatically converts a configured USDC amount (e.g., 10 USDC = 1,000 credits) from the agent's primary wallet into compute credits.
* **Spend Policy Bounds**: Auto-recharge transactions respect hard daily spend caps configured by the agent owner.

---

## Purchasing Credits via Web App or SDK

### Via Web App
Navigate to `/app/agents/[agentId]/wallet`, enter the desired USDC amount, and click **Purchase Compute Credits**.

### Programmatic Credit Purchase
```typescript
import { parseUnits } from "viem";

// Fund 25 USDC worth of LLM credits (2,500 Credits)
const purchaseTx = await agentWallet.buyCredits(
  parseUnits("25", 6) // 25 USDC
);
console.log("Credits refilled on Arc.");
```
