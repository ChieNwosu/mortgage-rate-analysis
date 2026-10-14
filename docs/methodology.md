# Methodology

**Project:** Mortgage Rate Analysis: Financial Modeling & Time-Series Research  
**Phase:** 1 — Excel Financial Modeling & Dashboard  
**Last Updated:** October 2026

---

## Overview

This document describes the analytical methods, design decisions, and modeling conventions used in Phase 1 of this case study. It is intended to make the workbook's logic transparent and auditable for technical reviewers.

---

## 1. Data Acquisition and Preparation

### Source

The FRED/Freddie Mac Primary Mortgage Market Survey series `MORTGAGE30US` was downloaded in CSV format directly from the Federal Reserve Bank of St. Louis Economic Data (FRED) portal on May 19, 2026.

**URL:** https://fred.stlouisfed.org/series/MORTGAGE30US

### Dataset Characteristics

- Frequency: Weekly (Thursday observations)
- Coverage: April 2, 1971 – May 14, 2026
- Record count: 2,877 observations
- Units: Percent (not seasonally adjusted); e.g., `6.36` represents 6.36%
- No missing values in the FRED series

### Preprocessing

The raw CSV is loaded into the `Rate_Data` worksheet of the Excel workbook. Four helper columns are added to the `tblMortgageRates` Excel Table:

| Column | Formula | Purpose |
|---|---|---|
| `Rate_Decimal` | `=[@MORTGAGE30US]/100` | Converts percent to decimal for financial functions |
| `Year` | `=YEAR([@observation_date])` | Enables year-level grouping and filtering |
| `Month_Year` | `=TEXT([@observation_date],"MMM-YYYY")` | Chart axis labels |
| `CurrentRateLine` | `=Rate_Data!$H$2` (constant) | Flat horizontal reference line for chart annotation |

A summary block computes five statistics from the full series: latest rate, historical minimum, historical maximum, historical average, and 52-week trailing average. All statistics use structured table references and update automatically when new data is appended.

---

## 2. Financial Modeling Approach

### Design Philosophy

The workbook is designed as a **configurable decision-support template**, not a hardcoded calculator. All borrower-specific assumptions are isolated in the `Assumptions` sheet as named, validated input cells. All model sheets reference these inputs through workbook-scoped named ranges — no hardcoded cell addresses appear in model formulas.

This architecture means the workbook remains fully functional when inputs change: adjusting the home price, rate, or refinance scenario instantly propagates through all seven sheets.

### Loan Term Decision

The new-purchase model uses a **fixed 30-year (360-month) term**. This is intentional — the source dataset is the FRED MORTGAGE30US series, which specifically tracks 30-year fixed-rate mortgages. Allowing a variable term would create a conceptual mismatch between the rate series and the model. The refinance remaining term remains fully user-editable, since borrowers refinancing mid-loan have a variable remaining horizon.

### Sign Convention

All financial functions follow Microsoft's standard cash-flow sign convention:

- **PMT, PPMT, IPMT:** The present value (loan amount) is passed as a **negative argument** so that the function returns a **positive payment**. A leading minus is not applied to the function itself.
  ```excel
  =PMT(rate/12, 360, -LoanAmount)  → returns positive monthly payment
  ```

- **CUMIPMT:** Returns a **negative value** (interest is a cash outflow). A **leading minus** converts it to a positive display value.
  ```excel
  =-CUMIPMT(rate/12, 360, LoanAmount, 1, 360, 0)  → positive total interest
  ```

- **PV:** Returns a **negative value** (loan amount is a liability). A **leading minus** converts it to a positive affordable principal.
  ```excel
  =-PV(rate/12, 360, MonthlyBudget)  → positive affordable principal
  ```

Consistent application of this convention ensures all cells display economically intuitive positive values without sign errors.

---

## 3. Scenario Analysis Method

### Rate Shock Table

The `Rate_Shock_Model` sheet computes six scenarios by applying fixed offsets to the base mortgage rate (linked from the latest FRED observation):

| Scenario | Offset |
|---|---|
| Rate −1.00% | −0.010 |
| Rate −0.50% | −0.005 |
| Base Case | 0.000 |
| Rate +0.50% | +0.005 |
| Rate +1.00% | +0.010 |
| Rate +1.50% | +0.015 |

