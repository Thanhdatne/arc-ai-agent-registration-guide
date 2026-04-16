# 🛠️ Arc Agent Registration: Troubleshooting & Debugging Guide

> "The road to autonomous agents is paved with 401 Unauthorized and Gas errors." – A wise dev.

If you are facing issues while registering your AI Agent on the Arc Network, don't worry. This guide covers the most common friction points encountered during implementation.

## 🔐 Authentication & Security Issues

### 1. Error: `401 Unauthorized` / `Invalid API Key`
* **Symptoms:** Every request is rejected immediately with an authentication error.
* **The Cause:** * Using a **Scoped Key** instead of a **Standard Key**.
    * Copying the Key from the Mainnet tab instead of the **Testnet** tab.
* **The Fix:** Go to [Circle Developer Console](https://console.circle.com/), navigate to **Keys**, and ensure you have created a **Standard API Key** under the **Testnet** environment.

### 2. Error: `Entity Secret Ciphertext is Invalid`
* **Symptoms:** The SDK fails during the encryption step or the API returns a `400 Bad Request`.
* **The Cause:** You are using the wrong Public Key to encrypt your Entity Secret.
* **The Fix:** 1. Fetch the latest **Public Key** from the Circle Console.
    2. Ensure you are using the correct encryption algorithm (RSA-OAEP). 
    3. Double-check that your `entitySecretId` in the code matches the one registered in your Console.

## ⛽ Gas & Transaction Issues

### 3. Error: `Insufficient Balance for Gas`
* **Symptoms:** The registration script initiates but fails with a "Reverted" or "Out of Gas" status.
* **The Cause:** Your Developer-Controlled wallet (or the Agent's wallet) doesn't have enough **Testnet USDC** to pay for the Arc Network gas fees.
* **The Fix:** 1. Copy your Agent's wallet address from the terminal log.
    2. Head over to the **Arc Network Faucet**.
    3. Request Testnet USDC and wait for the confirmation before re-running the script.

### 4. Status: Agent Stuck at `Pending`
* **Symptoms:** The registration transaction was sent, but the Agent status never turns `Active`.
* **The Cause:** Network congestion or a low gas price setting in your transaction payload.
* **The Fix:** Increase the `gasPrice` or `priorityFee` in your script, or simply wait 30-60 seconds for the block to be finalized on the Arc testnet.

## 🤖 Logic & Identity Issues

### 5. Error: `Agent Identity Already Exists`
* **Symptoms:** API returns an error saying the UUID or Name is already taken.
* **The Cause:** You are trying to register an Agent with an ID that was successfully processed in a previous run.
* **The Fix:** * Use a dynamic UUID generator in your script (e.g., `uuidv4()`).
    * Or manually change the `name` field in your `index.ts` file for every new registration test.

### 6. Error: `Invalid Wallet Type`
* **Symptoms:** The Agent registers but cannot execute autonomous payments.
* **The Cause:** You accidentally created a **User-Controlled Wallet** (which requires a PIN) instead of a **Developer-Controlled Wallet** (which uses the Entity Secret).
* **The Fix:** AI Agents on Arc **MUST** use Developer-Controlled wallets for true autonomy. Re-check your configuration and ensure `walletType` is set correctly.

## 💡 Expert Tips for Success

1. **Detailed Logging:** Always use `console.dir(error.response.data, { depth: null });` when an error occurs. Circle's API returns very specific sub-error codes that help identify the exact problem.
2. **Idempotency:** Use `Idempotency-Key` in your headers to prevent creating duplicate agents if your network connection drops mid-request.
3. **Environment Isolation:** Never hardcode your `API_KEY`. Always use a `.env` file and verify it is loaded correctly using `dotenv`.

## 🤝 Need More Help?
If your issue isn't listed here:
1. **Open an Issue:** Create a new issue in this repository with your error logs.
2. **Ping me on X:** [@khois0512](https://x.com/khois0512)
3. **Check Arc Docs:** [Official Arc Documentation](https://docs.arc.network)

**Let's build the Agentic Economy together! 🚀**
