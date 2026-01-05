# 🔌 Oracle API Documentation

Integrate Consult Oracle into your project using the x402 protocol or $BASEDBOT token-gating.

## Base URL

```
https://raid.based-bot.fun/api/oracle/v1/analyze
```

## Authentication Methods

The Oracle API supports two authentication methods. **x402 Payment takes priority** - if a payment is provided, wallet signature is not required.

| Method | Headers Required | Description |
| :--- | :--- | :--- |
| **x402 Payment** | `X-PAYMENT` | Pay-per-use with USDC (recommended for integrations) |
| **Token Gate** | `X-WALLET` + `X-WALLET-SIG` + `X-CHALLENGE-TOKEN` | Free for $BASEDBOT holders |

---

## Method 1: x402 Payment (Recommended)

For pay-per-use access, no wallet signature is needed. Just pay with USDC.

### Pricing
- **Basic Analysis:** 0.05 USDC
- **PRO Report:** 0.10 USDC

### The x402 Flow
1. Make a request without payment → receive `402 Payment Required`
2. Sign a USDC transfer transaction (do NOT broadcast)
3. Encode the signed TX in the `X-PAYMENT` header
4. Retry the request → receive analysis result

```bash
# Step 1: Get payment requirements
curl "https://raid.based-bot.fun/api/oracle/v1/analyze?ca=TOKEN_ADDRESS"
# Returns 402 with payment details

# Step 2: After signing USDC transfer
curl "https://raid.based-bot.fun/api/oracle/v1/analyze?ca=TOKEN_ADDRESS" \
  -H "X-PAYMENT: BASE64_ENCODED_PAYMENT"
```

---

## Method 2: Token Gate (Free for Holders)

$BASEDBOT holders get free access based on their tier. **Wallet ownership must be proven via challenge-response signature.**

### Tier Requirements

| Tier | Requirement | Access |
| :--- | :--- | :--- |
| 🐋 **Whale** | 10M+ $BASEDBOT | Free PRO + 100 req/min |
| 🦍 **Based Ape** | 1M+ $BASEDBOT | Free PRO + 10 req/min |
| 💎 **Diamond Hands** | 500K+ $BASEDBOT | Basic + 5 req/min |
| 🌱 **Seedling** | 100K+ $BASEDBOT | Basic + 5 req/min |
| 🎰 **Degen** | Any amount | Basic + 5 req/min |

### Challenge-Response Flow

To prevent wallet spoofing, you must prove ownership via signature:

```mermaid
sequenceDiagram
    participant Client
    participant API
    Client->>API: GET /challenge?wallet=ABC
    API-->>Client: { token, nonce, message }
    Client->>Client: Sign message with wallet
    Client->>API: GET /analyze + headers
    Note over Client,API: X-WALLET, X-WALLET-SIG, X-CHALLENGE-TOKEN
    API-->>Client: { analysis: ... }
```

### Step 1: Request Challenge
```bash
curl "https://raid.based-bot.fun/api/oracle/v1/challenge?wallet=YOUR_WALLET"
```

Response:
```json
{
  "success": true,
  "token": "eyABCDEF...",
  "nonce": "abc123...",
  "message": "Oracle API Access\nNonce: abc123...\nWallet: YOUR_WALLET",
  "expiresIn": 300
}
```

### Step 2: Sign the Message
Sign the `message` field with your Solana wallet (ed25519 signature), then base64 encode.

### Step 3: Send Signed Request
```bash
curl "https://raid.based-bot.fun/api/oracle/v1/analyze?ca=TOKEN_ADDRESS" \
  -H "X-WALLET: YOUR_WALLET" \
  -H "X-WALLET-SIG: BASE64_ENCODED_SIGNATURE" \
  -H "X-CHALLENGE-TOKEN: eyABCDEF..."
```

---

## Endpoints

### GET `/api/oracle/v1/challenge`

Generate a challenge for wallet signature verification. Returns a stateless token valid for 5 minutes.

| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `wallet` | string | Yes | Wallet address to verify |

### GET `/api/oracle/v1/analyze`

Analyze a Solana token contract address.

#### Query Parameters

| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `ca` | string | Yes | Token contract address |
| `pro` | boolean | No | Request PRO analysis |

#### Headers

| Header | Required | Description |
| :--- | :--- | :--- |
| `X-WALLET` | For token-gate | User wallet address |
| `X-WALLET-SIG` | If X-WALLET | Base64 signature of challenge message |
| `X-CHALLENGE-TOKEN` | If X-WALLET | Token received from challenge endpoint |
| `X-PAYMENT` | For x402 | Signed USDC payment (bypasses signature requirement) |

#### Example Requests

**Basic Analysis (x402 Payment):**
```bash
curl "https://raid.based-bot.fun/api/oracle/v1/analyze?ca=TOKEN_ADDRESS" \
  -H "X-PAYMENT: BASE64_SIGNED_TX"
```

**PRO Report (x402 Payment):**
```bash
curl "https://raid.based-bot.fun/api/oracle/v1/analyze?ca=TOKEN_ADDRESS&pro=true" \
  -H "X-PAYMENT: BASE64_SIGNED_TX"
```

