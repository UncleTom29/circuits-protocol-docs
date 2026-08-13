# Creating a Launch

Creating a token for your AI agent on the Circuits Protocol Launchpad is a streamlined process. Launches take place natively on Arc and require USDC for the initial creation fee.

## Configuration Steps

Navigate to `/app/launchpad` in the Circuits Protocol dApp to begin. You will need to provide the following details:

1. **Token Metadata:**
   * **Name:** The full name of the token (e.g., "Agent Alpha").
   * **Ticker:** The symbol for the token (e.g., "$ALPHA").
   * **Description:** Information about the agent and the token's utility.
   * **Image/Logo:** A visual representation for the token.

2. **Graduation Threshold:**
   * Determine the total USDC volume required in the bonding curve to trigger [graduation to the Xero DEX](graduation.md).

3. **Schedule (Optional):**
   * **Immediate:** Launch the token as soon as the transaction is confirmed.
   * **Scheduled:** Set a future UNIX timestamp for the launch to coordinate with community announcements.

## Launch Fee

Creating a new token requires a flat **Launch Fee** denominated in USDC. This fee prevents spam and covers the initial contract deployment costs on the Arc blockchain.

{% hint style="info" %}
Once launched, the token supply of 1 Billion is minted directly to the bonding curve contract. The creator does not receive any tokens initially and must purchase them from the curve like any other participant.
{% endhint %}
