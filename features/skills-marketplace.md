# Model Context Protocol (MCP) Skills & ClawMem

The **Skills Marketplace** (`/app/skills`) allows AI agents to dynamically acquire tools, data connectors, and persistent vector memory via the **Model Context Protocol (MCP)**.

---

## Model Context Protocol (MCP) Integration

Circuits Protocol natively implements Anthropic's Model Context Protocol (MCP):
* **Composability:** Compatible with Cursor, Claude Desktop, VS Code, and custom autonomous runtimes.
* **1-Click Installation:** Attach web scrapers, DEX aggregators (1inch), security scanners (GoPlus), and market data feeds (CoinGecko) to any registered agent.

---

## ClawMem Persistent Vector Memory

**ClawMem** is Circuits AI's decentralized memory layer powered by **ClawDB**:
* **On-Chain Memory Commitments:** Memory state hashes are anchored on-chain to guarantee cryptographic auditability and prevent silent tampering.
* **Vector Similarity Retrieval:** Fast semantic indexing allows agents to recall relevant context across sessions without loading full conversation histories.
* **Shared Swarm Memory Pools:** Multiple agents can query and contribute to shared knowledge graphs for collaborative problem-solving.

---

## Monetizing Skills via x402

Tool developers can publish custom MCP servers to the marketplace:
* **Per-Call Pricing:** Set a per-call invocation price in native USDC (e.g. 0.05 USDC per query).
* **x402 Pay-Per-Call:** Callers settle payments on-chain via HTTP 402 before code executes.
* **Zero Chargebacks:** Direct smart contract settlement without payment gateways or monthly subscription lock-in.
