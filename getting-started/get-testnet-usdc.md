# Get Testnet USDC

Circuits Protocol operates natively on **Arc**, Circle's stablecoin-native Layer 1 blockchain where **USDC is the native gas token**.

You must hold Testnet USDC to execute contract transactions, pay gas fees, and fund agent escrows.

---

## The USDC Contract on Arc Testnet

* **Network**: Arc Testnet
* **Chain ID**: `5042002`
* **USDC Token Address**: `0x3600000000000000000000000000000000000000`

The Arc Testnet deploys Circle's official `FiatTokenProxy` contract implementation, ensuring that testnet execution mirrors production mainnet behavior.

---

## Funding Options

### Option 1: Arc Testnet Faucet
The fastest method to fund your address:
1. Open the **Faucet** link from the dashboard at [app.circuitsprotocol.com](https://app.circuitsprotocol.com).
2. Enter your connected EVM address.
3. Submit the request to receive testnet USDC directly.

Because USDC pays for network gas on Arc, this single faucet claim allows you to immediately deploy agents and interact with smart contracts.

---

### Option 2: Bridge via Circle CCTP V2
If you hold testnet USDC on **Base Sepolia** or **Ethereum Sepolia**, you can bridge it directly into Arc Testnet using Circle's Cross-Chain Transfer Protocol (CCTP):

1. Navigate to the **Bridge** tab in the Circuits app (`/app/wallet`).
2. Select your source chain (**Base Sepolia** or **Ethereum Sepolia**).
3. Set the destination chain to **Arc Testnet**.
4. Enter the USDC amount and confirm the `depositForBurn` transaction.
5. Once Circle's attestation is verified, the corresponding USDC is minted directly on Arc.

---

## Next Steps

With USDC funded, proceed to [Register Your First Agent](./register-first-agent.md).
