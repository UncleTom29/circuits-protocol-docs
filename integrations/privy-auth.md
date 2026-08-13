# Privy Authentication

Circuits Protocol utilizes **Privy** to provide a seamless, Web2-like onboarding experience while maintaining the security and self-custody benefits of Web3.

## Overview

For users interacting with the Circuits Protocol frontend (app.circuitsprotocol.com), managing private keys, seed phrases, and browser extension wallets can be a significant barrier to entry.

Privy solves this by enabling simple email and social logins, which automatically provision an embedded EVM-compatible wallet for the user in the background.

{% hint style="info" %}
Agents utilize **Circle Developer-Controlled Wallets**, while human users utilize **Privy Embedded Wallets**. Both settle natively on the Arc blockchain.
{% endhint %}

## Authentication Flow

1. **User Login**: The user enters their email address or selects a social login provider on the dApp frontend.
2. **Verification**: The user enters the one-time passcode (OTP) sent to their email.
3. **Wallet Provisioning**: Upon successful verification, Privy provisions a secure embedded wallet for the user.
4. **Session Token**: Privy returns a JWT (JSON Web Token) that the frontend uses to authenticate API requests to the Circuits backend.

## Security & Seed Phrases

Privy uses Shamir's Secret Sharing to split the user's private key across multiple isolated environments (the user's device and Privy's HSMs).

- **No Seed Phrases required**: Users do not need to write down or secure a 12-word seed phrase.
- **Non-Custodial**: Neither Privy nor Circuits Protocol has full access to the user's private key. The user remains in full control of their assets.

## Integration & Configuration

To integrate Privy in a development or self-hosted environment, the following environment variables must be configured:

```env
NEXT_PUBLIC_PRIVY_APP_ID=your_privy_app_id
PRIVY_APP_SECRET=your_privy_app_secre
```

### JWT Verification (Backend)

When the frontend makes requests to the Circuits multi-chain indexer or API backend, it includes the Privy JWT in the `Authorization` header.

The backend verifies this token using Privy's JWKS (JSON Web Key Set) endpoint to ensure the request is genuinely coming from the authenticated user before exposing sensitive data or executing actions.

```typescrip
// Example conceptual verification flow
const token = req.headers.authorization?.replace('Bearer ', '');
const verifiedPayload = await privy.verifyAuthToken(token);
const userId = verifiedPayload.userId;
```
