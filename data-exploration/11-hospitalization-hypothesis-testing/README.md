# 11 — Hospitalization Hypothesis Testing (Apollo Hospitals)

StrataScratch data project: decode regional patterns and drivers of hospitalization charges using hypothesis testing and OLS regression.

## Questions
1. Which variables are significant in predicting the reason for hospitalization for different regions?
2. How well do viral load, smoking, and severity level describe the hospitalization charges?

## Data
`apollo_data.csv` — 1,338 anonymized COVID-19 hospital patients (Delhi regions).

Columns: age, sex, smoker, region, viral load, severity level, hospitalization charges.

## Key findings
- Viral load differs strongly across regions (ANOVA p ≈ 0).
- Hospitalization charges differ modestly by region (p = 0.031).
- Sex, smoker status, and severity do not differ by region.
- Smoker is the dominant cost driver (+≈ ₹59,000).
- OLS (viral load + smoker + severity) explains ~66% of charge variation (R² ≈ 0.66).

## StrataScratch evaluation
Score: **7.5 / 10** (Strong).  
Main feedback: add assumption checks (Levene, Shapiro, VIF, Breusch-Pagan) and effect-size notes for the borderline ANOVA.

## Files
- `01_eda.ipynb` — full analysis notebook (push from local)
- `apollo_data.csv` — raw data (optional; can be downloaded from StrataScratch)

## Run
```text
cd data-exploration/11-hospitalization-hypothesis-testing
jupyter notebook 01_eda.ipynb
```
