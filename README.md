# Amazon Bestselling Books Analysis (2009-2019)

Exploratory data analysis of Amazon's top 50 bestselling books for each year from 2009 to 2019, using Python (pandas, seaborn, matplotlib).

## Dataset

- **Source:** Kaggle, *Amazon Top 50 Bestselling Books 2009 - 2019* (`bestsellers with categories.csv`). *(Add the link to the dataset page here.)*
- **Size:** 550 rows and 7 columns (50 titles per year across 11 years)
- **Missing values:** none
- **Exact duplicate rows:** none. Only 351 titles are unique, because many books are bestsellers in more than one year.

| Column | Type | Description |
|---|---|---|
| `Name` | text | Book title |
| `Author` | text | Author or publisher (248 unique) |
| `User Rating` | decimal | Average Amazon rating, 3.3 to 4.9 |
| `Reviews` | integer | Number of reviews, 37 to 87,841 |
| `Price` | integer | List price (assumed to be US dollars), 0 to 105 |
| `Year` | integer, then datetime | Year the book was a bestseller, 2009 to 2019 |
| `Genre` | text | Fiction (240 rows) or Non Fiction (310 rows) |

## Methods

1. **Loaded** the CSV with pandas and checked its shape and data types.
2. **Checked data quality:** confirmed there were no nulls with `info()`, and ran `drop_duplicates()` (no rows were removed).
3. **Converted** `Year` from integer to datetime (`pd.to_datetime(..., format="%Y")`).
4. **Formatted** `Price` as a dollar amount for display, keeping the underlying column numeric.
5. **Aggregated** with `groupby` and visualised the results:
   - Authors with the most bestseller appearances (bar chart)
   - Most reviewed titles, ranked by review count (bar chart)
   - Price over time by genre (line chart, mean with 95% confidence band)
   - Mean list price per year (line chart)
   - Total list price per year (bar chart)
6. **Tested the relationship** between price and number of reviews with a scatter plot and regression line, plus Pearson and Spearman correlation coefficients.

**Tools:** Python, pandas, seaborn, matplotlib, Jupyter Notebook

## Key observations

- The average list price of bestsellers fell from about $15.40 in 2009 to about $10.08 in 2019.
- Non-fiction bestsellers cost more on average than fiction (about $14.84 vs $10.85).
- Jeff Kinney has the most bestseller appearances of any author (12), followed by Suzanne Collins, Rick Riordan and Gary Chapman (11 each).
- The most reviewed titles are *Where the Crawdads Sing* (about 87,800 reviews), *The Girl on the Train* (about 79,400), *Becoming* (about 61,100), *Gone Girl* (about 57,300) and *The Fault in Our Stars* (about 50,500).
- Price and number of reviews have a very weak negative relationship (Spearman ρ ≈ -0.15, Pearson r ≈ -0.11): cheaper books tend to have slightly more reviews, but price explains very little of the variation.

## Limitations

- **The data contains no sales figures.** `Price` is a list price, so summing it measures total list price across entries, not revenue or units sold. Results should not be read as "sales".
- **Repeat entries.** Books that appear in several years are counted several times in yearly totals, and the rows are not fully independent.
- **Skewed review counts.** A few titles have far more reviews than the rest, which is why Spearman correlation is reported alongside Pearson.
- **12 books have a price of 0** (possibly free editions); it is unclear whether these are real values or missing data.
- This is descriptive analysis only. It shows patterns, not causes.

## How to run

```bash
pip install pandas seaborn matplotlib jupyter
jupyter notebook Analysis.ipynb
```

Place `bestsellers with categories.csv` in the same folder as the notebook.

## Possible next steps

- Compare average rating and price by genre across years
- Rank titles by rating only among books with a minimum number of reviews
- Test whether genre changes the price-review relationship
- Build a simple model to predict review count from price, genre and year
