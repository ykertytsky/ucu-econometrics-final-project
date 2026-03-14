# Dataset Summary — D8: Startup_Data.csv

**Path:** `data/mega-dataset/D8/Startup_Data.csv`
**Dictionary:** `data/mega-dataset/D8/Startup_Data_Dictionary.csv`
**Role in project:** Primary dataset for key-drivers analysis

---

## At a Glance

| Property | Value |
|----------|-------|
| Rows | 472 |
| Columns | 116 (+ 1 outcome) |
| Overall null rate | 5.4% |
| Encoding | latin1 |
| Company identifiers | Anonymized (`Company1`, `Company2`…) — cannot link to D1/D4 |

**Outcome variable:** `Dependent-Company Status`

| Class | n | % |
|-------|---|---|
| Success | 305 | 64.6% |
| Failed | 167 | 35.4% |

Good class balance. No resampling required for logistic regression.

---

## Sample Coverage

**Geography:** 65% North America, 16% Europe, 3% Asia. US alone = 305 companies (64.6%). Results will be US/tech-sector centric — caveat generalizability.

**Founding years:** 2005–2013, peak 2009–2012. 59 companies (12.5%) have no founding year recorded.

**Industry:** Analytics dominates (53 obs), followed by Analytics|Marketing (16), E-Commerce (9), Marketing (8). 26% of companies have no industry tag — treat as a separate "Unknown" category or impute by description.

---

## Variable Groups

### 1. Company Basics

| Variable | Type | Null % | Notes |
|----------|------|--------|-------|
| Age of company in years | Numeric | 9.3% | Derived from founding date |
| Internet Activity Score | Numeric | 13.8% | Social media presence proxy; range −725 to 1535, mean 114 |
| Industry of company | Categorical | 26.3% | 74 unique tags, often compound (`Analytics\|Marketing`) |
| Country / Continent | Categorical | 15.0% | |

### 2. Team & Founders

| Variable | Type | Null % | Corr. with success | Notes |
|----------|------|--------|--------------------|-------|
| Number of Co-founders | Numeric | 0% | **0.206** | Mean 1.87, max 7 |
| Team size — senior leadership | Numeric | 0% | **0.256** | Mean 3.7 |
| Team size — all employees | Numeric | 0% | — | |
| Employee Count | Numeric | 35.2% | 0.101 | Mean 31, median 13, max 594 — heavy right skew |
| Employees count MoM change | Numeric | 43.4% | **0.277** | Actual growth metric; mean −1.3%, range −100% to +50% |
| Has the team size grown | Categorical | 10.6% | — | Needs case normalization (Yes/yes/YES) |
| Number of advisors | Numeric | 0% | 0.189 | |
| Average Years of experience (founders) | Categorical | — | — | High/Medium/Low; 17% "No Info" |
| Breadth of experience across verticals | Categorical | — | — | Low/Medium/High |
| Worked in top companies | Categorical | — | — | 80% No, 15% Yes |
| Average size of companies worked for | Categorical | — | — | Small/Medium/Large |
| Have been part of startups in the past | Categorical | — | — | 63% Yes |
| Have been part of *successful* startups | Categorical | — | — | 55% Yes |
| Consulting experience | Categorical | — | — | 43% Yes |
| Big 5 consulting partner | Categorical | — | — | Only 5% Yes |

### 3. Founder Education & Pedigree

| Variable | Null % | Distribution |
|----------|--------|--------------|
| Highest education | — | Bachelors 36%, Masters 35%, PhD 7%, No Info 22% |
| Degree from Tier 1 or Tier 2 university | 30.5% | Tier_1: 139, Tier_2: 58, Both: 43 |
| Relevance of education to venture | — | 60% Yes |
| Relevance of experience to venture | — | 64% Yes |
| Experience in Fortune 100/500/1000 | 17% | Binary; ~22–24% have Fortune experience |
| Number of Recognitions | 0% | |
| Renowned in professional circle | 0% | |

### 4. Funding & Investment

