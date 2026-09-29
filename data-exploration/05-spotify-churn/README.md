# 05 — Churn model (Spotify assignment file)

The notebook is named `spotify_churn_model_mlasssignment.ipynb` but the table is a classic telecom churn file: plans, minutes, customer-service calls, area code.

Notebook: [../spotify_churn_model_mlasssignment.ipynb](../spotify_churn_model_mlasssignment.ipynb)

## Problem

Predict which customers churn. Compare a linear model to two tree models, then talk about what actually moves churn.

## Data

Typical columns: `international plan`, `voice mail plan`, `customer service calls`, `area code`, usage minutes/charges, `churn`, plus an id (`phone number`, `state`) dropped before fit.

## Approach

1. EDA: churn rate by international plan, voice-mail plan, and service-call count.
2. Drop id columns. Map yes/no plans to 0/1. Dummy `area code`.
3. 80/20 stratified split. Scale features for logistic regression only (fit on train).
4. Fit LogReg (`class_weight=balanced`), Random Forest, XGBoost (`scale_pos_weight`).
5. Compare precision/recall/F1, ROC-AUC, PR-AUC. Plot ROC and precision-recall.
6. Read feature importance / coefficients against the EDA bars.

## Concepts used

- Class imbalance and stratified split
- Scaling for linear models only
- `class_weight` / `scale_pos_weight`
- ROC-AUC vs PR-AUC when positives are rare
- Leakage hygiene: no id columns, scaler fit on train

## Q & A

**What should you look at first?**  
International plan and customer-service calls. Those two usually separate churners in this dataset before any model runs.

**Which model to ship?**  
Use the notebook metrics, not a default. Trees often beat LogReg on F1 here; LogReg is still the readable baseline. Pick on validation PR-AUC / F1 for the churn class, not accuracy.

**What would you do in production?**  
A call or offer after the 3rd+ service call, and a different playbook for international-plan customers. Do not treat area-code dummies as a causal story.

## Caveats

- Filename says Spotify; features say telecom. Label the write-up honestly.
- 0.5 threshold is a starting point, not an ops threshold.
- No time-based split in the notebook — if this were sequential customers, random 80/20 overstates performance.

## Tools

Python, pandas, scikit-learn, XGBoost, matplotlib, Jupyter
