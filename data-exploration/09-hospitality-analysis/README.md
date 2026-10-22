# 09 — Hospitality Analysis (AtliQ Grands)

Business analysis of a hotel chain: occupancy, revenue, booking patterns, and property performance.

Notebook: [analysis.ipynb](analysis.ipynb)

## Problem

Analyze AtliQ Grands hotel chain performance across cities, room categories, and properties to improve occupancy and revenue.

## Data

Dimension and fact tables:

- `data/dim_hotels.csv`
- `data/dim_rooms.csv`
- `data/dim_date.csv`
- `data/fact_aggregated_bookings.csv`
- `data/fact_bookings.csv` (large)

Source: AtliQ Grands hospitality dataset.

## Approach

1. Load dimension and fact tables.
2. Occupancy rates by city, property, and room category.
3. Revenue generation and realization trends.
4. Weekday vs weekend booking patterns.
5. Identify top- and under-performing properties/cities.
6. Derive actionable recommendations.

## Key findings

- Mumbai generates the highest revenue.
- Occupancy is significantly higher on weekends than weekdays.
- Presidential rooms show higher occupancy rates.
- Certain properties consistently underperform.

## Recommendations

1. Focus marketing on underperforming cities (e.g. Bangalore).
2. Introduce weekend-specific packages and promotions.
3. Optimize pricing for Standard rooms to improve occupancy.
4. Investigate and improve low-revenue properties.

## Tools

Python, pandas, NumPy, matplotlib, seaborn, Jupyter

## How to run

From the repo root, with the project environment activated:

```text
jupyter notebook data-exploration/09-hospitality-analysis/analysis.ipynb
```
