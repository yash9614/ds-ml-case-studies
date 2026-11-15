# Laptop Price Prediction

**StrataScratch Data Project** | E-commerce & Retail Data Scientist Interview Loop (Round 3)

Predict laptop `buynow_price` from specifications. Goal: minimize **RMSE**.

## Approach

- Dropped incomplete rows for cleaner signal (following official solution style)
- Feature engineering:
  - Split resolution into `resolution_x` / `resolution_y`
  - Extracted numeric RAM (GB) and screen size
  - Multi-hot encoded list columns (`communications`, `input devices`, `multimedia`, `operating system`)
  - One-hot encoded remaining categoricals
- Iterative **VIF** filtering (removed features with VIF > 20)
- Compared multiple models (Linear, RandomForest, GradientBoosting, ExtraTrees, Voting)
- Final model: **Weighted Voting Regressor** (GradientBoosting + ExtraTrees + RandomForest)

## Results (approximate, depends on exact run)

| Model              | Test RMSE |
|--------------------|-----------|
| RandomForest       | ~557      |
| GradientBoosting   | ~527      |
| ExtraTrees         | ~578      |
| **Voting Regressor** | **~505** |

## How to run

1. Download the three JSON files from StrataScratch (`train_dataset.json`, `val_dataset.json`, `test_dataset.json`).
2. Place them in a `data/` folder next to the notebook.
3. Open `analysis.ipynb` and run all cells.

## Dataset

The original datasets are **not included** in this repository (they require a StrataScratch login).  
Download them from:  
https://platform.stratascratch.com/data-projects/laptop-price-prediction

## Notes

- Inspired by the official StrataScratch solution approach (VIF filtering + weighted Voting Regressor).
- Best single model was GradientBoosting; the ensemble further improved it.
- Feature importance is dominated by RAM, resolution, CPU, and certain binary flags (e.g. illuminated keyboard).
