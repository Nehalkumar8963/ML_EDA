# ML_EDA - Machine Learning & Exploratory Data Analysis Projects

A collection of 8 EDA (Exploratory Data Analysis) projects covering diverse domains: healthcare, aviation, environment, mobile apps, HR, education, travel, and immigration. Each project performs data cleaning, feature engineering, visualization, and insight extraction. All content in this README is based strictly on what is present in the project notebooks.

---

## Project Index

| # | Project | Domain | Dataset | Target | Notebook(s) |
|---|---------|--------|---------|--------|-------------|
| 1 | [Chronic Kidney Disease](#1-chronic-kidney-disease-eda) | Healthcare | kidney_disease.csv (400x26) | class (ckd/notckd) | 2 |
| 2 | [Flight Price](#2-flight-price-eda--feature-engineering) | Aviation | flight_price.xlsx (10,683x11) | Price | 2 |
| 3 | [Forest Fire](#3-forest-fire-eda) | Environment | Algerian forest fires (246x14) | Classes (fire/not) | 1 |
| 4 | [Google Play Store](#4-google-play-store-eda) | Mobile apps | googleplaystore.csv (10,841x13) | none (EDA only) | 2 |
| 5 | [HR Analytics](#5-hr-analytics-eda) | Human resources | HRDataset_v14.csv (311x36) | none (EDA only) | 1 |
| 6 | [Student Performance](#6-student-performance-eda) | Education | stud.csv (1,000x8) / student-por.csv (649x33) | scores / absences | 2 |
| 7 | [Travel Package](#7-travel-package-eda) | Travel | Travel.csv (4,888x20) | ProdTaken (0/1) | 1 |
| 8 | [USA Visa](#8-usa-visa-eda--feature-engineering) | Immigration | us_perm_visas.csv (374,362x154) | case_status | 1 |

---

## 1. Chronic Kidney Disease EDA

**Notebooks:** `EDA-Chronic data.ipynb` (richer), `3. EDA cronic data analysis.ipynb`
**Dataset:** kidney_disease.csv - 400 rows x 26 columns, clinical lab results and patient history. Target: `class` (ckd/notckd).
**Objective:** Not stated in notebooks (no markdown). Implied: binary classification of CKD; notebooks stop at X/y split with comment `#train test split and build model`.
**Libraries:** pandas, numpy, matplotlib, seaborn, plotly (interactive 2D/3D), LabelEncoder, warnings.

**EDA steps:** shape/info/describe -> drop id, rename columns -> type coercion -> categorical/numeric split -> univariate (hist/count/pie) -> bivariate (scatter/box/violin/crosstab/swarm) -> multivariate (PairGrid, pairplot, correlation heatmaps, Plotly 3D) -> median/mode imputation -> label encoding.

**Cleaning:** dropped `id`; renamed columns; cleaned dirty strings (`' yes'`, `'\tyes'`, `'ckd\t'`); `pd.to_numeric(errors='coerce')` on pcv/wc/rc; median imputation (numeric), mode imputation (categorical) - verified 0 nulls. NOTE: the two notebooks use opposite target encodings (ckd->0 vs ckd->1).

**Key visualizations:** age histogram, condition countplots, appetite/diabetes pie & donut, age-vs-BP scatter (hue=class), blood_urea boxplot, serum_creatinine violin, diabetes x hypertension stacked bar, PairGrid, correlation heatmaps, interactive Plotly 2D/3D.

**ML models:** None.

**Key findings:** Strongest correlates of class: specific_gravity (0.73), albumin (0.63), haemoglobin (-0.64), packed_cell_volume (-0.61), rbc (-0.57). ~150/400 have hypertension. CKD patients have higher blood urea. Diabetics: 106/137 have hypertension.

**Issues:** no problem statement, no model, contradictory skew comments and encodings between notebooks, typo column `aanemia`, most charts untitled.

---

## 2. Flight Price - EDA & Feature Engineering

**Notebooks:** `6. EDA-Flight Price data.ipynb` (richer, produces final_df), `1.0-EDA_FE_Flight Price.ipynb` (unfinished).
**Dataset:** flight_price.xlsx - 10,683 rows x 11 columns, Indian domestic flights (2019). Target: `Price` (mean ~9,087; range 1,759-79,512).
**Objective:** "EDA And Feature Engineering Flight Price Prediction" - prepare data for flight price prediction.
**Libraries:** pandas, numpy, matplotlib/seaborn (imported, never used), OneHotEncoder.

**EDA steps:** load -> shape/info/nulls (Route=1, Total_Stops=1) -> date split into day/month/year -> arrival/departure time split into hour/min -> Total_Stops mapped 0-4 -> drop Route (redundant) -> Duration hours extracted (minutes = homework) -> OneHotEncoder on Airline/Source/Destination (+Additional_Info) -> final_df built.

**Cleaning:** dropna (nb6) or mode-impute (nb1); datetime decomposition; OneHot encoding; dropped Date_of_Journey, Arrival/Dep_Time, Route, Duration. No scaling, no split, no model.

**Visualizations:** **None** - matplotlib/seaborn imported but never called; zero charts.

**ML models:** None.

**Key findings:** Nearly clean data; Additional_Info is 78% "No info"; Total_Stops mode "1 stop"; 12 airlines/5 sources/6 destinations.

**Issues:** title promises EDA but no plots exist; nb1 unfinished (empty last cell, encoding never merged); Duration minutes never extracted; feature-description markdown describes a schema that doesn't match the actual data.

---

## 3. Forest Fire EDA

**Notebook:** `3.0-Forest Fire EDA.ipynb`
**Dataset:** Algerian Forest Fires Dataset (UCI) - Algerian_forest_fires_dataset_UPDATE.csv, 246 rows x 14 cols (243x15 after cleaning). Target: `Classes` (fire/not fire); FWI noted for regression. Regions: Bejaia (1) and Sidi-Bel Abbes (2), June-Sept 2012.
**Objective:** Task by instructor Krish Naik: import data, do EDA + report, perform preprocessing. Mentioned intent: classification of fires and regression on FWI - **not implemented**.
**Libraries:** pandas, numpy, matplotlib, seaborn, warnings. (MongoDB ops referenced but no pymongo import - abandoned detour.)

**EDA steps:** load with header=1 (messy CSV with region-title rows) -> drop null/duplicate-header rows -> add Region column -> strip whitespace -> type casting -> Classes cleaned to fire 137 / not fire 106 -> region split -> encode Classes -> histograms, pie, correlation heatmap, FWI boxplot -> month-wise fire countplots -> fire count vs Temperature/Rain/Ws/RH bar charts -> per-feature histplots (hue=Classes) -> written weather-system REPORT.

**Cleaning:** header=1; region title rows dropped; duplicate column-name row dropped; str.strip() on names/values; int/float casts; Classes label-encoded; cleaned CSV exported. No scaling/split/feature selection.

**Visualizations:** all-feature histograms, Classes pie (fire 56.4%), correlation heatmap, FWI boxplot, monthwise countplots, weather-variable bar charts, whole-dataset boxplot, FWI-component histplots.

**ML models:** None.

**Key findings (from notebook REPORT):** Most fires at temp 30-37C, rain 0-0.3mm, wind 13-19 km/hr, RH 50-80%. FFMC>75, DMC 10-30, DC>25, ISI>3, BUI>10, FWI 3-25 -> higher fire chance. "August and September had the most forest fires for both regions."

**Issues:** no modeling; failed/abandoned cells (FileNotFoundError, NameError, MongoDB); undefined variables (corr, barplots) with stale outputs; region countplots actually plot full data (identical charts); dataset version mismatch vs current CSV.

---

## 4. Google Play Store EDA

**Notebooks:** `2.0-EDA&FE Google Playstore.ipynb` (problem statement + insights), `1. EDA-Google playstore data.ipynb` (deeper cleaning).
**Dataset:** googleplaystore.csv - 10,841 rows x 13 columns, Android apps marketplace. No target (EDA only).
**Objective (quoted):** "Our Objective is to find the Most Popular Category, find the App with largest number of installs, the App with largest size etc."
**Libraries:** pandas, numpy, seaborn, matplotlib, warnings. No sklearn.

**EDA steps:** load/inspect -> 483 exact duplicates removed -> 1 malformed Reviews row removed ("3.0M") -> Reviews int -> Size parsed -> Installs/Price stripped of +/,$ -> Last Updated -> datetime -> day/month/year -> Android Ver cleaned -> App duplicates removed (1,181) -> categorical/numerical split -> univariate (count/dist/KDE) -> category popularity (pie, top-10, installs per category) -> Rating boxplots.

**Cleaning:** duplicate removal, punctuation stripping, custom Size parser (nb1), date decomposition. **Nulls never handled** (Rating 1,474 nulls left). No encoding/scaling.

**Visualizations:** Type/Content Rating countplots, Price/Rating distplots + KDE, Category pie (Family ~19%), top-10 categories barplot, installs-by-category bar (GAME 13.9B, COMMUNICATION 11.0B, TOOLS 8.0B), Rating boxplots.

**ML models:** None.

**Key findings:** Free apps 92.2%; Family largest category (~18-19%), Beauty least (<1%); Games most installed; Content Rating: Everyone 8,714; "Rating and Year left skewed, Reviews/Size/Installs/Price right skewed".

**Issues:** no ML; broken cells (typo `df['/Reviews']`, SyntaxError `19M=19000`); **Size conversion bug** in nb2 ('M'->'000' gives 19M->19000 but 8.7M->8.7 - inconsistent); markdown claims 20 cols (actual 13); unanswered "internal assignments"; plots use uncleaned df.

---

## 5. HR Analytics EDA

**Notebook:** `2. EDA-HR Analytics.ipynb`
**Dataset:** HRDataset_v14.csv (Kaggle "Employees Engagement") - 311 rows x 36 columns. No explicit target (descriptive EDA).
**Objective (quoted):** "performing different analysis and visualizations using the Employees Engagement Dataset to obtain some valuable insights."
**Libraries:** pandas, numpy, seaborn, matplotlib, warnings. No sklearn.

**EDA steps:** load/info -> null fill -> salary top-10 -> performance scores (13 PIP employees) -> absences -> marital status -> special projects (70 with none) -> salary bar chart -> recruitment sources -> performance trend lineplot -> satisfaction stem plot -> multivariate (salary by dept boxplot, engagement by position, marital x gender, avg engagement by dept) -> internal homework Q&A (terminations, median salary by sex, absences by dept) -> unfinished questions at end.

**Cleaning:** nulls filled with **string "0"** (DateofTermination 207, ManagerID 8) - flawed for numeric column; duplicates 0. No encoding/scaling.

**Visualizations:** top-10 salaries bar, recruitment source barh (Indeed 87, LinkedIn 76), performance trend lineplot (Fully Meets 243), satisfaction stem plot (3->108), salary-by-department boxplot, engagement-by-position barplot, marital x gender countplot.

**ML models:** None.

**Key findings:** 13 employees on PIP; most common satisfaction = 3; 70 employees with no special project; Indeed top recruitment source; Executive Office highest avg engagement (4.83); terminations highest in Production Technician roles; top termination reason "Another position" (20); median salary M 63,353 vs F 62,066; Production has most absences (2,120).

**Issues:** no ML; wrong insight (187 is MarriedID==0 i.e. NOT married); string-"0" fill bug; no conclusions; unfinished final questions; many typos; redundant df.columns cells.

---

## 6. Student Performance EDA

**Notebooks:** `2.0-Student Performance EDA  .ipynb` (structured, insights), `5. EDA-Student Performance.ipynb` (exploratory, unfinished).
**Datasets:**
- stud.csv (Kaggle, URL stated): 1,000 rows x 8 cols - gender, race_ethnicity, parental_level_of_education, lunch, test_preparation_course, math/reading/writing_score.
- student-por.csv (source not stated): 649 rows x 33 cols - Portuguese secondary students; target `absences`.

**Objective (quoted, nb 2.0):** "This project understands how the student's performance (test scores) is affected by other variables such as Gender, Ethnicity, Parental level of education, Lunch and Test preparation course."
**Libraries:** pandas, numpy, seaborn, matplotlib, warnings; train_test_split (nb 5 only).

**EDA steps (nb 2.0):** problem statement -> null/dup checks (clean data) -> feature segregation (5 cat/3 num) -> feature engineering (total_score, average) -> average distributions by gender/lunch/parent education/race_ethnicity -> correlation heatmap.
**EDA steps (nb 5):** univariate (school, age, address, reason, activities, alcohol) -> bivariate (Medu/Fedu, studytime vs G3/G2, internet vs G3) -> multivariate (sex x address vs G3) -> boxplots -> correlation heatmap -> IQR outlier detection (22 detected, not removed) -> train_test_split (target absences) -> ends at "#internal homework: data encoding / scaling".

**Cleaning:** nb 2.0: no nulls/dups, no imputation. nb 5: nulls 0; IQR outlier detection only; split done; **encoding/scaling NOT done**; G1/G2/G3 vanish from features without visible drop code.

**Visualizations:** average histograms + KDE (overall, by gender/lunch/parent education/race), annotated heatmap (nb 2.0); school countplot, age histplot, address countplot, reason/activities pies, Medu/Fedu countplots, studytime/internet/sex barplots, numeric boxplots, correlation heatmap (nb 5).

**ML models:** None (only train_test_split).

**Key findings (nb 2.0):** means 66-69, std 14.6-15.19; "Female student tend to perform well than male students"; "Standard Lunch help students perform well in exams"; "In general parent's education don't help student perform well in exam"; "Students of group A and group B tends to perform poorly in exam".
**Key findings (nb 5):** GP > MS students; majority urban, age 16-17; 48.5% in activities; study 1h -> ~11 avg grade, 2h -> ~12; internet users ~12; urban students higher marks; mothers more educated at higher levels.

**Issues:** nb 5 has no problem statement/source; arbitrary target choice (absences) with grades dropped; outliers detected but unused; no encoding/scaling/model in either notebook; subplot layout inconsistency in nb 2.0; nb 2.0 ends with empty cell, no conclusions.

---

## 7. Travel Package EDA

**Notebook:** `4. EDA-Travel.ipynb`
**Dataset:** Travel.csv - 4,888 rows x 20 cols (4,128 after cleaning). Target: `ProdTaken` (binary, ~19.3% positive - imbalanced).
**Objective:** Not stated (zero markdown cells). Implied from code: binary classification of product taken; notebook stops after train/test split + preprocessing.
**Libraries:** pandas, numpy, matplotlib, seaborn, mpl_toolkits.mplot3d, train_test_split, OneHotEncoder, StandardScaler, ColumnTransformer.

**EDA steps:** load/inspect -> Gender typo fix ('Fe Male'->'Female') -> null analysis + dropna (760 rows, ~15.5%) -> cats/nums split -> univariate (ProdTaken countplot, 12 categorical countplots, 8 numeric histplots, Age histogram) -> bivariate (Age vs DurationOfPitch scatter, MaritalStatus x ProdTaken stacked bar, ProductPitched vs satisfaction, followups vs satisfaction lineplot) -> multivariate (violin, swarm, 3D scatter) -> correlation heatmap -> feature engineering (TotalVisiting) -> train_test_split (80/20, random_state=1) -> ColumnTransformer (OneHotEncoder drop='first' + StandardScaler).

**Cleaning:** typo fix; dropna (no imputation, no discussion); discrete columns cast to object; CustomerID dropped; TotalVisiting engineered; one-hot + scaling applied to train/test.

**Visualizations:** target countplot (imbalance), 12 categorical countplots, 8 numeric histplots, Age histogram, TypeofContact countplot, Age x pitch-duration scatter, marital stacked bar, product-satisfaction barplot, followup-satisfaction lineplot, age violin (hue=OwnCar), gender swarm (hue=ProdTaken), 3D scatter, correlation heatmap.

**ML models:** None (preprocessing only, no evaluation).

**Key findings:** "30-40 age group are travelling more"; Single customers take product most (36.4%), Divorced least (13.3%); TypeofContact mostly Self Enquiry; CityTier mean of 1.66 "doesn't make sense" -> treated as categorical.

**Issues:** no narrative/markdown; no model or metrics; transform(X_test) not stored; 15.5% rows dropped without discussion; most plots untitled.

---

## 8. USA Visa EDA & Feature Engineering

**Notebook:** `7. EDA US Visa.ipynb`
**Dataset:** us_perm_visas.csv - 374,362 rows x 154 columns, US PERM labor-certification applications. Target: `case_status` (Certified 92.8% / Denied 7.2% after preparation).
**Objective:** Not stated (no markdown). Code comments: "This eda has a lot of visulaisation and feature engineering", "preparatrion of target variable case_status".
**Libraries:** pandas, numpy, matplotlib, seaborn, LabelEncoder, warnings.

**EDA steps:** load (374K x 154) -> case_no/case_number investigation (same concept, complementary missingness; merged into casenumber) -> case_status cleaning (drop Withdrawn 18,194; Certified-Expired -> Certified) -> missing-value audit + all-empty column/row drops -> decision_date -> datetime -> year/month/day -> year-wise status countplot (upward trend, 2016 highest) -> employer city analysis (NEW YORK 15,992 top) -> top-10 employers bar -> economic sector pie (IT dominant, 49,311) -> job title normalization (software engineer top, 18,582) -> top-7 countries by status -> application_type & education countplots -> % non-null audit -> prune to columns with >=330,000 non-nulls (20 cols) -> target encoding -> mode-fill states/cities/countries, median-fill wages -> pw_soc_code cleaning -> select 9 columns -> LabelEncoder all -> final frame 356,168 x 9.

**Cleaning:** case-number merge; class-imbalance handling (binary 92.8/7.2); mode imputation (6 categorical cols); median imputation (pw_amount_9089 - though later excluded); date decomposition; text normalization (upper, job-title splits, state abbreviations); numeric coercion; label encoding; column pruning. Some small-null columns excluded rather than imputed.

**Visualizations:** year x status countplot, top-10 cities by year countplot, top employers bar, sector pie, top job titles bar, top-7 countries countplot, application_type countplot, education countplot.

**ML models:** None.

**Key findings:** "7.2% of the visa application were denied"; upward trend with 2016 highest; IT dominant sector; software engineers apply most; top cities NEW YORK/COLLEGE STATION/SANTA CLARA/SAN JOSE/REDMOND; 9-column clean frame ready for modeling.

**Issues:** no markdown/prose; no modeling; hard-coded row-135,269 merge split (fragile); wage column cleaned then excluded with no rationale; unresolved small nulls; "#internal homework: deal with missing value treatement"; typos; untitled plots.

---

# Overall Folder Summary

## Stats
- **8 projects, 11 notebooks**, all EDA/preprocessing-focused
- **Common libraries:** pandas, numpy, matplotlib, seaborn (+ plotly in Chronic, sklearn preprocessing in 5 projects)
- **Common techniques:** null/duplicate checks, type corrections, datetime decomposition, one-hot/label encoding, median/mode imputation, univariate -> bivariate -> multivariate structure, correlation heatmaps
- **ML algorithms used:** **none anywhere** - the folder contains zero trained models and zero evaluation metrics (only preprocessing + train_test_split)

## Skills Demonstrated
- Data cleaning: dirty strings, typos, duplicates, mixed dtypes, missing-value strategies
- Feature engineering: datetime parsing, encoding, derived features
- EDA: ~50 charts across projects (count/hist/box/violin/pie/heatmap/swarm/pairplot/3D/interactive Plotly)
- Handling messy, large, real-world data (USA Visa: 374K x 154)

## Strongest Projects (for resume/interviews)
1. **USA Visa** - scale, messy-data handling, target engineering
2. **Chronic data** - complete statistical EDA + interactive visuals
3. **Forest data** - hardest cleaning + written domain report
4. **Student Performance (2.0)** - cleanest narrative and insights

## Interview Talking Points
For each project be ready to explain: dataset size/columns/target, 3-5 concrete insights, why each cleaning decision was made, top correlated features, and the next modeling step (model choice + metric + imbalance handling).

## Gaps to Improve (recommendations, not found in files)
1. **Add models** - no project trains/evaluates one; add at least Logistic Regression + Random Forest on Travel/USA Visa/Chronic with metrics
2. **Add conclusions** - every notebook ends abruptly; add summary markdown cells
3. **Fix known bugs** - Playstore Size conversion, HR string-"0" fill, Chronic contradictory encodings, Travel's undocumented 15% row drop, Forest's broken region plots
4. **Document datasets** - several notebooks have no stated source or problem statement
5. **Title/label charts** and save key figures for portfolio use