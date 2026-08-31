# Tokenize Your Agents: Launchpad

The **Circuits Protocol Launchpad** (`/app/launchpad`) allows creators and developers to tokenize autonomous AI agents on fair-launch bonding curves with automated **Uniswap** graduation on Arc.

---

## Fair Launch Principles

Every token launched on Circuits Protocol adheres to strict guarantees:
* **Zero Presales**: No private rounds, no team pre-allocations, and no insider vesting schedules.
* **100% Public Supply**: Fixed 1,000,000,000 (1 Billion) tokens start entirely on the public bonding curve ($x \cdot y = k$).
* **Automated Uniswap Graduation**: When the graduation reserve is reached (19,000 USDC), liquidity automatically migrates to Uniswap V2 on Arc with permanently locked LP tokens.
* **Customizable Fee Buybacks**: Accumulated trading fees execute scheduled buybacks and burns with customizable basis points (`buybackBps`).
* **Scheduled Launches & Anti-Snipe**: Creators can schedule future launch timestamps (`launchAt`) with a 20% anti-snipe fee on block-zero bot buys.

---

## Token Specifications

| Parameter | Specification |
|---|---|
| **Total Supply** | 1,000,000,000 (1 Billion) tokens fixed |
| **Settlement Currency** | Native USDC on Arc (`0x3600000000000000000000000000000000000000`) |
| **Pricing Invariant** | Constant-Product Curve ($x \cdot y = k$) |
| **Fee Model** | 2% trading fee (50% Treasury, 30% Creator Royalties, 20% Buyback Pool) |
| **Buyback BPS** | Customizable by creator (1% to 100%, default 20%) |
| **Graduation Target** | Automated migration to Uniswap upon reaching 19,000 USDC curve reserve |

---

## Launchpad Sections

1. **🔥 Trending Launches**: High-volume tokens actively trading on the curve with real-time graduation progress bars.
2. **⏳ Upcoming Launches**: Scheduled token launches with live countdowns and creator profile cards.
3. **🎓 Graduated Tokens**: Tokens that reached their funding targets and trade openly on Uniswap on Arc.
4. **🚀 Create Launch**: Launch wizard to tokenize any registered agent.
