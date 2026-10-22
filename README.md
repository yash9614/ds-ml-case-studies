# DS / ML Case Studies

Portfolio of data science case studies. Each numbered folder has a write-up and a notebook.

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

- 6.31M rows, 51 state files
- James 5.05M all-time; Mary leads girls
- Ambiguity is a ratio with a volume floor: Nikita in 2013, Lavern in 1945
- Share-change misses debuts (Harper, Sawyer) and names that die out

Path: [data-exploration/04-baby-names](data-exploration/04-baby-names)

### 05 — Telecom churn model

Classification on a telecom churn table. The notebook filename used to say Spotify.

- 3,333 customers, 14.5% churn
- International plan and service calls separate churners before the model
- XGBoost leads on PR-AUC 0.815 and class-1 F1 0.759; accuracy ties the forest and is the wrong metric

Path: [data-exploration/05-spotify-churn](data-exploration/05-spotify-churn)

### 06 — Diversity clustering

US industry workforce composition, 2020–2023. Summary rows, not employee records. Sector and industry clustering on gender and race/ethnicity shares.

- Scale errors repaired before any fit. Hispanic share overlaps race and is not renormalized.
- Sector k = 2, silhouette 0.544: construction, agriculture, mining vs the rest. Split is composition, not gender.
- Industry k = 3, silhouette 0.305: a high-Asian pocket and two overlapping groups (service/care, trades/property).
- Questions on imbalance, year shift, dominance, and Simpson diversity are sorts, not models.

Path: [data-exploration/06-diversity-clustering](data-exploration/06-diversity-clustering)

### 07 — AeroFit Treadmill Buyer Profile

Customer profiling for AeroFit treadmills (KP281, KP481, KP781) using EDA, contingency tables, and conditional probability.

- 180 buyers, 9 features, 0 missing values
- Mix: KP281 44.4% · KP481 33.3% · KP781 22.2%
- P(Male | KP781) = 82.5%; P(KP781 | Female) = 9.2%
- KP781 buyers have higher fitness, income, usage, and expected miles
- Age and marital status are weak splitters

Path: [data-exploration/07-aerofit-treadmill-buyer-profile](data-exploration/07-aerofit-treadmill-buyer-profile)

### 08 — Adult Income Classification

UCI Adult / OpenML adult: predict income >50K from 1994 US Census features.

- ~48,842 rows, ~24% >50K
- Compared Logistic Regression, Decision Tree, Random Forest, Linear SVM, GaussianNB
- Random Forest best (CV F1 ~0.689, ROC-AUC ~0.915)
- Leakage-free Pipeline + ColumnTransformer; class_weight="balanced"

Path: [data-exploration/08-adult-income-classification](data-exploration/08-adult-income-classification)

## Setup

```text
uv venv
.\.venv\Scripts\Activate.ps1
uv pip install -r requirements.txt
jupyter notebook
```

## Tools

Python, pandas, scikit-learn, XGBoost, matplotlib, NLTK (VADER), Jupyter, uv
