# Forest Fire EDA - Algerian Forest Fires Dataset

## 1. Project Overview
EDA of the Algerian Forest Fires Dataset (UCI ML Repository) covering two regions of Algeria (Bejaia and Sidi-Bel Abbes, June-September 2012). The notebook performs extensive data cleaning (the raw CSV is messy - it contains region-title rows, duplicate header rows and whitespace issues), EDA with visualizations, and produces a written weather-system report linking weather variables to fire occurrence. A modeling step (classification / regression on FWI) is mentioned as the task but **not implemented**.

**Notebook:** `3.0-Forest Fire EDA.ipynb`

## 2. Dataset
- **Source:** Algerian Forest Fires Dataset, UCI ML Repository (URL stated in notebook)
- **File:** `Algerian_forest_fires_dataset_UPDATE.csv` (cleaned copy exported as `Algerian_forest_fires_dataset_CLEANED.csv`)
- **Rows x Columns:** 246 rows x 14 columns as loaded (after cleaning: 243 rows x 15 columns, incl. added Region column)
- **Domain:** Forest-fire weather observations (Algeria)
- **Target variable:** `Classes` (fire / not fire); notebook notes FWI "can be considered for Regression problem"
- **Columns:** day, month, year, Temperature, RH, Ws, Rain, FFMC, DMC, DC, ISI, BUI, FWI, Classes (+ Region added: 1=Bejaia, 2=Sidi-Bel Abbes)
- **Note:** The CSV on disk currently has 249 lines (title row + header per region, 123 data rows per region), which differs slightly from the notebook's stored outputs (122/121 rows) - the file appears to have changed after last execution.

## 3. Objective / Problem Statement
Task given by instructor Krish Naik: (1) import the dataset, (2) do proper EDA and create a report, (3) perform necessary preprocessing. The notebook also states intent to "predict forest fires in these regions using few Classification algorithms" and choosing "regression problem to predict fire weather index". **Only EDA + preprocessing are actually implemented; no modeling code exists.**

## 4. Technologies & Libraries
- Python 3 (Jupyter Notebook)
- pandas, numpy
- matplotlib.pyplot (%matplotlib inline), seaborn
- warnings
- MongoDB operations referenced (`db.fire_records.insert_many`) but no pymongo import exists

## 5. EDA Steps Performed
1. Load CSV with `header=1` (region title rows above headers)
2. (Abandoned) MongoDB detour: convert df to dict, insert into `fire_records` collection, rebuild from cursor
3. `df.info()` - 246 rows, all 14 columns object dtype
4. Identify null rows: row 122 = "Sidi-Bel Abbes Region Dataset" title row; row 167 = missing Classes
5. Add Region column (1 for first 122 rows, 2 for the rest)
6. `dropna()` -> (244, 15); drop row 122 (duplicate column names as data) -> 243 rows
7. Strip whitespace from column names; cast types (int: month/day/year/Temperature/RH/Ws; float: others)
8. Target cleaning: `Classes.value_counts()` shows mispaced values -> `str.strip()` -> fire 137, not fire 106
9. Split by region (122 Bejaia / 121 Sidi-Bel Abbes); export cleaned CSV
10. Modeling-frame prep: drop day/month/year; encode Classes (not fire=0, fire=1)
11. Distribution histograms, pie chart, correlation heatmap, FWI boxplot
12. Month-wise fire countplots (per region), fire-count bar charts vs Temperature/Rain/Ws/RH
13. Boxplot of all features; per-feature histplots with hue=Classes
14. Written weather-system REPORT

## 6. Data Cleaning / Preprocessing
- `header=1` reading; Region column added (1=Bejaia, 2=Sidi-Bel Abbes)
- Null rows dropped (both region-title rows + missing-Class row); duplicated-column-names row dropped
- Whitespace fixed in column names and target values (`str.strip()`)
- Type conversions: int for date/weather columns, float for fire-weather indices
- Classes label-encoded 0/1 via np.where
- day/month/year dropped for the modeling dataframe; cleaned CSV exported
- **Not present:** no date parsing, no scaling/normalization, no train/test split, no feature selection

## 7. Visualizations Used
| Chart | What it shows |
|---|---|
| `df1.hist(bins=50)` | Distribution of all 12 features |
| Pie chart of Classes | Fire 56.4% vs not fire 43.6% |
| Correlation heatmap (annotated) | Multicollinearity check (note: code uses undefined `corr` var) |
| Boxplot of FWI | Spread/outliers of the proposed regression target |
| 2 countplots: month vs Classes | "Fire Analysis Month wise for Bejaia/Sidi-Bel Abbes Region" |
| Bar charts: fire count vs Temperature, Rain, Ws, RH | Fire occurrence vs each weather variable |
| Boxplot of whole dataset | Feature ranges and outliers |
| Histplots of FFMC, DMC, DC, ISI, BUI, FWI with hue=Classes | FWI component distributions by fire class |

## 8. ML Models Used
**None.** No models trained; no accuracy/F1/metrics exist. Prose mentions classification intent and regression on FWI, but there is no modeling code.

## 9. Key Findings (from the notebook's written REPORT)
- **Temperature:** highest fire counts at 30-37 deg C
- **Rain:** most fires at 0.0-0.3 mm (little/no rain)
- **Wind speed:** highest fire counts at 13-19 km/hr
- **Relative humidity:** highest fire counts at 50-80%
- **FWI components:** FFMC above ~75 -> higher fire chance; DMC 10-30 -> high evidence; DC above 25 -> higher chance; ISI above 3 -> higher chance; BUI above 10 -> higher chance; FWI 3-25 -> higher chance (0-3 lower)
- **Monthly:** "August and September had the most number of forest fires for both regions"; "Most of the fires happened in August... Less Fires was on September"

## 10. Missing / Incomplete / Unclear
- **No ML section** despite the task promising classification/regression - notebook ends after the EDA report
- Failed cells stored: FileNotFoundError (cell 6) and NameError (cell 10)
- Abandoned MongoDB detour: `db`/`list_cursor` never defined, no pymongo import, leftover comment referencing "hotel_records" collection
- Undefined identifiers: cell 53 uses `corr` (never assigned); cell 67 calls `barplots(...)` (only `barchart` defined) - stale outputs not matching current code
- Region countplot bug: both charts plot the full dataset, not the region-filtered data, so the two "region" charts are identical
- Output/code mismatch: cell 69 stores 7 figures for a 6-feature loop; duplicated assignment `dftemp = dftemp = ...`
- Duplicate heading "3.5 Exploratory Data Analysis (EDA)"; empty final code cell
- Dataset version discrepancy between notebook outputs and current CSV on disk