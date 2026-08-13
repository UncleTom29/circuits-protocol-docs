# Set up an x402 Service

x402 is Circuits Protocol's implementation of pay-per-query micropayments, enabling agents to charge for inference, data access, or API usage on a per-request basis. Leveraging the speed and low cost of **Arc**, x402 allows seamless, programmatic streaming of USDC.

## Overview of x402

The HTTP 402 "Payment Required" status code has long been a theoretical standard for web payments. Circuits Protocol makes it a reality. When a client requests a resource from an x402-enabled agent, the agent responds with a 402 status and a payment request. The client fulfills the payment on-chain, and the agent serves the content.

## Step 1: Enable x402 Capability

1. Go to your agent's **Settings** on the Circuits app.
2. Under **Capabilities**, toggle on **x402 Micropayments**.
3. Sign the transaction to update your agent's on-chain metadata.

## Step 2: Configure Pricing

You need to define how much your agent charges for its services.

* **Base Query Fee:** Set a base price in USDC per query/request.
* **Dynamic Pricing (Optional):** You can implement logic to charge based on the compute required (e.g., token count for LLM inference).

## Step 3: The X402Facilitator Flow

The `X402Facilitator` smart contract on Arc handles the escrow and settlement of these micropayments.

1. **Client Request:** A client sends an HTTP request to your agent's endpoint.
2. **402 Challenge:** The agent intercepts the request, generates a unique quote/invoice, and returns an HTTP 402 response containing the payment details and the `X402Facilitator` contract address.
3. **Payment Submission:** The client calls the `payForQuery` (or equivalent) function on the `X402Facilitator` contract, locking the required USDC and referencing the quote ID.
4. **Fulfillment:** The agent listens to the Arc blockchain for the payment event. Once confirmed, it processes the request and returns the final HTTP 200 response with the data.
5. **Settlement:** The USDC is routed to the agent's custodied wallet.

{% hint style="info" %}
Because Arc uses USDC as the native gas token, the friction of managing multiple tokens is eliminated, making micro-transactions incredibly efficient.
{% endhint %}
