# Customer Churn Analysis & Customer Intelligence (OTT Subscription)

End-to-end churn analytics project using **SQL + Python** to find high-risk subscribers, measure revenue impact and recommend retention actions.

## Business Problem
In the competitive OTT market, retention drives survival. This project answers **Who** churns, **Why** they leave and **When** the danger zone occurs, using customer, subscription and support data.

## Tech Stack
Python · Pandas · NumPy · SQLite3 · Matplotlib · Seaborn · Jupyter Notebook

## Dataset (`customer_churn.db`)
| Table | Key Columns |
|---|---|
| `db_customer` | customerid, name, country, state, gender, dob |
| `db_subscription` | plan_type, contract_type, monthly_charges, cltv, churn_score, cancellation_date, cancellation_reason |
| `db_support` | complaint_date, escalations, csat_score |

## Workflow
1. **Extract:** connect SQLite to Python and load all tables as DataFrames
2. **Clean:** rename columns, fix data types, standardize gender, fill missing country, drop empty columns, remove duplicates
3. **Feature Engineering:** `churn_flag`, `tenure_days`, `complaint_count`, `churn_risk` (low / med / high)
4. **Analysis:** 10+ KPIs using groupby, aggregation and pivot tables
5. **Visualization:** monthly churn trend, churn by plan and state, correlation heatmap, pairplot, catplot

## Calculated Metrics
| KPI | Formula | Result |
|---|---|---|
| Churn rate | churned customers / total customers | 28.57% |
| Retention rate | 1 - churn rate | 71.43% |
| Churn by plan type | churn rate GROUP BY plan_type (Basic / Standard / Premium) | 60% / 22.22% / 14.29% |
| Churn by state | churn rate GROUP BY country, state | Karnataka 100%, Meghalaya 66.67% |
| ARPU | SUM(monthly_charges) / COUNT(customerid) | Rs 18.85 |
| Average customer tenure | AVG(DATEDIFF(cancellation_date OR NOW(), subscription_start_date)) | calculated in notebook |
| Revenue at risk | SUM(monthly_charges) WHERE churn_score > 70 | Rs 73.94 |
| Escalation rate | SUM(escalations) / COUNT(complaints) x 100 | 19.05% |
| Avg complaints per customer | COUNT(complaints) / COUNT(DISTINCT customerid) | 0.43 |
| Correlation: escalations vs churn | churn rate WHERE escalations >= 1 vs 0 | 0.88 |

## Insights
- Churn rate is **28.6%** and retention rate is **71.4%**
- Most churn is from the **Basic** plan, so the revenue impact is limited
- Most churn happened in **Sep 2024**, and **Karnataka** is the most affected state
- Total revenue = 395 | Revenue loss due to churn = 74 | CLTV lost = 2,047 | Revenue loss = 18.7%
- Monthly vs annual churn = **55.6% vs 8.3%**
- Escalations are strongly linked to churn (correlation 0.88)
- One user moved to a competitor

## Action Items
- Check what happened in Karnataka: price increase, user complaints, tech issues, etc.
- Check if the Basic plan price or any other change was made, especially in September
- Check what competitors are doing, because one user has moved to a competitor
- Focus on customers with **High** and **Med** churn risk: check their CLTV to make a priority list, review complaint requests, and reach out by email, SMS or call to fix their issues

## Repository Structure
```
├── README.md
├── churn_analysis.ipynb
├── customer_churn.db
├── exported_churn_data.csv
├── Churn_Analysis_Report.pdf
├── requirements.txt
└── .gitignore
```

## How to Run
```bash
git clone https://github.com/AnuragArya93/customer-churn-analysis.git
cd customer-churn-analysis
pip install -r requirements.txt
jupyter notebook churn_analysis.ipynb
```
Use the relative path `customer_churn.db` in the notebook's `sqlite3.connect(...)`.

## Author
**Anurag Arya** · B.Tech (CSE - Data Science) · anurag1803arya@gmail.com · [GitHub](https://github.com/AnuragArya93)
