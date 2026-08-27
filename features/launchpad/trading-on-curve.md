# Trading on the Curve

During the bonding curve phase, all token purchases and sales execute directly against the `ClawdHQLaunchpad.sol` smart contract on Arc.

---

## How to Buy Tokens (USDC $\rightarrow$ Token)

1. Open `/app/launchpad/[launchId]` in the web app.
2. Enter the amount of **USDC** you wish to spend (e.g., `25 USDC`).
3. The interface calculates your estimated token output based on the constant-product invariant ($x \cdot y = k$).
4. Adjust your **Slippage Tolerance** (e.g., 0.5%, 1%, 2.5%).
5. Click **Buy Tokens** and approve the USDC transaction.
6. The contract deducts the 2% trade fee, adds the net USDC to the curve's reserve ($x$), and transfers the purchased tokens to your wallet.

---

## How to Sell Tokens (Token $\rightarrow$ USDC)

1. On `/app/launchpad/[launchId]`, switch the trade tab to **Sell**.
2. Enter the token amount or click **Max** to select your entire balance.
3. The interface previews the exact USDC you will receive after deducting the 2% fee.
4. Click **Approve Token** (one-time allowance for `ClawdHQLaunchpad`), then click **Sell Tokens**.
5. The contract returns your tokens to the curve reserve ($y$) and transfers the net USDC directly into your wallet.

---

## Pricing Mechanics & Anti-Snipe Protection

* **Deterministic Spot Price**: The price at any block is the ratio of virtual USDC reserve to remaining token supply ($P = \frac{x}{y}$).
* **Zero Gas Volatility**: All trades and network fees settle purely in USDC on Arc.
* **Anti-Snipe Protection**: Buys during the initial launch window from non-creators incur an anti-snipe fee of 20%, deterring bot snipers and redirecting fees to the buyback reserve.
