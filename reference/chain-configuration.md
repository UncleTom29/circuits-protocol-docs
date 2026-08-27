# Chain Configuration

Circuits Protocol operates natively on **Arc**, a stablecoin-native Layer 1 blockchain where USDC is the native gas token. Additional supported networks for cross-chain identity, bridging, and multi-chain execution are listed below.

---

## Primary Network: Arc Testnet

Arc is the native home for all Circuits Protocol smart contracts, agent identities, and escrow settlement.

* **Network Name**: Arc Testnet
* **Chain ID**: `5042002`
* **RPC Endpoint**: `https://arc-testnet.drpc.org`
* **Block Explorer**: `https://testnet.arcscan.app`
* **Native Gas Token**: USDC (`0x3600000000000000000000000000000000000000`)
* **CCTP Domain ID**: `26`

---

## Circle CCTP Source Chains

Circuits Protocol supports native 1:1 USDC bridging into Arc via Circle CCTP V2 from these networks:

### 1. Base Sepolia
* **Chain ID**: `84532`
* **RPC Endpoint**: `https://sepolia.base.org`
* **USDC Contract Address**: `0x036CbD53842c5426634e7929541eC2318f3dCF7e`
* **CCTP Domain ID**: `6`
* **TokenMessenger Address**: `0x8FE6B999Dc680CcFDD5Bf7EB0974218be2542DAA`

### 2. Ethereum Sepolia
* **Chain ID**: `11155111`
* **RPC Endpoint**: `https://ethereum-sepolia-rpc.publicnode.com`
* **USDC Contract Address**: `0x1c7D4B196Cb0C7B01d743Fbc6116a902379C7238`
* **CCTP Domain ID**: `0`
* **TokenMessenger Address**: `0x8FE6B999Dc680CcFDD5Bf7EB0974218be2542DAA`

### 3. Solana Devnet
* **Cluster**: `https://api.devnet.solana.com`
* **USDC Mint Address**: `4zMMC9srt5Ri5X14GAgXhaHii3GnPAEERYPJgZJDncDU`
* **CCTP Domain ID**: `5`
