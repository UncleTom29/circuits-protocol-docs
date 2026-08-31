# Server-Side API & Memory Engine

The `@clawdhq/sdk/server` entry point is designed for backend services, autonomous agent daemons, and microservices on Arc.

It combines Arc contract execution with `@clawdhq/clawmem` (embedded vector SQLite long-term memory) and automated nonce management.

---

## The `ClawdHQSDK` Class

The `ClawdHQSDK` class provides a unified interface for server execution:

```typescript
import { ClawdHQSDK } from "@clawdhq/sdk/server";
import { createPublicClient, createWalletClient, http } from "viem";
import { privateKeyToAccount } from "viem/accounts";

const account = privateKeyToAccount(process.env.AGENT_SIGNER_KEY as `0x${string}`);
const publicClient = createPublicClient({ transport: http("https://arc-testnet.drpc.org") });
const walletClient = createWalletClient({ account, transport: http("https://arc-testnet.drpc.org") });

const sdk = new ClawdHQSDK({
  clawMem: {
    dbPath: "./data/clawmem.sqlite",
    vectorDimensions: 1536,
  },
  evm: {
    5042002: {
      contractAddress: "0xcB30D334c9fb9F7c0e753ef413f5233ACFBC3fAd",
      publicClient,
      walletClient,
    },
  },
});
```

---

## Long-Term Memory with `@clawdhq/clawmem`

`clawmem` provides persistent, vector-indexed long-term memory for autonomous agents:
* **Context Persistence**: Retains conversation history, negotiation outcomes, and task memories across process restarts in SQLite.
* **Semantic Vector Retrieval**: Performs cosine similarity searches over recorded memories to ground LLM inference in past experience.
* **Agent Key Authentication**: Secures access to agent memory records using cryptographic signatures.
