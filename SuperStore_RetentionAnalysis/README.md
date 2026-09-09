## 📊 E-Commerce Sales Analytics — Superstore Dataset

An end-to-end sales analytics project on real transaction data — from data validation through SQL analysis, profitability breakdown, and cohort retention — built to answer one question: **where is this business actually making and losing money?**

### Dataset
[Superstore Sample Dataset](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final) (Kaggle) — 9,994 order line items from a US office-supply retailer, 2014–2017. Fetched programmatically via [`kagglehub`](https://pypi.org/project/kagglehub/) (falls back to a local copy in `data/` if Kaggle credentials aren't set up).

### What this project covers
- **Data validation & cleaning** — null/duplicate/date-integrity checks, plus a real bug caught along the way: postal codes stored as integers silently drop the leading zero on New England ZIP codes (`02138` → `2138`).
- **SQL analysis (SQLite)** — KPIs, monthly revenue trend, category/sub-category profitability, discount-band profitability, regional/segment breakdowns, and customer ranking using a `RANK() OVER (...)` window function.
- **Profitability analysis** — isolates *why* margin is thin in specific areas, not just where revenue comes from.
- **Cohort retention analysis** — first-purchase-month cohorts, correctly masked against the dataset's own cutoff date (so unobserved future months aren't miscounted as churn), plus a purchase-frequency retention metric better suited to an infrequent-purchase B2B business.
- **Visualizations** — revenue trend, category revenue-vs-profit, sub-category profit (loss-makers highlighted), discount-band profit impact, regional revenue, retention.

### Key findings
| Finding | Detail |
|---|---|
| Revenue growth | 2017 revenue up 20.4% YoY, the strongest year in the data |
| Margin gap | Furniture nets only **2.5% margin** despite being 32% of revenue |
| Loss-making sub-categories | **Tables (−8.6% margin)** and **Bookcases (−3.0% margin)** lose money outright |
| Discount impact | Order lines with **>20% discount lose $97/line on average**, a $135K aggregate loss |
| Weakest region | **Central**, at ~7.9% margin vs. West/East in the high teens |
| Retention | Strict monthly cohort retention (6.1% month-1) understates loyalty — a 6-month purchase-frequency window shows **44.6%** repeat rate, a fairer metric for this business |

### Tools
`pandas` · `numpy` · `sqlite3` · `matplotlib` · `seaborn` · `kagglehub`

### Notebook
[`ecommerce_sales_analytics_project.ipynb`](./ecommerce_sales_analytics_project.ipynb) — fully executed, outputs included, runs end-to-end from a fresh environment.

### Why this project
Most sales-analytics portfolio pieces stop at "revenue by category." This one goes a step further into **margin diagnostics** — finding exactly which sub-categories, discount bands, and regions are structurally unprofitable, and validating that a headline retention number (e.g., a naive month-over-month cohort grid) isn't silently distorted by data-cutoff effects before trusting it.