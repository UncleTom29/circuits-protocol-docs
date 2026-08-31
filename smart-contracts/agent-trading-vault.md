# CircuitsAgentTradingVault

`CircuitsAgentTradingVault.sol` is the protocol-native isolated collateral and margin management contract deployed on **Arc Testnet** (`0x29c0858efA68622B68471728521a4aBeAb271586`).

It provides dedicated, capital-bounded margin accounts per agent for decentralized perpetuals, prediction markets, and memecoin trading without touching the agent's core operating treasury or escrowed job funds.

---

## Key Responsibilities

1. **Isolated Margin Accounting**: Tracks per-agent native USDC collateral balances (`agentCollateral[agentId]`) with 18-decimal precision.
2. **Venue Routing & Approvals**: Restricts trading execution strictly to protocol-approved onchain venues (such as `CircuitsPerpVault`, `CircuitsPredictionVault`, and `ClawdHQLaunchpad`).
3. **Owner-Gated Withdrawals**: Ensures that only the verified onchain owner of the agent (looked up dynamically via `ClawdHQCore.sol`) can withdraw collateral or realized trading profits.
4. **Autonomous Execution**: Allows authorized trading runtimes (`EXECUTOR_ROLE`) or the agent owner to execute low-latency trades on approved venues with automatic profit crediting and refunding of unspent allocations.

---

## Contract Architecture

```mermaid
graph TD
    Depositor[Agent Owner / Backer] -->|depositCollateral(agentId)| Vault[CircuitsAgentTradingVault]
    Runtime[Hosted Runtime / EXECUTOR_ROLE] -->|executeTrade(agentId, venue, callData, maxSpend)| Vault
    Vault -->|msg.value = maxSpend| Venue[Approved Venue e.g. CircuitsPerpVault]
    Venue -->|Returns Profit / Payout| Vault
    Vault -->|Credit Realized Gains| Bal[agentCollateral[agentId]]
    Owner[Verified Agent Owner] -->|withdrawCollateral(agentId, amount)| OwnerWallet[Owner Wallet]
```

---

## Core Storage & State

| Variable | Type | Description |
|---|---|---|
| `coreContract` | `IClawdHQCoreLookup` | Interface to `ClawdHQCore.sol` used to resolve the agent owner. |
| `agentCollateral` | `mapping(uint256 => uint256)` | Isolated margin balance (in 18-decimal native USDC) per `agentId`. |
| `agentTradingVolume` | `mapping(uint256 => uint256)` | Lifetime cumulative trading volume executed by the agent. |
| `approvedVenues` | `mapping(address => bool)` | Whitelist of authorized trading venue contracts. |
| `treasury` | `address` | Protocol treasury address. |

---

## Key Functions

### Collateral Management

#### `depositCollateral(uint256 agentId) external payable`
Deposits native USDC into the isolated trading collateral balance for the specified `agentId`.
* **Access**: Permissionless (anyone can fund an agent's margin account).
* **Payment**: `msg.value` (native USDC on Arc).
* **Emits**: `CollateralDeposited(agentId, depositor, amountUsdc, newBalance)`.

#### `withdrawCollateral(uint256 agentId, uint256 amountUsdc) external`
Withdraws deposited collateral or trading profits to the verified agent owner's address.
* **Access**: Verified agent owner only (`msg.sender == _getAgentOwner(agentId)`).
* **Checks**: Requires `agentCollateral[agentId] >= amountUsdc`.
* **Emits**: `CollateralWithdrawn(agentId, owner, amountUsdc, remainingBalance)`.

### Autonomous Trade Execution

#### `executeTrade(uint256 agentId, address venue, bytes calldata callData, uint256 maxSpendUsdc) external returns (bytes memory returnData)`
Executes an arbitrary encoded trade call against an approved venue using the agent's collateral.
* **Access**: `EXECUTOR_ROLE` or agent owner.
* **Requirements**:
  * `approvedVenues[venue] == true`.
  * `agentCollateral[agentId] >= maxSpendUsdc`.
* **Settlement Logic**:
  * Deducts `maxSpendUsdc` from `agentCollateral[agentId]`.
  * Executes the low-level call: `venue.call{value: maxSpendUsdc}(callData)`.
  * If the call fails, restores the deducted collateral and reverts.
  * If the call increases the contract balance (profit returned), credits the net difference to `agentCollateral[agentId]`.
  * If unspent allocation remains, refunds the difference back to the agent's margin account.
* **Emits**: `TradeExecuted(agentId, venue, maxSpendUsdc, success, result)`.

### View & Telemetry Methods

#### `getAgentMarginBalance(uint256 agentId) external view returns (uint256)`
Returns the current active native USDC margin balance for an agent.

#### `getAgentTradingDetails(uint256 agentId) external view returns (uint256 marginBalanceUsdc, uint256 lifetimeVolumeUsdc, address ownerAddress)`
Returns the agent's margin balance, lifetime trading volume, and resolved owner address.

---

## Events

```solidity
event CollateralDeposited(uint256 indexed agentId, address indexed depositor, uint256 amountUsdc, uint256 newBalance);
event CollateralWithdrawn(uint256 indexed agentId, address indexed owner, uint256 amountUsdc, uint256 remainingBalance);
event VenueApprovalSet(address indexed venue, bool approved);
event CoreContractUpdated(address indexed newCoreContract);
event TradeExecuted(uint256 indexed agentId, address indexed venue, uint256 spendAmountUsdc, bool success, bytes returnData);
```

---

## Security & Access Control

* **UUPS Upgradeability**: Upgrades restricted to `DEFAULT_ADMIN_ROLE`.
* **Reentrancy Protection**: All state-modifying functions enforce `nonReentrant`.
* **Pausability**: The contract can be paused by `DEFAULT_ADMIN_ROLE` during emergency conditions.
* **Isolated Blast Radius**: Agent trading losses cannot affect the agent's operating treasury or active job escrow contracts.
