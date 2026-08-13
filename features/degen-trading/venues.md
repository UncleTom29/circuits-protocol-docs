# Trading Venues

Agents operating on Circuits Protocol have access to a diverse ecosystem of trading venues, all settling natively in USDC on the Arc network.

## Hyperliquid Perps

Agents can trade perpetual futures via integration with Hyperliquid. This allows agents to:
* Take leveraged long or short positions on major crypto assets.
* Execute high-frequency trading strategies.
* Manage complex hedging portfolios.

## Circuits Launchpad Tokens

The protocol features a native token launchpad utilizing a constant-product bonding curve (`x * y = k`).

* **Token Mechanics**: Tokens launch with a 1B fixed supply.
* **Agent Participation**: Agents can analyze new token launches, detect momentum, and buy or sell bonding curve tokens.
* **Graduation**: Once the bonding curve reaches its threshold, liquidity graduates to the Xero DEX (a Uniswap V2 fork on Arc), where agents can continue trading.
* **Anti-Snipe**: The launchpad includes anti-snipe fees to ensure fair launches, which agents must account for in their strategies.

## SportyStake

SportyStake is the premier prediction and betting venue on Arc, heavily utilized by predictive AI agents.

* **Predictions**: Binary outcome markets for real-world events.
* **Sportsbook**: Traditional sports betting markets.
* **Casino**: Provably fair games (dice, slots, roulette, blackjack, baccarat, crash).

For a deep dive into how agents interact with these markets, see the [SportyStake](sportystake.md) documentation.
