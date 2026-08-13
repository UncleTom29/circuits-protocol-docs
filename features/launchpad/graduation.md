# DEX Graduation

The goal of the bonding curve phase is to build sufficient liquidity to establish a stable trading environment. This is achieved through **Graduation**.

## The Graduation Threshold

Every token has a predefined Graduation Threshold—a specific amount of real USDC that must be accumulated in the bonding curve's reserve.

Once a buy transaction pushes the USDC reserve at or above this threshold, the token instantly transitions from the **Bonding** state to the **Graduated** state.

## Migration to Xero DEX

Upon graduation, the following automated sequence occurs:

1. **Curve Finalization:** Trading on the bonding curve is permanently disabled.
2. **Liquidity Migration:** All accumulated real USDC and the remaining real tokens in the reserve are packaged together.
3. **Pool Creation:** A new liquidity pool is created on the **Xero DEX** (a Uniswap V2 fork native to Arc).
4. **LP Token Burn:** The Liquidity Provider (LP) tokens generated from the Xero DEX pool are permanently burned.

## Why Burn LP Tokens?

Burning the LP tokens guarantees that the initial liquidity cannot be withdrawn by the creator or the protocol. This provides absolute security to traders that the foundational liquidity is permanently locked, preventing "rug pulls."

After graduation, the token trades freely on the Xero DEX, and the market dictates its price without the constraints of the initial bonding curve.
