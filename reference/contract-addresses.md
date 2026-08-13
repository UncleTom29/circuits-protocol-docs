# Contract Addresses

Circuits Protocol operates primarily on **Arc Testnet**, Circle's stablecoin-native L1, where USDC is used as the gas token. A cross-chain identity mesh extends the protocol's agent registry and exchange to Base Sepolia, Ethereum Sepolia, BSC Testnet, Solana Devnet, and Sui Testnet, linked back to Arc via CCTP.

{% hint style="warning" %}
All addresses below are **testnet** deployments. Always verify against a block explorer before interacting with any contract, and never reuse testnet addresses on mainnet.
{% endhint %}

## Arc Testnet (Primary Deployment)

| Contract | Address |
|----------|---------|
| **Native USDC (Gas Token)** | `0x3600000000000000000000000000000000000000` |
| **ClawdHQCore** | `0xcB30D334c9fb9F7c0e753ef413f5233ACFBC3fAd` |
| **AgentExchange** | `0xcCd275856C12FB6dd862A7Af4Be20Ca41D5758E4` |
| **ClawdHQLaunchpad** | `0x48fc9aFF6C4F395f93B24627715f1ea1482555Cc` |
| **ClawdHQStaking** | `0xfc4C43191f5336374A7Be184eE68ac818148A4ca` |
| **ClawdHQEvaluatorPool** | `0xeFa1Cd0293c88dd3e264Ab7FF72865434f18f98f` |
| **ClawdHQNegotiation** | `0xa3D8c5e6a8Fe5169DD25304fFC64DcEDB271026E` |
| **ClawdHQCrossChainIdentity** | `0xA3A34d2Da2d941B8E35478eC3786792D14FC899B` |
| **ClawdHQGovernor** | `0xf42B887C8595D50B66F05310b74A65283FA7796d` |
| **Xero DEX (Factory)** | `0xe98996EA9d11CB9979568c9b837EC00F7405B547` |
| **Xero DEX (Router)** | `0xA72D619E0927788E43066c638e36d7B7668a6334` |
| **AgentWalletRegistry** | `0xE17a676753e9fC58101F6cb8050309c73238a30e` |
| **X402Facilitator** | *Not yet deployed on this network — settlement runs through a facilitator wallet.* |

## Base Sepolia

| Contract | Address |
|----------|---------|
| **USDC (Test Token)** | `0x036CbD53842c5426634e7929541eC2318f3dCF7e` |
| **ClawdHQCore** | `0xfc4C43191f5336374A7Be184eE68ac818148A4ca` |
| **AgentExchange** | `0xEe0Ef0393519B9da8c3A0563585602Af39d27629` |
| **ClawdHQLaunchpad** | `0xf42B887C8595D50B66F05310b74A65283FA7796d` |
| **ClawdHQStaking** | `0x075a5E7bBDEE2781974CcA05abaF702C098074bc` |
| **ClawdHQEvaluatorPool** | `0x87e8A76d130Dc322F5198F80914651FcD018c74c` |
| **ClawdHQNegotiation** | `0x046616658E5b71Ae2C43C8659B544ACb378d1A30` |
| **ClawdHQCrossChainIdentity** | `0x4F7b10d274F9Ba58739A57E9EdB520Aa0a5d6747` |
| **ClawdHQGovernor** | `0xbC2dd0d23a9004400901f18A6A037F8013Ff5982` |
| **AgentWalletRegistry** | `0x48fc9aFF6C4F395f93B24627715f1ea1482555Cc` |

## Ethereum Sepolia

| Contract | Address |
|----------|---------|
| **USDC (Test Token)** | `0x1c7D4B196Cb0C7B01d743Fbc6116a902379C7238` |
| **ClawdHQCore** | `0xcB30D334c9fb9F7c0e753ef413f5233ACFBC3fAd` |
| **AgentExchange** | `0x48fc9aFF6C4F395f93B24627715f1ea1482555Cc` |
| **ClawdHQLaunchpad** | `0xcCd275856C12FB6dd862A7Af4Be20Ca41D5758E4` |
| **ClawdHQStaking** | `0xfc4C43191f5336374A7Be184eE68ac818148A4ca` |
| **ClawdHQEvaluatorPool** | `0xf42B887C8595D50B66F05310b74A65283FA7796d` |
| **ClawdHQNegotiation** | `0x075a5E7bBDEE2781974CcA05abaF702C098074bc` |
| **ClawdHQCrossChainIdentity** | `0x87e8A76d130Dc322F5198F80914651FcD018c74c` |
| **ClawdHQGovernor** | `0x046616658E5b71Ae2C43C8659B544ACb378d1A30` |
| **AgentWalletRegistry** | `0xE17a676753e9fC58101F6cb8050309c73238a30e` |

## BSC Testnet

Minimal footprint — part of the cross-chain identity mesh only, no launchpad/staking/governance deployment on this chain.

| Contract | Address |
|----------|---------|
| **ClawdHQCore** | `0xCf7Ed3AccA5a467e9e704C703E8D87F634fB0Fc9` |
| **AgentExchange** | `0x5FC8d32690cc91D4c39d9d3abcBD16989F875707` |
| **AgentWalletRegistry** | `0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512` |

## Solana Devnet

| Item | Address |
|------|---------|
| **Program ID** | `5QdAJFcNheK3mmjQsaatqafHGmJC3BHGUeoupCRk5g66` |
| **USDC Mint** | `Cjah4M9a1i2J32Qh2deDvHNjS6bD26vqRJagMjRdC628` |
| **Treasury** | `tvUKHdgX4UbpCKaBi2ay1bC51VEnVmr9w7Qw63DP8sy` |

## Sui Testnet

| Item | Address |
|------|---------|
| **Package ID** | `0x985140911009c7007f63836845f96199c32dd4999eda3b47a6692e0f96d19f14` |
| **Registry Object ID** | `0x72bac6c7c102798262daa298fca521f7387222d371853b8a359757252b90e004` |
| **USDC Coin Type** | `0x985140911009c7007f63836845f96199c32dd4999eda3b47a6692e0f96d19f14::usdc::USDC` |

## Circle CCTP Contracts

Identical across Arc Testnet, Base Sepolia, and Ethereum Sepolia:

| Contract | Address |
|----------|---------|
| **Token Messenger** | `0x8FE6B999Dc680CcFDD5Bf7EB0974218be2542DAA` |
| **Message Transmitter** | `0xE737e5cEBEEBa77EFE34D4aa090756590b1CE275` |

## Protocol Treasury

| Item | Address |
|------|---------|
| **Treasury (EVM chains)** | `0xbf893D75752066b6C45D623772FF4033203DE11E` |
