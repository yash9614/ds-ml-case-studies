# 05 — Telecom churn model

The source notebook was named as a Spotify assignment. The table is a telecom churn file: plans, minutes, charges, customer-service calls, area code. The write-up uses the table, not the filename.

Notebook: [analysis.ipynb](analysis.ipynb)

Data on Kaggle: `paprikaryash/dataset/Data_Science_Challenge.csv`.

## Problem

Predict which customers churn. Compare a linear model to two tree models, then say what actually moves churn.

## Data

3,333 customers, 21 columns, no missing values, unique phone numbers. Churn is 483 / 3,333, about 14.5%.

Columns used: international plan, voice mail plan, customer service calls, area code, usage minutes and calls. Phone number is an id and is dropped. State (51 levels) is dropped rather than one-hot encoded. Day, evening, night, and international charge columns are near-copies of the matching minute columns, so the charges are not a second signal.

## Approach

1. EDA: churn rate by international plan, voice-mail plan, and service-call count.
2. Map yes/no plans to 0/1. Dummy area code.
3. 80/20 stratified split. Test set still has about 97 churners. Scale features for logistic regression only, fit on train.
4. Logistic regression with `class_weight='balanced'`. Random forest with `class_weight='balanced'`. XGBoost with `scale_pos_weight`.
5. Compare precision, recall, F1, ROC-AUC, and PR-AUC at a 0.5 threshold. Plot ROC and precision-recall.
6. Read XGBoost importance against the EDA bars.

## Concepts used

- Class imbalance and a stratified split
- Scaling for the linear model only
- `class_weight` / `scale_pos_weight`
- ROC-AUC vs PR-AUC when positives are about 15%
- Leakage hygiene: no id columns, scaler fit on train
- Collinear minute and charge columns

## Q & A

**What separates churners before any model?**  
International plan = yes, and customer service calls at 4 or more. Voicemail plan is slightly protective. Accuracy is a bad headline: predicting nobody churns is already about 85.5% accurate.

**Which model, on the held-out 667 rows?**

| Model | Precision | Recall | F1 | ROC-AUC | PR-AUC | Accuracy |
|---|---:|---:|---:|---:|---:|---:|
| LogReg | 0.346 | 0.732 | 0.470 | 0.815 | 0.419 | 0.760 |
| Random forest | 0.891 | 0.588 | 0.708 | 0.891 | 0.789 | 0.930 |
| XGBoost | 0.755 | 0.763 | 0.759 | 0.895 | 0.815 | 0.930 |

Ship XGBoost. It wins PR-AUC and class-1 F1, and it does not trade recall away the way the forest does (57 of 97 churners caught by RF, 74 of 97 by XGB). LogReg recalls well and floods the offer list: 134 false positives against XGB's 24. Do not pick on accuracy. RF and XGB both print 0.930.

**What would ops do?**  
A call or offer after the third or fourth service call, and a different playbook for international-plan customers. Do not treat area-code dummies as a cause. Set the threshold from offer cost versus lost value, not from 0.5.

## Caveats

- Filename says Spotify. Features say telecom.
- No timestamp, so a random split is valid here. If this were sequential customers, 80/20 would overstate performance.
- The label is a snapshot flag, not “will leave in the next 30 days.”
- If high-risk customers later get discounts, the next training label is biased. Log the treatment.

## Tools

Python, pandas, scikit-learn, XGBoost, matplotlib, seaborn, Jupyter
