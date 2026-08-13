# Chronic Kidney Disease (CKD) - EDA Project

## 1. Project Overview
Exploratory Data Analysis (EDA) of a clinical chronic kidney disease (CKD) dataset. The analysis covers univariate, bivariate and multivariate exploration of patient lab results and medical history, followed by data cleaning and preparation of a `class` target variable for a future binary classification task.

**Notebooks:**
- `EDA-Chronic data.ipynb` (richer, more explanatory comments)
- `3. EDA cronic data analysis.ipynb`

## 2. Dataset
- **File:** `kidney_disease.csv`
- **Rows x Columns:** 400 rows x 26 columns (25 after dropping the `id` column)
- **Domain:** Clinical / medical - chronic kidney disease diagnosis
- **Target variable:** `classification` (renamed to `class`) - binary: `ckd` / `notckd`
- **Columns (after renaming):** age, blood_pressure, specific_gravity, albumin, sugar, red_blood_cells, pus_cell, pus_cell_clumps, bacteria, blood_glucose_random, blood_urea, serum_creatinine, sodium, potassium, haemoglobin, packed_cell_volume, white_blood_cell_count, red_blood_cell_count, hypertension, diabetes_mellitus, coronary_artery_disease, appetite, peda_edema, aanemia, class
- **Note:** Dataset source/URL is **not stated** in the notebooks.

## 3. Objective / Problem Statement
**Not stated in the notebooks** (no markdown cells exist). The implied objective, based on the code, is binary classification of CKD vs non-CKD. Both notebooks end with the placeholder comment `#train test split and build model`, so no modeling was actually performed.

## 4. Technologies & Libraries
- Python 3 (Jupyter Notebook)
- pandas, numpy
- matplotlib.pyplot, seaborn
- plotly.express, plotly.graph_objects (interactive 2D/3D plots)
- sklearn.preprocessing.LabelEncoder
- warnings

## 5. EDA Steps Performed
1. Load data and inspect head, shape (400x26), info(), dtypes and null counts
2. Drop `id` column; rename all columns to descriptive names
3. Summary statistics via `describe()`
4. Type correction (`pd.to_numeric(errors='coerce')`) for packed_cell_volume, white_blood_cell_count, red_blood_cell_count
5. Separate features into categorical (11) and numeric (14) columns
6. Print unique values per categorical column; clean whitespace/tab artifacts in string values
7. **Univariate:** histplots, countplots, pie/donut charts
8. **Bivariate:** scatterplots, boxplots, violinplots, crosstab stacked bar, swarmplot
9. **Multivariate:** PairGrid, pairplot, correlation matrix + heatmaps (seaborn and interactive Plotly)
10. Null imputation (median for numeric, mode for categorical)
11. Label-encode all categorical columns; prepare `X`/`y` (split only - no model)

## 6. Data Cleaning / Preprocessing
- Dropped the `id` column (irrelevant identifier)
- Renamed columns to descriptive names
- Cleaned dirty strings: `' yes'` -> `'yes'`, `'\tyes'` -> `'yes'`, `'\tno'` -> `'no'` (diabetes_mellitus, coronary_artery_disease), `'ckd\t'` -> `'ckd'` (class)
- Type coercion with `errors='coerce'` (non-numeric entries like `'\t?'` become NaN)
- **Null handling:** median imputation for 14 numeric columns, mode imputation for categorical columns (verified 0 nulls remain)
- **Target encoding:** NOTE - the two notebooks use opposite label conventions (NB1: ckd->0/notckd->1, NB2: ckd->1/notckd->0)
- Label encoding of all categorical columns
- **Not done:** no train/test split, no scaling, no outlier treatment, no feature selection, no class-balance check

## 7. Visualizations Used
| Chart | What it shows |
|---|---|
| Histogram (KDE) of age | Age distribution (skewed) |
| Countplots: hypertension, aanemia, pus_cell_clumps, coronary_artery_disease, peda_edema, bacteria | Prevalence of each condition |
| Pie/donut charts: appetite, diabetes_mellitus | Proportion of patients by appetite and diabetes status |
| Scatterplot age vs blood_pressure (with/without hue=class) | Age-BP relationship ("as age is increasing, bp is increasing") |
| Boxplot class vs blood_urea | CKD patients have higher blood urea (with outliers) |
| Violinplot class vs serum_creatinine | Creatinine distribution by class |
| Boxplot/violinplot diabetes_mellitus vs albumin | Albumin by diabetes status |
| Stacked bar (crosstab) diabetes x hypertension | Co-occurrence of both conditions |
| Swarmplot diabetes_mellitus x age (hue=hypertension) | Point distribution of age by diabetes/HTN |
| PairGrid / pairplot (hue=class) | Multi-feature relationships |
| Correlation heatmap (seaborn + Plotly `go.Heatmap`) | Numeric correlations |
| Plotly interactive 2D and 3D scatterplots | Age-BP-creatinine vs class, haemoglobin gradient |

## 8. ML Models Used
**None.** No model was trained. The notebooks stop after `X = df.drop('class', axis=1)`, `y = df['class']` and a placeholder comment. No metrics exist.

## 9. Key Findings
- Strongest numeric correlates of the class label: specific_gravity (+/-0.73), albumin (+/-0.63), haemoglobin (-/+0.64), packed_cell_volume (-/+0.61), red_blood_cell_count (-/+0.56)
- ~150 of 400 patients have hypertension
- CKD patients have higher blood urea (higher median, outliers)
- Majority of patients do not suffer from anaemia
- Age and blood pressure increase together
- Crosstab: among non-diabetics 220/261 have no hypertension; among diabetics 106/137 have hypertension
- All rows end with zero missing values after imputation

## 10. Missing / Incomplete / Unclear
- No problem statement, dataset source/provenance, or narrative conclusions (zero markdown cells)
- **No ML modeling** - both notebooks end at X/y split with an unexecuted placeholder cell
- Contradictory age-skew comments between the two notebooks ("right skewed" vs "left skewe")
- Contradictory target encoding between notebooks (ckd->0 vs ckd->1)
- Mislabeled PairGrid comments (map_lower/map_diag swapped)
- Typo column name `aanemia`; various comment typos
- Most charts lack titles; no charts saved to disk
- No outlier treatment, no scaling, no statistical tests, no class balance analysis
