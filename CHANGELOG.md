# Changelog

All notable changes to this project are documented here.

---

## [1.1.0] — 2026-10-14

### Repository Modernization — Portfolio Readiness Update

**Scope:** Documentation, branding, and organization improvements. No financial formulas, datasets, or analytical results were changed.

#### Rebranding
- Renamed project identity from "QuantPath Mortgage Rate Intelligence Stack" to "Mortgage Rate Analysis: Financial Modeling & Time-Series Research" across all project-authored documentation
- Updated repository references from `quantpath-mortgage-rate-intelligence` to `mortgage-rate-analysis` in all internal links and configuration
- Replaced "QuantPath portfolio" framing with neutral "independent financial analytics case study" language throughout

#### Files Modified
- `README.md` — Complete rewrite; 15-section professional structure; verified dataset stats; concrete analytical findings; full phase status; accurate relative links
- `_config.yml` — Updated title, description, baseurl, URL comment; corrected author name
- `index.md` — Updated project title and GitHub Issues URL
- `docs/roadmap.md` — Updated title and contact section repo link
- `docs/phase1_workbook_brief.md` — Updated project name in header
- `data/README.md` — Updated project name in overview paragraph
- `phase2_r/README.md` — Updated status disclaimer
- `phase3_sql/README.md` — Updated status disclaimer

#### Files Created
- `docs/methodology.md` — Analytical methods, design decisions, sign conventions, QA approach, named range architecture
- `docs/findings.md` — Documented Phase 1 findings across all five business questions with quantitative results
- `docs/limitations.md` — Consolidated scope boundaries, modeling assumptions, and data constraints
- `docs/portfolio_summary.md` — Portfolio summary, competency table, three resume bullet candidates, reviewer entry-point guide

#### What Was Not Changed
- `data/raw/MORTGAGE30US.csv` — Dataset preserved exactly as downloaded
- `excel/Rate_Shock_Loan_Affordability_Refinance_Dashboard.xlsx` — Workbook preserved; no formula or data changes
- `docs/formula_reference.md` — Accurate technical reference; no changes needed
- `docs/data_dictionary.md` — Accurate named range inventory; no changes needed
- `specs/` — Historical build artifacts preserved intact
- `screenshots/` — All five workbook screenshots preserved

---

## [1.0.0] — 2026-05-19

### Phase 1 — Excel Financial Modeling & Dashboard (Complete)

**Workbook**: `Rate_Shock_Loan_Affordability_Refinance_Dashboard.xlsx`

#### Added
- **Rate_Data** sheet: imported FRED/Freddie Mac MORTGAGE30US weekly series (Apr 1971 – May 2026, ~2,877 observations); helper columns for Rate_Decimal, Year, Month_Year, and CurrentRateLine; summary statistics block (latest rate, historical min/max/avg, 52-week trailing average)
- **Assumptions** sheet: central input panel for loan inputs (home price, down payment, loan amount, term, base rate, monthly budget) and refinance inputs (remaining balance, current/proposed rates, remaining term, closing costs, holding period); data validation on all user-editable cells
- **Rate_Shock_Model** sheet: six-scenario rate shock analysis (−1.00% to +1.50%) computing monthly payment (PMT), payment delta vs. base, total lifetime interest (CUMIPMT), total loan cost, and affordable principal (PV)
- **Amortization_Schedule** sheet: full 360-payment base-case amortization schedule using PPMT/IPMT; summary block with PASS/FAIL formula-consistency checks
- **Refinance_Analysis** sheet: break-even model computing current vs. new payment, monthly savings, break-even months, and a conditional decision flag ("Refinance Makes Sense" / "Does Not Break Even in Holding Period")
- **Dashboard** sheet: five KPI cards (latest rate, base case payment, total lifetime interest, affordable loan amount, refinance break-even); chart placeholder zones for four charts (to be inserted manually in Excel); refinance summary table
- **Project_Map** sheet: executive overview with project objective, business questions table, workbook navigation map, formula family summary, scope notes, portfolio framing statement, data source attribution, and workbook health check formula
- 29 workbook-scoped named ranges covering all cross-sheet references
- Spec-driven development artifacts: requirements.md, design.md, tasks.md (via Kiro)

#### Technical notes
- All PMT/PPMT/IPMT formulas use the standard cash-flow sign convention: negative present value argument, no leading minus on the function itself
- CUMIPMT and PV formulas use a leading minus to convert their negative return values to positive display values
- No macros or VBA; workbook operates in standard Excel desktop without add-ins
