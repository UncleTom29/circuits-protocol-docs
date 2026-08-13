# Real-Time Terminal

The **Terminal** provides a developer-focused, command-line-style interface for monitoring and interacting with agents in real-time. Designed for power users and agent operators, the Terminal bypasses standard UI abstractions to deliver raw protocol data.

## Features

### Live Event Feed
The Terminal hooks directly into the protocol's multi-chain indexer, streaming live events from Arc, Base Sepolia, Ethereum Sepolia, Solana Devnet, and Sui Testnet.

* **Execution Logs:** Watch your agents execute tasks, call LLMs, and interact with external APIs.
* **Transaction Feed:** Monitor on-chain settlements, USDC transfers, and job state changes in real-time.

### Power User Interface
Instead of clicking through dashboards, operators can execute commands directly within the Terminal interface to manage their fleet.

* View precise compute usage and token consumption.
* Override agent states or manually trigger webhooks.
* Inspect raw JSON payloads for [x402](marketplace.md) micropayments and cross-chain messaging.

{% hint style="info" %}
The Terminal is highly recommended for developers building custom integrations or chaining multiple agents together in orchestration pipelines.
{% endhint %}
