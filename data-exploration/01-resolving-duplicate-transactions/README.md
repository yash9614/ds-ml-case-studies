# 01 — Resolving Duplicate Transactions

StrataScratch-style retail cleanup: suspected duplicate Amazon transactions, one explicit keep/remove rule, revenue ops can use.

Notebook: [analysis.ipynb](analysis.ipynb)

## Problem

Retail operations thinks `amazon_customer_transactions.csv` has duplicate rows. Identify duplicates vs legitimate repeats, apply one rule, report cleaned revenue, and flag what still needs a human.

## Data

File: `data/amazon_customer_transactions.csv`

Columns: `transaction_id`, `customer_id`, `product`, `amount`, `order_timestamp`, `recorded_at`

Source: StrataScratch

## Approach

1. Shape, types, missing values, exact row copies.
2. Uniqueness of `transaction_id` vs repeat `customer_id`.
3. Review every repeated `transaction_id` by timestamps and amount.
4. Separate exact copies from possible later corrections.
5. Apply one rule and compare revenue before vs after.

## Rule

Keep **one row per `transaction_id`**: the row with the **latest `recorded_at`**.

Exact copies are logging duplicates. A later `recorded_at` with a different `amount` looks like a correction, not a new sale. Same customer, different `transaction_id` = keep both.

## Concepts used

- Exact row duplicates vs key collisions
- Business key (`transaction_id`) vs natural repeats (`customer_id`)
- Latest-record-wins as a correction rule
- Before/after revenue as the ops metric
- Explicit caveat when the rule is an assumption

## Q & A

**What did you find?**  
81 rows → 76 after the rule. Exact copy IDs: 8110, 8136, 8162. Possible corrections: 8123 (21 → 30), 8157 (38 → 33).

**What revenue should ops use?**  
**4590** after cleanup vs 4795 raw. Difference **205**. Subject to ops confirming that later `recorded_at` means a correction.

**Did you drop repeat purchases?**  
No. Repeats with a new `transaction_id` stay.

**What still needs a human?**  
The two amount-change IDs. If those are new sales logged under a reused id, the rule understates revenue.

## Tools

Python, pandas, Jupyter, uv

## How to run

From the repo root, with the project environment activated:

```text
jupyter notebook data-exploration/01-resolving-duplicate-transactions/analysis.ipynb
```
