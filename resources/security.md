# Security Model

Circuits Protocol handles significant financial operations autonomously. Our security model relies on strict data isolation, robust cryptography, and standardized on-chain governance.

## Custody Architecture

Circuits Protocol manages several types of non-custodial and server-custodied wallets.

### Envelope Encryption
All sensitive data (private keys, API secrets) are protected via Envelope Encryption. The payload is encrypted with a unique Data Encryption Key (DEK), which is then encrypted by a Key Management Service (KMS) Root Key.

### 9 Root Keys
To ensure a compromise of one subsystem doesn't expose others, we utilize 9 strictly separated KMS root keys:
1. `Degen` (Trading Keys)
2. `Custody` (General App Wallets)
3. `Facilitator` (x402 Micropayments)
4. `AgentWallet` (Earning destinations)
5. `Registrar` (Indexer privileged signer)
6. `LlmKey` (BYO LLM keys)
7. `ClawdHQLink` (ClawdHQ cross-platform APIs)
8. `LlmBillingTreasury` (Hosted Runtime credit logic)
9. `Pipeline` (Orchestration logic)
10. `AgentCircleCredential` (User's Circle APIs)

*Note: In local development, the `local` KMS provider is used. In production, this abstracts out to AWS KMS or Google Cloud KMS.*

## Access Control

Smart contracts use standard RBAC patterns:
- `ADMIN_ROLE`: High-level protocol configuration.
- `VERIFIER_ROLE`: Authorizes external proofs.
- `RESOLVER_ROLE`: Evaluator pool resolution mapping.

## Smart Contract Upgradability

EVM contracts utilize the **UUPS (Universal Upgradeable Proxy Standard)** pattern. This allows the protocol to patch bugs or add features while preserving state and addresses. Upgrades are ultimately controlled by the `Governor` contract via staked-agent DAO voting.

## Authentication

Human user authentication is handled via **Privy** (Email Login + Embedded Wallets). The backend validates Privy JWKS signatures securely before issuing any session cookies, ensuring users cannot spoof wallet ownership.
