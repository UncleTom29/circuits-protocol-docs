# Bonding Curve Mechanics

The Circuits Protocol Launchpad utilizes a **Constant-Product Bonding Curve** ($x \times y = k$) to govern token pricing and guarantee continuous liquidity prior to Uniswap graduation.

---

## The Invariant ($x \times y = k$)

The curve is defined by the standard automated market maker invariant:

$$ x \times y = k $$

Where:
* **$x$** = Virtual USDC Reserve
* **$y$** = Real Token Reserve (1,000,000,000 fixed supply)
* **$k$** = Constant Product

At deployment, the pool is initialized with a **Virtual USDC Reserve** and the total supply of **Real Tokens**. The virtual reserve sets the initial floor price without requiring the creator to supply upfront capital.

---

## Price Discovery & Spot Price

The spot price of a token is the ratio of the virtual USDC reserve to the remaining token reserve:

$$ P = \frac{x}{y} $$

* **Buying:** Adds USDC to the reserve and removes tokens, moving the price up along the curve.
* **Selling:** Returns tokens to the curve and withdraws USDC, moving the price down.

---

## Fee Structure (50/30/20)

Every trade on the bonding curve incurs a **2% transaction fee**, distributed as follows:
* **50% (1.0% of trade):** Protocol Treasury & Liquidity Reserve.
* **30% (0.6% of trade):** Creator Royalties, paid directly to the agent owner's wallet.
* **20% (0.4% of trade):** Monthly Buyback & Burn Pool.

---

## Anti-Snipe Protection

To protect retail participants and prevent MEV bot manipulation on block zero:
* An **Anti-Snipe Fee of up to 20%** is applied during the initial launch blocks.
* This fee decays exponentially over a short block window back to the standard 2% fee.
* All excess anti-snipe proceeds are routed directly into the token's buyback contract.
