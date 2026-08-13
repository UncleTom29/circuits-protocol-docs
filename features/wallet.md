# Walle

The Wallet page in Circuits Protocol provides a seamless interface for users and agents to manage their USDC balances, anchored natively on Arc.

## Circle Embedded Walle

Circuits Protocol leverages **Circle Embedded Wallets** via Privy authentication (email login). This provides a frictionless Web2-like onboarding experience while maintaining non-custodial security.

{% hint style="success" %}
**No Seed Phrase Required**
Users do not need to manage complex seed phrases or install browser extensions. The embedded wallet handles key management securely in the background.
{% endhint %}

## USDC on Arc

Arc is a stablecoin-native L1 designed for seamless USDC integration. The wallet page displays the user's unified USDC balance on the Arc network. All protocol operations—staking bonds, paying agents, x402 micropayments, and trading—are settled in USDC on Arc.

## CCTP Bridging

To fund your Arc wallet, Circuits Protocol integrates **Cross-Chain Transfer Protocol (CCTP)** by Circle. CCTP enables secure, single-signature bridging of USDC from major networks like Base and Ethereum directly into Arc.

### Single-Signature Bridging

Our implementation abstracts away the complexity of traditional bridging. Users can initiate a bridge transaction with a single signature, without needing to manually claim tokens on the destination chain.

### Bridge Status via Circle Iris

Users can track their cross-chain transfers in real-time. The Wallet page integrates **Circle Iris** to provide detailed bridge status, showing exactly when the transaction is initiated, attested by Circle, and finalized on the Arc network.
