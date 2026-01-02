# 🪬 Consult Oracle

The AI-powered token analysis tool for $BASEDBOT holders.

{% hint style="info" %}
**Access Requirements**

* 🔐 **Basic Access:** Hold any amount of $BASEDBOT tokens
* 🦍🐳 **PRO Report:** Based Ape (1M+) or Whale (10M+) tier holders
{% endhint %}

## What is Consult Oracle?

Consult Oracle is BasedBot's on-chain intelligence system. Paste any Solana token contract address (CA) and receive an instant AI-powered analysis including:

* **Raidability Score** (0-100)
* **Safety Checks** (Mint/Freeze Authority status)
* **AI Verdict** (BasedBot's mystical assessment)

## 🎯 Basic Features (All Holders)

| Feature                  | Description                         |
| ------------------------ | ----------------------------------- |
| 📊 **Raidability Score** | 0-100 score indicating token safety |
| 🔒 **Mint Authority**    | Check if minting is disabled        |
| ❄️ **Freeze Authority**  | Check if freezing is disabled       |
| 🤖 **AI Verdict**        | Poetic assessment using Pro data    |

## 🦍 PRO Report Features (Ape & Whale Only)

PRO Report unlocks deep analytics that reveal what others can't see:

| Feature                      | Description                              |
| ---------------------------- | ---------------------------------------- |
| 🏥 **Holder Health**         | Fish/Dolphin ratio vs Whales             |
| 📈 **Holder Trend**          | 24h wallet growth/decline                |
| 🛡️ **Whale Risk**           | Penalty for high whale concentration     |
| ✅ **RugCheck Audit**        | External security audit integration      |
| 💰 **Market Data**           | Live price, market cap, 24h volume       |
| 👨‍💻 **Dev Holding (Grid)**  | Developer % shown in metrics grid        |
| 🎯 **Bundle Detection**      | Identifies coordinated wallet clusters   |

## 🧮 Trust Score Breakdown (New)

The Trust Score is now dynamic, reacting to live market behavior:

| Metric | Bonus/Penalty | Condition |
| :--- | :--- | :--- |
| **Base Score** | +50 pts | Starting score for all tokens |
| **Mint Authority Revoked** | +25 pts | Token supply cannot be inflated |
| **Freeze Authority Revoked** | +15 pts | Holders cannot be frozen |
| **Concentration Penalty** | -1 pt per % | Applied if Top 20 (excl LP) > 40% |
| **Holder Health** | ±5 pts | Based on Fish/Dolphin vs Whale ratio |
| **Holder Trend** | ±5 pts | Rewards growth >20 wallets, penalizes exodus |
| **Whale Risk** | +3 / -5 pts | Penalizes if >10 whales control supply |
| **RugCheck Audit** | ±10 pts | Boosts "Good" audits, penalizes "Danger" |
| **Token Age Penalty** | -15 pts | Applies if token is < 24 hours old |
| **Low Liquidity Penalty** | -10 pts | Applies if liquidity < $5,000 USD |

## 🚦 Risk Thresholds

### Holder Health Score

| Color    | Range | Status         | Effect |
| -------- | ----- | -------------- | ------ |
| 🟢 Green | ≥ 60% | Healthy        | +5 Pts |
| ⚪ Gray  | 40-59%| Neutral        | 0 Pts  |
| 🔴 Red   | < 40% | Whale Dominated| -5 Pts |

### 24h Holder Trend

| Color    | Range        | Status    | Effect |
| -------- | ------------ | --------- | ------ |
| 🟢 Green | > +20 wallets| Growth    | +5 Pts |
| ⚪ Gray  | ±20 wallets  | Stable    | 0 Pts  |
| 🔴 Red   | < -20 wallets| Dumping   | -5 Pts |

### Top 10 Holders % (Concentration)

| Color    | Range  | Risk Level               |
| -------- | ------ | ------------------------ |
| 🟢 Green | < 20%  | Healthy distribution     |
| 🟡 Amber | 20-35% | Moderate concentration   |
| 🔴 Red   | > 35%  | High centralization risk |

### Developer Holdings %

| Color    | Range | Risk Level            |
| -------- | ----- | --------------------- |
| 🟢 Green | < 2%  | Fair launch standard  |
| 🟡 Amber | 2-5%  | Acceptable allocation |
| 🔴 Red   | > 5%  | High dump risk        |

## 🔧 How It Works

{% stepper %}
{% step %}
### Connect Wallet

Connect your Solana wallet containing $BASEDBOT.
{% endstep %}

{% step %}
### Paste CA

Enter any Solana token contract address.
{% endstep %}

{% step %}
### Analyze

The Oracle scans on-chain data in real-time.
{% endstep %}

{% step %}
### Review

Read the verdict and PRO metrics (if eligible).
{% endstep %}
{% endstepper %}

## 🛠️ Technical Details

The Oracle integrates multiple data sources for comprehensive analysis:

| Source | Data Provided |
| --- | --- |
| **HolderScan API** | Holder distribution, trends, whale counts |
| **RugCheck API** | Security audits, risk flags |
| **Solana RPC** | Authority checks, supply data |
| **Bundle Analysis** | Coordinated wallet detection |

### 🔄 Loading Bar

A synchronized progress bar tracks the analysis in real-time:
-   **0-90%**: Simulates processing speed based on data complexity.
-   **100%**: Snaps to completion when results are ready.

### 💡 Tips

*   **41.7% != 28.33%?** - The Oracle excludes LP/bonding curve addresses from concentration calculations.
*   **Trend 0?** - Small fluctuations (<20 wallets) are considered neutral.
*   **Slow Analysis?** - High-activity tokens require deeper chain traversal.

## 🌐 Network

| Property            | Value                         |
| ------------------- | ----------------------------- |
| 🌐 **Analytics**    | Solana Mainnet                |
| 🎮 **dApp**         | Solana Mainnet                |

{% hint style="warning" %}
**Disclaimer**

The Oracle provides on-chain data analysis only. This is NOT financial advice. Always DYOR (Do Your Own Research) before trading.
{% endhint %}
