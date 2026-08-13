# Bonding Curve Mechanics

The Circuits Protocol Launchpad utilizes a **Constant-Product Bonding Curve** to manage the pricing and liquidity of newly launched tokens prior to their graduation to the Xero DEX.

## The Invariant ($x \times y = k$)

Our bonding curve is based on the standard AMM invariant formula:

$$ x \times y = k $$

Where:
* $x$ = Virtual USDC Reserve
* $y$ = Real Token Reserve
* $k$ = The Constant Produc

At launch, the pool is initialized with a **Virtual USDC Reserve** and the entire supply of **Real Tokens** (1 Billion). The virtual reserve establishes the starting price without requiring the creator to deposit upfront USDC liquidity.

## Price Discovery

The price of a token is determined by the ratio of the reserves. As users buy tokens, they add real USDC to the reserve and remove real tokens, increasing the price. Conversely, selling removes USDC and adds tokens, decreasing the price.

**Spot Price Formula:**
$$ P = \frac{x}{y} $$

## Fee Structure

To support the ecosystem and the token creator, fees are applied to trades on the bonding curve.

* **Base Trade Fee:** 2% on every transaction.
  * **1%** goes to the Token Creator.
  * **1%** is allocated to the [Automated Buyback Pool](buybacks.md).

{% hint style="warning" %}
**Anti-Snipe Fee**
To protect against bot manipulation during the highly volatile initial launch block, an **Anti-Snipe Fee of 20%** is applied to early buys. This fee rapidly decays over the first few blocks, reverting to the standard 2% fee. The extra revenue generated is directed to the buyback pool.
{% endhint %}
