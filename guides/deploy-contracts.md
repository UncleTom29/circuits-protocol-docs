# Deploy Smart Contracts

Circuits Protocol's smart contracts are built using Solidity and are fully upgradeable using the UUPS (Universal Upgradeable Proxy Standard) pattern. Because Circuits is native to **Arc**, this guide focuses on deploying our EVM contracts to the Arc Testnet.

## Prerequisites

Ensure you have the repository cloned and dependencies installed:

```bash
git clone https://github.com/UncleTom29/Clawd-HQ.gi
cd Clawd-HQ
npm install
```

## Hardhat Setup

Our EVM contracts are managed using Hardhat. The configuration for Arc Testnet is already included in `hardhat.config.ts`.

1. Create a `.env` file in the root directory (or in your smart contracts package directory) based on `.env.example`.
2. Add your deployment private key and the Arc Testnet RPC URL:

```env
DEPLOYER_PRIVATE_KEY=your_private_key_here
ARC_TESTNET_RPC_URL=https://rpc-testnet.arc.circle.com
```

{% hint style="warning" %}
Ensure your deployer wallet has sufficient testnet USDC on Arc, as USDC is the native gas token.
{% endhint %}

## Deployment Scripts

Deployment scripts are located in the `scripts/deploy-evm` directory. We use Hardhat Ignition or custom scripts depending on the module.

To run the full deployment suite on Arc Testnet:

```bash
npx hardhat run scripts/deploy-evm/deploy_all.ts --network arcTestne
```

This script will sequentially deploy:
1. **Core:** Identity registry and capability managers.
2. **Marketplace:** The USDC escrow and job tracking contracts.
3. **Launchpad:** The bonding curve factory and Xero DEX pairs.
4. **Staking:** The reliability bond contracts.

The script will output the deployed proxy addresses for each contract. Save these addresses; you will need them to configure the multi-chain indexer and the frontend application.

## Contract Verification

Verifying your contracts on the block explorer provides transparency. Since Arc is EVM-compatible, you can use Hardhat's verification plugin if the Arc explorer supports the standard API.

```bash
npx hardhat verify --network arcTestnet <DEPLOYED_CONTRACT_ADDRESS> "Constructor_Argument_1"
```

*Note: Check the latest Arc developer documentation for the specific Blockscout/Etherscan API URL and API keys if required for verification.*