**Token-Gate Request (requires signature):**
```bash
curl "https://raid.based-bot.fun/api/oracle/v1/analyze?ca=TOKEN_ADDRESS" \
  -H "X-WALLET: YOUR_WALLET" \
  -H "X-WALLET-SIG: BASE64_SIGNATURE" \
  -H "X-CHALLENGE-TOKEN: TOKEN_FROM_CHALLENGE"
```

---

## Response Schemas

### Basic Analysis Response

```json
{
  "success": true,
  "tier": "Pay-per-use",
  "analysis": {
    "score": 85,
    "verdict": "Looking pretty based, ser.",
    "safety": {
      "mintAuthorityDisabled": true,
      "freezeAuthorityDisabled": true,
      "topHoldersSafe": true,
      "topHoldersPercent": 15.2
    },
    "tokenInfo": {
      "name": "Example Token",
      "symbol": "EX",
      "supply": "1000000000",
      "decimals": 6
    },
    "holderCount": 5420
  }
}
```

### PRO Report Response (0.10 USDC or 1M+ $BASEDBOT)

PRO includes everything in Basic, plus deep analytics:

```json
{
  "success": true,
  "tier": "Based Ape",
  "proAccess": true,
  "analysis": {
    "score": 85,
    "verdict": "The oracle sees strength in this one...",
    "safety": {
      "mintAuthorityDisabled": true,
      "freezeAuthorityDisabled": true,
      "topHoldersSafe": true,
      "topHoldersPercent": 15.2
    },
    "tokenInfo": {
      "name": "Example Token",
      "symbol": "EX",
      "supply": "1000000000",
      "decimals": 6
    },
    "holderCount": 5420,
    "scoreBreakdown": {
      "base": 50,
      "mintAuthority": 25,
      "freezeAuthority": 15,
      "concentration": -5,
      "holderHealth": 5,
      "holderTrend": 3,
      "whaleRisk": 0,
      "rugCheckBonus": 10,
      "tokenAgePenalty": 0,
      "liquidityPenalty": 0,
      "bundlePenalty": -10,
      "devHoldingPenalty": -3,
      "total": 90
    },
    "holderStats": {
      "topHolders": [
        { "address": "ABC...", "percent": 5.2, "isLP": true },
        { "address": "DEF...", "percent": 3.1 }
      ],
      "whaleCount": 3,
      "lpCount": 2,
      "concentration": 18.5,
      "concentrationExcludingLP": 12.3,
      "priceUsd": "0.0042",
      "marketCap": "4200000",
      "volume24h": "150000",
      "priceChange24h": 12.5,
      "developerHolding": {
        "address": "GHI...",
        "percent": 2.1,
        "found": true
      },
      "bundleAnalysis": {
        "isBundled": true,
        "bundleSize": 5,
        "holdingPercent": 8.3,
        "funderAddress": "JKL..."
      },
      "whaleActivity": {
        "status": "Accumulating",
        "netChange": 2.5,
        "txCount": 12
      },
      "rugCheck": {
        "score": 85,
        "rating": "Good",
        "risks": []
      },
      "holderDeltas": {
        "h24": 120,
        "d7": 450
      }
    }
  }
}
```

---

## Error Codes

| Code | Error | Description |
| :--- | :--- | :--- |
| 400 | Invalid address | Contract address format is invalid |
| 401 | Signature required | Missing wallet signature for token-gate |
| 401 | Invalid token | Challenge token expired or invalid |
| 402 | Payment required | Need x402 payment or token holdings |
| 429 | Rate limit exceeded | Wait for rate limit reset |
| 500 | Internal error | Server-side issue |

## CORS

The API supports CORS for browser-based integrations. Preflight (`OPTIONS`) requests are handled automatically.

---

## Integration Guide

Choose your integration method based on your use case:

| Use Case | Recommended Method | UI Needed? |
| :--- | :--- | :--- |
| **Telegram/Discord Bot** | x402 Payment | ❌ No |
| **Backend API Service** | x402 Payment | ❌ No |
| **Frontend dApp** | Token-Gate | ✅ Yes (wallet popup) |
| **CLI Tool** | x402 Payment | ❌ No |

### For Bots & Backend Services (x402)

No UI required. Sign USDC transactions programmatically:

```javascript
// Node.js example
import { Keypair, Connection } from '@solana/web3.js';

const keypair = Keypair.fromSecretKey(YOUR_PRIVATE_KEY);
// 1. Call /analyze without payment → get 402 with payment details
// 2. Sign USDC transfer to treasury (do NOT broadcast)
// 3. Retry with X-PAYMENT header containing base64 encoded signed tx
```

### For Frontend dApps (Token-Gate)

Requires wallet-adapter UI for user to sign challenge:

```javascript
// React example with wallet-adapter
const { publicKey, signMessage } = useWallet();

// 1. Fetch challenge: GET /challenge?wallet=...
// 2. User signs message via wallet popup
// 3. Send all 3 headers: X-WALLET, X-WALLET-SIG, X-CHALLENGE-TOKEN
```

---

{% hint style="info" %}
**Integration Support**
Need help integrating? Find us on [Twitter/X](https://x.com/basedbotsol).
{% endhint %}
