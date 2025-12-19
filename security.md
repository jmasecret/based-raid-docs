# Security

BandAid is built with security as a top priority. This document explains the security measures in place.

{% hint style="info" %}
This page describes BandAid's security model, protections for donors and creators, smart contract safeguards, and responsible reporting procedures.
{% endhint %}

## Trustless Architecture

### PDA Vaults

All funds are held in **Program Derived Addresses (PDAs)** controlled by the smart contract—not by any individual:

* Creators cannot access funds until target is met
* Funds cannot be withdrawn early
* No single party can steal funds

### On-Chain Logic

All business logic is enforced on-chain:

* Target verification
* Lock period enforcement
* Fee calculations
* Refund eligibility

## Security Features

### For Donors

| Protection           | Description                             |
| -------------------- | --------------------------------------- |
| 100% Refunds         | Full refund if target not met (no fees) |
| Withdrawal Lock      | 30min-1hr delay prevents instant rugs   |
| Verified Creators    | Trust badges based on history           |
| Transparent Progress | Real-time on-chain data                 |

### For Creators

| Protection       | Description                       |
| ---------------- | --------------------------------- |
| Immutable Vault  | No one can take your raised funds |
| Automatic Unlock | No admin approval needed          |
| Cancellation     | Cancel before donations received  |

## Smart Contract Security

### Input Validation

* Maximum target: 1000 SOL
* Maximum deadline: 30 days
* Minimum target: 0.1 SOL
* String length limits enforced

### Overflow Protection

All arithmetic uses checked math to prevent overflow/underflow attacks.

### Treasury Validation

The treasury address is hardcoded in the contract—no one can redirect fees.

### Checks-Effects-Interactions

All functions follow the secure CEI pattern to prevent reentrancy.

## What BandAid Cannot Do

* ❌ Access your wallet funds
* ❌ Modify smart contract behavior
* ❌ Reverse on-chain transactions
* ❌ Take funds from vaults
* ❌ Change fee percentages

## Best Practices

### For Donors

{% stepper %}
{% step %}
### Verify the token

Check the contract address on a block explorer.
{% endstep %}

{% step %}
### Check creator history

Look for trust badges.
{% endstep %}

{% step %}
### Start small

Don't put all funds in one raid.
{% endstep %}

{% step %}
### Do your research

Join the community, verify socials.
{% endstep %}
{% endstepper %}

### For Creators

{% stepper %}
{% step %}
### Be transparent

Clearly explain your goals.
{% endstep %}

{% step %}
### Provide proof

Link socials and verify identity.
{% endstep %}

{% step %}
### Set realistic targets

Build trust with smaller raids first.
{% endstep %}

{% step %}
### Communicate

Keep your community updated.
{% endstep %}
{% endstepper %}

## Reporting Issues

{% hint style="warning" %}
If you discover a security vulnerability, please report it responsibly. Contact the team directly before public disclosure.
{% endhint %}
