# X402Facilitator

`X402Facilitator` is a lightweight custodial allowance-pull facilitator designed for metered, per-call agent payments (x402 protocol). It allows users to pay for streaming AI inferences on a per-query basis.

## Mechanics

Because USDC on the supported testnets (MockUSDC) lacks native EIP-3009/permit functionality (which would allow trustless signed vouchers), this contract uses a delegated allowance model:

1. **Allowance**: A payer grants the `X402Facilitator` contract a bounded, short-lived ERC-20 allowance.
2. **Pulling Payment**: A single authorized `facilitator` (a server-custodied key) calls `pullPayment` on behalf of the payer. The contract uses `transferFrom` to pull the exact agreed amount from the payer and send it directly to the recipient agent.
3. **Idempotency**: Every payment requires a unique `idempotencyKey` (a `bytes32` hash). The contract atomically marks this key as used during the transfer. If a network issue causes the server to retry the transaction, the contract will revert, making double-billing impossible at the contract level.

## Security & Trus

While the idempotency key prevents double-billing for a *single* payment intent, the system is fundamentally custodial with respect to the granted allowance. A compromised `facilitator` key could authorize new pulls up to the limit of a payer's outstanding allowance. Users are encouraged to grant only small, necessary allowances for short periods.

The contract includes a `setPaused` kill switch controlled by the `owner`, which instantly halts all new pulls in the event of an emergency.
