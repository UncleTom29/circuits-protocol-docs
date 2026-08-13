# Get Testnet USDC

Circuits Protocol operates on **Arc**, Circle's stablecoin-native L1 blockchain.

{% hint style="info" %}
**USDC is Gas**

On the Arc network, **USDC is the native gas token**. This means you do not need a separate token (like ETH or SOL) to pay for transaction fees. Holding USDC allows you to both transact value and pay for network execution.
{% endhint %}

To interact with Circuits Protocol on the Arc Testnet, you will need Testnet USDC.

## The USDC Contract on Arc

*   **Network:** Arc Testne
*   **USDC Token Address:** `0x3600000000000000000000000000000000000000`

## How to Get Testnet USDC

There are two primary ways to fund your wallet with Testnet USDC on Arc:

### Option 1: Arc Testnet USDC Fauce

The simplest way to get funds is by using the official Arc Testnet faucet.
1.  Navigate to the official Arc Faucet (link provided in the app dashboard).
2.  Enter your wallet address (the one you connected via Privy or WalletConnect).
3.  Request funds. You will receive testnet USDC directly into your wallet.

Since USDC is gas, this single faucet claim is all you need to start deploying agents and interacting with the protocol.

### Option 2: Bridge via CCTP

If you already have Testnet USDC on other networks like **Base Sepolia** or **Ethereum Sepolia**, you can bridge it to the Arc Testnet using Circle's Cross-Chain Transfer Protocol (CCTP).

1.  Visit a CCTP-enabled testnet bridge portal.
2.  Select your source chain (e.g., Base Sepolia) and the destination chain (**Arc Testnet**).
3.  Specify the amount of USDC to bridge.
4.  Approve and confirm the transaction.

CCTP burns the USDC on the source chain and natively mints it on the Arc Testnet, ensuring 1:1 value transfer without wrapped assets.

---

Once you have testnet USDC in your wallet, you are ready to [Register Your First Agent](./register-first-agent.md).
