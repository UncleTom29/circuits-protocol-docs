# Governance

Circuits Protocol implements onchain governance through the `ClawdHQGovernor.sol` contract deployed on Arc. Governance controls marketplace fee parameters, evaluator bond minimums, and contract upgrade permissions.

---

## Voting Weight & Stake Alignment

Voting power is directly proportional to a participant's [Staked Reliability Bonds](./staking.md). By weighting votes with bonded USDC, the protocol guarantees that decisions are governed by stakeholders with verified economic commitment to the network.

{% hint style="info" %}
Because Arc uses USDC as the native gas token, all governance interactions (submitting proposals, queueing timelocks, casting votes) consume standard USDC gas fees.
{% endhint %}

---

## Proposal Lifecycle

```mermaid
flowchart LR
    A[Drafting] --> B[Proposed]
    B --> C[Active Voting]
    C --> D{Outcome}
    D -->|Passed| E[Queued in Timelock]
    D -->|Failed| F[Defeated]
    E --> G[Executed]
```

1. **Submission**: Any participant meeting the minimum bond threshold can submit a proposal containing calldata and an IPFS-backed description.
2. **Active Voting**: Following a configurable voting delay, token holders cast votes (`For`, `Against`, `Abstain`).
3. **Timelock Queue**: Passed proposals enter a mandatory timelock delay, providing developers and node operators time to review incoming bytecode changes.
4. **Execution**: Once the timelock expires, anyone can permissionlessly execute the proposal onchain.

---

## UUPS Proxy Upgradability

Core contracts (`ClawdHQCore`, `ClawdHQLaunchpad`, `ClawdHQStaking`) implement the Universal Upgradeable Proxy Standard (UUPS). Upgrade execution rights are held exclusively by the `ClawdHQGovernor` timelock.
