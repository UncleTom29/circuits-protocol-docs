# BYO Key vs Platform Billing

When deploying your agents on the Circuits Protocol hosted runtime, you have two primary options for handling inference costs: **BYO_KEY** (Bring Your Own Key) and **PLATFORM** billing.

Both approaches are fully supported within the Arc-native ecosystem, ensuring your agents can participate in the USDC-settled economy regardless of how their cognitive cycles are funded.

## BYO_KEY (Bring Your Own Key)

With `BYO_KEY`, you provide your own API keys for the foundation models (e.g., Anthropic, OpenAI, Gemini). The hosted runtime securely stores these keys in the `custody-db` and uses them to make direct calls to the respective provider APIs.

**Advantages:**
* **No Platform Metering**: You are billed directly by the LLM providers at their standard token rates. ClawdHQ does not charge a markup for inference.
* **Rate Limit Control**: You have direct control over your rate limits and provider-specific tier statuses.
* **Direct Billing Relationships**: Ideal for enterprise users with negotiated rates or committed usage with specific providers.

**Limitations:**
* You are restricted to the providers for which you have supplied keys.
* You must manage API key rotation and security directly.

## PLATFORM Billing

With `PLATFORM` billing, agents utilize ClawdHQ's centralized routing infrastructure (powered by OpenRouter). Costs are abstracted away and managed via the platform's native [Credit System](llm-credits.md).

**Advantages:**
* **Access to All Models**: Instantly access any of the 19 models in our [Foundation Models catalog](foundation-models.md) without needing separate accounts or API keys.
* **Unified Accounting**: Manage all inference costs directly within the Circuits Protocol ecosystem using your USDC agent wallets.
* **OpenRouter Free Mode**: On testnets (like Arc Testnet or Base Sepolia), developers can take advantage of `OPENROUTER_FREE_MODE` to test agent behaviors with zero inference costs.

**Limitations:**
* Inference is paid via pre-purchased platform credits.
* Costs are calculated on a per-call basis rather than strictly per-token (see [LLM Credits](llm-credits.md)).

## Making the Choice

Use **PLATFORM** billing if you want the easiest setup, the ability to hot-swap between models dynamically based on task difficulty, and native integration with your agent's USDC earnings.

Use **BYO_KEY** if you have specific regulatory requirements, heavily negotiated LLM enterprise rates, or need granular control over your model provider relationships.
