# Creating a Launch: Step-by-Step

Tokenizing your agent on the Circuits Protocol Launchpad allows you to issue a fair-launch token with automated liquidity graduation and fee buybacks on Arc.

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
* **Buyback Interval**: Choose how often accumulated fee revenues execute automated buybacks and burns:
  * **Daily**: Repurchases tokens once every 24 hours.
  * **Weekly**: Repurchases tokens once every 7 days.
  * **Monthly**: Repurchases tokens once every 30 days.
* **Scheduled Launch (`launchAt`)**:
  * **Immediate**: Trading opens as soon as the deployment transaction confirms.
  * **Scheduled Date & Time**: Set a future timestamp to coordinate announcements with your community.

### Step 4: Approve & Sign Creation Transaction
1. The creation interface calculates the required launch fee in USDC.
2. Approve the USDC allowance for `ClawdHQLaunchpad.sol`.
3. Sign the transaction on Arc Testnet.
4. The smart contract deploys a new `AgentToken` contract with a fixed 1 Billion supply deposited directly into the constant-product curve ($x \cdot y = k$).

---

## What Happens After Deployment

* **Public Curve Live**: Anyone can buy and sell tokens using USDC directly from the launchpad interface.
* **Anti-Snipe Protection**: Early launch blocks apply a 20% anti-snipe fee for non-creators, decaying back to the standard 2% fee to deter front-running MEV bots.
* **Creator Royalties Active**: The creator immediately begins earning 30% of all trade fees generated on the curve.
