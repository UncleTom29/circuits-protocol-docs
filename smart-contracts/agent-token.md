# AgentToken

`AgentToken` is the ERC-20 contract deployed for every agent token launched via `ClawdHQLaunchpad`. It enforces transfer restrictions during the bonding curve phase and a deflationary fee model after graduation.

## Pre-Graduation: The Bonding Curve Phase

When an `AgentToken` is constructed:
* **Fixed Supply**: The entire fixed supply (`1,000,000,000`) is minted directly to the `ClawdHQLaunchpad` contract.
* **Transfers Locked**: To prevent secondary markets from forming off-curve, peer-to-peer transfers are strictly blocked. The only allowed transfers are buys (Launchpad -> User) and sells (User -> Launchpad).
* **Buyback Burns**: The Launchpad can call `burnFromLaunchpad` during this phase to permanently burn tokens repurchased via the automated buyback pool.

## Post-Graduation: Secondary Market Phase

When the Launchpad's graduation threshold is met, the `graduateToken` function is called.
* **Transfers Unlocked**: The `graduated` flag is set to true, allowing normal peer-to-peer and DEX transfers.
* **Treasury Designation**: The token saves the `agentTreasury` address (typically the agent's registered custodied wallet).

### Deflationary Transfer Fee

After graduation, a strict 2% fee (`TRANSFER_FEE_BPS`) applies to every transfer (matching the 2% fee that was charged during the bonding curve phase, ensuring consistency).

This 2% fee is split 50/50:
1. **1% Burned**: Half of the fee is sent to `address(0)` and added to the `burnedSupply`, providing deflationary pressure on the token supply.
2. **1% Treasury**: Half of the fee is sent directly to the `agentTreasury`, providing continuous revenue to the agent owner based on trading volume.
