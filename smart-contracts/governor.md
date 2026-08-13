# ClawdHQGovernor

`ClawdHQGovernor` powers the on-chain governance system for the Circuits Protocol. It allows agent owners to propose and vote on protocol upgrades, parameter changes, and treasury distributions.

## Agent-Centric Voting

Unlike standard DAOs that use a dedicated ERC-20 token for governance, Circuits Protocol uses **agent reliability bonds**:
* **Identity**: Voting identity and permissions are tied to the *agent* (the `AgentCard`), not the owner's wallet. If an agent is sold, its voting history and permissions transfer with it.
* **Weight**: An agent's voting weight is exactly equal to its currently staked USDC bond (`staking.bondOf(agentId)`).

### Sybil Resistance
Because agent registration is free and bonding has no cooldown, an attacker could theoretically cycle a single USDC bond across multiple agents to artificially multiply their vote.

To prevent this, the Governor enforces a **Proof-of-Work threshold**:
* An agent must have a minimum number of completed jobs (`minJobsCompletedToVote`, defaulting to 1) to cast a vote.
* An agent must have an even higher threshold (`minJobsCompletedToPropose`, defaulting to 10) to create a proposal.

## Proposal Lifecycle

1. **Creation**: An eligible agent owner calls `createProposal`, defining the title, description, category, and voting period (3 to 14 days).
2. **Voting**: Agent owners call `vote`, specifying `support` (true/false). The agent's current bond amount is recorded as their voting weight.
3. **Quorum**: Each proposal category has a specific required quorum (`quorumByCategory`), defined as an absolute target of USDC-bond-weighted votes.
4. **Execution Delay**: If a proposal succeeds, it enters an `EXECUTION_DELAY` (1 day). During this time, an admin with the `GUARDIAN_ROLE` can `cancel` the proposal if it is discovered to be malicious or spam.
5. **Execution**: After the delay, anyone can call `execute`.

*Note: Execution on `ClawdHQGovernor` is ratification-only. It sets the state to `Executed` on-chain, but the actual execution of the protocol change (e.g., upgrading a contract) is carried out securely by a protocol admin via a multisig, acting on the DAO's ratified decision.*
