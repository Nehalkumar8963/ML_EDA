# Flight Price Prediction - EDA & Feature Engineering

## 1. Project Overview
EDA and feature engineering on an Indian domestic flight price dataset (2019). The notebooks focus on cleaning raw string-based columns (dates, times, duration, stops), extracting structured features, and one-hot encoding categorical variables to produce a modeling-ready DataFrame for flight ticket price prediction.

**Notebooks:**
- `6. EDA-Flight Price data.ipynb` (richer, step-by-step with explanations; produces `final_df`)
- `1.0-EDA_FE_Flight Price.ipynb` (compact pass; ends unfinished)

## 2. Dataset
- **File:** `flight_price.xlsx`
- **Rows x Columns:** 10,683 rows x 11 columns (10,682 after null removal)
- **Domain:** Airline flight ticket pricing (Indian domestic flights, journeys in 2019)
- **Target variable:** `Price` (int) - mean ~9,087, std ~4,611, range 1,759 - 79,512
- **Columns:** Airline, Date_of_Journey, Source, Destination, Route, Dep_Time, Arrival_Time, Duration, Total_Stops, Additional_Info, Price
- **Nulls:** Route (1), Total_Stops (1), rest 0
- **Note:** Dataset source/URL is **not stated**. The markdown feature-description cells describe a cleaned schema (Flight, Class, Days Left, etc.) that does NOT match the raw 11 columns actually loaded.

## 3. Objective / Problem Statement
The stated heading is "EDA And Feature Engineering Flight Price Prediction". The intended task is flight ticket price prediction (Price = target), with EDA and feature engineering as the current stage. No explicit formal problem statement is written.

## 4. Technologies & Libraries
- Python 3 (Jupyter Notebook)
- pandas, numpy
- matplotlib.pyplot, seaborn (imported but **never used**)
- sklearn.preprocessing.OneHotEncoder
- warnings

## 5. EDA Steps Performed
1. Load xlsx; view dataframe, sample, shape, info(), dtypes, null counts
2. Null handling (dropna in notebook 6; mode impute NaN->1 stop in notebook 1)
3. Parse `Date_of_Journey` into day/month/year int columns; drop original
4. Parse `Arrival_Time` (strip trailing day token like "22 Mar", split into Arrival_hour/Arrival_mins); drop original
5. Parse `Dep_Time` into Dept_hour/Dept_mins; drop original
6. `Total_Stops`: inspect uniques, mode = '1 stop', map to 0-4 integers
7. Drop `Route` (redundant: stops count + source/destination already captured)
8. Extract `duration_hours` from Duration (minutes extraction left as "homework")
9. Inspect `Additional_Info` uniques/value_counts (dominated by "No info" ~78%)
10. OneHotEncoder on Airline, Source, Destination (+ Additional_Info in notebook 6)
11. Build `final_df` = cleaned df + encoded columns (notebook 6); ready for modeling

## 6. Data Cleaning / Preprocessing
- Null rows dropped (notebook 6) or imputed with mode (notebook 1)
- Date splitting: Date_of_Journey -> day/month/year integers
- Time splitting: arrival/departure HH:MM -> hour/minute integer columns
- Duration: hours extracted only; minutes never completed
- OneHotEncoder on nominal categorical columns (4 in notebook 6, 3 in notebook 1)
- Dropped: Date_of_Journey, Arrival_Time, Dep_Time, Route, Duration
- **Not done:** no scaling, no train/test split, no modeling

## 7. Visualizations Used
**None.** matplotlib/seaborn are imported in both notebooks but never called - there are zero plot statements and zero chart outputs. All "visual" output is DataFrame prints.

## 8. ML Models Used
**None.** Only preprocessing (OneHotEncoder). No accuracy/R2/RMSE or any metric exists. Notebook 6 ends with a homework list: univariate/bivariate/multivariate analysis, X/y split, train-test split, scaling.

## 9. Key Findings
- Dataset is nearly clean: only 2 null values total (one each in Route, Total_Stops)
- `Route` is redundant with Source/Destination + Total_Stops, hence dropped
- `Additional_Info` is 78% "No info"
- `Total_Stops` mode is "1 stop"; mapped to 0-4
- 12 unique airlines, 5 sources, 6 destinations
- Price: mean ~9,087, range 1,759-79,512
- Notebook 6 concludes the data is ready for modeling (remaining steps listed as homework)

## 10. Missing / Incomplete / Unclear
- **No EDA plots at all** despite the notebook title promising "EDA"
- **No modeling or evaluation** - ends at feature encoding
- Notebook 1 is unfinished (last cell empty; one-hot result displayed but never merged into a DataFrame)
- Duration minutes never extracted
- Feature-description markdown describes a different (cleaned) schema than the raw data actually loaded
- Ambiguous comment in notebook 6 ("either you drop additional info or drop it")
- No source citation or date-range summary for the data