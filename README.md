# 🤖 Arc AI Agent Registration Kit
> **A comprehensive developer kit for registering AI Agents on Arc Network. Featuring on-chain identity implementation, programmable wallet integration, and a detailed troubleshooting guide for the Agentic Economy.**

## 🧠 Why Agentic Identity?
Most AI Agents today are "trapped" in sandboxed environments, unable to interact with the real-world economy. By leveraging **Arc Network’s Identity Registry**, we are moving from **Passive Bots** to **Autonomous Financial Entities**.

This project isn't just about running a script; it's about solving the **Identity & Liquidity Paradox**:
1. **Identity:** How does an Agent prove it's a unique entity without a centralized ID?
2. **Liquidity:** How does an Agent pay for its own compute and settle transactions autonomously?

## 📋 Prerequisites
Before you begin, make sure you have:
1. **Circle Developer Console account:** Sign up at [console.circle.com](https://console.circle.com/).
2. **Standard API Key:** Created via `Keys` → `Create a key` → `Standard Key`.
3. **Registered Entity Secret:** Ensure your Entity Secret is registered in the Console `Config` section.
4. **Testnet USDC:** Ensure your dev-controlled wallet is funded for gas fees.
5. You need Node.js version 22 or later (check using the command `node -v`).

## 🏗️ Architecture Workflow
```mermaid
graph LR
    A[Agent Intent] --> B{Arc Registry}
    B --> C[Programmable Wallet Creation]
    C --> D[USDC Gas Sponsoring]
    D --> E[On-chain Active Status]
```
## 🚀 Getting Started
1. Installation

```mkdir erc8004-quickstart
cd erc8004-quickstart
npm init -y
npm pkg set type=module
npm pkg set scripts.start="tsx --env-file=.env index.ts"
npm install @circle-fin/developer-controlled-wallets viem
npm install --save-dev tsx typescript @types/node
```
2. Create a tsconfig.json file:

```
npx tsc --init
```


Delete everything and paste it in.
```
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "ESNext",
    "moduleResolution": "bundler",
    "strict": true,
    "types": ["node"]
  }
}
```
3. An API key created in the Console: Keys → Create a key → API key → Standard Key

4. Register Your Entity Secret
Install the SDK
```
npm install @circle-fin/developer-controlled-wallets --save
```
Create a generate-secret.ts file:
fill:
```
import { generateEntitySecret } from "@circle-fin/developer-controlled-wallets";

generateEntitySecret();
```
Run 
```
npx tsx generate-secret.ts
```
Create a register-secret.ts file:

fill:
```
import { registerEntitySecretCiphertext } from "@circle-fin/developer-controlled-wallets";

const response = await registerEntitySecretCiphertext({
  apiKey:
    "****_API_KEY:5bef73***************d000:89a4aa************************b09", // Change your API key
  entitySecret: "ecd4d5e33b8e***************************************c546", // change your entitySecret
  recoveryFileDownloadPath: "",
});
console.log(response.data?.recoveryFile);
```

Run:
```
npx tsx register-secret.ts
```

5. Setting environment variables `.env`

Create a `.env` file.

```
touch .env
```

Copy the Entity Secret (64 hexadecimal characters) and paste it into the `.env` file:

`CIRCLE_API_KEY=your_actual_api_key_here
CIRCLE_ENTITY_SECRET=paste_entity_secret_here`

6. Create developer-controlled wallets
