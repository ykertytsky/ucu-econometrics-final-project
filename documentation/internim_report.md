# **Topic and motivation**

**Topic -** The quantitative path to success: Identifying key drivers of startup growth

### **Authors:**

- Roman Pempus
- Pavlunyshyn Bohdan
- Yarema Kertytsky

The global entrepreneurial ecosystem sees the launch of hundreds of new ventures each year, creating a significant challenge for investors tasked with identifying startups with high potential. Traditional by-hand analysis is still applicable, however can be significantly optimised using econometrics methods to distinguish future market leaders from those destined to fail. 

This project aims to bridge this gap by performing analysis of historical startup dataset to isolate the core factors of success. The findings of this research carry significant implications for investment firms and corporate venture capital. By transitioning from manual qualitative reviews to automated predictive modeling, these organizations can efficiently filter over 100s of applicants quickly and  focus their resources on the most viable ones. Furthermore, the model provides an evidence-based framework to justify investment decisions and optimize capital allocation.

# **The aim and the task**

## Primary research aim

The central objective of this study is to identify and quantify the core determinants of startup success by leveraging a cross-sectional dataset of **472 venture-backed companies**. The research seeks to move beyond qualitative intuition, using data-driven insights to determine which variables carry the greatest predictive weight in distinguishing high-growth ventures from those destined for failure.

## Core Hypotheses

### 2 cofounders is ideal number of people in leadership team

Garry Tan (President of YC, leading Startup Accellerator in the world) suggests that best team is team of 2 cofounders. We want to prove it statistically - e. g. startups with 2 cofounders have greatest chance to succeed ceteris paribus (Formal version of this hypothesis is in progress)

### B2B is the way

Many investors argue that B2B contracts create **more stable and predictable revenue streams** than B2C, thanks to multi‑year enterprise deals and lower churn - this way it’s higher probability for startup to succed in safer environment

### The best startups are the best from the start

The dataset includes the variable `time_to_first_investment`. We assume that venture capitalists are able to identify high-potential startups at an early stage. Therefore, startups that receive their first investment sooner may have a higher probability of achieving success.

# Literature review

### **1. Econometric Estimation of the Factors That Influence Startup Success(article)**

**What it is:** A modern econometric study that uses multivariate logistic regression on a sample of 340 startups to identify which variables predict startup survival. It defines "success" in two distinct ways: achieving significant revenue (>€100k/year) and securing external financing.

**Insights:**

- **For revenue success:** The probability heavily increases with founders' full-time dedication, strong commercial skills, a technical background, having non-promoting partners (advisors), and reaching the breakeven point. Older founder age and participating in an incubator/accelerator actually *negatively* impact
- **For securing financing:** The probability increases with founders' dedication, prior startup experience (serial entrepreneurs), and participating in an incubator. Conversely, reaching the breakeven point *negatively* impacts the odds of getting funding, as profitable companies seek less external capital.

**Link:** https://www.mdpi.com/2071-1050/13/4/2242

### **2. CB Insights - The top 9 reasons startups fail(report)**

**What it is:** A data-driven analysis of hundreds of failed startups

**Insights:** Report highlights these biggest drivers of failure: poor product-market fit (43%), bad timing (29%), and unsustainable unit economics (19%) 

**Link:** https://www.cbinsights.com/research/report/startup-failure-reasons-top/

These studies provide a validated logistic regression blueprint for predicting startup survival and identify what factors are crucial for success

# **Data Description**

We found our dataset in the internet - [source of the dataset](https://github.com/dhirsch/CAX_Startup/blob/master/data/CAX_Startup_Data.csv). It is cross-sectional dataset of 472 anonymized venture-backed startups with a binary outcome variable - Success (305 obs., 64.6%) or Failed (167 obs., 35.4%). The dataset is already in our possession and requires no additional collection. 

It contains 116 predictor variables across five domains: founder human capital (education tier, years of experience, Fortune 500 background, prior startup experience), funding characteristics (last funding amount, investor count, time to first investment), business model attributes (B2B/B2C, subscription, platform, capital intensity), technology and market environment (industry trend, disruptiveness, competitive barriers), and 14 founder skill-share variables derived from LinkedIn profiles. The sample covers startups founded primarily between 2007 and 2012, with 65% based in the United States. 

Considering presence of significant numbers of irrelevant variables dataset would be futher cleaned from columns that we  have no interest in

Overall missing data rate is 5.4%, with categorical missing values encoded as "No Info"
requiring preprocessing before modeling.

# Methods

Our method is mainly determined by the fact that outcome variable is binary: startup success or failure - this way primary estimation method will be logistic regression (Logit), which models the probability of success as a function of founder, team, funding, and business model characteristics. 

Marginal effects will be computed to quantify each factor's contribution to the probability of success. 

# Schedule

- **25.03** Finish data clean up proccess and removing variables that we have no interest it
- **01.04** Finish testing hypotheses
- **14.04** Finish working on final report