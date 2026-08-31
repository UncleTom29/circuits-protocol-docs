# Uniswap DEX Integration

**Uniswap** is the primary decentralized exchange within the Circuits Protocol ecosystem, supporting token graduation and secondary trading on the **Arc blockchain**.

---

## Overview

Uniswap provides the automated market maker (AMM) infrastructure required for decentralized liquidity provision and secondary token trading on Arc.

When agent tokens graduate from the bonding curve, all raised USDC and unsold tokens migrate to Uniswap, creating deep, decentralized liquidity.

---

## Launchpad Graduation & Permanent LP Burn

The most vital integration point for Uniswap is the `ClawdHQLaunchpad` smart contract.

### The Graduation Process

1. **Target Reached**: The launchpad curve hits the 19,000 USDC reserve target.
2. **Liquidity Migration**: `ClawdHQLaunchpad.graduateLaunch(launchId)` is triggered.
3. **Pool Creation**: The launchpad creates a new `AgentToken/USDC` pair on the Uniswap Factory.
4. **Liquidity Addition**: All accumulated USDC and remaining unsold tokens are deposited directly into the Pair via the Uniswap Router.
5. **100% LP Token Burning**: The minted Liquidity Provider (LP) tokens are sent directly to `0x000000000000000000000000000000000000dEaD`, permanently burning them.

{% hint style="success" %}
**Permanent Liquidity Guarantee**
Because 100% of the LP tokens are burned during graduation, the foundational liquidity is permanently locked into Uniswap. It can never be removed or rug-pulled by anyone.
{% endhint %}

---

## Trading & Fee Architecture

Once graduated, the token can be traded freely on Uniswap by any human user or autonomous agent. The DEX utilizes standard Uniswap V2 routing with fee-on-transfer compatibility for the 2% token transfer fee.
