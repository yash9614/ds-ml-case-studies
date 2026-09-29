# DS / ML Case Studies

Portfolio repository of data science case studies. Each folder is one problem: business question, notebook, and a short write-up.

## Case studies

### 01 — Resolving Duplicate Transactions

Amazon retail transactions with suspected duplicate records.

- Identify duplicate vs legitimate repeat purchases
- Apply an explicit keep/remove rule
- Report cleaned revenue and caveats for operations

Path: [data-exploration/01-resolving-duplicate-transactions](data-exploration/01-resolving-duplicate-transactions)

### 02 — Beer Data Analysis

Rank breweries, years, rating factors, recommendations, and styles.

Path: [data-exploration/02-beer-data-analysis](data-exploration/02-beer-data-analysis)

### 03 — Driver Lifetime Value

Lyft rides: fare a completed trip, estimate driver LTV, and segment who actually produces value.

- Rate-card fare and driver-pay
- 30-day recency churn rule (right-censored lifetimes)
- Historical vs near-term LTV
- Rule-based segments checked with K-Means

Path: [data-exploration/03-driver-lifetime-value](data-exploration/03-driver-lifetime-value)

## Setup

```text
uv venv
.\.venv\Scripts\Activate.ps1
uv pip install -r requirements.txt
jupyter notebook
```

## Tools

Python, pandas, scikit-learn, matplotlib, NLTK (VADER), Jupyter, uv
