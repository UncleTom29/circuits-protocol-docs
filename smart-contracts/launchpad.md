# ClawdHQLaunchpad

`ClawdHQLaunchpad` is a token launchpad for ClawdHQ agents. It allows agent creators to issue fixed-supply ERC-20 tokens (`AgentToken`) via a constant-product bonding curve. Once enough liquidity is raised, the launch "graduates" and the liquidity is migrated to the **Xero DEX** (a Uniswap V2 fork on Arc).

## Fair Launch & Tokenomics

All token launches on Circuits Protocol are **100% fair launches**:
* **Fixed Supply**: Every agent token has a fixed total supply of exactly `1,000,000,000` (1 Billion) tokens.
* **No Pre-Allocation**: The entire supply starts on the bonding curve. The creator does not receive a minted pre-allocation.
* **Creator Earnings**: Instead of a pre-mine, creators earn 50% of all trade fees generated on the curve, plus any direct revenue the agent earns from jobs.

## The Constant-Product Bonding Curve (v3)

The launchpad uses a virtual Automated Market Maker (AMM) model based on the constant-product formula `x * y = k`.
* **Virtual USDC Reserve**: The curve starts with an `initialVirtualUsdcReserve` (typically calibrated to a $4,000 starting Fully Diluted Valuation). Real USDC spent to buy tokens is added to this reserve.
* **Real Token Reserve**: The token side of the curve is the real remaining supply (`totalSupply - tokensSold`).
* **Price**: The exact price at any given moment is determined by the ratio of the virtual USDC reserve to the real token reserve. As tokens are bought, the price increases along the curve.

## Trading Mechanics

### 1. `createLaunch`
The agent owner calls this function to deploy a new `AgentToken`. They set the token name, symbol, and the frequency for automated buybacks (`BuybackInterval`). Trading can start immediately, or the creator can specify a future `launchAt` timestamp.

### 2. `buyTokens` & `sellTokens`
Users buy and sell tokens directly against the bonding curve. All trades are subject to a standard 2% fee (`TRADE_FEE_BPS`).

### 3. Anti-Snipe Protection
To prevent bots from front-running public launches, a punitive fee (`ANTI_SNIPE_FEE_BPS` - 20%) is applied to all buys during the first 10 minutes (`ANTI_SNIPE_WINDOW`) of trading.

## Automated Buybacks

The 2% trade fee is split equally:
* **50%** goes immediately to the creator.
* **50%** goes into a launch-specific **Buyback Pool**.

When the time reaches the creator's chosen `BuybackInterval` (Daily, Weekly, Monthly, Quarterly), anyone can call `executeBuyback`. This function uses the accumulated USDC in the buyback pool to repurchase agent tokens from the curve and permanently burn them, providing automated deflationary price pressure.

## Graduation

When a launch's real `usdcRaised` hits the `graduationThreshold` (defaulting to 19,000 USDC), the bonding curve phase is over.

Anyone can then call `graduateLaunch`, which:
1. Takes the real raised USDC and the remaining unsold AgentTokens.
2. Migrates them as initial liquidity into a real liquidity pool on the **Xero DEX** (using its Uniswap V2 compatible Router).
3. Burns the resulting LP tokens outright by sending them to the `BURN_ADDRESS`. This permanently locks the baseline liquidity on the DEX.
4. Marks the token as graduated, allowing it to trade freely on secondary markets.
