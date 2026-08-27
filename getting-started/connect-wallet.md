# Connect Wallet

Circuits Protocol provides secure authentication and non-custodial wallet connectivity across all protocol interfaces.

Authentication is powered by [Privy](https://privy.io/) and standard Web3 wallet connectors, enabling onboarding for both native crypto developers and Web2 builders.

---

## Connection Methods

When you click **Connect** on [app.circuitsprotocol.com](https://app.circuitsprotocol.com), you can choose between two authentication paths:

### 1. Email Login (Embedded Non-Custodial Wallet)
* Privy generates a secure, embedded EVM wallet for your account.
* Private keys are managed via distributed key management with zero seed phrase friction.
* Ideal for rapid prototyping, mobile access, and automated scripts.

### 2. External Web3 Wallets (WalletConnect)
* Connect using existing Web3 browser extensions or hardware wallets (MetaMask, Rabby, Coinbase Wallet, Rainbow).
* Full support for hardware-backed signing via Ledger and Trezor.

---

## Arc Testnet Auto-Configuration

When you connect, Circuits Protocol automatically requests your wallet to switch to or add the **Arc Testnet**:

| Parameter | Value |
|---|---|
| **Network Name** | Arc Testnet |
| **RPC URL** | `https://arc-testnet.drpc.org` |
| **Chain ID** | `5042002` |
| **Currency Symbol** | `USDC` |
| **Block Explorer** | `https://testnet.arcscan.app` |

Because Arc is a stablecoin-native Layer 1, your wallet will display **USDC** as the native currency and gas token.

---

## Authentication Architecture

To authenticate API and WebSocket requests with the Circuits Protocol backend:

1. **Client Authentication**: You sign in via Privy on the frontend.
2. **JWT Token Issuance**: Privy issues a signed JSON Web Token (JWT) to the client session.
3. **Authorized API Calls**: The client sends the JWT in the `Authorization: Bearer <token>` header for protected endpoints.
4. **JWKS Verification**: The backend verifies the cryptographic signature against Privy's JSON Web Key Set (JWKS), confirming your address and authorization.

This ensures secure, authenticated management of your registered agents, hosted runtime policies, and trading vaults.
