# Launchpad

{% hint style="info" %}
Circuits Protocol is **Arc-native** — built on Arc, Circle's stablecoin-native L1 where USDC is the gas token. All launchpad transactions are denominated in USDC.
{% endhint %}

The **Circuits Protocol Launchpad** provides a fair, decentralized mechanism for creating and launching agent-specific tokens on the Arc blockchain. Inspired by models like pump.fun, the launchpad uses a bonding curve mechanism to ensure immediate liquidity and deterministic price discovery from block zero.

## 100% Fair Launches

All tokens launched on the Circuits Protocol Launchpad are inherently fair:
* **No Pre-mines:** Creators do not receive free tokens.
* **No Team Allocations:** Every participant must buy from the curve.
* **Instant Liquidity:** The bonding curve guarantees liquidity at all times.

## Key Properties

* **Fixed Supply:** Every token launched has a fixed total supply of 1,000,000,000 (1 Billion) tokens.
* **USDC Denominated:** Purchases, sales, and liquidity provision are handled entirely in USDC.
* **Automated DEX Graduation:** Once a token's bonding curve reaches a predefined threshold, liquidity is automatically migrated to Uniswap.

## Launchpad Lifecycle

1. **[Creation](creating-a-launch.md):** A user configures the token metadata and launch parameters.
2. **[Bonding Phase](trading-on-curve.md):** Traders buy and sell tokens directly against the [bonding curve](bonding-curve.md), driving the price up or down based on supply and demand.
3. **[Graduation](graduation.md):** Once the liquidity threshold is met, the curve is finalized, and the pool migrates to Uniswap.
4. **[Buybacks](buybacks.md):** A portion of trading fees accrued during the bonding phase is used for automated buyback-and-burns.
