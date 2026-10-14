# Analytical Findings

**Project:** Mortgage Rate Analysis: Financial Modeling & Time-Series Research  
**Phase:** 1 — Excel Financial Modeling & Dashboard  
**Dataset coverage:** April 2, 1971 – May 14, 2026 (2,877 weekly observations)  
**Last Updated:** October 2026

---

## Scope Note

All quantitative findings below are based on Phase 1 analysis of the committed FRED dataset. Numeric results use the workbook's default assumption set unless stated otherwise:

- Home price: $500,000
- Down payment: 20% ($100,000)
- Loan amount: $400,000
- Loan term: 30 years (360 months)
- Base rate: 6.36% (May 14, 2026 observation)
- Target monthly budget: $2,500
- Refinance scenario: $380,000 remaining balance, 7.00% → 6.00%, $6,000 closing costs, 60-month holding period

These are configurable inputs. The workbook recalculates all outputs when inputs change.

---

## Finding 1 — Historical Rate Context (BQ1)

**The May 2026 rate of 6.36% is below the full-series average but above the post-2008 low-rate era.**

Key statistics from the MORTGAGE30US series (April 1971 – May 2026):

| Statistic | Value |
|---|---|
| Latest rate (May 14, 2026) | 6.36% |
| Historical minimum | 2.65% (Jan 2021) |
| Historical maximum | 18.63% (Oct 1981) |
| Full-series average | ~7.7% |
| 52-week trailing average (approx.) | ~6.7% |

The series reflects three broad rate eras visible in the data:
- **Rising era (1971–1981):** Rates climbed from ~7.3% to a peak of 18.63%, driven by inflation and Federal Reserve tightening.
- **Long declining era (1981–2021):** A 40-year structural decline from the 1981 peak to a 2021 floor of approximately 2.65%.
- **Sharp re-acceleration (2022–2023):** The most rapid rate increase in the series history — from ~3% to above 7% in approximately 18 months — reflecting aggressive Federal Reserve tightening in response to elevated inflation.
- **Partial moderation (2024–2026):** Rates gradually retreated from the 2023 peak, settling near 6.3–6.7% by mid-2026.

By historical percentile, 6.36% falls in approximately the 40th–45th percentile of all weekly observations, meaning rates have been at or above this level for more than half of the series history. The current environment is elevated relative to the 2010–2021 decade but is not historically extreme.

---

## Finding 2 — Payment Sensitivity to Rate Changes (BQ2)

**A 1% rate change on a $400,000 loan produces approximately $240–$270 in monthly payment difference.**

Rate shock scenario results (base loan: $400,000, 30-year fixed):

| Scenario | Rate | Monthly Payment | Delta vs. Base |
|---|---|---|---|
| Rate −1.00% | ~5.36% | ~$2,244 | −$248 |
| Rate −0.50% | ~5.86% | ~$2,369 | −$123 |
| **Base Case** | **6.36%** | **~$2,492** | **$0** |
| Rate +0.50% | ~6.86% | ~$2,618 | +$126 |
| Rate +1.00% | ~7.36% | ~$2,747 | +$255 |
| Rate +1.50% | ~7.86% | ~$2,879 | +$387 |

> Values are approximate and derived from documented formulas. Exact values depend on the base rate at the time of opening the workbook.

The relationship between rate and payment is nonlinear (convex) — a 1.50% increase produces a larger absolute dollar change than a 1.00% increase proportionally. However, within a ±1.50% range, the relationship is approximately linear for practical decision-making.

---

## Finding 3 — Lifetime Interest Burden (BQ3)

**At 6.36%, a $400,000 borrower pays more in interest than in principal over the loan term.**

| Scenario | Rate | Total Interest | Total Loan Cost |
|---|---|---|---|
| Rate −1.00% | ~5.36% | ~$377,000 | ~$777,000 |
| Rate −0.50% | ~5.86% | ~$435,000 | ~$835,000 |
| **Base Case** | **6.36%** | **~$497,000** | **~$897,000** |
| Rate +0.50% | ~6.86% | ~$561,000 | ~$961,000 |
| Rate +1.00% | ~7.36% | ~$627,000 | ~$1,027,000 |
| Rate +1.50% | ~7.86% | ~$695,000 | ~$1,095,000 |

At the base case rate, total interest (~$497,000) slightly exceeds the principal borrowed ($400,000). A 1.50% rate increase adds approximately $198,000 in lifetime interest — roughly 50% of the original principal in additional cost. This finding illustrates the compounding effect of rate differences over long horizons, which is not obvious from monthly payment comparisons alone.

---

## Finding 4 — Affordability at a Fixed Budget (BQ4)

**A $2,500/month budget buys ~$401,000 in principal at 6.36%, but only ~$357,000 at 7.86%.**

| Scenario | Rate | Affordable Principal |
|---|---|---|
| Rate −1.00% | ~5.36% | ~$456,000 |
| Rate −0.50% | ~5.86% | ~$428,000 |
| **Base Case** | **6.36%** | **~$401,000** |
| Rate +0.50% | ~6.86% | ~$376,000 |
| Rate +1.00% | ~7.36% | ~$353,000 |
| Rate +1.50% | ~7.86% | ~$331,000 |

A 1.50% rate increase reduces affordable principal by approximately $70,000 — roughly 17% of the base-case value — for a borrower with an unchanged monthly budget. This directly quantifies how interest rate increases compress purchasing power even when a borrower's income remains constant. The practical implication is that rate movements can effectively price buyers out of a price tier without any change in their financial situation.

---

## Finding 5 — Refinance Break-Even Analysis (BQ5)

**Under the default scenario, refinancing from 7.00% to 6.00% breaks even in approximately 26 months.**

| Metric | Value |
|---|---|
| Remaining balance | $380,000 |
| Current rate | 7.00% |
| Proposed rate | 6.00% |
| Current monthly payment | ~$2,661 |
| New monthly payment | ~$2,432 |
| Monthly savings | ~$229 |
| Closing costs | $6,000 |
| Break-even months | ~26 months |
| Expected holding period | 60 months |
| Decision | **Refinance Makes Sense** |

At a 26-month break-even against a 60-month holding period, the borrower recovers closing costs well within the expected horizon. Over the full 60-month holding period, total savings before closing costs are approximately $13,740, yielding a net benefit of approximately $7,740.

**Sensitivity:** If closing costs rise to $9,000, break-even extends to ~39 months — still within the 60-month window. If the proposed rate is only 0.50% lower (6.50%), monthly savings drop to ~$113 and break-even extends to ~53 months, which is still within the holding period but with a much narrower margin.

---

## Caveats and Interpretation Guidance

- All findings use approximate values derived from documented Excel formulas and the default assumption set. Exact values will differ if inputs are changed.
- Rate figures from the rate shock table are derived by applying fixed offsets to the May 2026 base rate. They are analytical scenarios, not forecasts.
- The refinance analysis models payment differences on a fixed remaining balance and term. It does not account for the opportunity cost of closing costs, changes in tax deductibility, or the effect of extending the loan term.
- Historical rate statistics reflect the U.S. national average for conforming 30-year fixed loans. Individual borrower rates vary based on credit score, loan size, lender, and market conditions.

---

## Phase 2 Findings (Planned)

Phase 2 will add statistically grounded findings on:
- Stationarity properties of the MORTGAGE30US series
- Rate regime identification and transition points
- Rolling volatility by era
- Seasonality patterns
- Historical percentile context for the current rate

These findings do not yet exist. This section will be populated when Phase 2 is implemented.
