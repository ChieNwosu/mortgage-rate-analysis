# Mortgage Rate Analysis: Financial Modeling & Time-Series Research

**Independent Financial Analytics Case Study**

**Phase 1 — Excel Financial Modeling & Dashboard** ✅ Complete  
**Phase 2 — R Time-Series Analysis** 🔲 Planned (Summer 2026)  
**Phase 3 — SQL / Cloud Analytics** 🔲 Planned (TBD)

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Research Objectives and Business Questions](#research-objectives-and-business-questions)
3. [Dataset Description and Sources](#dataset-description-and-sources)
4. [Technologies and Analytical Methods](#technologies-and-analytical-methods)
5. [Repository Structure](#repository-structure)
6. [Project Phases and Implementation Status](#project-phases-and-implementation-status)
7. [Excel Financial Modeling](#excel-financial-modeling)
8. [R Statistical and Time-Series Analysis](#r-statistical-and-time-series-analysis)
9. [SQL and Cloud Analytics](#sql-and-cloud-analytics)
10. [Analytical Findings and Interpretation](#analytical-findings-and-interpretation)
11. [Reproducibility and Setup Instructions](#reproducibility-and-setup-instructions)
12. [Limitations and Assumptions](#limitations-and-assumptions)
13. [Future Improvements](#future-improvements)
14. [Portfolio Summary](#portfolio-summary)
15. [Author and References](#author-and-references)

---

## Executive Summary

This case study applies financial modeling and data analytics techniques to the FRED/Freddie Mac 30-Year Fixed Mortgage Rate series (`MORTGAGE30US`) — a weekly time series spanning April 1971 through May 2026 (~2,877 observations).

Phase 1 delivers a fully functional Excel workbook that answers five concrete business questions about mortgage affordability, payment sensitivity, lifetime interest burden, and refinance decision-making. The workbook is built on native Excel financial formula families (PMT, PV, CUMIPMT, PPMT, IPMT), 29 workbook-scoped named ranges, and configurable borrower inputs — producing a reusable, auditable decision-support template.

Phase 2 will extend the analysis with R-based time-series methods. Phase 3 will add a structured SQL data layer. Both are planned but not yet implemented.

---

## Research Objectives and Business Questions

The project investigates how the interest-rate environment affects household financial outcomes across five dimensions:

| # | Business Question | Phase | Status |
|---|---|---|---|
| BQ1 | How have 30-year fixed mortgage rates changed historically, and where does the latest rate sit relative to the past? | 1 | ✅ Answered |
| BQ2 | How much does a mortgage rate increase or decrease change the monthly payment on a representative loan? | 1 | ✅ Answered |
| BQ3 | How does the interest-rate environment affect total interest paid over the full life of the loan? | 1 | ✅ Answered |
| BQ4 | Given a fixed monthly payment budget, how much loan principal is affordable at different mortgage rates? | 1 | ✅ Answered |
| BQ5 | Under what conditions does refinancing become financially attractive, and how long does it take to break even? | 1 | ✅ Answered |
| BQ6 | What are the historical trends and rate regimes in the 30-year fixed rate series? | 2 | 🔲 Planned |
| BQ7 | How volatile have mortgage rates been in different eras, and where does the current environment fit? | 2 | 🔲 Planned |
| BQ8 | Are there seasonal patterns in mortgage rate movements? | 2 | 🔲 Planned |

---

## Dataset Description and Sources

**Series:** MORTGAGE30US — 30-Year Fixed Rate Mortgage Average in the United States  
**Provider:** Federal Reserve Bank of St. Louis (FRED) / Freddie Mac Primary Mortgage Market Survey  
**Frequency:** Weekly (Thursday)  
**Coverage:** April 2, 1971 – May 14, 2026  
**Observations:** 2,877  
**Units:** Percent, not seasonally adjusted  
**Latest observation in committed dataset:** 6.36% (May 14, 2026)  
**FRED URL:** https://fred.stlouisfed.org/series/MORTGAGE30US

The dataset was downloaded directly from FRED on May 19, 2026. It requires manual refresh to incorporate observations after that date. The workbook's `Rate_Data` sheet imports this CSV and adds helper columns for decimal conversion, year extraction, and chart annotation.

| Column | Type | Description |
|---|---|---|
| `observation_date` | Date (YYYY-MM-DD) | Weekly Thursday observation date |
| `MORTGAGE30US` | Numeric (percent) | 30-year fixed mortgage rate (e.g., `6.36` = 6.36%) |

See [`data/README.md`](data/README.md) and [`docs/data_dictionary.md`](docs/data_dictionary.md) for full column definitions, named range inventory, and data quality notes.

---

## Technologies and Analytical Methods

### Phase 1 (Complete)

| Tool / Technology | Role |
|---|---|
| **Microsoft Excel** | Financial modeling, scenario analysis, amortization, dashboard |
| **PMT / PV / CUMIPMT / PPMT / IPMT** | Core financial formula families |
| **Named ranges** (29 workbook-scoped) | Cross-sheet references, maintainability |
| **FRED / Freddie Mac** | Primary mortgage rate data source |
| **Python / openpyxl** | Workbook build automation (spec-driven, not committed) |
| **Kiro** | Spec-driven development workflow (requirements → design → tasks) |
| **Git / GitHub** | Version control and portfolio hosting |

### Phase 2 (Planned)

R, tidyverse, tseries, zoo, forecast, ggplot2, fredr — time-series diagnostics, rolling statistics, regime analysis, seasonality decomposition.

### Phase 3 (Planned)

SQL (platform TBD), structured data layer for rate series queries and joins with additional economic indicators.

---

## Repository Structure

```
mortgage-rate-analysis/
├── README.md                          # This file
├── CHANGELOG.md                       # Version history
├── index.md                           # GitHub Pages entry point
├── _config.yml                        # Jekyll configuration
├── .gitignore
│
├── data/
│   ├── raw/
│   │   └── MORTGAGE30US.csv           # FRED weekly 30-yr fixed rate data
│   └── README.md                      # Dataset provenance and column definitions
│
├── excel/
│   ├── Rate_Shock_Loan_Affordability_Refinance_Dashboard.xlsx
│   └── README.md                      # Workbook guide and sheet-by-sheet usage
│
├── screenshots/
│   └── workbook/
│       ├── Project_Map.png
│       ├── Assumptions.png
│       ├── Rate_Shock_Model.png
│       ├── Refinance_Analysis.png
│       └── Amortization_QA.png
│
├── docs/
│   ├── phase1_workbook_brief.md       # Business questions, scope, formula families
│   ├── data_dictionary.md             # Column and named range definitions
│   ├── formula_reference.md           # Formula patterns and sign convention
│   ├── roadmap.md                     # Phase 1–3 roadmap with honest status
│   ├── methodology.md                 # Analytical methods and design decisions
│   ├── findings.md                    # Documented analytical findings
│   └── limitations.md                # Consolidated scope and limitations
│
├── specs/                             # Kiro spec-driven development artifacts
│   ├── requirements.md
│   ├── design.md
│   └── tasks.md
│
├── phase2_r/                          # R time-series analysis (planned)
│   └── README.md
│
└── phase3_sql/                        # SQL / cloud layer (planned)
    └── README.md
```

---

## Project Phases and Implementation Status

| Phase | Description | Status | Deliverables |
|---|---|---|---|
| **Phase 1** | Excel financial modeling & dashboard | ✅ Complete | Workbook, 5 screenshots, full documentation |
| **Phase 2** | R time-series analysis | 🔲 Planned | Placeholder README; no scripts yet |
| **Phase 3** | SQL / cloud data layer | 🔲 Planned | Placeholder README; no scripts yet |

Phase 1 is complete and production-ready. Phases 2–3 are scoped and documented but not yet implemented. See [`docs/roadmap.md`](docs/roadmap.md) for the full phased plan, timeline, and honest status notes.

---

## Excel Financial Modeling

### Workbook: `Rate_Shock_Loan_Affordability_Refinance_Dashboard.xlsx`

The workbook is a reusable decision-support template organized across seven interconnected worksheets. All inputs are centralized in the `Assumptions` sheet; model sheets and the Dashboard recalculate automatically.

**No macros or VBA required — standard Excel desktop only.**

### Worksheet Overview

| Worksheet | Role | Key Outputs |
|---|---|---|
| `Project_Map` | Executive overview and workbook health check | Business questions, navigation map, QA formula |
| `Rate_Data` | FRED dataset and summary statistics | Latest rate, historical min/max/avg, 52-week trailing avg |
| `Assumptions` | Central input panel | All user-configurable loan and refinance inputs |
| `Rate_Shock_Model` | Six-scenario rate sensitivity analysis | Monthly payment, payment delta, total interest, affordable principal |
| `Amortization_Schedule` | Full 360-payment base-case schedule | Principal/interest breakdown per period, PASS/FAIL QA checks |
| `Refinance_Analysis` | Refinance break-even model | Current vs. new payment, monthly savings, break-even months, decision flag |
| `Dashboard` | Executive visual summary | Five KPI cards, four chart zones, refinance summary table |

### Configurable Inputs (Assumptions Sheet)

**Loan Inputs:**
- Home price · Down payment % · Loan amount (derived) · Base rate (auto-linked from Rate_Data) · Target monthly payment budget

**Refinance Inputs:**
- Remaining balance · Current rate · Proposed rate · Remaining term · Closing costs · Expected holding period

> The workbook does not model income, DTI ratio, credit score, taxes, insurance, PMI, or ARM products. It focuses on principal-and-interest scenarios using fixed-rate assumptions.

### Core Formula Families

| Formula | Purpose |
|---|---|
| `PMT(rate/12, term, -pv)` | Monthly principal-and-interest payment |
| `-PV(rate/12, term, pmt)` | Affordable principal at a fixed monthly budget |
| `-CUMIPMT(rate/12, term, pv, 1, term, 0)` | Total lifetime interest over the full loan term |
| `PPMT(rate/12, per, term, -pv)` | Principal component of a specific payment |
| `IPMT(rate/12, per, term, -pv)` | Interest component of a specific payment |

All cross-sheet references use named ranges. See [`docs/formula_reference.md`](docs/formula_reference.md) for the complete formula reference with sign-convention guidance.

### Workbook Screenshots

| Worksheet | Preview |
|---|---|
| Project Map | ![Project Map worksheet](screenshots/workbook/Project_Map.png) |
| Assumptions | ![Assumptions input panel](screenshots/workbook/Assumptions.png) |
| Rate Shock Model | ![Rate Shock Model worksheet](screenshots/workbook/Rate_Shock_Model.png) |
| Refinance Analysis | ![Refinance Analysis worksheet](screenshots/workbook/Refinance_Analysis.png) |
| Amortization QA | ![Amortization schedule QA checks](screenshots/workbook/Amortization_QA.png) |

### Quality Assurance

- 32/32 formula-consistency checks passed at build time
- `Amortization_Schedule` carries two live PASS/FAIL cells verifying total principal and final balance
- `Project_Map` health check formula (`F2`) surfaces any downstream formula errors across the workbook
- No circular references; no hardcoded cell addresses in model formulas

---

## R Statistical and Time-Series Analysis

**Status: 🔲 Planned — Summer 2026**

Phase 2 will apply R-based time-series methods to the MORTGAGE30US series. Planned focus areas:

- Stationarity testing (ADF, KPSS)
- Rolling averages and rolling volatility
- Rate-regime identification and visualization
- Historical percentile analysis
- Seasonality decomposition
- Optional baseline forecasting (exploratory)

No R scripts have been implemented yet. See [`phase2_r/README.md`](phase2_r/README.md) for the full planned scope and folder structure.

---

## SQL and Cloud Analytics

**Status: 🔲 Planned — Timeline TBD**

Phase 3 will build a structured data layer for querying and joining the mortgage rate series with additional economic context. Platform decisions (PostgreSQL, SQLite, cloud-native) have not been finalized.

No SQL scripts or cloud infrastructure have been implemented. See [`phase3_sql/README.md`](phase3_sql/README.md) for the planned scope.

---

## Analytical Findings and Interpretation

The following findings are based on Phase 1 analysis of the committed dataset (coverage through May 14, 2026). Quantitative values use the workbook's default assumptions: $500,000 home price, 20% down payment, $400,000 loan, 30-year fixed term.

**Historical rate context (BQ1):**  
The MORTGAGE30US series shows a long declining trend from its 1981 peak of 18.63% to the 2021 floor near 2.65%, followed by a sharp rise to above 7% in 2023 and gradual moderation. The May 2026 rate of 6.36% sits above the series historical average of approximately 7.7% when the full 1971–2026 history is considered, but below the elevated 7–8% range of late 2023. By percentile, 6.36% places in roughly the 40th–45th percentile of all weekly observations — meaning rates have been higher than this for more than half of recorded history.

**Payment sensitivity (BQ2):**  
At the $400,000 base-case loan, a 1% rate increase (from ~6.36% to ~7.36%) adds approximately $270 to the monthly principal-and-interest payment. A 1% rate decrease reduces it by a comparable amount. The six-scenario rate shock table in the workbook quantifies this across the full −1.00% to +1.50% range.

**Lifetime interest burden (BQ3):**  
At the base rate of 6.36%, total interest paid over a 30-year term on a $400,000 loan is approximately $497,000 — meaning the borrower pays more in interest than in principal. A 1.50% increase in rate raises total interest by approximately $130,000 over the loan term.

**Affordability at a fixed budget (BQ4):**  
With a $2,500/month budget, a 1% increase in mortgage rate reduces the affordable loan amount by approximately $35,000–$40,000. This quantifies how rate changes compress purchasing power even when a borrower's income and budget are unchanged.

**Refinance break-even (BQ5):**  
Under the default refinance scenario (7.00% → 6.00%, $380,000 remaining balance, $6,000 closing costs), the monthly savings are approximately $229, and the break-even point is approximately 26 months. With a 60-month expected holding period, refinancing is financially attractive under these assumptions.

> See [`docs/findings.md`](docs/findings.md) for additional interpretation and context.

---

## Reproducibility and Setup Instructions

### Open the Workbook

1. Open `excel/Rate_Shock_Loan_Affordability_Refinance_Dashboard.xlsx` in Microsoft Excel (desktop, Windows or Mac).
2. No macros, VBA, or add-ins are required.
3. Navigate to the `Assumptions` sheet and adjust the yellow-highlighted input cells to your scenario.
4. All model sheets and the Dashboard recalculate automatically.

### Refreshing the Dataset

The committed dataset covers through May 14, 2026. To update it:

1. Download the latest CSV from: https://fred.stlouisfed.org/series/MORTGAGE30US
2. Replace `data/raw/MORTGAGE30US.csv` with the new file (preserve the `observation_date,MORTGAGE30US` header).
3. In the workbook's `Rate_Data` sheet, extend or refresh the `tblMortgageRates` Excel Table to include the new rows.
4. All summary statistics and downstream model sheets will recalculate automatically.

> Do not rename columns or change the CSV structure — the workbook expects `observation_date` and `MORTGAGE30US` as column headers.

### Phase 2 Prerequisites (when implemented)

- R (≥ 4.2.0) — https://cran.r-project.org/
- RStudio or equivalent IDE
- R packages: `tidyverse`, `tseries`, `zoo`, `forecast`, `ggplot2`, `fredr`
- FRED API key for the `fredr` package: https://fred.stlouisfed.org/docs/api/api_key.html

See [`phase2_r/README.md`](phase2_r/README.md) for the planned setup procedure.

---

## Limitations and Assumptions

### Financial Model (Phase 1)

- **Fixed-rate only:** Models 30-year fixed-rate loans. Adjustable-rate mortgages (ARMs) and 15-year loans are out of scope.
- **Principal and interest only:** Does not include property taxes, homeowners insurance, HOA fees, or PMI.
- **No income or DTI modeling:** Affordability is computed from a target monthly P&I budget, not from borrower income or debt obligations.
- **Single scenario:** The workbook models one loan configuration at a time. Multi-loan comparison requires duplicating the file.
- **No prepayment:** Amortization assumes no extra principal payments.
- **Manual data refresh:** No live FRED API integration. The dataset must be updated manually.
- **Manual chart insertion:** The four Dashboard charts require manual insertion in Excel. The build-automation tool (openpyxl) does not reliably support complex chart types.

### Dataset

- **National average rates:** MORTGAGE30US reflects conforming-loan national averages. Regional and lender-specific rates vary.
- **Weekly frequency:** Daily rate fluctuations within the week are not captured.
- **No forward-looking data:** The series is historical only. No rate forecasts are included.
- **Dataset coverage:** The committed CSV covers through May 14, 2026. Observations after that date require a manual refresh.

See [`docs/limitations.md`](docs/limitations.md) for the consolidated limitations reference.

---

## Future Improvements

Planned enhancements, in approximate priority order:

**Phase 2 (R — time-series analysis):**
- ADF/KPSS stationarity tests on the MORTGAGE30US series
- Rolling 12-week and 52-week averages with visualization
- Rolling volatility analysis by rate era
- Historical percentile ranking for the current rate
- Seasonality decomposition
- R Markdown or Quarto report for reproducible output

**Phase 3 (SQL — data layer):**
- Structured table for the MORTGAGE30US series in a local or cloud SQL database
- Aggregation queries: monthly averages, year-over-year changes, rate-change detection
- Joins with additional FRED series (e.g., federal funds rate, unemployment rate, CPI)
- Python-based FRED ingestion script with reproducible setup steps

**Future extensions (exploratory, not scheduled):**
- Interactive visualization layer (Tableau Public or equivalent)
- 15-year fixed-rate comparison
- Prepayment and biweekly-payment modeling
- Property tax, insurance, and PMI layer
- Cloud-native architecture (AWS, Databricks) — only if it serves a clear analytical purpose

---

## Portfolio Summary

This project demonstrates a complete applied financial analytics workflow: data acquisition from a primary economic source, financial formula modeling in Excel, structured decision-support output, and reproducible documentation.

**Completed competencies demonstrated:**
- Financial modeling (PMT, PV, CUMIPMT, PPMT, IPMT formula families)
- Rate sensitivity and scenario analysis
- Amortization schedule construction with QA validation
- Refinance break-even analysis and decision logic
- Data cleaning and transformation (FRED CSV → workbook-ready table)
- Named-range architecture for maintainable cross-sheet references
- Structured analytical documentation (requirements, design, tasks, data dictionary, formula reference)
- Version control and reproducibility practices

**Pending competencies (planned):**
- R time-series analysis (stationarity, rolling statistics, regime identification)
- SQL data layer design and query development

See [`docs/portfolio_summary.md`](docs/portfolio_summary.md) for resume bullets and recruiter-facing summary.

---

## Author and References

**Author:** Chiemela Joseph Nwosu  
Undergraduate Information Technology student, North Carolina Central University (NCCU)  
Concentration: Data Analytics

**GitHub:** [ChieNwosu](https://github.com/ChieNwosu)  
**LinkedIn:** [Chiemela Joseph Nwosu](https://www.linkedin.com/in/chiemela-nwosu-23a791144)  
**Repository:** [ChieNwosu/mortgage-rate-analysis](https://github.com/ChieNwosu/mortgage-rate-analysis)

### Data Sources

- **FRED MORTGAGE30US:** https://fred.stlouisfed.org/series/MORTGAGE30US — Federal Reserve Bank of St. Louis / Freddie Mac Primary Mortgage Market Survey

### Excel Function References

- [PMT function](https://support.microsoft.com/en-us/office/pmt-function-0214da64-9a63-4996-bc20-214433fa6441)
- [PV function](https://support.microsoft.com/en-us/office/pv-function-23879d31-0e02-4321-be01-da16e8168cbd)
- [CUMIPMT function](https://support.microsoft.com/en-us/office/cumipmt-function-61067bb0-9016-427d-b95b-1a752af0e606)
- [PPMT function](https://support.microsoft.com/en-us/office/ppmt-function-c370d9e3-7749-4ca4-beea-b06c6ac95e1b)
- [IPMT function](https://support.microsoft.com/en-us/office/ipmt-function-5cce0ad6-8402-4a41-8d29-61a0b054cb6f)

### Academic Context

- Applied Time Series Analysis coursework — North Carolina Central University (NCCU)
- IBM Data Analytics with Excel and R Professional Certificate — Coursera (applied learning; not a completed IBM capstone project)
