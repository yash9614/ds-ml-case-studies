# 07 — AeroFit Treadmill Buyer Profile

Customer profiling for AeroFit treadmills (KP281, KP481, KP781) using EDA, contingency tables, and conditional probability.

Notebook: [analysis.ipynb](analysis.ipynb)

**StrataScratch:** Treadmill Buyer Profile (Easy, Business Analysis)

## Problem

Recommend the right treadmill to new customers.
- KP281: $1,500 entry-level
- KP481: $1,750 mid-level
- KP781: $2,500 premium

## Data

File: `data/aerofit_treadmill_data.csv`

180 customers, 9 columns, 0 missing values.

Columns: `Product`, `Age`, `Gender`, `Education`, `MaritalStatus`, `Usage`, `Fitness`, `Income`, `Miles`

Source: StrataScratch / AeroFit

## Approach

1. Data quality check (shape, types, missing values, describe).
2. Product mix (counts and proportions).
3. Two-way contingency tables for categorical features.
4. Conditional probabilities: P(feature | product) and P(product | feature).
5. Grouped medians and boxplots for numeric features (Age, Education, Usage, Fitness, Income, Miles).

## Concepts used

- Contingency tables (crosstab) and marginals
- Conditional probability from row vs column normalization
- Buyer profiles from joint distributions
- Separating strong splitters (gender, fitness, income) from weak ones (age, marital status)
- Sample is buyers only — not the full market

## Key findings

- Mix: KP281 44.4% · KP481 33.3% · KP781 22.2%
- P(Male | KP781) = 82.5%; P(KP781 | Female) = 9.2%
- KP781 buyers have higher fitness, income, usage, and expected miles
- Age does not separate products well
- Marital status is a weak splitter compared with gender and fitness

## Product profiles

- **KP281:** first-time / general buyers, mixed gender, moderate fitness
- **KP481:** mid-range buyers, slightly higher usage than KP281
- **KP781:** high-fitness, higher-income, mostly male, higher weekly miles

## Recommendations

1. Default to KP281 unless fitness, miles, and income are high.
2. Gate KP781 on fitness 4–5 + higher usage/income.
3. Do not use the same pitch for male and female customers.
4. Ask usage, fitness, and budget before recommending.
5. Treat this as a buyer-only sample, not the full market.

## Q & A

**What separates the products?**  
Fitness, income, usage, and expected miles. KP781 is the clear high-end cluster.

**Does gender matter?**  
Yes for the premium model. Females rarely buy KP781 (9.2%).

**Is age useful?**  
No. Medians are similar across products.

**What should sales ask first?**  
Usage, fitness level, and budget.

## Tools

Python, pandas, numpy, matplotlib, seaborn, Jupyter

## How to run

From the repo root, with the project environment activated:

```text
jupyter notebook data-exploration/07-aerofit-treadmill-buyer-profile/analysis.ipynb
```