| Variable | Type | Null % | Notes |
|----------|------|--------|-------|
| Last Funding Amount | Numeric | 33.9% | Mean $6.4M, median $2.8M, max $77M — log-transform needed |
| Last round of funding (million USD) | Numeric | 0% | |
| Number of Investors in Seed | Numeric | 0% | |
| Number of Investors in Angel/VC | Numeric | 0% | |
| Number of repeat investors | Mixed | — | Stored as string with "No Info"; 65% = 0 |
| Presence of top angel/VC fund | Categorical | — | 20% Yes, 21% "No Info" |
| Time to 1st investment (months) | Numeric | 0% | |
| Avg time between investment rounds | Numeric | 0% | |
| Invested through incubation competitions | Categorical | — | 11% Yes |

### 5. Business Model

| Variable | Distribution |
|----------|-------------|
| B2B vs B2C | B2B 65%, B2C 34% |
| Product or service company | Service 49%, Product 44%, Both 5% |
| Subscription based | Yes 57%, No 41% |
| Cloud or platform based | Platform 63%, Both 14%, Cloud 13% |
| Online vs Offline | Online 87%, Offline 10% |
| Linear vs Non-linear model | Non-Linear 68%, Linear 28% |
| Capital intensive | No 70%, Yes 25% |
| Marketplace / aggregator | No 71%, Yes 23% |
| Machine Learning based | No 71%, Yes 27% |
| Big Data business | No 53%, Yes 46% |
| Crowdfunding based | No 94%, Yes 5% |

### 6. Market & Technology

| Variable | Type | Null % | Notes |
|----------|------|--------|-------|
| Industry trend in investing | Numeric (0–5) | 17.4% | Mean 2.9 |
| Disruptiveness of technology | Categorical | — | Medium 40%, High 23%, Low 20% |
| Gartner hype cycle stage | Categorical | 36.4% | Plateau/Peak/Trigger/Trough/Slope |
| Time to maturity of technology | Categorical | 36.4% | 0–2 yrs / 2–5 yrs / 5–10 yrs |
| Barriers of entry for competitors | Categorical | 0% | Yes 53%, No 47% |
| Number of Direct competitors | Numeric | 0% | |

### 7. Founder Skills (14 variables, all 0% null)

`Percent_skill_*` for: Entrepreneurship, Operations, Engineering, Marketing, Leadership, Data Science, Business Strategy, Product Management, Sales, Domain, Law, Consulting, Finance, Investment

Each = percentage share of that skill in the founding team's LinkedIn profile skill set. Stored as string with some "No Info" values (≈13%).

### 8. Composite Scores

| Variable | Null % |
|----------|--------|
| Skills score | 0% |
| Team Composition score | ~18% |
| Renown score | 0% |

---

## Data Quality Issues (Must Fix Before Modeling)

| Issue | Affected Columns | Fix |
|-------|-----------------|-----|
| "No Info" as missing indicator | ~40 categorical columns | Replace with `NaN` before encoding |
| Case inconsistency | `Local/local/LOCAL/GLOBAL`, `Yes/yes/YES` | `.str.strip().str.lower()` normalization |
| Numeric columns stored as string | Percent_skill_*, repeat investors | `pd.to_numeric(..., errors='coerce')` |
| High-null columns | Partners (60%), Publications (53%), MoM change (43%) | Impute or drop depending on model |
| Gartner / maturity columns | 36.4% null | Impute or create binary "tech mature" flag |

---

## Columns to Drop Before Modeling

| Column | Reason |
|--------|--------|
| `Company_Name` | Anonymized identifier, no signal |
| `Short Description of company profile` | Free text, 32% null |
| `Est. Founding Date` / `Last Funding Date` | Redundant with derived age/timing variables |
| `Investors` | Free-text list, 30% null |
| `Employee benefits and salary structures` | 74% "No Info" |
| `Client Reputation` | 58% "No Info" |
| `Focus functions of company` | Free text |

---

## Modeling Notes

- **n=472** → use LASSO/Ridge (Elastic Net) to reduce 116 features to ~30–40 regressors
- **Recommended flow:** impute → encode → LASSO path → logistic regression on selected features → 10-fold CV → report AUC, coefficients, odds ratios
- **Cannot establish causality** — cross-sectional, no panel structure, no instrument candidates
- **Skewness confirmed** (real data): Employee Count skew=5.05, Last Funding=3.28 — log-transform funding before entering model
- **Interaction terms worth testing:** `education_tier × founder_experience`, `team_size × funding_amount`, `B2B × subscription`
