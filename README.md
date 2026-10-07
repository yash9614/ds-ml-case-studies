# DS / ML Case Studies

Portfolio of data science case studies. Each numbered folder has a write-up. Notebooks live in the folder when they were added that way; two older notebooks still sit under `data-exploration/` and are linked from 04 and 05.

## Case studies

### 01 — Resolving Duplicate Transactions

Amazon retail transactions with suspected duplicate records.

- Identify duplicate vs legitimate repeat purchases
- Latest `recorded_at` per `transaction_id`
- Cleaned revenue 4590 vs 4795 raw

Path: [data-exploration/01-resolving-duplicate-transactions](data-exploration/01-resolving-duplicate-transactions)

### 02 — Beer Data Analysis

Rank breweries by ABV, years by rating, which score factors matter, recommend three beers, favourite style from text.

Path: [data-exploration/02-beer-data-analysis](data-exploration/02-beer-data-analysis)

### 03 — Driver Lifetime Value

Lyft rides: fare a completed trip, estimate driver LTV, segment who produces value.

- Rate-card fare and driver-pay
- 30-day recency churn (right-censored lifetimes)
- Historical vs near-term LTV
- Rule-based segments checked with K-Means

Path: [data-exploration/03-driver-lifetime-value](data-exploration/03-driver-lifetime-value)

### 04 — US Baby Names

SSA 1910–2021: all-time popular names, gender-ambiguous names, share swings vs the 1980s.

Path: [data-exploration/04-baby-names](data-exploration/04-baby-names)  
Notebook: [data-exploration/baby-names-project.ipynb](data-exploration/baby-names-project.ipynb)

### 05 — Churn model

Classification on a telecom-style churn table (notebook filename says Spotify).

Path: [data-exploration/05-spotify-churn](data-exploration/05-spotify-churn)  
Notebook: [data-exploration/spotify_churn_model_mlasssignment.ipynb](data-exploration/spotify_churn_model_mlasssignment.ipynb)

### 06 — Diversity clustering

US industry workforce composition, 2020–2023. Summary rows, not employee records. Sector and industry clustering on gender and race/ethnicity shares.

- Scale errors repaired before any fit. Hispanic share overlaps race and is not renormalized.
- Sector k = 2, silhouette 0.544: construction, agriculture, mining vs the rest. Split is composition, not gender.
- Industry k = 3, silhouette 0.305: a high-Asian pocket and two overlapping groups (service/care, trades/property).
- Questions on imbalance, year shift, dominance, and Simpson diversity are sorts, not models.

Path: [data-exploration/06-diversity-clustering](data-exploration/06-diversity-clustering)

## Setup

```text
uv venv
.\.venv\Scripts\Activate.ps1
uv pip install -r requirements.txt
jupyter notebook
```

## Tools

Python, pandas, scikit-learn, XGBoost, matplotlib, NLTK (VADER), Jupyter, uv
