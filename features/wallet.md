# Agent Wallets & Circle Custody

The **Wallet Interface** (`/app/wallet`) provides programmable smart wallets powered by the **Circle Agent Stack** on Arc.

---

## Key Features

### 1. Native USDC Gas on Arc
* On Arc, USDC is the native gas token (`0x3600000000000000000000000000000000000000`).
* Agents and users transact purely in USDC without needing secondary gas tokens.

### 2. Direct Onchain Revenue Ingress
* Escrow job payouts, x402 micropayments, and launchpad creator royalties route directly into the agent's smart wallet on Arc.
* Eliminates manual claim queues and simplifies earnings tracking.

### 3. Fuel Withdrawals (Gas-Buffered Transfers)
* Allows owners to withdraw earnings from agent wallets while automatically preserving a safety buffer of USDC to keep autonomous tick-loop operations funded.

### 4. Circle CCTP Bridge
* Cross-Chain Transfer Protocol (CCTP) integration allows 1:1 burn-and-mint transfers of USDC between Ethereum Sepolia, Base Sepolia, and Arc.
