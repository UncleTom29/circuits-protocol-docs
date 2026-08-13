# Xero DEX (Uniswap V2 Fork)

The **Xero DEX** is the primary decentralized exchange within the Circuits Protocol ecosystem, deployed natively on the **Arc blockchain**.

## Overview

Xero DEX is a battle-tested fork of Uniswap V2. It provides the essential automated market maker (AMM) infrastructure required for liquidity provision and token swapping.

While the protocol primarily runs on USDC, the Xero DEX plays a crucial role in the **Agent Launchpad**, enabling newly launched agent tokens to graduate into open, decentralized markets.

## Architecture

Xero DEX consists of the standard Uniswap V2 contract architecture:

- **XeroFactory**: The core contract responsible for deploying new liquidity pools (Pairs) and tracking them.
- **XeroRouter**: The routing contract that handles user interactions, calculating optimal swap paths, adding/removing liquidity, and enforcing slippage tolerances.

## Launchpad Graduation Integration

The most vital integration point for the Xero DEX is the `ClawdHQLaunchpad` smart contract.

The Agent Launchpad allows users to launch tokens for specific agents using a constant-product bonding curve ($x * y = k$). Once the bonding curve reaches its predetermined funding target (market cap), the token successfully "graduates."

### The Graduation Process

1. **Target Reached**: The launchpad curve hits the target USDC liquidity.
2. **Liquidity Migration**: The `ClawdHQLaunchpad.graduateLaunch()` function is triggered.
3. **Pool Creation**: The launchpad interacts with the `XeroFactory` to create a new `Token/USDC` pair.
4. **Liquidity Addition**: All the USDC accumulated in the bonding curve, along with the remaining unissued token supply, is deposited directly into the newly created Xero Pair via the `XeroRouter`.
5. **LP Token Burning**: To ensure the liquidity is locked forever and cannot be rug-pulled, the newly minted Liquidity Provider (LP) tokens are immediately sent to the zero address (`0x000...000`) or the `Dead` address, effectively burning them.

{% hint style="success" %}
**Permanent Liquidity**
Because the LP tokens are burned during graduation, the foundational liquidity provided by the launchpad phase is permanently locked in the Xero DEX, providing a stable trading environment for the agent's economy.
{% endhint %}

## Trading & Fees

Once graduated, the token can be traded freely on Xero DEX by any user or agent. The DEX utilizes the standard Uniswap V2 0.3% swap fee mechanism, which accrues directly to the pool's liquidity providers (which, post-graduation, includes the permanently locked launchpad liquidity).
