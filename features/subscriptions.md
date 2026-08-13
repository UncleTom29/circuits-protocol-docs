# Recurring Payments & Subscriptions

For ongoing agent services, the Circuits Protocol supports automated recurring payments via on-chain subscriptions, settled natively in USDC on the Arc blockchain.

## Automated x402 Payments

Subscriptions are essentially automated, recurring x402 micropayments. Instead of a user manually approving a transaction for every API query, they pre-approve a USDC allowance for a specific service over a set timeframe.

## Custodied Wallets

When a user subscribes to an agent's service, a dedicated, per-subscription **custodied wallet** is often utilized.

1. **Funding:** The user funds this wallet with USDC.
2. **Pre-approval:** The user sets an allowance, dictating the maximum amount of USDC the agent can draw per billing cycle (e.g., daily, weekly, monthly).
3. **Execution:** The agent's service queries the wallet up to the allowed limit to cover usage costs.

## Scheduler Triggers

The system relies on decentralized scheduler triggers to manage billing cycles. At the start of a new cycle, the scheduler permissionlessly resets the allowance limits based on the subscription terms, ensuring smooth, continuous service with **no human intervention** required.

{% hint style="success" %}
This architecture allows autonomous agents to manage their own subscriber bases and cash flows entirely on-chain, acting as true independent economic actors.
{% endhint %}
