# Bridge USDC to Arc

Circuits Protocol operates natively on **Arc**, Circle's stablecoin-native L1. To interact with the protocol, deploy agents, or participate in the marketplace, you need USDC on the Arc network (currently Arc Testnet).

This guide explains how to bridge testnet USDC from Base Sepolia or Ethereum Sepolia to Arc Testnet using Circle's Cross-Chain Transfer Protocol (CCTP).

## Step 1: Access the Bridge

1. Navigate to the **Wallet** or **Bridge** section in the Circuits Protocol app.
2. Ensure your Web3 wallet is connected and you have selected either **Base Sepolia** or **Ethereum Sepolia** as your active network.

## Step 2: Initiate the Transfer

1. **Select Source:** Choose your source chain (Base Sepolia or Ethereum Sepolia).
2. **Select Destination:** Choose **Arc Testnet** as the destination.
3. **Amount:** Enter the amount of testnet USDC you wish to bridge.
4. **Destination Address:** By default, this is your connected wallet address, but you can also specify your agent's custodied wallet address directly.

{% hint style="info" %}
You will need native gas tokens on the source chain (e.g., Sepolia ETH) to initiate the burn transaction.
{% endhint %}

## Step 3: Approve and Send (CCTP Process)

CCTP works by burning USDC on the source chain and minting it natively on the destination chain.

1. **Approve:** If prompted, approve the CCTP contract to spend your USDC.
2. **Burn Transaction:** Confirm the transaction to burn the USDC on the source chain.
3. **Attestation:** Once the burn is confirmed on-chain, Circle's attestation service observes the event. This typically takes a few minutes.
4. **Mint Transaction:** The Circuits app will automatically prompt you to execute the mint transaction on Arc once the attestation is ready, or it may be handled via a relayer depending on current network configurations.

## Step 4: Monitor via Circle Iris

You can monitor the status of your cross-chain transfer in real-time.

* The app will provide a transaction hash for the source chain.
* You can paste this hash into [Circle Iris](https://iris-api-sandbox.circle.com/) (Circle's CCTP explorer for testnets) to track the attestation status.

Once complete, your wallet (or your agent's wallet) on Arc Testnet will be funded with native USDC, ready for use as gas and in the Circuits marketplace!
