# ClawdHQLaunchpad

`ClawdHQLaunchpad` is the token launchpad contract for Circuits Protocol agents. It allows agent creators to tokenize their agents with fixed-supply ERC-20 tokens (`AgentToken`) via a constant-product curve. Once enough liquidity is raised, the launch graduates and liquidity is automatically migrated to **Uniswap** on Arc.

---

## Fair Launch & Tokenomics

All token launches on Circuits Protocol are **100% fair launches**:
* **Fixed Supply**: Every agent token has a fixed total supply of exactly `1,000,000,000` (1 Billion) tokens.
* **No Pre-Allocation**: The entire supply starts on the curve. The creator does not receive a minted pre-allocation.
* **Creator Royalties**: Instead of a pre-mine, creators earn 30% of all trade fees generated on the curve, plus any direct revenue the agent earns from jobs.

---

## The Constant-Product Curve ($x \cdot y = k$)

The launchpad uses an AMM model based on the constant-product formula $x \cdot y = k$:
* **Virtual USDC Reserve**: The curve starts with an `initialVirtualUsdcReserve` setting the initial floor price without requiring upfront creator capital. Real USDC spent to buy tokens is added to this reserve.
* **Real Token Reserve**: The token side of the curve is the real remaining supply (`totalSupply - tokensSold`).
* **Price**: Determined by the ratio of the virtual USDC reserve to the real token reserve. As tokens are bought, the price increases along the curve.

---

## Trading Mechanics

### 1. `createLaunch`
The agent owner calls this function to deploy a new `AgentToken`. They set the token name, symbol, and buyback frequency (`BuybackInterval`). Trading can start immediately, or the creator can specify a future `launchAt` timestamp.

### 2. `buyTokens` & `sellTokens`
Users buy and sell tokens directly against the curve. All trades are subject to a standard 2% fee (`TRADE_FEE_BPS`).

### 3. Anti-Snipe Protection
To prevent bots from front-running public launches, an anti-snipe fee (`ANTI_SNIPE_FEE_BPS` = 20%) is applied to buys during the anti-snipe block window for non-creators.

---

## Trade Fee Distribution & Automated Buybacks

Every 2% trade fee (or anti-snipe fee) is distributed onchain via `_distributeTradeFee`:
* **50%** routes to the **Protocol Treasury** (`treasury`).
* **30%** routes to the **Creator / Agent Treasury** (`agentTreasury`).
* **20%** accumulates in the launch-specific **Buyback Pool** (`buybackPoolUsdc`).

When block time passes the configured `BuybackInterval` (Daily, Weekly, Monthly), anyone can call `executeBuyback`. This function uses accumulated USDC in the buyback pool to repurchase tokens from the curve and burn them, providing automated deflationary pressure.

---

## Uniswap Graduation

When a launch's real `usdcRaised` hits the `graduationThreshold` (defaulting to 19,000 USDC), the curve phase completes.

Anyone can call `graduateLaunch`, which:
1. Takes the real raised USDC and the remaining unsold `AgentToken` supply.
2. Seeds them as initial liquidity into **Uniswap V2** on Arc.
3. Permanently locks the resulting LP tokens in the contract.
4. Marks the token as graduated, allowing secondary trading on Uniswap with fee-on-transfer support.
