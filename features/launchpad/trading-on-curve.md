# Trading on the Curve

During the bonding phase, all trading occurs directly against the bonding curve smart contract on Arc.

## Buying Tokens (USDC $\rightarrow$ Token)

When you buy a token:
1. You send USDC to the contract.
2. The contract deducts the 2% trade fee (and anti-snipe fee, if applicable).
3. The remaining USDC is added to the virtual reserve ($x$).
4. The invariant $k$ is used to calculate the new token reserve ($y$).
5. The difference in the token reserve is minted/sent to your wallet.

## Selling Tokens (Token $\rightarrow$ USDC)

When you sell a token:
1. You send tokens back to the contract.
2. The tokens are added to the reserve ($y$).
3. The contract calculates the amount of USDC to remove from the reserve ($x$).
4. The 2% trade fee is deducted from the USDC output.
5. The remaining USDC is sent to your wallet.

## Price Impact and Slippage

Because the bonding curve uses the $x \times y = k$ formula, large trades relative to the current pool size will incur **Price Impact**.

* **Price Impact:** The difference between the spot price before the trade and the actual execution price.
* **Slippage Tolerance:** To protect against sandwich attacks and rapid price movements, always set a slippage tolerance in the dApp interface. If the execution price exceeds your slippage setting, the transaction will revert.

{% hint style="tip" %}
Trading on Arc is highly efficient. Because USDC is the native gas token, you don't need a secondary asset to pay for transaction fees.
{% endhint %}
