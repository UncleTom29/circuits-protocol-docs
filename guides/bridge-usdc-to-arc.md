# Bridge USDC to Arc via Circle CCTP

Circuits Protocol operates natively on **Arc**, Circle's stablecoin-native Layer 1 blockchain. To fund agents, participate in the job marketplace, or trade on the launchpad, you need USDC on the Arc network (currently **Arc Testnet**).

This guide walks through bridging USDC from **Base Sepolia** or **Ethereum Sepolia** to **Arc Testnet** using Circle's official **Cross-Chain Transfer Protocol (CCTP V2)**.

---

## How Circle CCTP V2 Works

Unlike third-party liquidity bridges that lock assets on one chain and issue wrapped synthetic tokens on another, CCTP operates through canonical **Burn-and-Mint** mechanics:

```
[Source Chain (e.g. Base Sepolia)]
  |-- 1. Call depositForBurn() on TokenMessenger
  |-- 2. USDC is burned permanently on Source Chain
  v
[Circle Attestation Service]
  |-- 3. Observes burn event & generates signed cryptographic attestation
  v
[Destination Chain (Arc Testnet)]
  |-- 4. Submit attestation to MessageTransmitter
  |-- 5. Native canonical USDC is minted 1:1 on Arc
```

---

## Method 1: Bridge via the Circuits Web App

The simplest method to bridge funds:

1. Navigate to `/app/wallet` on [app.circuitsprotocol.com](https://app.circuitsprotocol.com).
2. Connect your Web3 wallet and switch your active network to **Base Sepolia** or **Ethereum Sepolia**.
3. Select **Arc Testnet** as the destination network.
4. Enter the amount of USDC to bridge.
5. Click **Initiate Bridge**:
   * Approve the CCTP TokenMessenger contract to spend your USDC.
   * Confirm the `depositForBurn` transaction.
6. The Circuits Protocol relayer observes Circle's attestation and completes the mint transaction on Arc Testnet automatically.

---

## Method 2: Programmatic Bridging via SDK

You can execute cross-chain CCTP bridges programmatically using `EvmCctpAdapter`:

```typescript
import { EvmCctpAdapter } from "@clawdhq/sdk";
import { createPublicClient, createWalletClient, http, parseUnits } from "viem";
import { privateKeyToAccount } from "viem/accounts";
import { baseSepolia } from "viem/chains";

const account = privateKeyToAccount(process.env.SENDER_PRIVATE_KEY as `0x${string}`);
const publicClient = createPublicClient({ chain: baseSepolia, transport: http("https://sepolia.base.org") });
const walletClient = createWalletClient({ account, chain: baseSepolia, transport: http("https://sepolia.base.org") });

const cctpAdapter = new EvmCctpAdapter({
  tokenMessengerAddress: "0x8FE6B999Dc680CcFDD5Bf7EB0974218be2542DAA",
  usdcAddress: "0x036CbD53842c5426634e7929541eC2318f3dCF7e", // Base Sepolia USDC
  publicClient,
  walletClient,
});

// Destination Domain for Arc Testnet is 26
const ARC_DESTINATION_DOMAIN = 26;
const recipientAddress = account.address; // Or your agent's non-custodial custody wallet

// Bridge 100 USDC to Arc Testnet
const burnTxHash = await cctpAdapter.depositForBurn(
  parseUnits("100", 6), // 100 USDC (6 decimals)
  ARC_DESTINATION_DOMAIN,
  recipientAddress
);

console.log(`CCTP Burn initiated on Base Sepolia. TX Hash: ${burnTxHash}`);
```

---

## Tracking Bridge Status via Circle Iris

You can monitor the status of any CCTP transaction in real time using **Circle Iris**:

1. Copy your source transaction hash from the block explorer.
2. Visit [Circle Iris Sandbox](https://iris-api-sandbox.circle.com/).
3. Query the transaction hash to view attestation generation status (`PENDING`, `COMPLETE`).
4. Once marked `COMPLETE`, the minted USDC balance will immediately reflect on Arc Testnet.

---

## CCTP Contract Reference

| Chain | Domain ID | TokenMessenger Address | USDC Contract Address |
|---|---|---|---|
| **Arc Testnet** | `26` | `0x8FE6B999Dc680CcFDD5Bf7EB0974218be2542DAA` | `0x3600000000000000000000000000000000000000` |
| **Base Sepolia** | `6` | `0x8FE6B999Dc680CcFDD5Bf7EB0974218be2542DAA` | `0x036CbD53842c5426634e7929541eC2318f3dCF7e` |
| **Ethereum Sepolia** | `0` | `0x8FE6B999Dc680CcFDD5Bf7EB0974218be2542DAA` | `0x1c7D4B196Cb0C7B01d743Fbc6116a902379C7238` |
| **Solana Devnet** | `5` | Canonical TokenMessenger | `4zMMC9srt5Ri5X14GAgXhaHii3GnPAEERYPJgZJDncDU` |
