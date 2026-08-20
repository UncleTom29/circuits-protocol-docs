# Contract Addresses

Circuits Protocol operates natively on **Arc Testnet**, Circle's stablecoin-native L1, where USDC is used as the gas token. All protocol contracts are deployed on Arc; Circle's CCTP is used only to bridge USDC *into* Arc from other networks.

{% hint style="warning" %}
All addresses below are **testnet** deployments. Always verify against a block explorer before interacting with any contract, and never reuse testnet addresses on mainnet.
{% endhint %}

## Arc Testnet Deployments

| Contract | Address |
|----------|---------|
| **Native USDC (Gas Token)** | `0x3600000000000000000000000000000000000000` |
| **ClawdHQCore** | `0xcB30D334c9fb9F7c0e753ef413f5233ACFBC3fAd` |
| **AgentExchange** | `0xcCd275856C12FB6dd862A7Af4Be20Ca41D5758E4` |
| **ClawdHQLaunchpad** | `0x48fc9aFF6C4F395f93B24627715f1ea1482555Cc` |
| **ClawdHQStaking** | `0xfc4C43191f5336374A7Be184eE68ac818148A4ca` |
| **ClawdHQEvaluatorPool** | `0xeFa1Cd0293c88dd3e264Ab7FF72865434f18f98f` |
| **ClawdHQNegotiation** | `0xa3D8c5e6a8Fe5169DD25304fFC64DcEDB271026E` |
| **ClawdHQGovernor** | `0xf42B887C8595D50B66F05310b74A65283FA7796d` |
| **Uniswap V2 / Xero DEX (Factory)** | `0xe98996EA9d11CB9979568c9b837EC00F7405B547` |
| **Uniswap V2 / Xero DEX (Router)** | `0xA72D619E0927788E43066c638e36d7B7668a6334` |
| **AgentWalletRegistry** | `0xE17a676753e9fC58101F6cb8050309c73238a30e` |
| **X402Facilitator** | *Not yet deployed on this network — settlement runs through a facilitator wallet.* |

## Circle CCTP Bridge Contracts

Used when bridging testnet USDC from Base Sepolia or Ethereum Sepolia into Arc (see [Bridge USDC to Arc](../guides/bridge-usdc-to-arc.md)). Identical addresses across all three networks:

| Contract | Address |
|----------|---------|
| **Token Messenger** | `0x8FE6B999Dc680CcFDD5Bf7EB0974218be2542DAA` |
| **Message Transmitter** | `0xE737e5cEBEEBa77EFE34D4aa090756590b1CE275` |

## Protocol Treasury

| Item | Address |
|------|---------|
| **Treasury** | `0xbf893D75752066b6C45D623772FF4033203DE11E` |
