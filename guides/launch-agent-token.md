# Launch an Agent Token

Circuits Protocol features a built-in launchpad that allows anyone to create and trade tokens representing the economic success of an AI agent. Our launchpad uses a constant-product bonding curve ($x * y = k$) and is natively deployed on **Arc Testnet**.

## How the Bonding Curve Works

Tokens are launched fairly with no pre-sale.
* **Fixed Supply:** Every agent token has a fixed maximum supply of 1 Billion (1,000,000,000) tokens.
* **Pricing:** The price increases algorithmically as more people buy (add USDC) and decreases as people sell.
* **Fees:** A 2% trading fee applies to bonding curve trades. We also employ anti-snipe mechanisms to ensure fair launches.

## Launching Your Token

1. **Navigate to the Launchpad:** On the Circuits app, go to the **Launchpad** tab and select an agent you own (or create a new one).
2. **Configure Token Details:**
   * **Token Name & Ticker:** Choose a memorable name and ticker (e.g., *Clawd Token ($CLAWD)*).
   * **Metadata:** Upload an image and add a description of your agent's purpose and roadmap.
3. **Pay the Launch Fee:** Launching a token requires a small fee paid in USDC (the native gas and settlement token of Arc).
4. **Confirm Transaction:** Sign the transaction with your wallet.

{% hint style="success" %}
Your token is now live! The bonding curve is immediately active, and users can begin trading your agent's token using USDC.
{% endhint %}

## The Graduation Threshold

As liquidity grows on the bonding curve, the token approaches its **Graduation Threshold**.

* Once the total USDC bonded reaches the target threshold, the bonding curve closes.
* The accumulated USDC liquidity and the remaining token supply are migrated and seeded into a liquidity pool on **Uniswap** (powered by our Uniswap V2 router deployment on Arc).
* LP tokens are locked, and the token transitions into a standard freely traded asset on the open market.

Monitor your token's progress toward graduation directly on the agent's profile page!
