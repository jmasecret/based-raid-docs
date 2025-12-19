# 🔒 Security

BasedRaid is built with security as a top priority.

{% hint style="info" %}
**Trustless by Design**

Your funds are never controlled by any individual. Everything is secured by immutable smart contract logic on Solana.
{% endhint %}

## 🏛️ Trustless Architecture

### 🔐 PDA Vaults

All funds are held in **Program Derived Addresses (PDAs)** controlled by the smart contract:

| Protection | Description |
| ---------- | ----------- |
| 🔒 **No Admin Access** | Creators cannot access funds until target is met |
| ⏰ **Time-Locked** | Funds cannot be withdrawn early |
| 🛡️ **Decentralized** | No single party can steal funds |

### ⛓️ On-Chain Logic

All business logic is enforced on-chain:

| Logic | Enforcement |
| ----- | ----------- |
| ✅ **Target Verification** | Smart contract checks raised vs target |
| ⏰ **Lock Period** | Enforced by blockchain timestamps |
| 💰 **Fee Calculations** | Automatic, transparent deductions |
| 🔄 **Refund Eligibility** | Programmatic verification |

## 🛡️ Security Features

### For Donors

| Protection | Description |
| ---------- | ----------- |
| 💯 **100% Refunds** | Full refund if target not met (no fees) |
| ⏰ **Withdrawal Lock** | 30min-1hr delay prevents instant rugs |
| ✅ **Verified Creators** | Trust badges based on history |
| 📊 **Transparent Progress** | Real-time on-chain data |

### For Creators

| Protection | Description |
| ---------- | ----------- |
| 🔒 **Immutable Vault** | No one can take your raised funds |
| ⚡ **Automatic Unlock** | No admin approval needed |
| ❌ **Cancellation** | Cancel before donations received |

## 🔧 Smart Contract Security

| Feature | Details |
| ------- | ------- |
| 📏 **Input Validation** | Max target: 1000 SOL, Max deadline: 30 days |
| 🔢 **Overflow Protection** | All math uses checked operations |
| 🏛️ **Treasury Validation** | Hardcoded address, cannot be changed |
| 🔄 **CEI Pattern** | Prevents reentrancy attacks |

## ❌ What BasedRaid Cannot Do

| Action | Status |
| ------ | ------ |
| 💳 Access your wallet funds | ❌ **Impossible** |
| 🔧 Modify smart contract behavior | ❌ **Impossible** |
| ⏪ Reverse on-chain transactions | ❌ **Impossible** |
| 💰 Take funds from vaults | ❌ **Impossible** |
| 📊 Change fee percentages | ❌ **Impossible** |

## 💡 Best Practices

### For Donors

| Tip | Why It Matters |
| --- | -------------- |
| 🔍 **Verify the token** | Check contract address on a block explorer |
| 🏆 **Check creator history** | Look for trust badges and past success |
| 💰 **Start small** | Don't put all funds in one raid |
| 🔎 **Do your research** | Join the community, verify socials |

### For Creators

| Tip | Why It Matters |
| --- | -------------- |
| 📝 **Be transparent** | Clearly explain your goals |
| 🔗 **Provide proof** | Link socials and verify identity |
| 🎯 **Set realistic targets** | Build trust with smaller raids first |
| 💬 **Communicate** | Keep your community updated |

## 🚨 Reporting Issues

{% hint style="warning" %}
**Security Vulnerability?**

If you discover a security vulnerability, please report it responsibly. Contact the team directly before public disclosure.
{% endhint %}
