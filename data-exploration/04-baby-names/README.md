# 04 — US Baby Names

SSA state files, 1910–2021: all-time popular names, gender-ambiguous names, and which names swung between the early 1980s and 2017–21.

Notebook (still at the data-exploration root): [../baby-names-project.ipynb](../baby-names-project.ipynb)

Data on Kaggle: `paprikaryash/datasets-1` (51 state files, no header).

## Problem

- A1 — What is in the files (years, states, sexes, quality)?
- A2 — Most popular name of all time?
- A3 — Most gender-ambiguous name in 2013 and in 1945?
- A4 / A5 — Which names rose or fell in birth-share, 1980–84 vs 2017–21? What does that metric miss?
- B — How much of births sit in names used by both sexes, and do those names stay balanced?

## Data

Grain: `state`, `sex`, `year`, `name`, `count`.

~6.31M rows, 1910–2021, 51 files (states + DC). SSA privacy floor: names with fewer than 5 births in that state-year-sex are absent.

## Approach

1. Concatenate 51 files, name the columns, check nulls and duplicate keys.
2. A2: sum `count` by `name` across states, years, sexes.
3. A3: for a year, unstack M/F, keep names with both sexes and total ≥ 50, rank by `min(M,F)/max(M,F)`.
4. A4: change in mean birth-share, 1980–84 vs 2017–21, only names present in both windows.
5. A5: list debuts and extinct names that A4 cannot score.
6. B: yearly unisex volume vs balance; pick a few name trajectories.

## Concepts used

- Multi-file concat and a privacy floor
- Raw count vs popularity (share of that year's births)
- Ratio metric for gender split, plus a volume floor
- Panel comparison across two time windows
- Censoring: names that appear or vanish cannot get a finite % change
- Unisex volume vs unisex balance

## Q & A

**Most popular all-time?**  
**James** (~5.05M). Longevity at the top for boys, not a current-trend result. **Mary** leads among girls.

**Ambiguous in 2013 / 1945?**  
Ambiguity = min(M,F)/max(M,F), both sexes, ≥50 births that year. 2013 headline: **Nikita** (47/47). 1945 inventory looks different (Frankie / Leslie / Jessie class), not the same names getting more even.

**Biggest share swings?**  
Among names in both windows: winners in the notebook include **Grayson** / **Jill** depending on direction. Recognizable cousins: Liam, Ava vs Kristin / Jennifer-class. Bigger moves sit in debuts (Harper, Sawyer, River) and names that died out — A4 cannot score those.

**Are more babies getting unisex names?**  
Volume in names used by both sexes is not the same as those names staying 50/50. Many “unisex” names drift female and stay there (Taylor, Leslie).

## Caveats

- Spellings are separate names.
- SSA coverage is weak before ~1937.
- Min count 5 hides rare names.
- Raw count ≠ popularity when birth totals change.

## Tools

Python, pandas, matplotlib, Jupyter
