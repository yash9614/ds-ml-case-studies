# 06 — Diversity clustering

US industry workforce composition, 2020–2023. Summary rows from the benchmark tables published with Google's Diversity Annual Report, not employee-level Google HR data. A row is a sector, subsector, industry group, or industry in a year.

Notebook: [analysis.ipynb](analysis.ipynb)

Data is not in the repo. Place `dataset-google.csv` next to the notebook, or run on Kaggle where the file is already mounted. The notebook checks both paths.

## Questions

1. Which sectors have a similar gender and ethnic structure?
2. Which three sectors are most gender-imbalanced, and how does that relate to size?
3. Which three sectors shifted most between 2021 and 2023?
4. Which sectors are dominated by one ethnic group?
5. Which sectors have the highest ethnic diversity, and how does that relate to size?
6. Can industries be grouped by ethnic composition?

Only 1 and 6 are clustering. The rest are sorts and indexes. K-Means on questions 2–5 would be the wrong tool.

## Decisions

- Grain is not mixed. Sector totals have a null `subsector`. Industry clustering uses rows with an industry name.
- `Total, 16 years and over` is a benchmark, not a sector.
- Shares are proportions. Two rows were stored on a 0–100 scale and divided by 100. The 2021 overall Asian share of 0.660 was divided by 10. Nail salons (~0.40 Asian) and computer equipment (~0.30) repeat across years and were left alone.
- Hispanic/Latino overlaps race. Shares are not renormalized to 1. Simpson diversity uses white, Black, Asian, and a residual other-race bucket.
- Employment is not a clustering feature. It is used to read clusters and to drop industries under 100,000 employed.
- Gender imbalance is distance from 50% women, not the lowest female share.
- Features are standardized before K-Means. Women's share otherwise dominates Euclidean distance.

## Results

Sector fit, 2023, k = 2, silhouette 0.544. Outlier group: construction, agriculture, mining (about 18% women, 89% white, low Black, low Asian, elevated Hispanic). 14.8 million employed, 11.9 million of it construction. The other ten sectors stay together, including education and health at 74% women. The split is composition, not gender.

Gender gaps, 2023: construction 10.8% women, mining 15.3%, transportation 24.3%. Education and health is fourth and female-skewed (74.4%). Mining is small. Construction and transportation are the scale gaps.

Largest mix shifts, 2021 to 2023: mining (Hispanic +5.4 points on 590,000 employed), financial activities, professional and business services. Shifts are a few points.

Every sector is white-dominated. Extreme: agriculture 92.6%, mining 87.7%, construction 87.5%. Simpson race diversity is highest in transportation (0.461) and public administration (0.440), lowest in agriculture (0.140). Larger sectors are not more diverse.

Industry fit, 81 industries with at least 100,000 employed, k = 3, silhouette 0.305. A three-industry high-Asian pocket (electronics, computer equipment, nail salons) sits apart. The other two groups — service and care, trades and property — overlap on the PCA plane. PC1 and PC2 explain 43.5% and 26.2%.

## What this uses from the ML notes

From [Nrish_Karik_SataDience/ML](https://github.com/yash9614/Nrish_Karik_SataDience/tree/main/ML):

- K-Means: choose k, `n_init`, `random_state`, inertia as within-cluster sum of squares. Silhouette replaces accuracy because there is no label.
- Scale before a distance model. Same reason the KNN notes scale features.
- PCA as a view of the fit, not as a clustering method.
- Hierarchical clustering is the natural alternative on 13 sector points. Not fit here. The sector silhouette is sharp enough that a dendrogram cut should land in the same place.
- DBSCAN is a poor fit for 13 sector points. No dense region versus noise, and epsilon would be a guess.
- Not used, on purpose: logistic regression, trees, boosting, RMSE, accuracy. Those need a target. The scale-error rows are data bugs, not isolation-forest anomalies.
