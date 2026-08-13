# Google Play Store Apps - EDA Project

## 1. Project Overview
Exploratory Data Analysis of the Google Play Store apps dataset (10,841 apps). The work focuses on data cleaning (dirty string formats for Size, Installs, Price, Reviews, Android Version, dates), duplicate removal, and univariate/multivariate visualizations to answer questions about app categories, installs, ratings, and popularity. EDA-only - no machine learning.

**Notebooks:**
- `2.0-EDA&FE Google Playstore.ipynb` (has problem statement + markdown observations/insights)
- `1. EDA-Google playstore data.ipynb` (deeper technical cleaning, zero narrative)

## 2. Dataset
- **Source:** Google Play Store apps dataset (notebook 2 loads from krishnaik06/playstore-Dataset GitHub raw URL)
- **File:** `googleplaystore.csv`
- **Rows x Columns:** 10,841 rows x 13 columns
- **Domain:** Mobile app marketplace (Android apps)
- **Target variable:** none - EDA-only, no prediction task
- **Columns:** App, Category, Rating, Reviews, Size, Installs, Type, Price, Content Rating, Genres, Last Updated, Current Ver, Android Ver
- **Note:** Notebook 2's markdown incorrectly claims "20 column and 10841 rows" (actual: 13 columns).

## 3. Objective / Problem Statement (quoted from notebook 2)
> "Today, 1.85 million different apps are available for users to download... Our Objective is to find the Most Popular Category, find the App with largest number of installs, the App with largest size etc."

Planned steps: 1. Data Cleaning, 2. Exploratory Data Analysis. (Notebook 1 has no stated objective.)

## 4. Technologies & Libraries
- Python 3 (Jupyter Notebook)
- pandas, numpy
- seaborn, matplotlib.pyplot (%matplotlib inline)
- warnings
- No sklearn, plotly, or other ML libraries

## 5. EDA Steps Performed
1. Load CSV; inspect columns, head/tail/sample, shape, describe(), info()
2. Duplicate handling: 483 exact duplicates -> drop_duplicates() (10,358 rows)
3. Type inspection: Reviews object dtype; `isnumeric()` check finds 1 bad row ("Life Made WI-Fi Touchscreen Photo Frame", Reviews="3.0M") -> dropped
4. Reviews -> int; Size parsed via custom function -> float; Installs/Price punctuation stripped -> int/float
5. `Last Updated` -> datetime; extract day/month/year; drop the date column
6. Android Ver cleaned (" and up" / "Varies with device" removed)
7. Drop duplicates on App (keep first) -> 10,357 rows (notebook 1)
8. Feature split: categorical vs numerical
9. Univariate: value counts, countplots, distplots, KDE
10. Category popularity: pie chart, top-10 barplot, installs per category (groupby sum)
11. Boxplots of Rating (alone and vs Installs)
12. (Notebook 2) Missing-value check: Rating 1474, Type 1, Content Rating 1, Current Ver 8, Android Ver 3

## 6. Data Cleaning / Preprocessing
- Exact duplicates removed (483); duplicate Apps removed (1,181 in notebook 2, keep first)
- One malformed Reviews row removed; Reviews cast to int
- Size parsing: notebook 1 uses custom function (M->x1024 KB, k->value); notebook 2 uses string replace (`M`->`000`) - **flawed**, see section 10
- Installs/Price: stripped `+`, `,`, `$` -> int/float
- Last Updated -> datetime -> day/month/year columns
- Android Ver text stripped
- **Null handling: none** - Rating (1,474 nulls), Type, Content Rating, Current Ver, Android Ver nulls left untouched. No imputation anywhere.
- **Encoding/scaling: not found** in either notebook

## 7. Visualizations Used
| Chart | What it shows |
|---|---|
| countplots: Type, Content Rating | Free (92.2%) vs Paid (7.8%); content rating distribution |
| distplot/KDE: Price, Rating | Distributions of price and ratings |
| Pie chart of Category | Category share - Family ~19% is the largest |
| Top-10 category barplot | FAMILY 1832, GAME 959, TOOLS 827, ... |
| Installs per category barplot (billions) | "Most Popular Categories in Play Store" - GAME 13.88B, COMMUNICATION 11.04B, TOOLS 8.00B |
| Boxplot: Rating; Installs x Rating | Rating distribution and outliers |

## 8. ML Models Used
**None.** No models, no train/test split, no metrics, no correlation or sentiment analysis in either notebook.

## 9. Key Findings
- Free apps dominate: 92.17% Free vs 7.83% Paid
- Most popular category: **Family** with ~18-19% of apps, followed by Games (~11%) and Tools; least: Beauty (<1%)
- Most-installed categories: GAME (~13.9B), COMMUNICATION (~11.0B), TOOLS (~8.0B)
- Content Rating: Everyone 8,714, Teen 1,208, Mature 17+ 499, Everyone 10+ 414, Adults only 18+ 3, Unrated 2
- "Rating and Year is left skewed while Reviews, Size, Installs and Price are right skewed"
- Dataset has missing values and 1,181 duplicate apps

## 10. Missing / Incomplete / Unclear
- **No ML anywhere** despite "Feature Engineering" in notebook 2's title
- Broken cells in notebook 2: `df['/Reviews'].astype('int')` typo (KeyError); `19M=19000` SyntaxError left as code
- **Size conversion bug** (notebook 2): `'M'->'000'` yields "19M"->19000 but "8.7M"->8.7 - inconsistent units
- Markdown/actual data mismatch (claims 20 columns, actually 13)
- Unanswered "Internal Assignments": largest-install category (chart only, no text answer), top-5 installed apps per category (not done), 5-star app count (not done)
- Nulls never imputed (Rating's 1,474 missing values unhandled)
- Inconsistent dataframe usage: several plots use uncleaned `df` instead of `df_copy`
- Notebook 2 cells have no execution counts (outputs appear stale)
- Android Ver empty string left as a category (10.25% of apps)
- No conclusions section in either notebook