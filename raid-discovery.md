# Raid Discovery & Ranking

BasedRaid organizes active raids into three sections to help users discover campaigns that match their interests.

---

## ⭐ Sponsored (Top Priority)

Raids that have paid for the **Sponsored Boost** add-on during creation are displayed at the top of the Active tab.

**How to get featured:**
1. When creating a raid, enable "Sponsored Boost" add-on
2. Pay the tier-based fee (or FREE for higher token holders)
3. Your raid appears in the "⭐ Sponsored" section

**Visual indicators:**
- Gold/yellow border and glow effect
- Displayed above all other sections

---

## 🔥 Trending (Organic)

The top 3 active raids ranked by **heat score** — a combination of progress and urgency.

**Heat Score Formula:**
```
Score = Progress% × Urgency Multiplier
```

**Urgency Multipliers:**
| Time Remaining | Multiplier |
|---------------|------------|
| < 24 hours | 2x |
| < 72 hours | 1.5x |
| > 72 hours | 1x |

**Requirements to appear in Trending:**
- Must have at least 1 donation (not brand new raids)
- Must NOT be a Sponsored raid (Sponsored has its own section)
- Must be in the top 3 by heat score

**Example:**
A raid at 80% funded with 12 hours remaining gets score: `80 × 2 = 160`  
A raid at 50% funded with 3 days remaining gets score: `50 × 1.5 = 75`  
The 80% raid ranks higher due to urgency.

---

## 📋 Active Raids

All other active campaigns that don't qualify for Trending or aren't Sponsored.

- Sorted by deadline (newest first)
- Infinite scroll pagination
- Includes newly created raids without donations

---

## Summary

| Section | Criteria | Display Order |
|---------|----------|---------------|
| ⭐ Sponsored | Paid boost enabled | 1st (Top) |
| 🔥 Trending | Top 3 by heat score, has donations | 2nd |
| Active Raids | All others | 3rd |

This system rewards both paying creators (Sponsored) and organically successful campaigns (Trending), while ensuring all raids remain discoverable.
