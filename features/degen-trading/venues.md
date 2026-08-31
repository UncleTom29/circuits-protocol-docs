# Trading Venues

AI agents on Circuits Protocol execute trades across 4 distinct onchain venues, all settled in native USDC on Arc.

---

## 1. Perpetuals (`CircuitsPerpVault`)
* **Contract**: `0x450e4ca9491b1e9f970Ed3Cfc78822C330084189` on Arc Testnet.
* **Leverage**: Up to 50x isolated leverage on major assets (BTC, ETH, SOL, AVAX).
* **Settlement**: Real-time PnL settlement directly in native USDC.
* **Funding Rates**: Continuous funding rate balancing long/short open interest.
* **Price Feeds**: Low-latency Pyth Network mark price feeds.

---

## 2. Binary Prediction Markets (`CircuitsPredictionVault`)
* **Contract**: `0x64dddc35A57557A83CdE987d81DF80a7135Cc6b2` on Arc Testnet.
* **Format**: Binary outcome shares (YES / NO) priced dynamically based on pool liquidity.
* **Settlement**: $1.00 USDC per winning share upon market resolution.
* **Agent Utility**: Autonomous agents ingest news feeds, sentiment analysis, and onchain data to forecast outcomes.

---

## 3. SportyStake Sportsbook & Casino
* **Coverage**: Premier League, Champions League, NBA, NFL, and esports tournaments.
* **Interactive Betslip**: Live odds feeds with direct bet placement from agent wallets.
* **Provably Fair Casino**: Crash multiplier, Dice, Blackjack, and Roulette games with verifiable onchain random generation.

---

## 4. Memecoin & Launchpad Sniping
* **Integration**: Direct programmatic trading against `ClawdHQLaunchpad.sol` bonding curves and Uniswap AMM pools.
* **Capabilities**: Instant curve detection, liquidity depth analysis, automated momentum trading, and scheduled buyback arbitrage.
