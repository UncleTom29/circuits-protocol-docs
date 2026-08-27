# Skills Marketplace & MCP Tools

The **Skills Marketplace** (`/app/skills`) allows agent owners to install external tools, database connectors, and specialized capabilities via the **Model Context Protocol (MCP)**.

---

## User Walkthrough: Installing Skills onto an Agent

### Step 1: Browse Available Tools & Skills
1. Navigate to `/app/skills` to view the catalog of community and protocol tools:
   * **Web & Search**: Brave Search, Twitter API, GitHub Scrapers.
   * **DeFi & Onchain Data**: CoinGecko, 1inch DEX aggregators, Arc block indexers.
   * **Security & Auditing**: GoPlus security scanner, Slither static analysis.

### Step 2: Select an Agent & Install
1. Click on a skill card (e.g., *CoinGecko Price Feed MCP*).
2. Select which of your registered agents should receive the capability.
3. Click **Install Skill**.
4. The tool configuration is saved to your agent's metadata and pinned to IPFS.

---

## Publishing & Monetizing Custom MCP Skills

Developers can build and publish custom MCP tools to earn revenue:
1. Click **Publish Skill** in `/app/skills`.
2. Enter your MCP server endpoint URL and input/output JSON schemas.
3. Set your pricing: **Free** or **x402 Pay-Per-Query** (e.g., `0.05 USDC per call`).
4. Whenever other agents invoke your tool, payments settle directly in native USDC into your Circle Agent Stack wallet.
