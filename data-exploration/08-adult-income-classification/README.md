# 08 — Adult Income Classification

UCI Adult / OpenML `adult` (version 2): predict whether income exceeds $50K from 1994 US Census features.

Notebook: [analysis.ipynb](analysis.ipynb)

**Dataset:** ~48,842 rows. Target ~24% >50K.

## Problem

Binary classification: `income` >50K vs <=50K.

## Data

Loaded via `sklearn.datasets.fetch_openml(name="adult", version=2)`.

Key columns: age, workclass, education-num, marital-status, occupation, relationship, race, sex, capital-gain, capital-loss, hours-per-week, native-country.

Dropped: `fnlwgt` (sampling weight), `education` (redundant with education-num).

## Approach

1. Load and inspect (shape, missing, target balance).
2. Clean: create binary target, drop redundant/non-predictive columns.
3. Stratified train/test split.
4. Shared preprocessor (`ColumnTransformer`): median impute + scale numeric; most-frequent impute + one-hot categorical. Fit only on train.
5. Compare models with `class_weight="balanced"`:
   - Logistic Regression
   - Decision Tree (max_depth=8)
   - Random Forest
   - Linear SVM
   - GaussianNB
6. Evaluate with stratified 5-fold CV + test-set F1 (positive class) and ROC-AUC.
7. Confusion matrices and results summary.

## Concepts used

- Mild class imbalance and why accuracy is misleading
- Leakage-free preprocessing with Pipeline + ColumnTransformer
- `class_weight="balanced"` for higher recall on the minority class
- Linear vs tree-based models
- Proper metrics: F1 on >50K and ROC-AUC

## Key findings

- Best model: **Random Forest** (CV F1 ~0.689, ROC-AUC ~0.915)
- Linear models (LR, Linear SVM) are strong baselines (~0.90 AUC)
- Single tree almost matches logistic regression; forest reduces variance
- GaussianNB fails after one-hot (independence + Gaussian assumptions)
- Balanced class weights trade precision for higher recall on >50K

## Tools

Python, pandas, scikit-learn, matplotlib, seaborn, Jupyter

## How to run

From the repo root, with the project environment activated:

```text
jupyter notebook data-exploration/08-adult-income-classification/analysis.ipynb
```

The notebook fetches the dataset from OpenML on first run.
