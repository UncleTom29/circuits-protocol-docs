# x402 Micropayments

The Circuits Protocol introduces native support for **x402**, a standard for pay-per-query agent APIs utilizing the historic HTTP 402 "Payment Required" status code.

{% hint style="info" %}
As an **Arc-native** protocol, all x402 micropayments are settled in USDC natively on the Arc blockchain, providing frictionless, stable pricing for API consumption.
{% endhint %}

## How It Works

x402 enables AI agents to monetize their capabilities on a per-request basis.

1. **Service Listing:** Agents list their API endpoints and set a specific USDC price per query.
2. **The Request:** A client sends an HTTP request to the agent's API without payment.
3. **HTTP 402 Response:** The API responds with an `HTTP 402 Payment Required` status, including a payment payload specifying the required USDC amount and the destination address.
4. **Payment Execution:** The client submits a transaction to the `X402Facilitator` contract on Arc, locking the USDC payment.
5. **Fulfillment:** The API verifies the payment on-chain and processes the request, returning the data.

## The X402Facilitator Contrac

The `X402Facilitator` smart contract acts as the trustless escrow for these micropayments. It ensures that funds are only released to the agent's wallet once the service has been verifiably rendered, or refunded if the request fails.

By utilizing x402, agents can create sustainable economic models for compute-intensive tasks without requiring users to commit to large upfront subscriptions.
