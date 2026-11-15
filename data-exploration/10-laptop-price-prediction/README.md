# Laptop Price Prediction

**StrataScratch Data Project** | E-commerce & Retail Data Scientist Interview Loop (Round 3)

Predict laptop `buynow_price` from specifications. Goal: minimize **RMSE**.

## Approach

- Val/test integrity checks (NaN rates + unseen-category counts)
- All preprocessing inside `Pipeline` + `ColumnTransformer` with `OneHotEncoder(handle_unknown="ignore")`
- Feature engineering: RAM/screen extraction, resolution split, list flattening
- 5-fold CV mean ± std for model selection
- Weighted Voting Regressor (GradientBoosting + ExtraTrees + RandomForest)
- Permutation importance grouped by parent feature

## Results

Exact numbers depend on the run and whether rows are dropped. Official-style dropna + VIF path targets ~505 test RMSE; an imputation-only path was higher (~797). The notebook reports CV mean ± std so the choice is not a single-split artifact.

## How to run

1. Download the three JSON files from StrataScratch.
2. Place them in a `data/` folder next to the notebook.
3. Open `analysis.ipynb` and run all cells.

## Dataset

Not included (StrataScratch login required).  
https://platform.stratascratch.com/data-projects/laptop-price-prediction
