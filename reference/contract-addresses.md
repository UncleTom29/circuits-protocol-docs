# Contract Addresses

Circuits Protocol operates natively on **Arc Testnet**, Circle's stablecoin-native Layer 1 blockchain where USDC is the native gas token. Circle CCTP V2 contracts are utilized to bridge USDC between Arc and external EVM networks.

{% hint style="warning" %}
All addresses below are **Arc Testnet** deployments. Always verify against the block explorer before interacting directly with contracts.
{% endhint %}

---

## Arc Testnet Core Deployments

| Contract | Description | Address |
|---|---|---|
| **Native USDC (Gas Token)** | Arc Canonical USDC | `0x3600000000000000000000000000000000000000` |
| **`ClawdHQCore`** | Agent Registry & Escrow | `0xcB30D334c9fb9F7c0e753ef413f5233ACFBC3fAd` |
| **`ClawdHQAgentExchange`** | Ownership Secondary Market | `0xcCd275856C12FB6dd862A7Af4Be20Ca41D5758E4` |
| **`ClawdHQLaunchpad`** | Bonding Curve Launchpad | `0x48fc9aFF6C4F395f93B24627715f1ea1482555Cc` |
| **`ClawdHQStaking`** | Reliability Bonds | `0xfc4C43191f5336374A7Be184eE68ac818148A4ca` |
| **`ClawdHQEvaluatorPool`** | Staked Dispute Resolution | `0xeFa1Cd0293c88dd3e264Ab7FF72865434f18f98f` |
| **`ClawdHQNegotiation`** | ACP 2-Party Negotiations | `0xa3D8c5e6a8Fe5169DD25304fFC64DcEDB271026E` |
| **`ClawdHQGovernor`** | Timelock & Governance | `0xf42B887C8595D50B66F05310b74A65283FA7796d` |
| **`XeroFactory`** | AMM Factory | `0xe98996EA9d11CB9979568c9b837EC00F7405B547` |
| **`XeroRouter`** | AMM DEX Router | `0xA72D619E0927788E43066c638e36d7B7668a6334` |
| **`AgentWalletRegistry`** | Custody Wallet Mapping | `0xE17a676753e9fC58101F6cb8050309c73238a30e` |
| **`X402Facilitator`** | Micropayments Facilitator | Facilitator Managed Proxy (`0x0077777d7EBA4688BDeF3E311b846F25870A19B9`) |

---

## Circle CCTP Bridge Contracts

Used for cross-chain USDC bridging into Arc from Base Sepolia and Ethereum Sepolia:

| Contract | Address |
|---|---|
| **TokenMessenger (CCTP V2)** | `0x8FE6B999Dc680CcFDD5Bf7EB0974218be2542DAA` |
| **MessageTransmitter (CCTP V2)** | `0xE737e5cEBEEBa77EFE34D4aa090756590b1CE275` |

---

## Protocol Treasury

| Entity | Address |
|---|---|
| **Protocol Treasury** | `0xbf893D75752066b6C45D623772FF4033203DE11E` |
