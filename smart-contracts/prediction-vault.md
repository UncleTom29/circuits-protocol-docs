# CircuitsPredictionVault

`CircuitsPredictionVault.sol` is the protocol-native prediction market pool and vault on **Arc Testnet** (`0x64dddc35A57557A83CdE987d81DF80a7135Cc6b2`).

It enables autonomous AI agents and human participants to trade binary outcome shares (YES / NO) on real-world events, crypto milestones, sports outcomes, and macro metrics, settling completely in native USDC.

---

## Key Responsibilities

1. **Binary Market Creation**: Allows authorized creators or oracles (`ORACLE_ROLE`) to deploy binary forecasting markets with specific deadlines and resolution criteria.
2. **Outcome Share Trading**: Allows users and agents to buy YES or NO outcome shares directly from the pool with automatic share pricing based on pool depth.
3. **Decentralized Resolution**: Resolves markets through verified oracles or jury resolvers (`RESOLVER_ROLE`).
4. **Automated Winnings Claim**: Winning share holders can claim pro-rata shares of the total USDC market pool at $1.00 USDC per winning share.

---

## Market Parameters & Economics

| Parameter | Value | Description |
|---|---|---|
| **Protocol Fee** | `50 bps` (0.5%) | Protocol fee deducted on share purchases |
| **Minimum Stake** | `0.01 USDC` (`1e16` wei) | Minimum native USDC purchase per transaction |
| **Settlement Asset** | Native USDC on Arc | Zero conversion friction |
| **Outcome Types** | `YES`, `NO`, `INVALID` | Standard binary outcome states |

---

## Market Flow

```mermaid
graph TD
    Oracle[Oracle / Resolver] -->|createMarket(id, question, endTime)| Vault[CircuitsPredictionVault]
    TraderA[Predictive Agent A] -->|buyShares(id, YES)| Vault
    TraderB[Predictive Agent B] -->|buyShares(id, NO)| Vault
    Vault -->|Accumulate USDC Pool| Pool[Market Liquidity Pool]
    Oracle -->|resolveMarket(id, YES)| Vault
    TraderA -->|claimWinnings(id)| Winner[Payout: Pro-Rata Share of Total Pool]
```

---

## Key Functions

### Market Lifecycle

#### `createMarket(bytes32 marketId, string calldata question, uint256 endTime) external`
Deploys a new binary prediction market.
* **Access**: `ORACLE_ROLE` or `DEFAULT_ADMIN_ROLE`.
* **Checks**: Requires `endTime > block.timestamp`.
* **Emits**: `MarketCreated(marketId, question, endTime)`.

#### `buyShares(bytes32 marketId, Outcome outcome) external payable returns (uint256 sharesBought)`
Purchases YES or NO shares for an active market.
* **Access**: Permissionless.
* **Requirements**:
  * Market must be in `MarketStatus.OPEN` state and `block.timestamp < endTime`.
  * `outcome` must be `Outcome.YES` or `Outcome.NO`.
  * `msg.value >= MIN_STAKE`.
* **Fee Split**: Deducts 0.5% protocol fee to `feePool` and adds net USDC to `totalUsdcPool`.
* **Emits**: `SharesPurchased(marketId, buyer, outcome, msg.value, sharesBought)`.

#### `resolveMarket(bytes32 marketId, Outcome winningOutcome) external`
Resolves an open market to determine winning payouts.
* **Access**: `RESOLVER_ROLE` or `DEFAULT_ADMIN_ROLE`.
* **Requirements**: Market must be in `MarketStatus.OPEN` state.
* **Emits**: `MarketResolved(marketId, winningOutcome, resolvedAt)`.

#### `claimWinnings(bytes32 marketId) external returns (uint256 payoutUsdc)`
Claims winnings for a resolved market based on the caller's winning shares.
* **Requirements**: Market must be in `MarketStatus.RESOLVED` state.
* **Payout Formula**:
  $$\text{Payout} = \frac{\text{UserWinningShares}}{\text{TotalWinningShares}} \cdot \text{totalUsdcPool}$$
* **Emits**: `WinningsClaimed(marketId, claimant, payoutUsdc)`.

#### `cancelMarket(bytes32 marketId) external`
Cancels an unresolved or invalidated market and allows participants to refund their original capital.
* **Emits**: `MarketCancelled(marketId)`.

---

## View Functions

* `getMarket(bytes32 marketId) external view returns (Market memory)`: Returns the complete market struct.
* `getUserShares(bytes32 marketId, address user) external view returns (uint256 yesSharesCount, uint256 noSharesCount)`: Returns share balances for a given participant.
* `getMarketOdds(bytes32 marketId) external view returns (uint256 yesProbabilityBps, uint256 noProbabilityBps)`: Computes current implied probability based on share distribution.
