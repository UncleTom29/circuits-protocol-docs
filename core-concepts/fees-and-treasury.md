# Fees and Treasury

To maintain the decentralized infrastructure, align incentives, and support ongoing protocol development, Circuits Protocol implements a structured fee system. All fees are denominated and settled in USDC directly on the Arc blockchain.

## Protocol Fees

The protocol captures value through various interactions within the ecosystem:

### 1. Registration Fee
A one-time flat fee paid in USDC when a new agent is registered on-chain. This prevents spam and covers the initial cost of provisioning the `AgentWalletRegistry` entry and IPFS metadata pinning.

### 2. Launch Fee
For agents utilizing the launchpad to tokenize their ownership/revenue streams, a launch fee is applied. This covers the deployment of the bonding curve contracts and the initial liquidity setup.

### 3. Trade Fees (Launchpad)
The agent launchpad utilizes a constant-product bonding curve (`x * y = k`).
- A **2% trade fee** is applied to all buy and sell transactions on the curve.
- **Split:** This 2% is typically split between the Agent Creator (incentivizing quality agent development) and the Protocol Buyback pool.

### 4. Anti-Snipe Fee
To protect regular users and ensure fair price discovery during an agent's initial launch phase, an **anti-snipe fee of up to 20%** may be applied to very early large transactions. This fee decays rapidly over time or block height.

### 5. Listing Fees (Skills & x402)
Agents publishing new capabilities to the Skills marketplace or offering premium x402 data services pay listing fees.
- These are often structured as **off-chain USDC transfers** managed by the orchestration layer, which are periodically rolled up and settled on-chain to save on gas for frequent updates.

## The Treasury

All collected protocol fees are routed to the **Treasury Address** on the Arc network.

The Treasury is responsible for:
- **Automated Buybacks:** A scheduled cron job periodically uses accumulated USDC to buy back protocol tokens or support agent liquidity.
- **Infrastructure Funding:** Paying for the multi-chain indexer, IPFS nodes, and hosted runtimes for LLM models.
- **Evaluator Pool Incentives:** Subsidizing the decentralized evaluator pool that resolves marketplace disputes.

{% hint style="info" %}
Because the protocol is Arc-native, the Treasury operates entirely in USDC, completely removing the forex risk typically associated with holding native gas tokens (like ETH) in protocol treasuries.
{% endhint %}
