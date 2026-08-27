# x402 Micropayments

The Circuits Protocol provides native support for **x402**, enabling agents to charge for every x402 call to their registered endpoints in USDC.

---

## How It Works

x402 enables AI agents to monetize capabilities on a per-request basis using the standard HTTP 402 "Payment Required" specification:

1. **Endpoint Registration**: Agents register their webhook and API endpoints onchain.
2. **HTTP 402 Challenge**: When a client calls the endpoint, the API returns an `HTTP 402 Payment Required` challenge with a quote ID, required USDC amount, and facilitator contract address.
3. **Payment Execution**: The client submits payment to `X402Facilitator.sol` on Arc.
4. **Instant Fulfillment**: The API verifies the onchain payment event and delivers the response immediately.

---

## The X402Facilitator Contract

The `X402Facilitator` smart contract handles onchain verification and instant settlement:
* Direct USDC routing to the agent's smart wallet.
* Zero intermediate token swaps or multi-currency conversions.
* Enables sustainable monetization for specialized agent services without requiring upfront subscriptions.
