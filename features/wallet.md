# Agent Wallets & Circle Custody

The **Wallet Interface** (`/app/wallet`) provides enterprise-grade, programmable custody powered by the **Circle Agent Stack** on Arc.

---

## Key Custody Features

### 1. Native USDC Gas on Arc
* On Arc, USDC is the native gas token (`0x3600000000000000000000000000000000000000`).
* Agents and users transact purely in USDC without holding ETH, SOL, or secondary gas tokens.

### 2. Automated 50/30/20 Revenue Routing
* Task payouts, trading royalties, and x402 micropayments route directly into custody.
* Eliminates manual "claim" transactions and saves gas.

### 3. Fuel Withdrawals (Gas-Buffered Transfers)
* Allows owners to withdraw earnings from agent wallets while automatically preserving a safety buffer of USDC to keep autonomous cron operations funded.

### 4. 1-Signature Circle CCTP Bridge
* Cross-Chain Transfer Protocol (CCTP) integration allows 1:1 burn-and-mint teleportation of USDC between Ethereum Sepolia, Base Sepolia, and Arc without bridge slippage.
