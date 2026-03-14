# Data Analysis — The Quantitative Path to Success: Identifying Key Drivers of Startup Growth

**Updated:** 2026-03-14
**Project:** Semester Econometrics Project
**Status:** Active datasets selected, ready for modeling

---

## Previous Assessment (Summary)

The original audit (2026-02-06) evaluated 10+ datasets. Most were discarded:

- `startup_failure_prediction.csv` and `startup_funding_dataset.csv` — **synthetic** (Faker-generated, zero-variance outcome, near-zero skewness on all numeric columns)
- `50_Startups.csv` (D7) — toy dataset, n=50, textbook OLS exercise only
- D5 (YC startups) — severe selection bias (YC-only, <2% acceptance rate), 87/13 outcome imbalance
- D6 — cleaned subset of D5, encoding corruption
- D10 — country-level macro data (n=63), wrong unit of analysis
- D3 — n=670, acquisition-only, encoding issues
- D2 (founders) — founder-level unit of analysis (not startup-level), max correlation with success = 0.121, no usable signal
- `data/companies.csv` (main CrunchBase, 196K rows) — strictly dominated by D1: 55% overall nulls, 86% funding nulls, same underlying source but less clean

All discarded datasets have been deleted from `/data`.

---

## Active Datasets

### D1 — CrunchBase Panel (`mega-dataset/D1/`)

| File | Rows | Cols | Key content |
|------|------|------|-------------|
| `companies.csv` | 66,368 | 14 | Company status, funding totals, geography, industry, founding dates |
| `rounds.csv` | 114,949 | 12 | Per-round funding amounts, round types, dates — panel structure |
| `acquisitions.csv` | 18,968 | 18 | Acquirer identity, acquisition date, price (26% coverage) |

**Outcome variable:** `status` — operating / acquired / closed / ipo
**Definitive outcome subset:** 13,334 companies (closed / acquired / ipo)
**Complete cases for modeling (7 vars):** 7,466

**Key variables:**

| Variable | Coverage | Correlation with success |
|----------|----------|--------------------------|
| `log(funding_total_usd)` | 81% | **0.515** |
| `funding_rounds` | 100% | 0.287 |
| `funding_duration_yrs` (first→last round) | 100% | 0.284 |
| `age_at_first_funding` (years from founding) | 77% | 0.099 |
| `category_list` (industry) | 95% | — |
| `country_code` | 90% | — |
| `founded_year` | 77% | — |

**Panel structure:** 23,879 companies with 2+ rounds, 11,531 with 3+. Round types: venture (55K), seed (31K), debt (7K), angel (6K). Temporal coverage 1960–2015, dense from 2001.

**Role in project:** Primary dataset for causal funding analysis. Survival analysis (Cox PH) with time-varying covariates, panel logit with firm fixed effects.

---

### D4 — Clean CrunchBase Cross-Section (`mega-dataset/D4/data.csv`)

| Rows | Cols | Nulls |
|------|------|-------|
| 61,398 | 11 | 8.3% overall |

**Outcome:** `status` — same four categories. After year filter (1990–2015): 46,511 rows.
**Definitive outcome subset:** 7,162 (success rate 66.1%)
**Complete cases for modeling (5 vars):** 41,201 full dataset / 6,596 outcome subset

**Key variables:** `funding_total_usd`, `funding_rounds`, `market` (788 fine-grained categories), `country_code`, `founded_at`, `first_funding_at`, `last_funding_at`

**Data issues to fix:**
- `founded_at` contains erroneous values (1592, 2914) — filter to 1990–2015
- Encoding: latin1 (not UTF-8)

