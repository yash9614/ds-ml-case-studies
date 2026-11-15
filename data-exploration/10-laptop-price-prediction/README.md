# Laptop Price Prediction

**StrataScratch Data Project** | E-commerce & Retail Data Scientist Interview Loop (Round 3)

Predict laptop `buynow_price`. Goal: minimize **RMSE**.

## What this notebook does

- Integrity checks: NaN rates and % unseen categories on val/test vs train
- Feature engineering (RAM, screen, resolution split, list flattening)
- All preprocessing inside a `Pipeline` + `ColumnTransformer` with `OneHotEncoder(handle_unknown="ignore")`
  - Vocabularies learned from train only
  - No `drop_first`, no per-frame `get_dummies`, no `.align()`
- 5-fold CV RMSE mean ± std for Ridge, RandomForest, GradientBoosting, ExtraTrees, and a weighted Voting Regressor
- Mean-predictor baseline + MAE and MAPE on the test set
- Permutation importance grouped by parent feature
- Predicted-vs-actual plot

## What this notebook does **not** do

- Iterative VIF filtering
- Claim a specific test RMSE of ~505 (that figure comes from a different official solution that drops incomplete rows)
- Hyperparameter tuning (models use baseline settings)

## How to run

1. Download `train_dataset.json`, `val_dataset.json`, `test_dataset.json` from StrataScratch.
2. Place them in a `data/` folder next to the notebook.
3. Open `analysis.ipynb` and run all cells.

## Dataset

Not included (requires StrataScratch login).  
https://platform.stratascratch.com/data-projects/laptop-price-prediction
