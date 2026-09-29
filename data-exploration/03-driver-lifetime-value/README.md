# 03 — Driver Lifetime Value

Lyft / StrataScratch take-home: what is a driver worth over their time on the platform, and do all drivers look the same?

Notebook: [analysis.ipynb](analysis.ipynb)

Data lives on Kaggle (`paprikaryash/datasets1i`). Paths at the top of the notebook.

## Problem

After exploring the three tables, answer:

1. Recommend a Driver Lifetime Value.
2. What mainly moves LTV?
3. Once onboarded, how long does a driver typically stay?
4. Do drivers act alike, or are there higher-value segments?
5. What should the business do?

Rate card used for fare:

- Base $2.00, $1.15/mile, $0.22/min
- Service fee $1.75
- Min $5, max $400
- Prime time is a percent on the variable fare

## Data

| File | Grain | Fields |
|---|---|---|
| `driver_ids.csv` | driver | `driver_id`, `driver_onboard_date` |
| `ride_ids.csv` | completed ride | `driver_id`, `ride_id`, distance (m), duration (s), prime time |
| `ride_timestamps.csv` | ride event | `ride_id`, `event`, `timestamp` (UTC) |

Window we actually see: onboard 28 Mar–15 May 2016, events through 27 Jun 2016. Nobody in this file has a multi-year career.

## Approach

1. Check shapes, missingness, join keys, date range.
2. Price each ride from the rate card. Driver-pay = fare − $1.75 fee.
3. Roll up to one row per driver (including the 83 who never rode).
4. Call a driver churned if last trip was >30 days before the snapshot.
5. Historical LTV = sum of driver-pay in-window.
6. Near-term LTV (v2) = historical + 30 extra days at that driver's own $/active-day, but only if they are still active. v1 (use mean lifetime of *churned* people as "typical career") adds $0 of future value and is kept in the notebook as a cautionary example.
7. Name three operating segments by hand, then run 3-means on scaled rides / $/day / recency to see if the machine rediscovers them.

## Concepts used

- Unit conversion and a capped fare function (min/max fare, prime multiplier)
- Left joins and coverage gaps (rides without drop-off timestamps)
- Right-censoring: active drivers have not finished a lifetime
- Heuristic churn (recency threshold), not a survival model
- Historical value vs a labeled short-horizon projection
- Rule-based segmentation vs K-Means on standardized features
- Pareto / concentration (share of pay vs share of drivers)

## Q & A

**What LTV number do you recommend?**  
Two numbers, labeled. Mean historical driver-pay is about **$2,000** (median ~$1,890). If active drivers keep their current daily rate for 30 more days, mean near-term LTV is about **$2,900**. Do not publish a 3-year LTV from 90 days of data.

**Is that Lyft revenue?**  
No. It is driver-pay after the $1.75 fee. A rough Lyft fee floor is `$1.75 × rides` (~$347 mean historically; ~$696 on high workhorses, ~$53 on the exited cluster).

**What moves LTV?**  
Whether they take rides in week 1, how many days they stay spanning first→last trip, and intensity (`rides/day` and `$/active day`). Prime and average trip length barely differ across segments.

**How long do they last?**  
Not one number. Churned drivers last **~13 days** on average (**~20** if they completed at least one ride). Survivors have already been onboarded **~68 days** and are still active — that clock is censored. The blended 54-day mean is a bad headline.

**Do they act alike?**  
No. 83 never started (9%, $0). 159 rode then went quiet (17%, ~$558, 4.7% of pay). 695 workhorses (74%) produce **95% of driver-pay**. K-Means splits workhorses into high intensity (~$66/day, ~$4.0k hist) and steady (~$21/day, ~$1.3k hist).

**What should ops do?**  
Put effort on the first 7–14 days. Run two live playbooks (keep the $66/day group; raise frequency for the $21/day group). Win-back on 30-day silent drivers should be cheap — their historical value is already small. Plan a new onboard at $2.0k–$2.9k driver-pay with a ~25% chance it is near zero.

## Caveats

- 30-day silence will mis-label vacations.
- 8.6k rides have no drop-off timestamp; first/last trip can be slightly off.
- v2's extra 30 days is an assumption, not estimated remaining life.
- Sample is San Francisco, spring 2016.

## Tools

Python, pandas, numpy, scikit-learn (K-Means), matplotlib, Jupyter
