# DS / ML Case Studies

Portfolio repository of data science case studies. Each folder is one problem: business question, notebook, and a short write-up.

## Case studies

### 01 — Resolving Duplicate Transactions

Amazon retail transactions with suspected duplicate records.

- Identify duplicate vs legitimate repeat purchases
- Apply an explicit keep/remove rule
- Report cleaned revenue and caveats for operations

Path: [data-exploration/01-resolving-duplicate-transactions](data-exploration/01-resolving-duplicate-transactions)

## Setup

```text
uv venv
.\.venv\Scripts\Activate.ps1
uv pip install -r requirements.txt
jupyter notebook
```

## Tools
Python, pandas, NLTK (VADER), Jupyter, uv


In the **root** `README.md`, add this under Case studies (below the duplicate-transactions bullet):

```markdown
### 02 — Beer Data Analysis

Rank breweries, years, rating factors, recommendations, and styles.

Path: [data-exploration/02-beer-data-analysis](data-exploration/02-beer-data-analysis)