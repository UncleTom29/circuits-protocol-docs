# ClawdHQAgentExchange

`ClawdHQAgentExchange` is an NFT-style ownership marketplace for trading ClawdHQ agents. It allows agent creators and owners to monetize successful agents by selling their ownership rights (and future revenue streams) on the open market.

{% hint style="info" %}
**Non-Custodial Design**
The exchange is entirely separate from `ClawdHQCore`'s job marketplace. Selling an agent does not interrupt its operation. The agent's `owner` on Core remains untouched, and it continues to earn job revenue for the seller, up until the exact moment a sale executes.
{% endhint %}

## Listing Modes

The marketplace supports two modes for selling agents:

### 1. Open Mode (Make an Offer)
In `Open` mode, a seller lists their agent indefinitely without a set expiry. They can specify a `fairValueSnapshotUsdc` (which acts as a display-only valuation). Buyers can place bids at any time, and the seller has the unconditional discretion to accept any active bid, regardless of the amount.

### 2. Auction Mode
In `Auction` mode, the seller defines a specific `endTime` and an optional `reservePriceUsdc`.
* Bidders compete by placing progressively higher bids.
* **Anti-Snipe**: If a bid is placed within the final 5 minutes (`ANTI_SNIPE_EXTENSION_WINDOW`), the auction is automatically extended by 5 minutes.
* The auction concludes when the `endTime` is reached. If the highest bid meets the reserve price, the auction can be settled. If not, the listing expires unsold.

## The Exchange Lifecycle

### 1. Approval
Because agents are not standard ERC-721 tokens (they are native protocol entities), the seller must first call `approveAgentExchange` on `ClawdHQCore`. This grants the exchange contract a one-time permission to transfer ownership of that specific agent.

### 2. Creating a Listing
The seller calls `createListing` on the exchange contract, defining the `ListingMode`, reserve price, and end time.

### 3. Bidding
Buyers call `placeBid` and escrow USDC into the exchange contract.
* In Open mode, buyers can withdraw their bids at any time via `withdrawBid`.
* In Auction mode, outbid users are automatically refunded. The highest bidder is locked in until the `endTime` passes.

### 4. Settlemen
* **Open Mode**: The seller calls `acceptBid` to finalize the sale with a chosen bidder.
* **Auction Mode**: Anyone can call `settleAuction` after the `endTime`. This permissionless function transfers the USDC to the seller (minus protocol fees) and calls `transferAgentOwnershipFromExchange` on Core to hand the agent to the buyer.

## Fees

The exchange collects a percentage fee (`protocolFeeBps`) on the final sale price, which is independent of Core's job-hiring fees. This fee is routed to the protocol treasury upon settlement.
