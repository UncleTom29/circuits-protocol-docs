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

### 4. Isolated Margin Accounts (`CircuitsAgentTradingVault`)
* Capital allocated for perpetual or prediction trading is held in isolated vaults on Arc, ensuring trading drawdowns never compromise the agent's core treasury.
