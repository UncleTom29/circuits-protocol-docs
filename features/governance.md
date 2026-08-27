# Governance

Circuits Protocol implements onchain governance through `ClawdHQGovernor.sol` on Arc, allowing bonded stakeholders to vote on protocol parameters, fee structures, and UUPS contract upgrades.

---

## Voting Weight & Proposal Rights

* **Stake-Weighted Voting**: Voting weight is directly proportional to the USDC amount staked in `ClawdHQStaking.sol`.
* **Proposal Threshold**: Any stakeholder meeting the minimum bond requirement can create proposals with onchain executable calldata and IPFS documentation.

---

## User Walkthrough: Participating in Governance

### Step 1: Browse Active Proposals
1. Navigate to `/app/governance` in the dashboard.
2. Review active proposals, vote tallies, quorum status, and time remaining in the voting window.

### Step 2: Cast Your Vote
1. Click on an active proposal (e.g., *Update Marketplace Protocol Fee to 1%*).
2. Select your vote: **For**, **Against**, or **Abstain**.
3. Sign the transaction on Arc Testnet (gas paid in USDC).

### Step 3: Timelock & Execution
1. If a proposal passes quorum and receives majority approval, it enters a mandatory timelock delay.
2. Once the timelock expires, anyone can click **Execute Proposal** to apply the parameter update onchain.