For each scenario, five outputs are computed: monthly payment (PMT), payment delta vs. base case, total lifetime interest (CUMIPMT), total loan cost (principal + interest), and affordable principal at a fixed monthly budget (PV).

The offsets are designed to span a realistic near-term rate movement range — from a moderate decline to a significant increase — without overstating precision. They are not forecasts.

### Affordability Analysis

The "Affordable Principal" column answers the question: *Given a fixed monthly budget, how much can I borrow?* This reverses the typical PMT calculation: instead of computing payment from principal, it computes maximum principal from payment using the PV function. This directly quantifies how rate changes compress or expand purchasing power for a budget-constrained borrower.

---

## 4. Amortization Schedule

The `Amortization_Schedule` sheet computes a full 360-row base-case amortization using PPMT and IPMT for each period individually. This approach — rather than a single CUMIPMT lookup — produces the complete month-by-month breakdown of principal and interest, enabling visualization of balance decline over time.

Key design decisions:
- Beginning balance in month 1 is set to the loan amount
- Beginning balance in each subsequent month equals the prior month's ending balance
- Ending balance = Beginning balance − Principal paid (not derived from a running total, which could accumulate rounding error)
- PASS/FAIL QA checks verify that: (1) total principal paid equals the loan amount, and (2) the ending balance at month 360 is less than $1.00

---

## 5. Refinance Break-Even Model

The `Refinance_Analysis` sheet computes the classic break-even framework:

```
Break-Even Months = Closing Costs ÷ Monthly Savings
Monthly Savings = Current Payment − New Payment
```

Where both payments are computed using PMT applied to the **remaining balance** and **remaining term** (not the original loan), reflecting the actual economics of mid-loan refinancing.

A decision flag applies two conditions simultaneously:
1. Monthly savings must be positive (refinancing must lower the payment)
2. Break-even months must be ≤ the expected holding period

If either condition fails, the flag returns the appropriate negative outcome. The formula guards explicitly against division-by-zero when monthly savings ≤ 0.

---

## 6. Quality Assurance

Three layers of QA are built into the workbook:

**Layer 1 — Amortization PASS/FAIL cells (`Amortization_Schedule!I6`, `I8`):**  
Verify formula consistency using tolerance-based comparisons (`ABS(...) < 1`). These are always valid regardless of input values.

**Layer 2 — Project_Map health check (`Project_Map!F2`):**  
A single formula surveys the entire workbook — it fails if any amortization QA check fails, or if any key named-range cell returns an error.

**Layer 3 — Build-time QA:**  
At construction, 32 numeric checks were run against known expected values under the default assumption set ($400,000 loan, 6.36% rate). All 32 passed. These are documented in `specs/tasks.md` and remain informative for regression testing if inputs are reset to defaults.

---

## 7. Named Range Architecture

All 29 workbook-scoped named ranges are defined at the workbook (not sheet) level, making them accessible from any sheet without sheet-name prefixes. Naming conventions follow a prefix scheme for discoverability:

| Prefix | Scope |
|---|---|
| `Assump_` | Inputs from the Assumptions sheet |
| `RateData_` | Summary statistics from Rate_Data |
| `RSM_` | Outputs from Rate_Shock_Model |
| `Amort_` | Summary totals from Amortization_Schedule |
| `Refi_` | Outputs from Refinance_Analysis |

See [`docs/data_dictionary.md`](data_dictionary.md) for the complete named range inventory.

---

## 8. What This Methodology Does Not Cover

- Rate forecasting or prediction
- Bayesian or machine learning methods
- Multi-variable regression
- Income, DTI, or credit-score modeling
- ARM (adjustable-rate) products
- Tax or insurance components

These are addressed in the scope notes in [`docs/limitations.md`](limitations.md) and in the out-of-scope declarations in `specs/requirements.md`.

---

## References

- FRED MORTGAGE30US: https://fred.stlouisfed.org/series/MORTGAGE30US
- Excel PMT: https://support.microsoft.com/en-us/office/pmt-function-0214da64-9a63-4996-bc20-214433fa6441
- Excel CUMIPMT: https://support.microsoft.com/en-us/office/cumipmt-function-61067bb0-9016-427d-b95b-1a752af0e606
- Excel PV: https://support.microsoft.com/en-us/office/pv-function-23879d31-0e02-4321-be01-da16e8168cbd
