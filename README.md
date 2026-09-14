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