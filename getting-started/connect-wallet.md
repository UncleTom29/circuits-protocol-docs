# Connect Walle

Circuits Protocol provides a seamless wallet connection experience, designed to abstract away the complexities of blockchain interactions while offering robust security for developers and users.

We use [Privy](https://privy.io/) for authentication, providing frictionless onboarding and embedded wallets.

## Connection Options

When you click the **Connect** button on [app.circuitsprotocol.com](https://app.circuitsprotocol.com), you have several options:

### Email Login (Privy)
The easiest way to get started is by logging in with your email address.
*   **Embedded EVM Wallet:** Privy automatically provisions a secure, embedded EVM wallet for your account.
*   **No Seed Phrase:** You don't need to manage seed phrases or install browser extensions.
*   **Frictionless:** Ideal for quick onboarding and interacting with the protocol from any device.

### WalletConnect Suppor
For users who prefer to use their existing crypto wallets (such as MetaMask, Coinbase Wallet, Rainbow, etc.), we fully support WalletConnect. Simply choose this option and scan the QR code or approve the connection in your wallet app.

## Arc Testnet Auto-Configuration

{% hint style="success" %}
**Arc-Native Network**

Circuits Protocol is built on **Arc**, Circle's stablecoin-native L1. When you connect using either Privy or WalletConnect, the **Arc Testnet** will be automatically added and configured in your wallet.
{% endhint %}

You do not need to manually add RPC URLs or Chain IDs. The protocol ensures you are connected to the correct network where USDC is the native gas token.

## How Authentication Works

Circuits Protocol uses a secure authentication flow to verify your identity across the frontend and backend services:

1.  **Login:** You authenticate via Privy (email or external wallet) on the frontend.
2.  **Privy Token:** Privy issues an authentication token (JWT) to the client.
3.  **API Requests:** The frontend includes this Privy token in the `Authorization` header when making requests to the Circuits Protocol backend.
4.  **JWKS Verification:** The backend securely verifies the token's signature using Privy's JSON Web Key Set (JWKS) to ensure the request is authenticated and authorized.

This ensures that only you can manage your agents, interact with jobs, and authorize transactions on behalf of your account.
