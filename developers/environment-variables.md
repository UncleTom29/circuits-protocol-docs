# Environment Variables

The `.env` file configures all connections, API keys, and deployment specific settings for Circuits Protocol.

{% hint style="danger" %}
Never commit `.env` to version control. Always copy from `.env.example`. Ensure that mainnet keys are **never** placed in the `.env` during testnet development.
{% endhint %}

## Groupings

### EVM RPC URLs
Controls connections to blockchain networks:
- `BSC_TESTNET_RPC_URL`
- `BASE_SEPOLIA_RPC_URL`
- `ETH_SEPOLIA_RPC_URL`
- `ARC_TESTNET_RPC_URL`

### Deployer Keys
Wallets used for script deployments and relayer execution:
- `EVM_DEPLOYER_PRIVATE_KEY`
- `SOLANA_DEPLOYER_KEYPAIR_PATH`
- `SUI_DEPLOYER_ADDRESS`
- `RELAYER_PRIVATE_KEY`

### Treasury
Addresses designated for protocol fees:
- `TREASURY_ADDRESS`
- `NEXT_PUBLIC_TREASURY_ADDRESS`

### Databases
Connection URLs for isolated PostgreSQL instances:
- `MARKETPLACE_DATABASE_URL`
- `SOCIAL_DATABASE_URL`
- `DEGEN_DATABASE_URL`
- `CUSTODY_DATABASE_URL`

### Custody and KMS
Controls the KMS provider (currently `local` for dev) and root keys for envelope encryption. 9 distinct root keys exist to isolate risk:
- `DEGEN_LOCAL_ROOT_KEY`
- `CUSTODY_LOCAL_ROOT_KEY`
- `FACILITATOR_LOCAL_ROOT_KEY`
- `AGENT_WALLET_LOCAL_ROOT_KEY`
- `REGISTRAR_LOCAL_ROOT_KEY`
- `LLM_KEY_LOCAL_ROOT_KEY`
- `CLAWDHQ_LINK_LOCAL_ROOT_KEY`
- `LLM_BILLING_TREASURY_LOCAL_ROOT_KEY`
- `PIPELINE_LOCAL_ROOT_KEY`
- `AGENT_CIRCLE_CREDENTIAL_LOCAL_ROOT_KEY`

### Hosted Runtime & LLMs
Variables for BYO-key or platform billing models, overriding OpenRouter defaults:
- `HOSTED_RUNTIME_ANTHROPIC_MODEL`, `HOSTED_RUNTIME_OPENAI_MODEL`
- `HOSTED_RUNTIME_PLATFORM_OPENROUTER_KEY`
- `HOSTED_RUNTIME_OPENROUTER_SLUG_*`
- `PLATFORM_LLM_COST_*_USDC`

### Skill Catalog
Third-party integrations:
- `SKILL_1INCH_API_KEY`
- `SKILL_COINGECKO_API_KEY`

### Contracts
Deployed contract addresses on various chains, e.g.:
- `ARC_TESTNET_CONTRACT_ADDRESS`
- `ARC_TESTNET_EXCHANGE_ADDRESS`
- `NEXT_PUBLIC_ARC_TESTNET_LAUNCHPAD_ADDRESS`

### Circle Developer Platform
Settings for Embedded Wallets, CCTP, and Gateway:
- `CIRCLE_API_KEY`, `CIRCLE_ENTITY_SECRET`
- `ARC_TESTNET_CCTP_DOMAIN`

### Privy Authentication
- `NEXT_PUBLIC_PRIVY_APP_ID`
- `PRIVY_APP_SECRET`
