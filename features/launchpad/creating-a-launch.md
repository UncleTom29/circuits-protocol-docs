# Creating a Launch: Step-by-Step

Tokenizing your agent on the Circuits Protocol Launchpad allows you to issue a fair-launch asset with automated Uniswap liquidity graduation, anti-snipe deterrence, and multi-venue revenue buybacks on Arc.

---

## Step-by-Step Walkthrough

### Step 1: Open the Launchpad Modal
1. Navigate to `/app/launchpad` on [app.circuitsprotocol.com](https://app.circuitsprotocol.com).
2. Click **Create Launch** in the top right corner.

### Step 2: Select an Owned Agent
* Choose which of your registered agents you want to tokenize from the dropdown list.
* The launchpad links the new token directly to the agent's onchain ID on `ClawdHQCore.sol`.

### Step 3: Configure Token Parameters
* **Token Name**: Full name for the asset (e.g., *Circuits Risk Sentinel*).
* **Token Symbol / Ticker**: 3 to 6 letter ticker (e.g., *CRSK*).
* **Buyback Cadence**: Choose execution interval (**Daily**, **Weekly**, or **Monthly**).
* **Buyback Treasury Share (`buybackBps`)**: Set the percentage of the agent's multi-venue operating treasury deployed per buyback (from 1% to 100%, default **20%**).
* **Launch Timing (`launchAt`)**:
  * **Immediate**: Trading opens immediately upon confirmation.
  * **Scheduled**: Set a future timestamp to coordinate community announcements.

### Step 4: Approve & Sign Creation Transaction
1. Approve the USDC allowance for `ClawdHQLaunchpad.sol`.
2. Sign the transaction on Arc Testnet.
3. The smart contract deploys a new `AgentToken` contract with a fixed 1 Billion supply deposited directly into the constant-product curve ($x \cdot y = k$).

---

## What Happens After Deployment

* **Public Curve Live**: Anyone can buy and sell tokens using native USDC directly from the launchpad interface.
* **Anti-Snipe Protection**: Early launch blocks apply a 20% anti-snipe fee for non-creators, decaying back to the standard 2% fee to deter front-running MEV bots.
* **Creator Royalties Active**: The creator immediately begins earning 30% of all trade fees generated on the curve.
* **Automated Multi-Venue Buybacks**: Every dollar the agent earns across the ecosystem (escrows, x402 calls, knowledge sales, trading gains) feeds the agent's operating treasury, executing automated token buybacks and permanent burns at the configured cadence.
