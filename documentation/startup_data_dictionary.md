# Startup Data Dictionary

**Source file:** `data/Startup_Data_Dictionary.csv` / `data/Startup_Data.csv`
**Updated:** 2026-03-14

Variables are grouped by theme. Entries marked **(F&C)** apply to founders & co-founders.

---

## Table of Contents
1. [Target Variable](#1-target-variable)
2. [Company Identification & Profile](#2-company-identification--profile)
3. [Company Timeline & Funding History](#3-company-timeline--funding-history)
4. [Employees & Team Size](#4-employees--team-size)
5. [Funding & Investors](#5-funding--investors)
6. [Founder & Co-founder Background](#6-founder--co-founder-background)
7. [Business Model](#7-business-model)
8. [Technology Characteristics](#8-technology-characteristics)
9. [Market & Competitive Position](#9-market--competitive-position)
10. [Pricing, Operations & HR](#10-pricing-operations--hr)
11. [Media, Recognition & External Signals](#11-media-recognition--external-signals)
12. [Founder Education (F&C)](#12-founder-education-fc)
13. [Founder Professional Experience (F&C)](#13-founder-professional-experience-fc)
14. [Skill Scores (F&C)](#14-skill-scores-fc)
15. [Financial & Timing Metrics](#15-financial--timing-metrics)
16. [Legal & Reputational Risk](#16-legal--reputational-risk)

---

## 1. Target Variable

| Variable | Description |
|----------|-------------|
| Dependent-Company Status | **Dependent variable.** Binary label indicating whether the company succeeded (survived/acquired/IPO) or failed (closed/shutdown). |

---

## 2. Company Identification & Profile

| Variable | Description |
|----------|-------------|
| Company_Name | Name of the startup. |
| Short Description of company profile | Brief free-text description of the company's product or service. |
| Industry of company | Industry sector the company operates in (e.g., FinTech, HealthTech, SaaS). |
| Focus functions of company | Primary functional focus areas (e.g., analytics, marketing automation, logistics). |
| Solutions offered | Description or count of distinct solutions/products the company offers. |
| Country of company | Country where the company is headquartered. |
| Continent of company | Continent where the company is headquartered. |
| Internet Activity Score | Score measuring how actively the company engages on social media and online platforms. |
| google page rank of company website | Google PageRank score of the company's website (indicator of web authority). |

---

## 3. Company Timeline & Funding History

| Variable | Description |
|----------|-------------|
| year of founding | Calendar year the company was founded. |
| Age of company in years | Number of years since founding at the time of data collection. |
| Est. Founding Date | Estimated full date (month/year) the company was founded. |
| Last Funding Date | Date of the company's most recent funding event. |
| Last Funding Amount | Amount raised in the most recent funding round (in million USD). |

---

## 4. Employees & Team Size

| Variable | Description |
|----------|-------------|
| Employee Count | Total number of employees at the time of data collection. |
| Employees count MoM change | Month-over-month change in employee headcount (positive = growth). |
| Has the team size grown | Binary flag: whether the team has grown since the company's founding. |
| Team size Senior leadership | Number of people in senior leadership / C-suite roles. |
| Team size all employees | Total headcount including all full-time and part-time employees. |
| Employees per year of company existence | Average number of employees per year of operation (headcount ÷ age). |
| Dificulty of Obtaining Work force | Score indicating how difficult it is to recruit qualified talent for this company/industry. |
| Employee benefits and salary structures | Rating of the competitiveness of the company's compensation and benefits packages. |

---

## 5. Funding & Investors

| Variable | Description |
|----------|-------------|
| Investors | List of investor names (individuals and/or funds). |
| Number of Investors in Seed | Count of investors who participated in the seed funding round(s). |
| Number of Investors in Angel and or VC | Count of angel investors and/or venture capital firms who invested. |
| Presence of a top angel or venture fund in previous round of investment | Binary: whether a top-tier VC or angel fund participated in a prior round. |
| Number of of repeat investors | Number of investors who participated in more than one funding round for this company. |
| Number of Sales Support material | Count of sales and marketing support assets (e.g., pitch decks, white papers, case studies). |
| Last round of funding received (in milionUSD) | Value of the most recently completed funding round, in million USD. |
| Time to 1st investment (in months) | Months elapsed between company founding and the first external investment. |
| Avg time to investment | Average time (in months) between consecutive investment rounds across all funding events. |
| Industry trend in investing | Score or flag indicating whether the company's sector is currently in favor with investors. |
| Invested through global incubation competitions? | Binary: whether the company received investment through an incubator or accelerator competition (e.g., Y Combinator, Techstars). |

---

## 6. Founder & Co-founder Background

| Variable | Description |
|----------|-------------|
| Number of Co-founders | Total number of co-founders (excluding the primary founder). |
| Number of of advisors | Number of formal advisors attached to the company. |
| Number of  of Partners of company | Number of formal business partners. |
| Worked in top companies | Binary: whether any founder/co-founder previously worked at a recognized top-tier company. |
| Average size of companies worked for in the past | Average employee count of prior employers across founders & co-founders. **(F&C)** |
| Have been part of startups in the past? | Binary: whether any founder/co-founder has prior startup experience. **(F&C)** |
| Have been part of successful startups in the past? | Binary: whether any founder/co-founder was part of a previously successful startup. **(F&C)** |
| Was he or she partner in Big 5 consulting? | Binary: whether any founder/co-founder was a partner at a Big 5 consulting firm. **(F&C)** |
| Consulting experience? | Binary: whether any founder/co-founder has consulting background. **(F&C)** |
| Long term relationship with other founders | Binary: whether the founders had a pre-existing long-term personal/professional relationship before starting the company. |
| Controversial history of founder or co founder | Binary/flag: whether any founder/co-founder has a publicly known controversial past. |

---

## 7. Business Model

| Variable | Description |
|----------|-------------|
| Product or service company? | Binary: primarily a product company (tangible/software product) vs. a service company. |
| Catering to product/service across verticals | Binary: whether the company's offering spans multiple industry verticals. |
| Focus on private or public data? | Indicates whether the company's data strategy focuses on private proprietary data or publicly available data. |
| Focus on consumer data? | Binary: whether the core business revolves around consumer data. |
| Focus on structured or unstructured data | Type of data the company primarily works with (structured tables vs. unstructured text/media). |
| Subscription based business | Binary: whether the company uses a recurring subscription revenue model. |
| Cloud or platform based serive/product? | Binary: whether the product or service is delivered via cloud or a platform model. |
| Local or global player | Scope of operations: locally focused vs. globally operating. |
| Linear or Non-linear business model | Revenue model type: linear (one-to-one transactional) vs. non-linear (platform/marketplace with network effects). |
| Capital intensive business | Binary: whether the business requires significant capital expenditure (e.g., e-commerce fulfillment, hardware manufacturing). |
| Crowdsourcing based business | Binary: whether core operations rely on crowdsourced labor or content. |
| Crowdfunding based business | Binary: whether the company raises/has raised capital via crowdfunding platforms. |
| Online or offline venture | Binary: primarily an online (digital) venture vs. a physical/offline presence-based business. |
| B2C or B2B venture? | Primary customer type: Business-to-Consumer (B2C) or Business-to-Business (B2B). |

---

## 8. Technology Characteristics

| Variable | Description |
|----------|-------------|
| Machine Learning based business | Binary: whether machine learning is a core component of the product or service. |
| Predictive Analytics business | Binary: whether predictive analytics is a primary offering or capability. |
| Speech analytics business | Binary: whether speech analytics is a primary offering or capability. |
| Prescriptive analytics business | Binary: whether prescriptive analytics (recommending actions) is a primary capability. |
| Big Data Business | Binary: whether big data processing is a core part of the business. |
| Cross-Channel Analytics/ marketing channels | Binary: whether the company employs cross-channel analytics or multi-channel marketing. |
| Owns data or not? (monetization of data) | Binary: whether the company owns proprietary datasets it can commercialize (e.g., Factual, BlueKai). |
| Is the company an aggregator/market place? | Binary: whether the company functions as a data/service aggregator or marketplace (e.g., BlueKai). |
| Technical proficiencies to analyse and interpret unstructured data | Score: the company's technical capability to process and derive insights from unstructured data. |
| Disruptiveness of technology | Score assessing how disruptive the company's core technology is relative to existing solutions. |
| Gartner hype cycle stage | The Gartner Hype Cycle stage of the company's core technology (Innovation Trigger → Plateau of Productivity). |
| Time to maturity of technology (in years) | Estimated number of years until the company's technology reaches mainstream adoption. |

---

## 9. Market & Competitive Position

| Variable | Description |
|----------|-------------|
| Number of Direct competitors | Count of direct competitors operating in the same market segment. |
| Barriers of entry for the competitors | Score or assessment of how high the barriers to entry are for potential competitors. |
| Proprietary or patent position (competitive position) | Binary/score: whether the company holds patents or significant proprietary intellectual property. |
| Hyper localisation | Binary: whether the business targets hyper-local geographic markets. |

---

## 10. Pricing, Operations & HR

| Variable | Description |
|----------|-------------|
| Pricing Strategy | A categorisation of the company's pricing approach (e.g., freemium, premium, usage-based, cost-plus). |
| Time to market service or product | Time (in months or years) from development start to bringing the product/service to market. |
| Survival through recession | Binary: whether the company operated and survived through at least one economic recession period. |

---

## 11. Media, Recognition & External Signals

| Variable | Description |
|----------|-------------|
| Top forums like 'Tech crunch' or 'Venture beat' talking about the company/model | Score measuring the volume or intensity of coverage in top tech media outlets. |
| Company awards | Count or binary flag of formal awards the company has received. |

---

## 12. Founder Education (F&C)

> All variables in this section apply to **founders & co-founders**.

| Variable | Description |
|----------|-------------|
| Highest education | Highest academic degree attained (e.g., Bachelor, Master, PhD, MBA). |
| Years of education | Total number of years spent in formal education. |
| Specialization of highest education | Field of study / major of the highest degree (e.g., Computer Science, Finance, Medicine). |
| Relevance of education to venture | Score: how directly relevant the founder's education is to the startup's domain. |
| Degree from a Tier 1 or Tier 2 university? | Binary: whether the founder graduated from a top-tier (Tier 1) or second-tier (Tier 2) university. |

---

## 13. Founder Professional Experience (F&C)

> All variables in this section apply to **founders & co-founders**.

| Variable | Description |
|----------|-------------|
| Average Years of experience for founder and co founder | Average years of professional work experience across all founders and co-founders. |
| Exposure across the globe | Binary/score: whether founder/co-founder has international work or education experience. |
| Breadth of experience across verticals | Score: diversity of industry sectors the founder/co-founder has worked in. |
| Relevance of experience to venture | Score: how directly relevant prior professional experience is to the startup's domain. |
| Renowned in professional circle | Binary/score: whether the founder is well-known or respected within their professional community. |
| Experience in selling and building products | Binary: whether founder/co-founder has prior experience in product development and sales. |
| Experience in Fortune 100 organizations | Binary: whether any founder/co-founder previously worked at a Fortune 100 company. |
| Experience in Fortune 500 organizations | Binary: whether any founder/co-founder previously worked at a Fortune 500 company. |
| Experience in Fortune 1000 organizations | Binary: whether any founder/co-founder previously worked at a Fortune 1000 company. |
| Top management similarity | Score measuring the similarity in background, style, or function among top management team members (low = complementary, high = homogeneous). |
| Number of Recognitions for Founders and Co-founders | Count of formal professional awards, recognitions, or honors received by founders/co-founders. |
| Number of  of Research publications | Count of academic or professional publications authored by founders/co-founders. |

---

## 14. Skill Scores (F&C)

> All variables in this section represent the **percentage of founders & co-founders** who possess the listed skill.

| Variable | Description |
|----------|-------------|
| Skills score | Aggregate composite skill score across all skill dimensions for the founding team. |
| Team Composition score | Composite score reflecting the overall balance and quality of the team's skill composition. |
| Renown score | Composite score for overall team renown, combining professional recognition, publications, and reputation signals. |
| Percent_skill_Entrepreneurship | % of founding team with entrepreneurship skills/experience. |
| Percent_skill_Operations | % of founding team with operations management skills. |
| Percent_skill_Engineering | % of founding team with engineering skills. |
| Percent_skill_Marketing | % of founding team with marketing skills. |
| Percent_skill_Leadership | % of founding team with leadership skills. |
| Percent_skill_Data Science | % of founding team with data science/analytics skills. |
| Percent_skill_Business Strategy | % of founding team with business strategy skills. |
| Percent_skill_Product Management | % of founding team with product management skills. |
| Percent_skill_Sales | % of founding team with sales skills. |
| Percent_skill_Domain | % of founding team with deep domain/industry expertise relevant to the startup. |
| Percent_skill_Law | % of founding team with legal skills. |
| Percent_skill_Consulting | % of founding team with management consulting skills. |
| Percent_skill_Finance | % of founding team with finance/accounting skills. |
| Percent_skill_Investment | % of founding team with investment/VC skills. |

---

## 15. Financial & Timing Metrics

| Variable | Description |
|----------|-------------|
| Last round of funding received (in milionUSD) | Amount raised (in million USD) in the most recent funding round. |
| Time to 1st investment (in months) | Months elapsed from company founding to receipt of the first external investment. |
| Avg time to investment | Average number of months between consecutive investment rounds (measured from the prior round). |
| Survival through recession | Binary: whether the company's period of operation overlapped with and survived an economic recession. |

---

## 16. Legal & Reputational Risk

| Variable | Description |
|----------|-------------|
| Legal risk and intellectual property | Assessment of the company's exposure to legal risks and strength of its intellectual property position. |
| Client Reputation | Score or qualitative indicator of how the company is perceived by its clients/customers. |
| Controversial history of founder or co founder | Binary/flag: whether any founder or co-founder has a publicly documented controversial history that could affect the company. |
