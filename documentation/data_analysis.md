# Startup Ecosystem Data — Econometric Research Viability Assessment

**Date:** 2026-02-06  
**Analyst Role:** Senior Econometrics Analyst — Startup Ecosystem & Causal Inference  
**Verdict:** **CONDITIONAL GO** — Strong research possible with select datasets; two datasets are synthetic garbage.

---

## Table of Contents

1. [Dataset Inventory](#1-dataset-inventory)
2. [Data Quality Assessment](#2-data-quality-assessment)
3. [Research Questions Matrix](#3-research-questions-matrix)
4. [Methodology Recommendations](#4-methodology-recommendations)
5. [Risk Factors](#5-risk-factors)
6. [Data Enhancement Needs](#6-data-enhancement-needs)

---

## 1. Dataset Inventory

### 1.1 Main `/data` Directory

| Dataset | Rows | Cols | Completeness | Verdict |
|---------|------|------|-------------|---------|
| `startup_failure_prediction.csv` | 5,000 | 15 | 100% | ⛔ **SYNTHETIC — DISCARD** |
| `startup_funding_dataset.csv` | 2,000 | 7 | 100% | ⛔ **SYNTHETIC — DISCARD** |
| `50_Startups.csv` | 50 | 5 | 100% | ⚠️ Toy dataset, textbook example only |
| `companies.csv` | 196,553 | 44 | ~40% usable | ✅ **PRIMARY — CrunchBase full** |

#### `startup_failure_prediction.csv` — SYNTHETIC (DISCARD)

**Evidence of synthetic generation:**
- `Startup_Status` is **100% = 1** (all identical). Zero variance in the dependent variable. Useless.
- Startup names follow pattern `Startup_1`, `Startup_2`, ..., `Startup_5000`.
- Funding skewness = **-0.003** (essentially zero — hallmark of uniform random distribution).
- Revenue skewness = **-0.001** (same).
- Industry categories nearly perfectly balanced (672–743 per category).
- **This is Faker/random data. No econometric value whatsoever.**

#### `startup_funding_dataset.csv` — SYNTHETIC (DISCARD)

**Evidence of synthetic generation:**
- Company names follow Python Faker patterns: `"Williamson, Greer and Clark"`, `"Kelly LLC"`, etc.
- Funding stages nearly perfectly balanced (373–424 per stage).
- Countries nearly perfectly balanced (216–273 per country).
- Date range 2016-01-06 to 2026-01-03 looks generated.
- **This is Faker data. No econometric value.**

#### `50_Startups.csv` — TOY DATASET

- 50 observations, 3 states (New York, California, Florida).
- R&D Spend → Profit correlation = 0.97 (textbook multivariate regression exercise).
- **n=50 is insufficient for any serious econometric inference.** Useful only for demonstrating OLS mechanics.

#### `companies.csv` — PRIMARY DATASET ✅

- **196,553 companies** from CrunchBase.
- 44 columns including status (operating/acquired/closed/ipo), funding, geography, categories, dates.
- **27,874 companies** with numeric funding data.
- **726 companies** with ROI data.
- Status breakdown with funding data: operating (23,311), acquired (2,335), closed (1,748), ipo (480).
- Founded years: 1901–2014, peak coverage 2005–2013.
- 42 industry categories, 108+ countries.

**Column Taxonomy:**

| Variable Group | Columns | Coverage |
|---------------|---------|----------|
| Identifiers | `id`, `name`, `permalink` | >99% |
| Outcome | `status` (operating/acquired/closed/ipo) | 100% |
| Funding | `funding_total_usd`, `funding_rounds`, `first_funding_at`, `last_funding_at` | 14–16% |
| Investment | `investment_rounds`, `invested_companies`, `first_investment_at`, `last_investment_at` | 1.3% |
| Geography | `country_code`, `state_code`, `city`, `region` | 43–55% |
| Industry | `category_code` | 63% |
| Temporal | `founded_at`, `created_at`, `updated_at` | 46% |
| Web Presence | `homepage_url`, `twitter_username`, `domain` | 41–64% |
| Performance | `ROI` | 0.37% (726 obs) |
| Spatial | `lat`, `lng` | 43% |
| Descriptive | `description`, `overview`, `short_description`, `tag_list` | 33–65% |

---

### 1.2 Mega-Dataset (`/data/mega-dataset`)

| Sub-dataset | Key File(s) | Rows | Cols | Outcome Var | Verdict |
|------------|------------|------|------|-------------|---------|
| **D1** | companies.csv, rounds.csv, acquisitions.csv | 66K + 115K + 19K | 14 + 12 + 18 | `status` | ✅ **HIGH VALUE — Panel possible** |
| **D4** | data.csv | 61,398 | 11 | `status` | ✅ **HIGH VALUE — Clean cross-section** |
| **D8/D9** | Startup_Data.csv / CAX_Startup_Data.csv | 472 | 116 | `Dependent-Company Status` | ✅ **RICH FEATURES — Small n** |
| D5 | FullSet.csv, Startups.csv, Founders.csv | 508 / 688 / 998 | 31 / 19 / 3 | `Fate` (Operating/Dead) | ⚠️ Moderate (YC only) |
| D6 | AB.csv | 688 | 6 | `Satus` | ⚠️ Cleaned D5 subset |
| D7 | 50_Startups.csv | 50 | 5 | `Profit` | ⛔ Same toy dataset |
| D10 | Final - Copy.csv | 63 | 46 | Country-level GEM data | ⚠️ Macro-level, n=63 |
| D10 | Startup_failure.csv | 10 | 2 | Year vs Failure rate | ⛔ n=10, useless |
| D2 | founder_V0.3_founder.csv | ~varies | 3 | None | ⚠️ Founder demographics only |
| D3 | funding-data.csv | 670 | 8 | `status` | ⚠️ Small acquisition dataset |

#### D1: CrunchBase Panel Data ✅ (TOP PRIORITY)

**Companies (66,368 rows, 14 cols):**
- Status: operating (53,034), closed (6,238), acquired (5,549), ipo (1,547)
- 53,583 companies with funding data
- Founded dates available for 51,147 companies

**Rounds (114,949 rows, 12 cols):**
- **Panel structure confirmed**: 23,879 companies with 2+ funding rounds (36%), 11,531 with 3+ rounds
- Mean 1.7 rounds per company, max 19
- Temporal coverage: 1960–2015, dense from 2001 onward
- 14 round types: venture (55K), seed (31K), debt (7K), angel (6K), etc.
- Raised amount: mean $10.4M, median $1.7M, range $0–$21.3B

**Acquisitions (18,968 rows, 18 cols):**
- 5,747 companies match to companies table
- Price data only for 5,012 acquisitions (73.6% missing)
- Acquirer information: category, geography available

**This is the gold mine. Panel data with 23K+ companies observed across multiple funding rounds enables serious causal inference.**

#### D4: Clean Cross-Section ✅

- 61,398 companies with 11 clean columns
- Status: operating (51,896), acquired (4,845), closed (3,181), ipo (1,476)
- 788 unique market categories, 135 countries
- 47,789 complete cases (78%) with funding + status + founded date
- Funding: mean $13.9M, median $954K
- **Excellent for cross-sectional regression models.**

#### D8/D9: Rich Feature Set ✅ (COMPLEMENTARY)

- 472 startups with **116 features** — extraordinarily rich
- Outcome: Success (305) vs Failed (167) — 35.4% failure rate, good class balance
- Key econometric variables and coverage:
  - Number of Co-founders: 100%
  - Team size (all employees): 100%
  - Investors in Seed/VC rounds: 100%
  - Time to 1st investment: 100%
  - Founder experience: 100%
  - Education level: 100%
  - Last Funding Amount: 66%
  - Employee Count: 65%
- Rich categorical: education tier, B2B/B2C, product/service, ML-based, subscription model
- Founder skills distribution (14 skill percentages)
- **Limitation: n=472 constrains the number of regressors (~40 max for reliable inference).**

#### D5: YC Startups

- 508 Y Combinator startups (2005–2014)
- Fate: Operating (442) vs Dead (66) — heavily imbalanced (87/13)
- TotalFunds, City, Market categories, Investor info, Sentiment from HackerNews
- **Sample selection bias: YC-only. Not generalizable to broader startup population.**

#### D10: Global Entrepreneurship Monitor (Country-Level)

- 63 countries, 46 variables (HDI, entrepreneurship rates, policy variables)
- **Useful for macro-level cross-country analysis only.**
- n=63 severely limits degrees of freedom.

---

## 2. Data Quality Assessment

### 2.1 Missing Values Summary

| Dataset | Overall Null % | Critical Variable Gaps |
|---------|---------------|----------------------|
| companies.csv (main) | ~55% overall | funding (86% null), ROI (99.6% null), founded (54% null) |
| D1/companies | ~15% overall | founded_at (23%), state_code (13%) |
| D1/rounds | ~15% overall | raised_amount (17%), funding_round_code (73%) |
| D4/data.csv | ~12% overall | founded_at (22%), state_code (39%) |
| D8/Startup_Data | 5.4% overall | Partners (60%), Publications (53%), MoM change (43%) |
| D5/FullSet | 24.5% overall | Most missing in Founders3-4, Market3-5, Investors3-4 |

### 2.2 Outliers and Data Issues

1. **Funding distributions are heavily right-skewed** across all datasets (expected for startup funding — log transformation required)
2. **D4 founded_at dates**: Range includes 1592 and 2914 — clearly erroneous. Need to filter to reasonable range (e.g., 1990–2015)
3. **D8 categorical inconsistency**: `Local or global player` has 5 variants (`Local`, `local`, `GLOBAL`, `Global`, `global`) — case normalization needed
4. **D8 "No Info" values**: Many categoricals use "No Info" as missing indicator — treat as NA
5. **Main companies.csv**: funding_total_usd stored as string with "-" for missing — numeric conversion needed

### 2.3 Temporal Coverage

| Dataset | Time Range | Peak Years | Panel Depth |
|---------|-----------|------------|-------------|
| companies.csv | 1901–2014 | 2008–2013 | Cross-sectional only |
| D1/rounds | 1960–2015 | 2010–2014 | **2+ rounds: 23,879 firms** |
| D4/data.csv | 1592–2914 (needs filtering) | ~2005–2014 | Cross-sectional only |
| D5/FullSet | 2005–2014 | YC cohort years | Cross-sectional |
| D8/Startup_Data | Varies | ~2008–2013 | Cross-sectional |

### 2.4 Granularity

- **Firm-level**: All main datasets (good for microeconometric methods)
- **Firm-round level**: D1/rounds (enables panel/event study designs)
- **Country-level**: D10 only (macro analysis)
- **No individual founder-level panel data** (D2 has founders but no temporal dimension)

---

## 3. Research Questions Matrix

### Question 1: Does Funding Round Size Causally Affect Startup Survival?

| Criterion | Assessment |
|-----------|-----------|
| **Statement** | What is the causal effect of initial/early-stage funding amount on the probability of survival (vs. closure)? |
| **Required Variables** | Funding amount ✅, survival outcome ✅, controls (industry, geography, year) ✅, instrument candidates ⚠️ |
| **Minimum Sample** | n ≥ 1,000 for logistic regression with 20+ controls; **n = 47,789 (D4) or 66,368 (D1)** |
| **Econometric Method** | **IV-Probit** using supply-side shocks (VC fund vintage, regional funding climate) as instruments; **Propensity Score Matching**; Heckman selection correction |
| **Feasibility Score** | **8/10** |
| **Insight Value** | High — directly actionable for founders and investors |

**Data Support:**
- D4: 47,789 complete cases with funding + status + founded date
- D1: 66,368 companies with detailed round-level data
- D1/rounds: median raise $1.7M across 95K observations with amounts

**Identification Challenge:** Funding is endogenous (better companies get more funding). Need valid instruments.

---

### Question 2: Does the Number of Funding Rounds Improve Long-Term Outcomes? (Panel Analysis)

| Criterion | Assessment |
|-----------|-----------|
| **Statement** | Controlling for initial conditions, does progressing through additional funding rounds causally improve exit outcomes (IPO/acquisition vs. closure)? |
| **Required Variables** | Multiple rounds per firm ✅, round timing ✅, amounts ✅, outcome ✅, firm characteristics ✅ |
| **Minimum Sample** | n ≥ 500 firms with 3+ rounds; **n = 11,531 (D1)** |
| **Econometric Method** | **Survival analysis (Cox PH)** with time-varying covariates; **Panel logit** with firm fixed effects; **Discrete-time hazard model** |
| **Feasibility Score** | **9/10** |
| **Insight Value** | Very High — tests "runway extension" hypothesis with causal design |

**Data Support:**
- D1: 23,879 companies with 2+ rounds, 11,531 with 3+ rounds
- Round dates available (funded_at) for event-time modeling
- 14 round types enable heterogeneity analysis (seed vs. venture vs. angel)
- Can construct firm-round panel with time-varying status

**This is the strongest research design available in this data.**

---

### Question 3: What Founder/Team Characteristics Predict Startup Success Beyond Funding?

| Criterion | Assessment |
|-----------|-----------|
| **Statement** | After controlling for funding and market conditions, which founder human capital attributes (education, experience, team composition) significantly predict success? |
| **Required Variables** | Founder education ✅, experience ✅, team size ✅, skills ✅, funding controls ✅, outcome ✅ |
| **Minimum Sample** | n ≥ 200 for logistic regression with 30 predictors; **n = 472 (D8)** |
| **Econometric Method** | **Logistic regression** with LASSO/Ridge regularization; **Decomposition methods** (Oaxaca-Blinder for founder type gaps); **Mediation analysis** |
| **Feasibility Score** | **7/10** |
| **Insight Value** | High — founder-actionable insights, VC screening implications |

**Data Support:**
- D8: 472 firms, 116 features, Success/Failed outcome (305/167)
- 14 skill percentage variables for founders
- Education tier, consulting experience, Fortune 500 experience
- Product/service type, B2B/B2C, technology indicators

**Limitation:** n=472 limits model complexity. Feature selection (LASSO) mandatory. No panel structure — cross-sectional only. Potential omitted variable bias from unobserved founder quality.

---

### Question 4: Does Geographic Clustering Affect Startup Outcomes? (Spatial Econometrics)

| Criterion | Assessment |
|-----------|-----------|
| **Statement** | Do startups in dense entrepreneurial ecosystems (e.g., SF, NYC) have systematically better outcomes, controlling for funding and industry? |
| **Required Variables** | Location ✅, outcome ✅, funding ✅, industry ✅, coordinates ⚠️ (43% coverage) |
| **Minimum Sample** | n ≥ 5,000 across multiple geographies; **n = 47,789+ (D4)** |
| **Econometric Method** | **Spatial regression** (SAR, SEM); **Multi-level/HLM** with city/region clustering; **RDD** using metro area boundaries |
| **Feasibility Score** | **6/10** |
| **Insight Value** | Medium-High — policy implications for startup hubs |

---

### Question 5: Do Acquisitions Create Value? (Event Study)

| Criterion | Assessment |
|-----------|-----------|
| **Statement** | What is the average treatment effect of acquisition on the acquiring firm's subsequent investment behavior? |
| **Required Variables** | Acquisition event ✅, acquirer identity ✅, pre/post investment data ⚠️, price ⚠️ (73% missing) |
| **Minimum Sample** | n ≥ 500 acquisition events; **n = 18,968** |
| **Econometric Method** | **Event study** design; **DID** comparing acquirers vs matched non-acquirers |
| **Feasibility Score** | **5/10** |
| **Insight Value** | Medium — limited by missing price data |

---

### Research Questions Summary Table

| Rank | Question | Method | Data Source | Feasibility | Insight Value |
|------|----------|--------|-------------|-------------|---------------|
| 1 | Funding rounds → outcomes (panel) | Survival/Panel FE | D1 | 9/10 | Very High |
| 2 | Funding size → survival (IV) | IV-Probit/PSM | D4 + D1 | 8/10 | High |
| 3 | Founder human capital → success | Logit/LASSO | D8 | 7/10 | High |
| 4 | Geographic clustering effects | Spatial/HLM | D4 + companies.csv | 6/10 | Medium-High |
| 5 | Acquisition value creation | Event Study/DID | D1 | 5/10 | Medium |

---

## 4. Methodology Recommendations

### 4.1 Primary Analysis: Survival Analysis on D1 Panel (Question 2)

**Model:** Discrete-time hazard model / Cox Proportional Hazards

```
h(t|X) = h₀(t) × exp(β₁ × FundingAmount + β₂ × RoundType + β₃ × Industry + β₄ × Geography + β₅ × YearFounded)
```

**Setup:**
1. Construct firm-round panel from D1: each row = one firm × one funding round
2. Time variable = months since first funding round
3. Event = transition to `closed`, `acquired`, or `ipo`
4. Time-varying covariate = cumulative funding, number of rounds completed
5. Stratify by round type (seed, venture, angel)

**Assumptions to Test:**
- Proportional hazards (Schoenfeld residuals test)
- No informative censoring (check if "operating" firms are truly right-censored or data truncated)
- No unobserved heterogeneity (frailty models as robustness)

**Statistical Power:** With 23,879 firms having 2+ events, power is excellent (>99%) for detecting effect sizes as small as d=0.05.

### 4.2 Secondary Analysis: Cross-Sectional Logit on D4 (Question 2 Complement)

**Model:** Multinomial Logit for multi-category outcome

```
P(Status = k | X) = exp(Xβₖ) / Σⱼ exp(Xβⱼ)  where k ∈ {operating, acquired, closed, ipo}
```

**Variables:**
- Dependent: `status` (4 categories)
- Key independent: `funding_total_usd` (log-transformed), `funding_rounds`
- Controls: `market` (788 categories → group into top 20 + other), `country_code` (top 10 + other), `founded_year`

**Sample:** 47,789 complete cases — extremely well-powered.

### 4.3 Tertiary Analysis: Founder Quality Logit on D8 (Question 3)

**Model:** Penalized logistic regression (Elastic Net)

```
P(Success = 1 | X) = σ(Xβ)  with penalty: λ₁||β||₁ + λ₂||β||₂²
```

**Feature Engineering Required:**
1. Normalize case for all categorical variables
2. Convert "No Info" to NA, handle via imputation (MICE or mean/mode)
3. Feature selection via LASSO to reduce from 116 to ~20-30 predictors
4. Create interaction terms: education × experience, team_size × funding

**Cross-validation:** Required (k=10) given small n. Report out-of-sample AUC.

### 4.4 Robustness Checks (Apply to All)

1. **Heckman correction** for selection into funding (only funded companies observed)
2. **Bootstrapped standard errors** (1,000+ replications)
3. **Multiple comparison correction** (Bonferroni/BH for multiple tests)
4. **Sensitivity analysis** for missing data (bounds analysis, worst-case scenarios)
5. **Placebo tests** where possible (random assignment of treatment)

---

## 5. Risk Factors

### 5.1 Endogeneity Concerns

| Issue | Severity | Affected Questions | Mitigation |
|-------|----------|-------------------|------------|
| **Funding endogeneity** | 🔴 High | Q1, Q2 | IV estimation (fund vintage, regional shocks), PSM |
| **Survivorship bias** | 🔴 High | All | Only observe companies that made it into CrunchBase — unknown selection mechanism |
| **Omitted variable bias** | 🟡 Medium | Q1–Q3 | Rich controls in D8; proxy variables in D1/D4 |
| **Reverse causality** | 🟡 Medium | Q1 | Better startups attract more funding. Panel structure of D1 helps (timing) |
| **Measurement error** | 🟡 Medium | Q1, Q4 | Self-reported funding data; geographic coordinates 43% missing |

### 5.2 Selection Bias

1. **CrunchBase coverage bias**: Dataset over-represents VC-backed, tech-sector, US-based startups. Results may not generalize to bootstrapped businesses, non-tech sectors, or emerging markets.
2. **YC selection (D5)**: Y Combinator startups are a hyper-selected sample (<2% acceptance rate). Any finding from D5 is conditional on this extreme selection.
3. **Right-censoring**: "Operating" status may mean the company is alive OR the data simply hasn't been updated. No way to distinguish without additional data.
4. **Left-truncation**: Companies that failed before entering CrunchBase are invisible.

### 5.3 Where Reviewers Will Attack

1. **"Your instruments are weak."** — Need to report first-stage F-statistics >10 (Stock-Yogo critical values) for any IV approach.
2. **"You're confusing correlation with causation."** — The cross-sectional datasets (D4, D8) cannot establish causality without strong assumptions. Be explicit about this.
3. **"Survivorship bias invalidates your results."** — Acknowledge this is a fundamental limitation. Present bounds analysis.
4. **"Your sample is tech-heavy and US-centric."** — True. Report heterogeneity by country/industry and caveat generalizability.
5. **"n=472 is too small for 116 features."** — Regularization helps but doesn't solve the fundamental problem. Report effective degrees of freedom.

---

## 6. Data Enhancement Needs

### What would unlock higher-value research:

| Enhancement | Unlocked Analysis | Priority |
|------------|-------------------|----------|
| **Temporal outcome tracking** (actual closure/exit dates) | True survival analysis with exact timing | 🔴 Critical |
| **Founder demographic panel** (education, experience over time) | Human capital accumulation effects | 🟡 High |
| **Revenue/financial performance data** | Continuous DV instead of binary outcome | 🟡 High |
| **VC fund characteristics** (fund size, vintage year, GP experience) | IV for funding endogeneity | 🟡 High |
| **Failed startup graveyard** (companies that never made it to CrunchBase) | Correct survivorship bias | 🔴 Critical |
| **Patent/IP data** linked to startups | Innovation as mechanism | 🟢 Medium |
| **Macroeconomic controls** (GDP, interest rates, VC dry powder) | Time-series confounders | 🟢 Medium |
| **Matched employer-employee data** | Labor market dynamics | 🟢 Medium |

### Achievable Enhancements with Current Data:

1. **Merge D1 companies + rounds + acquisitions** → Rich panel dataset with funding trajectories
2. **Merge D4 + D1** → Cross-validate findings across overlapping companies
3. **Supplement D8 with D4/D1 funding data** → Match by company name (fuzzy matching needed)
4. **Derive funding velocity** from D1 rounds: time between rounds as additional variable
5. **Construct industry-year funding supply** from D1 rounds: potential instrument for firm-level funding

---

## Appendix A: Dataset Overlap Assessment

| Dataset Pair | Join Key | Expected Match Rate | Value |
|-------------|----------|-------------------|-------|
| companies.csv ↔ D1/companies | `permalink` or `name` | ~30-40% (D1 is subset) | High |
| D4/data.csv ↔ D1/companies | `name` / fuzzy | ~60-70% (likely same source) | High |
| D1/companies ↔ D1/rounds | `permalink` | **100%** (confirmed) | Essential |
| D1/companies ↔ D1/acquisitions | `permalink` | 8.7% (acquired subset) | Moderate |
| D8 ↔ any | `Company_Name` (anonymized) | 0% — names are masked | ⛔ None |

**Note:** D8/D9 company names are anonymized (`Company1`, `Company2`, ...) — cannot be linked to other datasets. This limits D8 to standalone analysis.

---

## Appendix B: Statistical Power Calculations

For logistic regression (primary method), minimum detectable odds ratio at α=0.05, power=0.80:

| Dataset | n (complete) | Max predictors (n/10 rule) | Min detectable OR |
|---------|-------------|---------------------------|-------------------|
| D4 | 47,789 | ~4,779 | 1.02 (tiny effects detectable) |
| D1 | 66,368 | ~6,637 | 1.01 (excellent power) |
| D8 | 472 | ~47 | 1.25 (moderate effects only) |
| D5 | 508 | ~51 | 1.24 (moderate effects only) |
| companies.csv | 27,874 (funded) | ~2,787 | 1.03 |

**Conclusion:** D1 and D4 have exceptional statistical power. D8 is viable but limited to detecting meaningful effect sizes (OR ≥ 1.25). The 50-row datasets are statistically underpowered for anything beyond toy demonstrations.
