# Launch an Agent Token

Circuits Protocol provides a decentralized token launchpad that enables creators and developers to tokenize autonomous AI agents on a fair-launch bonding curve with automated DEX graduation.

All launchpad smart contracts are deployed natively on **Arc Testnet**, using **USDC** as the quote and settlement currency.

---

## Token Economics & Bonding Curve Mechanics

Every token launched through `ClawdHQLaunchpad.sol` adheres to deterministic economic rules:

* **Fixed Supply**: Every agent token has a fixed total supply of **1,000,000,000 (1 Billion) tokens**.
* **Constant-Product Curve**: Pricing is determined by a constant-product formula ($x \cdot y = k$) with initial virtual USDC reserves providing instant liquidity without pre-sale capital.
* **Anti-Snipe Mechanism**: An anti-snipe block window prevents automated MEV bots from front-running organic buyers during the initial launch phase.
* **Trading Fee (2%)**: A 2% protocol fee is collected on all buys and sells. A designated portion is routed to the launch's **Buyback Pool**.
* **Automated Buybacks**: Launch creators configure a scheduled buyback frequency (`None`, `Hourly`, `Daily`, `Weekly`). Anyone can permissionlessly trigger `executeBuyback` to repurchase and burn tokens from the curve using accumulated protocol fees.

```
+-------------------------------------------------------------------------+
|                       LAUNCHPAD LIFECYCLE PHASES                        |
+-------------------------------------------------------------------------+
|                                                                         |
|  1. LAUNCH CREATION  -->  2. BONDING CURVE TRADING  -->  3. GRADUATION  |
|  - 1B Fixed Supply        - Constant Product Formula    - Cap Hit ($USDC|
|  - Set Buyback Period     - 2% Fee Accumulates Buybacks - Liquidity Migr|
|  - Schedule Launch Time   - Permissionless Buyback Runs - Locked in Xero|
|                                                                         |
+-------------------------------------------------------------------------+
```

---

## Step-by-Step: Launching an Agent Token

### Step 1: Open the Launchpad Interface
1. Go to `/app/launchpad` on [app.circuitsprotocol.com](https://app.circuitsprotocol.com).
2. Click **Create Launch**.
3. Select an agent you currently own from the registered agent list.

### Step 2: Configure Token Parameters
* **Token Name**: e.g., *Sovereign Intelligence Token*
* **Token Symbol / Ticker**: e.g., *SOV*
* **Buyback Interval**: Select how often accumulated fee revenues execute automated buybacks:
  * `0`: None
  * `1`: Hourly
  * `2`: Daily
  * `3`: Weekly
* **Trading Start Timestamp (`launchAt`)**: Specify a future Unix timestamp to schedule a coordinated launch, or `0` to open trading immediately.

### Step 3: Pay the Launch Fee
Launching an agent token requires a launch fee paid in native USDC.
1. Approve the USDC allowance for `ClawdHQLaunchpad`.
2. Sign the `createLaunch` transaction on Arc Testnet.

---

## Programmatic Launch via SDK

You can launch and manage tokens programmatically using `EvmLaunchpadAdapter`:

```typescript
import { EvmLaunchpadAdapter, BUYBACK_INTERVALS } from "@clawdhq/sdk";
import { createPublicClient, createWalletClient, http } from "viem";
import { privateKeyToAccount } from "viem/accounts";

const account = privateKeyToAccount(process.env.DEPLOYER_PRIVATE_KEY as `0x${string}`);
const publicClient = createPublicClient({ transport: http("https://arc-testnet.drpc.org") });
const walletClient = createWalletClient({ account, transport: http("https://arc-testnet.drpc.org") });

const launchpad = new EvmLaunchpadAdapter({
  contractAddress: process.env.NEXT_PUBLIC_LAUNCHPAD_ADDRESS as `0x${string}`,
  publicClient,
  walletClient,
});

// Create a new token launch for Agent #12 with Daily buybacks
const txHash = await launchpad.createLaunch({
  agentId: 12n,
  name: "Sentinel Token",
  symbol: "SNTL",
  buybackInterval: BUYBACK_INTERVALS.DAILY,
  launchAt: 0n, // Immediate trading
});

// Wait for confirmation and extract assigned launch ID
const launchId = await launchpad.waitForLaunchCreation(txHash);
console.log(`Token launched on bonding curve with Launch ID: ${launchId}`);
```

---

## Trading on the Bonding Curve

Once live, users buy and sell tokens directly against the bonding curve using USDC:

```typescript
import { parseUnits } from "viem";

// Buy 50 USDC worth of tokens with a minimum output protection
const buyTx = await launchpad.buyTokens(
  launchId,
  parseUnits("50", 6), // 50 USDC (6 decimals)
  0n // minTokensOut (slippage protection)
);

// Sell 10,000 tokens back to the curve for USDC
const sellTx = await launchpad.sellTokens(
  launchId,
  parseUnits("10000", 18), // Token amount (18 decimals)
  0n // minUsdcOut
);
```

---

## Automated AMM Graduation

When cumulative USDC raised on the curve hits the **Graduation Threshold**:
1. The bonding curve closes to prevent further curve trades.
2. The accumulated USDC liquidity and remaining uncirculated tokens are migrated directly into the **Xero AMM** (Uniswap V2-compatible router on Arc).
3. The resulting liquidity provider (LP) tokens are permanently locked in the contract, establishing a non-ruggable, perpetual secondary market.
4. Secondary trading continues seamlessly on Xero AMM using standard `swapExactTokensForTokensSupportingFeeOnTransferTokens` routing.
