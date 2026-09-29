# 02 — Beer Data Analysis

Beer reviews: strongest breweries, which years rate highest, which rating factors move overall score, three beers to recommend, and favourite style from written text.

Notebook: [analysis.ipynb](analysis.ipynb)

Data: `data/BeerDataScienceProject.tar.bz2` (~529k review rows).

## Problem

1. Which breweries produce the strongest beers (ABV)?
2. Which year has the highest ratings?
3. Which factors (appearance, palette, taste, aroma) matter most for overall score?
4. Recommend three beers with enough review volume.
5. Favourite style from review text, and does text sentiment match stars?

## Data

Columns include `beer_ABV`, `beer_beerId`, `beer_brewerId`, `beer_name`, `beer_style`, `review_appearance`, `review_palette`, `review_overall`, `review_taste`, `review_aroma`, `review_profileName`, `review_text`, `review_time`.

Source: StrataScratch / Whole Foods beer reviews.

## Approach

1. Drop 0 overall / 0 appearance ratings (3 rows).
2. Drop rows missing ABV, reviewer, or text (→ 508,355).
3. One review per user–beer, keep the highest overall (→ 503,697).
4. Q1: one row per beer, then mean ABV by brewery.
5. Q2: year from `review_time`, mean overall, watch small-n years.
6. Q3: beer-level mean ratings, correlation with overall.
7. Q4: beers with >200 reviews, rank by mean overall.
8. Q5: VADER on review text, style with highest mean sentiment; correlate sentiment vs stars for that style.

## Concepts used

- Deduping to the analysis grain (beer vs review vs user–beer)
- Avoiding review-volume bias on brewery ABV
- Small-n years vs high-volume years
- Correlation on aggregated ratings
- Volume floor before recommending a beer
- Lexicon sentiment (VADER) vs star ratings

## Q & A

**Strongest breweries?**  
By mean ABV, one row per beer: brewery `6513` (~24.7, 10 beers), `736` (~13.5, 3 beers), `24215` (~12.5, 3 beers). #2 and #3 are tiny samples.

**Best year?**  
2000 has the highest mean but only 29 reviews. Among years with real volume: **2010** (~3.87, n ≈ 90k).

**What moves overall score?**  
Aroma (corr ~0.88) > taste (~0.82) > palette (~0.77) > appearance (~0.64), on beer-level means.

**Three beers to recommend?**  
Citra DIPA, Heady Topper, Founders CBS Imperial Stout (mean overall, >200 reviews).

**Favourite style from text?**  
Quadrupel (Quad). Sentiment vs overall stars for Quads: **0.26** (positive, weak). Stars and write-ups are not the same thing.

## Caveats

- High-ABV brewery ranks are sensitive to a few extreme beers.
- Dropping missing ABV removes beers from Q1.
- VADER is a general English lexicon, not beer-specific.
- Notebook currently hard-codes a local Windows path; point it at `data/BeerDataScienceProject.tar.bz2`.

## Tools

Python, pandas, NLTK (VADER), Jupyter, uv
