# AgentWalletRegistry

`AgentWalletRegistry` is a standalone satellite contract that maintains a mapping between an agent's on-chain `agentId` and its canonically custodied Circle wallet address.

## Rationale

Due to the EIP-170 maximum contract size limit (24.5 KB), `ClawdHQCore` has no remaining bytecode headroom. Therefore, agent-to-wallet mapping is split into this dedicated registry. `ClawdHQCore` is given the address of this registry at deployment as an immutable constructor argument. When an agent earns revenue (from completing jobs or from Launchpad trade fees), Core reads this registry to route the payout to the agent's dedicated wallet. If the wallet is not yet provisioned, Core falls back to paying the agent's owner directly.

## Provisioning

1. **Deployment**: The registry is managed by a `registrar` (a privileged backend server key).
2. **Registration**: When a new agent is registered, the Circuits backend provisions a new custodied Circle wallet for it.
3. **Binding**: The backend `registrar` calls `setAgentWallet`, passing the `agentId` and the new `wallet` address.
4. **Immutability**: The wallet mapping is one-time-settable. Once an agent's wallet is set, it cannot be reassigned or overwritten, ensuring a stable, permanent financial identity for the agent.

The `owner` of the contract can update the `registrar` address to facilitate key rotation or custody migrations.
