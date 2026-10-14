# Portfolio Summary

**Project:** Mortgage Rate Analysis: Financial Modeling & Time-Series Research  
**Author:** Chiemela Joseph Nwosu  
**Repository:** https://github.com/ChieNwosu/mortgage-rate-analysis  
**Last Updated:** October 2026

---

## One-Minute Project Summary

This is an independent financial analytics case study built around the FRED/Freddie Mac 30-Year Fixed Mortgage Rate series — 2,877 weekly observations spanning April 1971 through May 2026.

**Phase 1 (complete)** delivers a production-ready Excel workbook that answers five concrete business questions: how rates have changed historically, how rate changes affect monthly payments, how they affect total interest paid, how they affect borrowing power at a fixed budget, and when refinancing becomes financially worthwhile. The workbook uses Excel's core financial formula families (PMT, PV, CUMIPMT, PPMT, IPMT), 29 named ranges, six-scenario rate shock analysis, a full 360-payment amortization schedule, a refinance break-even model, and a KPI dashboard.

**Phases 2–3** (planned) will add R-based time-series analysis and a SQL data layer.

**What this project demonstrates:** financial modeling rigor, structured data analysis, reproducible documentation, and the ability to translate raw economic data into actionable decision-support outputs.

---

## Demonstrated Competencies

| Competency | Evidence |
|---|---|
| Financial modeling | PMT/PV/CUMIPMT/PPMT/IPMT formulas; sign-convention discipline; six-scenario rate shock table |
| Amortization modeling | Full 360-row schedule with PPMT/IPMT per period; PASS/FAIL QA cells |
| Refinance analysis | Break-even model with division-by-zero guards and conditional decision flag |
| Data acquisition | FRED CSV download, column structure, provenance documentation |
| Data transformation | Percent-to-decimal conversion, date parsing, trailing averages, chart annotation helpers |
| Named range architecture | 29 workbook-scoped ranges; prefix naming convention; no hardcoded addresses in formulas |
| QA and validation | 32/32 build-time checks; live PASS/FAIL cells; workbook health check formula |
| Scenario analysis | Six-rate-shock scenarios with monotonicity and consistency verification |
| Structured documentation | Requirements spec, design doc, task tracker, data dictionary, formula reference |
| Reproducibility | Configurable inputs; manual refresh procedure documented; no macros required |
| Version control | Git/GitHub with meaningful commit history and changelog |
| Communication | README, findings doc, limitations doc — written for both technical and non-technical audiences |

---

## Resume Bullet Candidates

The following bullets are based exclusively on implemented and verified Phase 1 work. No performance metrics, dollar impacts, or results have been fabricated or estimated beyond what the dataset and formulas directly support.

---

**Bullet 1 — Financial Modeling Focus**

> Built a production-ready Excel financial model analyzing 2,877 weeks of FRED mortgage rate data (1971–2026); implemented PMT, PV, CUMIPMT, PPMT, and IPMT formula families with six-scenario rate shock analysis, a 360-payment amortization schedule with QA validation, and a refinance break-even model across configurable borrower assumptions.

---

**Bullet 2 — Data Analytics and Decision Support Focus**

> Designed a configurable mortgage decision-support workbook using 29 workbook-scoped named ranges and four interconnected model sheets; quantified that a 1.50% rate increase on a $400K loan adds ~$387/month in payments and ~$198K in lifetime interest, translating rate-environment context into household financial impact.

---

**Bullet 3 — Documentation and Reproducibility Focus**

> Delivered a reproducible financial analytics case study with full spec-driven development artifacts (requirements, design, task tracker), data dictionary, formula reference, methodology documentation, and analytical findings — structured for both technical review and recruiter-facing portfolio presentation.

---

## Usage Guidance for Reviewers

| Audience | Recommended Entry Point |
|---|---|
| Recruiter / hiring manager | Main [`README.md`](../README.md) — Executive Summary and Portfolio Summary sections |
| Financial analyst | [`excel/README.md`](../excel/README.md) and [`docs/formula_reference.md`](formula_reference.md) |
| Data analyst / data engineer | [`docs/data_dictionary.md`](data_dictionary.md) and [`docs/methodology.md`](methodology.md) |
| Technical reviewer | [`specs/design.md`](../specs/design.md) and [`specs/requirements.md`](../specs/requirements.md) |
| Anyone evaluating findings | [`docs/findings.md`](findings.md) |

---

## Honest Status

**Phase 1:** Complete. All five business questions answered. Workbook functional, documented, and QA-validated.

**Phase 2 (R):** Planned for Summer 2026. No R scripts exist yet. The `phase2_r/` folder is a structured placeholder.

**Phase 3 (SQL):** Planned, timeline TBD. No SQL scripts or cloud infrastructure exist yet. The `phase3_sql/` folder is a structured placeholder.

**Future extensions** (Databricks, Tableau, AWS): Exploratory ideas only — not scoped, not scheduled, not committed.
