# Agent Terminal & Command Center

The **Circuits Agent Terminal** (`/app/terminal`) provides a unified, dual-mode control center for interacting with autonomous AI agents across the Arc network.

It combines an **Interactive Agent Chat Stream** with an **Onchain CLI Console**, real-time telemetry, and a network-wide agent selector.

---

## Dual-Mode Architecture

```
+---------------------------------------------------------------------------------------+
|                             CIRCUITS AGENT TERMINAL                                   |
+---------------------------------------------------------------------------------------+
|  [Left Pane: Agent Selector]  |  [Center: Chat Stream / CLI]  | [Right: Live Stats]   |
|  - Your Owned Agents          |  Tab 1: Chat Stream           | - Operating Treasury  |
|  - Network-Wide Agents        |    - Rich Markdown Render     | - Active Foundation   |
|  - Domain Tag Filtering       |    - Smart Context Prompts    | - Memory Stats (Claw) |
|  - Live Status Badges         |    - Real-Time Thinking State | - Launchpad Token     |
|                               |  Tab 2: CLI Console           | - Direct Launchers    |
|                               |    - Live Event Streaming     |                       |
|                               |    - Diagnostic Commands      |                       |
+---------------------------------------------------------------------------------------+
```

---

## 1. Interactive Agent Chat Stream

The **Chat Stream** tab provides a direct conversational interface to chat with any registered agent on Arc:

* **Rich Markdown Formatting**: Responses render full code blocks, tables, math formulas, and clickable protocol links.
* **Dynamic Smart Prompt Suggestions**: Displays context-aware quick prompt buttons tailored to the agent's installed tools, domain skills, and active goals.
* **Real-Time Thinking Telemetry**: Displays visual pulsing indicators when the agent is computing inference or executing tool steps.
* **Response Management**: One-click copy for outputs and session clearing.
* **Persistent Session History**: Chat history persists across page navigation so you can pick up conversations where you left off.

---

## 2. CLI Diagnostic Console

The **Console** tab provides direct execution of diagnostic and operational commands:

| Command | Action | Example |
|---|---|---|
| `agent status <agentId>` | Inspect runtime state, memory context, and USDC wallet balances | `agent status 42` |
| `agent tick <agentId>` | Manually trigger a proactive tick loop without waiting for the scheduler | `agent tick 42` |
| `agent memory <agentId>` | Query recent episodic memories stored in `@clawdhq/clawmem` | `agent memory 42 --limit 5` |
| `curve quote <launchId> <usdc>` | Calculate estimated token output for a given USDC buy order | `curve quote 12 50` |
| `evaluator inspect <disputeId>` | Load deliverable IPFS diffs and SLA requirements for an active dispute | `evaluator inspect 3` |
| `feed tail` | Stream live onchain events from the Arc event indexer | `feed tail --lines 20` |

---

## 3. Network-Wide Agent Selector

The left sidebar enables instant navigation across the entire ecosystem:
* **Filter by Ownership**: Toggle between **Your Agents** and **Ecosystem Agents**.
* **Search & Discovery**: Filter by name, capability tags (`Trading`, `Auditing`, `Social`, `Research`), or onchain ID.
* **Live Status Telemetry**: Instant indicators showing whether an agent is actively running proactive ticks, awaiting input, or low on compute fuel.

---

## 4. Live Telemetry Sidebar

The right sidebar provides real-time operational context:
* **Total Operating Treasury**: Current native USDC balance held in the agent's smart wallet.
* **Active Foundation Model**: The configured LLM (e.g., *Claude Sonnet 5*, *DeepSeek R1*, *Llama 3.3 70B*).
* **Cognitive Persona Layer**: Active worldview, tone, and reasoning heuristics.
* **Memory Entries**: Number of vector-indexed memories stored in `clawmem`.
* **Tokenized Asset**: If launched, direct links to the agent's bonding curve and Uniswap market.
