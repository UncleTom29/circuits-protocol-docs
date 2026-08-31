# ClawdHQLaunchpad

`ClawdHQLaunchpad.sol` is the fair-launch bonding curve tokenization contract on **Arc Testnet** (`0x48fc9aFF6C4F395f93B24627715f1ea1482555Cc`).

It allows creators to tokenize their agents with constant-product bonding curves ($x \cdot y = k$), customizable fee buybacks (`buybackBps`), scheduled launch countdowns (`launchAt`), anti-snipe protections, and automated graduation to **Uniswap** on Arc.

---

## Key Features & Constants

| Constant | Value | Description |
|---|---|---|
| `TOTAL_SUPPLY` | `1,000,000,000` (1B) | Fixed total supply for every launched `AgentToken` |
| `TRADE_FEE_BPS` | `200` (2.0%) | Standard trading fee on bonding curve |
| `ANTI_SNIPE_FEE_BPS` | `2000` (20.0%) | Initial launch fee on non-creator buys to deter MEV bots |
| `DEFAULT_BUYBACK_BPS` | `2000` (20.0%) | Default percentage of treasury fee pool used per buyback |
| `GRADUATION_THRESHOLD` | `19,000 USDC` | Cumulative curve reserve required to trigger Uniswap graduation |

---

## Buyback & Burn Configuration

The launchpad contract supports customizable automated buybacks:
* **Configurable Buyback BPS**: Creators configure `buybackBps` (from 1 bps up to 10,000 bps = 100%, defaulting to 2,000 bps = 20%).
* **Cadence Intervals**: Daily (`BuybackInterval.DAILY`), Weekly (`BuybackInterval.WEEKLY`), or Monthly (`BuybackInterval.MONTHLY`).
* **Creator Updates**: Creators can modify buyback settings at any time using `updateBuybackConfig`.

---

## Core Functions

### Launch Lifecycle

#### `createLaunch(uint256 agentId, string memory name, string memory symbol, string memory tokenUri, BuybackInterval buybackInterval, uint16 buybackBps, uint64 launchAt) external payable returns (uint256 launchId, address tokenAddress)`
Deploys a new `AgentToken` contract with 1 Billion supply and initializes the constant-product curve.
* **Requirements**:
  * Caller must own `agentId` on `ClawdHQCore.sol`.
  * `buybackBps <= 10000`.
* **Emits**: `LaunchCreated(launchId, agentId, tokenAddress, creator, name, symbol, launchAt, buybackInterval, buybackBps)`.

#### `buy(uint256 launchId, uint256 minTokensOut) external payable returns (uint256 tokensOut)`
Buys agent tokens using native USDC against the bonding curve.
* **Requirements**: `block.timestamp >= launch.launchAt`.
* **Anti-Snipe**: Applies a 20% fee if executed in block zero by non-creators.

#### `sell(uint256 launchId, uint256 tokenAmount, uint256 minUsdcOut) external returns (uint256 usdcOut)`
Sells agent tokens back to the curve for native USDC.

#### `executeBuyback(uint256 launchId) external returns (uint256 tokensBurned)`
Permissionlessly executes a scheduled buyback when `block.timestamp >= launch.nextBuybackAt`.
* Spends `(treasuryBalance * launch.buybackBps) / 10000` USDC to market-buy tokens from the curve/AMM and transfers them permanently to `0x000000000000000000000000000000000000dEaD`.
* **Emits**: `BuybackExecuted(launchId, usdcSpent, tokensBurned, nextBuybackAt)`.

#### `updateBuybackConfig(uint256 launchId, BuybackInterval interval, uint16 buybackBps) external`
Allows the launch creator to update the buyback cadence and basis points.
* **Emits**: `BuybackConfigUpdated(launchId, interval, buybackBps)`.

#### `graduateLaunch(uint256 launchId) external`
Migrates accumulated USDC reserve and remaining tokens to the **Uniswap V2** liquidity pool on Arc, permanently burning the minted LP tokens.
* **Emits**: `LaunchGraduated(launchId, tokenAddress, pairAddress, usdcLiquidity, tokenLiquidity)`.
