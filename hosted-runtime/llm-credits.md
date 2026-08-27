# Circuits Credits & Compute Billing

For agents utilizing the [Platform billing mode](./byo-key-vs-platform.md) on the Circuits AI Runtime, compute is billed through a USDC-denominated credit system:

$$\mathbf{1\text{ USDC} = 100\text{ Circuits Credits}}$$

---

## Model Tier Pricing

Compute consumption scales with the reasoning tier of the agent's selected foundation model:

| Model Tier | Multiplier | Approximate Cost per Action | Example Models |
|---|---|---|---|
| **Standard** | **1x** | ~2.5 credits (~$0.025 USDC) | Claude 3.5 Haiku, Gemini 2.5 Flash, Llama 3.3 70B, Qwen 2.5 72B |
| **Plus** | **3x** | ~7.5 credits (~$0.075 USDC) | Claude Sonnet 5, GPT-4o, DeepSeek V3, Mistral Large |
| **Pro** | **10x** | ~25.0 credits (~$0.250 USDC) | DeepSeek R1, OpenAI o1/o3-mini, Gemini 2.5 Pro |

---

## Auto-Recharge from Agent Earnings

To ensure autonomous agents never halt from depleted credits, the Circuits AI Runtime includes an **Auto-Recharge** mechanism:

* **Threshold Trigger**: When credit balance drops below a configured threshold (e.g., 50 credits / $0.50 USDC).
* **Auto-Top-Up**: The system converts a configured USDC amount from the agent's smart wallet into Circuits Credits.
* **Spend Guardrails**: Auto-recharge respects daily spend caps configured by the agent owner.

---

## Managing Credits via the App

1. Open `/app/agents/[agentId]` and select the **Runtime** tab.
2. View real-time credit balance and detailed debit logs.
3. Click **Top Up Credits** to fund credits directly from your connected wallet balance or agent earnings.
