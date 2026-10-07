# 04 — US Baby Names

SSA state files, 1910–2021. All-time popular names, gender-ambiguous names, and which names swung in birth-share between the early 1980s and 2017–21.

Notebook: [analysis.ipynb](analysis.ipynb)

Data on Kaggle: `paprikaryash/datasets-1` (51 state files, no header). The notebook also checks a local `datasets/` folder.

## Problem

- A1 — What is in the files (years, states, sexes, quality)?
- A2 — Most popular name of all time?
- A3 — Most gender-ambiguous name in 2013 and in 1945?
- A4 / A5 — Which names rose or fell in birth-share, 1980–84 vs 2017–21? What does that metric miss?
- B — How much of births sit in names used by both sexes, and do those names stay balanced?

## Data

Grain: `state`, `sex`, `year`, `name`, `count`.

6,311,504 rows, 1910–2021, 51 files (states + DC). SSA privacy floor: a name with fewer than 5 births in that state-year-sex is absent. No header row.

## Approach

1. Concatenate 51 files, name the columns, check nulls and duplicate keys.
2. A2: sum `count` by `name` across states, years, and sexes.
3. A3: for a year, unstack M/F, keep names with both sexes and total ≥ 50, rank by `min(M,F)/max(M,F)`.
4. A4: change in mean birth-share, 1980–84 vs 2017–21, only names present in both windows. Drop the bottom half of 1980s shares so a tiny base cannot print a huge percent.
5. A5: list debuts and extinct names that A4 cannot score.
6. B: yearly unisex volume vs balance; a few name trajectories.

## Concepts used

- Multi-file concat and a privacy floor
- Raw count vs popularity (share of that year's births)
- Ratio metric for gender split, plus a volume floor
- Panel comparison across two time windows
- Censoring: names that appear or vanish cannot get a finite percent change
- Unisex volume vs unisex balance

## Q & A

**Most popular all-time?**  
**James**, 5,054,074 births. Longevity at the top for boys, not a current-trend result. Next are John, Robert, Michael, William. **Mary** leads girls at 3,747,982, then Patricia, Elizabeth, Jennifer, Linda.

**Ambiguous in 2013 / 1945?**  
Ambiguity is `min(M,F)/max(M,F)`, both sexes, at least 50 births that year. 2013: **Nikita**, 47 female / 47 male, ratio 1.00. Runners-up Jael and Milan. 1945: **Lavern**, 70 female / 74 male, ratio 0.95. Runners-up Frankie and Leslie, at higher volume. Different inventory, not the same names getting more even.

**Biggest share swings?**  
Among names in both windows, **Grayson** is the largest percent increase, on the order of +33,200% in mean birth-share. Liam and Ava are the recognizable version of the same move. The bigger story sits outside the metric: Harper, Sawyer, and River debut after the 1980s window, and names that die out have no finite percent change. A4 cannot score those.

**Are more babies getting unisex names?**  
Volume in names used by both sexes is not the same as those names staying 50/50. Many “unisex” names drift female and stay there (Taylor, Leslie).

## Caveats

- Spellings are separate names.
- SSA coverage is weak before about 1937.
- The count floor of 5 hides rare names.
- Raw count is not popularity when the number of births changes.

## Tools

Python, pandas, matplotlib, Jupyter
