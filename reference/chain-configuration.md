# Chain Configuration

Circuits Protocol heavily leverages **Arc**, a stablecoin-native L1 where USDC acts as the gas token. We also utilize other testnets primarily for Circle CCTP cross-chain bridging.

## Primary Chain: Arc Testne

Arc is the native home for Circuits Protocol contracts and agents.

- **Network Name**: Arc Testne
- **Chain ID**: `5042002`
- **RPC URL**: `https://rpc.testnet.arc.network` (Client-side fallback: `https://arc-testnet.drpc.org`)
- **Block Explorer**: *(Arc block explorer URL)*
- **Native Gas Token**: USDC (`0x3600000000000000000000000000000000000000`)
- **CCTP Domain ID**: `26`

## Bridging Chains

We support CCTP bridging and cross-chain identities from these EVM testnets:

### Base Sepolia
- **Chain ID**: `84532`
- **RPC URL**: `https://sepolia.base.org`
- **USDC Address**: `0x036CbD53842c5426634e7929541eC2318f3dCF7e`
- **CCTP Domain ID**: `6`

### Ethereum Sepolia
- **Chain ID**: `11155111`
- **RPC URL**: `https://ethereum-sepolia-rpc.publicnode.com`
- **USDC Address**: `0x1c7D4B196Cb0C7B01d743Fbc6116a902379C7238`
- **CCTP Domain ID**: `0`

## Non-EVM Chains

Circuits Protocol maintains indexer logic for integration with:
- **Solana Devnet**: `https://api.devnet.solana.com` (CCTP Domain 5)
- **Sui Testnet**: `https://fullnode.testnet.sui.io:443`
