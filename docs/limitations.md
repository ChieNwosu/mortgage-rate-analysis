# Limitations and Assumptions

**Project:** Mortgage Rate Analysis: Financial Modeling & Time-Series Research  
**Last Updated:** October 2026

This document consolidates all scope boundaries, modeling assumptions, data constraints, and known limitations across all phases of the project.

---

## Phase 1 — Excel Financial Model

### Modeling Scope

The workbook models **principal-and-interest (P&I) payment scenarios for 30-year fixed-rate loans**. The following are explicitly out of scope:

| Excluded Item | Reason |
|---|---|
| Property taxes | Highly location-specific; not part of the loan instrument |
| Homeowners insurance | Separate insurance product; varies by property and provider |
| Private mortgage insurance (PMI) | Requires LTV and credit inputs not modeled |
| HOA fees | Property-specific; not a loan component |
| Adjustable-rate mortgages (ARMs) | Requires rate-change schedule modeling; separate product from MORTGAGE30US |
| 15-year fixed loans | Out of scope for Phase 1; the dataset is specific to 30-year fixed |
| Income and DTI modeling | Affordability is budget-based, not income-based |
| Credit score pricing | Rate is taken directly from FRED; lender-specific pricing not modeled |
| Prepayment scenarios | No extra principal payments modeled |
| Bi-weekly payment schedules | Not modeled in Phase 1 |
| Multi-loan comparison | The workbook models one scenario at a time |
| Tax deductibility of mortgage interest | Not modeled |

### Formula Assumptions

- **Rate inputs are in decimal form** in the Assumptions sheet (e.g., `0.0636` for 6.36%), derived automatically from the FRED series. The formula divides the raw FRED percent value by 100.
- **Loan term is fixed at 360 months** for the new-purchase model. This is by design — the MORTGAGE30US series specifically tracks 30-year fixed rates. The refinance remaining term is editable.
- **Payments occur at end of period** (`type = 0` in all financial functions). This is the standard assumption for most fixed-rate mortgages.
- **No balloon payments, interest-only periods, or teaser rates** are modeled.
- **Closing costs are paid upfront** in the refinance model. No rolling of closing costs into the new loan balance is modeled.

### QA Caveats

- The 32/32 build-time QA checks are valid only under the default assumption set ($400,000 loan, 6.36% rate). The live PASS/FAIL cells in `Amortization_Schedule` remain authoritative and valid for any input values.
- The four Dashboard charts must be inserted manually — the build automation tool (openpyxl) does not reliably support complex chart types. The KPI cards and formula cells function correctly regardless of whether charts are present.

---

## Dataset Limitations

### Coverage

- The committed dataset (`data/raw/MORTGAGE30US.csv`) covers through **May 14, 2026**. Observations after that date are not included.
- No automated refresh mechanism exists. Updating the dataset requires manually downloading the latest CSV from FRED and updating the workbook's `Rate_Data` table.

### Representativeness

- MORTGAGE30US reports the **U.S. national average** for conforming 30-year fixed-rate loans. Actual borrower rates vary by:
  - Credit score (risk-based pricing)
  - Loan size (conforming vs. jumbo)
  - Lender and geographic market
  - Points and fee structure
  - Loan-to-value ratio

- The series is based on the **Freddie Mac Primary Mortgage Market Survey**, which surveys lenders. It reflects offered rates, not necessarily closed rates.

### Frequency

- Observations are weekly (Thursday). Daily rate fluctuations within the week are not captured.
- Intraday or real-time rates are not modeled.

### Seasonality and Calendar Effects

- The dataset is not seasonally adjusted. Any apparent seasonal patterns in the raw series have not been tested for statistical significance (planned for Phase 2).

---

## Phase 2 Limitations (Anticipated)

When Phase 2 is implemented, the following limitations will apply to the R analysis:

- Time-series methods (ADF, KPSS) test statistical properties of the series but do not constitute forecasts.
- Regime identification will use descriptive criteria (visual inspection, rolling statistics) rather than formal change-point detection algorithms, unless the coursework context warrants it.
- Seasonality decomposition on a weekly financial series can be sensitive to the decomposition method chosen; results should be interpreted cautiously.
- No machine learning or ARIMA/GARCH production forecasting is planned. Any forecasting component is exploratory.

---

## Phase 3 Limitations (Anticipated)

When Phase 3 is implemented, the following will apply:

- Cloud infrastructure (AWS, Databricks) will only be used if it serves a clear analytical purpose and can be set up at minimal or no cost. Credentials and configuration will not be committed to the repository.
- SQL queries will be tested against the existing FRED dataset. Joining with additional economic series requires additional data acquisition steps.

---

## General Research Limitations

- **No causal inference:** This project identifies descriptive patterns and computes financial metrics. It does not establish causal relationships between rate movements and economic outcomes.
- **No forward-looking statements:** Rate scenarios in the workbook are analytical constructs, not forecasts. Nothing in this project should be interpreted as investment advice.
- **Single data source:** The analysis relies entirely on the MORTGAGE30US series. Broader mortgage market dynamics (e.g., credit availability, underwriting standards, housing supply) are not modeled.
- **Static borrower profile:** The workbook models a single, anonymous borrower with configurable but static assumptions. Dynamic life events (job changes, refinancing multiple times, selling) are not modeled.

---

## Disclosure

This project is an independent educational and portfolio case study. It does not constitute financial, legal, or investment advice. All findings and scenarios are for analytical and demonstration purposes only.
