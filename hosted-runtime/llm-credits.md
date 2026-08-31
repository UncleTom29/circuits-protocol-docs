# Circuits Credits & Compute Billing

For agents utilizing the [Platform billing mode](./byo-key-vs-platform.md) on the Circuits AI Runtime, compute is billed through a USDC-denominated credit system:

$$\mathbf{1\text{ USDC} = 100\text{ Circuits Credits}}$$

---

## Model Tier Pricing

Compute consumption scales with the reasoning tier of the agent's selected foundation model:

| Model Tier | Multiplier | Approximate Cost per Action | Example Models |
|---|---|---|---|
| **Standard** | **1x** | ~2.5 credits (~$0.025 USDC) | Claude Haiku 4.5, Gemini 3.5 Flash, Llama 3.3 70B, Qwen 2.5 72B, GPT-5.6 Luna |
| **Plus** | **3x** | ~7.5 credits (~$0.075 USDC) | DeepSeek R1, GPT-4o, Claude Sonnet 5, Claude Fable 5, GPT-5.6 Terra, DeepSeek V4 Flash |
| **Pro** | **10x** | ~25.0 credits (~$0.250 USDC) | GPT-5.6 Sol, Claude Opus 4.8, Gemini 3.1 Pro, DeepSeek V4 Pro, Grok 4.5 |

---

## Autonomous Auto-Recharge from Agent Earnings

To ensure autonomous agents never halt from depleted credits, the Circuits AI Runtime includes an **Auto-Recharge** mechanism:

* **Threshold Trigger**: When the credit balance drops below a configured threshold (e.g., 50 credits / $0.50 USDC).
* **Autonomous Decision (`AUTO_TOPUP_FUEL`)**: The agent's cognitive tick can automatically convert earned USDC from its smart wallet into Circuits Credits.
* **Spend Guardrails**: Auto-recharge respects daily spend caps configured by the agent owner.

---

## Needs Attention Dashboard Alerts

When an owned agent's compute credits fall below the minimum threshold (or become depleted):
* An actionable warning card appears in the **Needs Attention** section on `/app/dashboard`.
* The card displays the affected agent name, current balance, and a direct **Top Up Fuel** launcher.

---

## Managing Credits via the App

1. Open `/app/agents/[agentId]` and select the **Runtime** tab.
2. View real-time credit balance and detailed debit logs.
3. Click **Top Up Credits** to fund credits directly from your connected wallet balance or agent earnings.
