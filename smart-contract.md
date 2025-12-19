# Smart Contract

Technical reference for the BasedRaid smart contract on Solana.

## Overview

| Property       | Value                                          |
| -------------- | ---------------------------------------------- |
| **Network**    | Solana Devnet                                  |
| **Program ID** | `DTS66x95eduAtc1pYYemwbE4Ry6riwSBsMTRCmtDPXkE` |
| **Framework**  | Anchor                                         |
| **Language**   | Rust                                           |

## Constants

| Constant                    | Value    | Description                    |
| --------------------------- | -------- | ------------------------------ |
| `MIN_TARGET_AMOUNT`         | 0.1 SOL  | Minimum fundraising target     |
| `MAX_TARGET_AMOUNT`         | 1000 SOL | Maximum fundraising target     |
| `MAX_DEADLINE_DURATION`     | 30 days  | Maximum time until deadline    |
| `WITHDRAWAL_DELAY_STANDARD` | 1 hour   | Lock period for standard raids |
| `WITHDRAWAL_DELAY_VERIFIED` | 30 min   | Lock period for verified raids |
| `BASE_FEE`                  | 0.02 SOL | Creation fee                   |
| `VERIFIED_FEE`              | 0.1 SOL  | Verified badge cost            |
| `PROMOTED_FEE`              | 0.05 SOL | Trending boost cost            |

## Account Structures

### Raid Account

```rust
pub struct Raid {
    pub creator: Pubkey,        // Raid creator
    pub contract_address: Pubkey, // Token CA
    pub ticker: String,         // Token symbol (max 10)
    pub raid_goal: String,      // Goal description (max 100)
    pub twitter_link: String,   // Social link (max 200)
    pub title: String,          // Raid title (max 50)
    pub description: String,    // Description (max 250)
    pub target_amount: u64,     // Target in lamports
    pub raised_amount: u64,     // Current raised amount
    pub deadline: i64,          // Unix timestamp
    pub target_met_at: i64,     // When target was met (0 if not)
    pub is_verified: bool,      // Has verified badge
    pub is_promoted: bool,      // Is promoted/trending
    pub is_withdrawn: bool,     // Has been withdrawn
    pub bump: u8,               // PDA bump
}
```

### Donation Account

```rust
pub struct Donation {
    pub donor: Pubkey,    // Donor's wallet
    pub raid: Pubkey,     // Associated raid
    pub amount: u64,      // Donation amount in lamports
    pub bump: u8,         // PDA bump
}
```

## Instructions

### initialize_raid

Creates a new raid.

**Parameters:**

* `raid_id`: u64 - Unique ID
* `contract_address`: Pubkey - Token CA
* `ticker`: String - Token symbol
* `raid_goal`: String - Goal description
* `twitter_link`: String - Social link
* `title`: String - Raid title
* `description`: String - Description
* `target_amount`: u64 - Target in lamports
* `deadline`: i64 - Unix timestamp
* `is_verified`: bool - Pay for verified
* `is_promoted`: bool - Pay for promotion

{% hint style="info" %}
Deadline must be in the future and within `MAX_DEADLINE_DURATION`. Target amount must be between `MIN_TARGET_AMOUNT` and `MAX_TARGET_AMOUNT`.
{% endhint %}

---

### donate

Donates SOL to a raid.

**Parameters:**
* `amount`: u64 - Amount in lamports

**Requirements:**
* Raid not expired
* Raid target not met

---

### withdraw_funds

Withdraws funds after target is met.

**Requirements:**
* Caller is creator
* Target is met
* Lock period has passed
* Not already withdrawn

{% hint style="warning" %}
Lock period depends on whether raid is verified (30 min) or standard (1 hour).
{% endhint %}

---

### cancel_raid

Cancels a raid and returns rent.

**Requirements:**
* Caller is creator
* No donations received

---

### refund

Claims refund from failed raid.

**Requirements:**
* Raid expired
* Target not met
* Caller made donation

{% hint style="success" %}
Refunds are 100% to donors (0% fee).
{% endhint %}

## Fee Structure

### Creation Fees

| Type           | Cost      |
| -------------- | --------- |
| Base Creation  | 0.02 SOL  |
| + Verified     | +0.1 SOL  |
| + Trending     | +0.05 SOL |

### Withdrawal Fees

| Type     | Fee |
| -------- | --- |
| Standard | 5%  |
| Verified | 3%  |

### Refund Fees

* 0% fee - Donors receive 100% back

## Error Codes

| Code                        | Message                               |
| --------------------------- | ------------------------------------- |
| `InvalidDeadline`           | Deadline must be in the future        |
| `TargetTooLow`              | Target amount too low (min 0.1 SOL)   |
| `TargetTooHigh`             | Target amount too high (max 1000 SOL) |
| `DeadlineTooFar`            | Deadline too far (max 30 days)        |
| `RaidExpired`               | Raid has expired                      |
| `TargetNotMet`              | Target has not been met               |
| `TargetMet`                 | Target already met                    |
| `AlreadyWithdrawn`          | Funds already withdrawn               |
| `WithdrawalTooEarly`        | Lock period not finished              |
| `CannotCancelWithDonations` | Cannot cancel with donations          |
| `Unauthorized`              | Not authorized for this action        |

## Events

| Event            | Emitted When         |
| ---------------- | -------------------- |
| `RaidCreated`    | New raid initialized |
| `DonationMade`   | Donation received    |
| `FundsWithdrawn` | Creator withdraws    |
| `RefundClaimed`  | Donor claims refund  |
| `RaidCancelled`  | Creator cancels raid |
