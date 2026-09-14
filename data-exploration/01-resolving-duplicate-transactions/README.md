# Resolving Duplicate Transactions

StrataScratch-style retail case study: clean suspected duplicate Amazon transaction records and report revenue the operations team can use.

## Problem

Retail operations suspects duplicate rows in `amazon_customer_transactions.csv`. The task is to identify duplicates, define a keep/remove rule, calculate cleaned revenue, and flag what still needs a human check.

## Dataset

File: `data/amazon_customer_transactions.csv`

Columns: `transaction_id`, `customer_id`, `product`, `amount`, `order_timestamp`, `recorded_at`

Source: StrataScratch

## Approach

1. Inspect shape, types, missing values, and exact row copies.
2. Check uniqueness of `transaction_id` vs repeat `customer_id`.
3. Review every repeated `transaction_id` by timestamps and amount.
4. Separate exact copies from possible later corrections.
5. Apply one explicit rule and compare revenue before vs after.

## Duplicate-resolution rule

Keep **one row per `transaction_id`**: the row with the **latest `recorded_at`**.

Why: exact copies are logging duplicates; a later `recorded_at` with a different `amount` looks like a correction, not a new sale. Repeat purchases by the same customer are kept if they have different `transaction_id`s.

## Key findings

- Rows: 81 → 76
- Exact copy IDs: 8110, 8136, 8162
- Possible corrections: 8123 (21 → 30), 8157 (38 → 33)
- Revenue before: 4795
- Revenue after: 4590
- Difference: 205

## Recommendation

Use **4590** as cleaned revenue, subject to ops confirming that later `recorded_at` means a correction.

## Tools

Python, pandas, Jupyter, uv

## How to run

From the repo root, with the project environment activated:

```text
jupyter notebook