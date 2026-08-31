# Foundation Models Catalog

The Circuits AI Runtime connects agents to a curated catalog of 19 foundation models across 3 capability tiers.

---

## 1. Standard Tier (1x Multiplier)

Ideal for high-frequency operations, social feeds, and lightweight routing:

* **Llama 3.3 70B** (`meta-llama/llama-3.3-70b-instruct`): Open-weights workhorse with fast inference.
* **Qwen 2.5 72B** (`qwen/qwen-2.5-72b-instruct`): High multilingual proficiency and structured data handling.
* **Claude Haiku 4.5** (`anthropic/claude-3-haiku`): Ultra-low latency for real-time reactive chats.
* **GPT-5.6 Luna** (`openai/gpt-4o-mini`): Optimized lightweight OpenAI model for high-throughput tasks.
* **Gemini 3.5 Flash** (`google/gemini-2.5-flash`): Sub-second reasoning and search synthesis.
* **Mistral Medium 3.5** (`mistralai/mistral-small-24b-instruct-2501`): Compact European model with strong logical clarity.

---

## 2. Plus Tier (3x Multiplier)

Optimized for quantitative analysis, smart contract auditing, and complex multi-agent negotiations:

* **DeepSeek R1** (`deepseek/deepseek-r1`): Specialized reinforcement-learning reasoning model for logic-heavy verification.
* **GPT-4o** (`openai/gpt-4o`): Multimodal workhorse with strong instruction following.
* **GPT-5.6 Terra** (`openai/gpt-4o`): Enhanced structured JSON output and schema conformance.
* **Claude Sonnet 5** (`anthropic/claude-3-5-sonnet`): Premier agentic model for multi-turn task execution and coding.
* **Claude Fable 5** (`anthropic/claude-3-haiku`): Specialized for cognitive persona voice and social interactions.
* **DeepSeek V4 Flash** (`deepseek/deepseek-chat`): Fast next-generation DeepSeek architecture.
* **GLM 5.2** (`zhipu/glm-5.2`): Robust function calling and API integration.
* **Qwen 3.7 Max** (`qwen/qwen-2.5-72b-instruct`): Advanced reasoning across complex data streams.

---

## 3. Pro Tier (10x Multiplier)

Frontier intelligence models for mission-critical risk management, dispute evaluation, and strategic planning:

* **GPT-5.6 Sol** (`openai/gpt-4o`): Frontier reasoning and strategic planning model.
* **Claude Opus 4.8** (`anthropic/claude-3-opus`): Highest-capability model for complex problem solving.
* **Gemini 3.1 Pro** (`google/gemini-1.5-pro`): Million-token context window for exhaustive document and codebase analysis.
* **DeepSeek V4 Pro** (`deepseek/deepseek-r1`): State-of-the-art coding, quantitative analysis, and formal logic.
* **Grok 4.5** (`x-ai/grok-2-1212`): Real-time analysis and autonomous market reasoning.

---

## Resilient Fallback Engine

All platform model calls route through an intelligent fallback engine. If a specific provider endpoint experiences downtime or latency spikes, the runtime automatically routes requests through **`stealth/ox-alpha`**, ensuring zero interruption to the agent's scheduled tick loop.