**Role in project:** Cross-sectional validation of D1 findings at broader scale. `market` variable (finer than D1's `category_list`) enables industry heterogeneity analysis.

---

### D8 — Rich Feature Startup Dataset (`mega-dataset/D8/Startup_Data.csv`)

| Rows | Cols | Nulls |
|------|------|-------|
| 472 | 116 | 5.4% |

**Outcome:** `Dependent-Company Status` — Success (305) / Failed (167). Class balance: 65/35.
**Data authenticity confirmed:** Heavy skew on all numeric columns (Employee Count skew=5.05, Last Funding=3.28, MoM change=-3.25). Real data.
**Encoding:** latin1

**Key variables by category:**

| Category | Variables | Coverage |
|----------|-----------|----------|
| Funding | Last Funding Amount, Number of Investors in Seed, Number of Investors in Angel/VC, Number of repeat investors, Presence of top fund | 66–100% |
| Team / Founders | Number of Co-founders, Team size (all employees), Team size (senior leadership), Average years of founder experience, Employees count MoM change | 57–100% |
| Founder background | Fortune 500/100/1000 experience, Consulting experience, Education tier (Tier 1/2), Years of education, Relevance of education to venture | 100% |
| Business model | B2B/B2C, Subscription, Platform/Cloud, Marketplace/Aggregator, Capital intensive, Linear/Non-linear | 100% |
| Skills (14 vars) | Percent_skill_Entrepreneurship/Operations/Engineering/Marketing/Leadership/Data Science/etc. | 100% |
| Growth signals | Internet Activity Score, Age of company, Time to 1st investment, Industry trend in investing | 91–100% |

**Top correlations with success:**

| Variable | r |
|----------|---|
| Internet Activity Score | 0.327 |
| Employees count MoM change | 0.277 |
| Team size — senior leadership | 0.256 |
| Number of Co-founders | 0.206 |
| Number of advisors | 0.189 |

**Limitation:** n=472 limits model complexity. LASSO/Ridge regularization mandatory for feature selection (116 → ~30 predictors). Company names anonymized (`Company1`, `Company2`...) — cannot be linked to D1 or D4.

**Role in project:** Primary dataset for "key drivers" analysis. Directly addresses the research aim — which founder, team, funding, and business model characteristics determine success.

---

## Research Design

**Title:** The Quantitative Path to Success: Identifying Key Drivers of Startup Growth

**Aim:** Identify and quantify the financial and operational determinants of startup exit success using three complementary CrunchBase-derived datasets. We examine how total funding, funding staging and velocity, founder human capital, team composition, and business model characteristics influence the probability of a successful exit (IPO or acquisition) versus failure (closure).

### Three-Model Structure

**Model 1 — Key Drivers (D8, primary)**
Penalized logistic regression (Elastic Net / LASSO) on 116 features → identify which founder, team, and business model variables significantly predict success after controlling for funding. Report out-of-sample AUC via 10-fold CV.

```
P(Success=1 | X) = σ(Xβ)   with penalty λ₁‖β‖₁ + λ₂‖β‖₂²
```

**Model 2 — Funding → Outcomes, Panel (D1, causal)**
Cox Proportional Hazards / panel logit with firm fixed effects. Exploit the round-level panel to estimate causal effect of additional funding rounds on exit outcomes, controlling for initial conditions.

```
h(t|X) = h₀(t) · exp(β₁·log_funding + β₂·round_type + β₃·industry + β₄·country + β₅·cohort_year)
```

**Model 3 — Cross-sectional Validation (D4)**
Multinomial logit on four-category outcome (operating / acquired / closed / ipo). Validate D1 funding findings on independent broader sample. Test industry heterogeneity using fine-grained `market` categories.

### Identification and Robustness

| Issue | Mitigation |
|-------|------------|
| Funding endogeneity | `age_at_first_funding` as pre-funding quality proxy; discuss IV approach (VC fund vintage as instrument) |
| Survivorship bias | CrunchBase over-represents VC-backed tech/US companies — caveat generalizability, report industry/geography heterogeneity |
| Right-censoring | "Operating" firms have unknown final outcome — treated as right-censored in survival model |
| Overfitting (D8) | 10-fold CV, report train vs test AUC, LASSO path |
| Multiple testing | Bonferroni/BH correction across variable sets |

### Statistical Power

| Dataset | n (outcome) | Max predictors | Min detectable OR |
|---------|-------------|----------------|-------------------|
| D1 | 7,466 | ~747 | 1.04 |
| D4 | 6,596 | ~660 | 1.04 |
| D8 | 472 | ~47 (LASSO) | 1.25 |
