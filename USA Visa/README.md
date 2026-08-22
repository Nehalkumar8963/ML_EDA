# US Visa (PERM) - EDA & Feature Engineering Project

## 1. Project Overview
EDA and feature engineering on a large US employment-based immigration (PERM labor certification) dataset - 374,362 applications x 154 columns. The notebook performs heavy cleaning on a very messy dataset (duplicate case-number columns, huge missing-value counts, text normalization, target preparation) and reduces it to a clean 9-column, fully label-encoded modeling frame with binary target `case_status` (Certified=1 / Denied=0). Extensive visualizations of statuses, cities, employers, sectors, job titles, and countries. **No model is trained.**

**Notebook:** `7. EDA US Visa.ipynb`

## 2. Dataset
- **File:** `us_perm_visas.csv`
- **Rows x Columns:** 374,362 rows x 154 columns (final cleaned frame: 356,168 rows x 9 columns)
- **Domain:** US employment-based immigration - PERM visa (labor certification) applications
- **Target variable:** `case_status` - values Certified, Denied, Certified-Expired, Withdrawn; reduced to binary Certified=1 (92.8%) / Denied=0 (7.2%)
- **Sample columns:** case_no, case_number, case_received_date, decision_date, case_status, class_of_admission, country_of_citizenship (plus misspelled duplicate country_of_citzenship), employer_* (name, city, state, address, postal code), job_info_* (job_title, work_state/city), us_economic_sector, naics_*, pw_* (prevailing wage: pw_amount_9089, pw_soc_code/title, pw_unit_of_pay_9089), wage_offer_from_9089, foreign_worker_info_*, application_type, agent_*
- **Note:** Dataset source/URL is **not stated** in the notebook.

## 3. Objective / Problem Statement
**Not stated** (zero markdown cells). Intent from code comments:
- "#This eda has a lot of visulaisation and feature engineering"
- "#also it is a great example of preparatrion of target variable case_status"
- Implied objective: extensive EDA + feature engineering on US visa applications and preparation of the `case_status` target for later modeling.

## 4. Technologies & Libraries
- Python 3 (Jupyter Notebook)
- pandas, numpy
- matplotlib.pyplot, seaborn
- sklearn.preprocessing.LabelEncoder
- warnings

## 5. EDA Steps Performed
1. Load CSV; shape (374,362 x 154); head/sample/tail; print all column names
2. Case-number investigation: `case_no` and `case_number` are the same concept (complementary missingness) -> merged into `casenumber` (split hard-coded at row 135,269); originals dropped
3. case_status exploration; drop Withdrawn (18,194); recode Certified-Expired -> Certified
4. Missing-value audit: isnull().sum(), drop all-empty columns/rows (dropna how='all'), per-column missing counts
5. Date handling: decision_date -> datetime -> year/month/day columns
6. Year-wise status countplot (upward trend; 2016 highest)
7. Employer city analysis: uniques, value_counts (NEW YORK 15,992, COLLEGE STATION 11,983, SANTA CLARA 10,446, SAN JOSE 9,004, REDMOND 8,469); uppercased; top-10 by year
8. Top-10 employers by application count (bar)
9. us_economic_sector: manual value_counts + pie of top 10 (IT dominant, 49,311)
10. job_info_job_title: top-20 counts, normalization, top-10 bar
11. country_of_citizenship: categorical; top-7 countplot by case_status
12. application_type and foreign_worker_info_education countplots
13. % non-null per column for all columns
14. Column pruning: keep only columns with >=330,000 non-null values -> 20 columns
15. Target encoding: Certified->1, Denied->0
16. Employer state: mode-fill (CALIFORNIA), standardize full names/abbreviations
17. pw_soc_code cleaning (strip '.', '-', truncate to 6 chars, mode-fill "nan"/"None", cast int)
18. Mode-fill for class_of_admission, country_of_citizenship, employer_city, employer_name, pw_source_name_9089
19. pw_amount_9089: remove commas -> float, median-fill
20. Select 9 columns by index; LabelEncoder on all; final df 356,168 x 9 all-integer
21. Ends with an empty final cell

## 6. Data Cleaning / Preprocessing
- **Case-number unification:** merged case_no + case_number into casenumber; dropped originals
- **Target preparation:** removed Withdrawn; merged Certified-Expired into Certified; binary mapping 1/0 (92.8% / 7.2% - imbalanced)
- **Null handling:** dropped all-empty rows/columns; mode imputation (employer_state, class_of_admission, country_of_citizenship, employer_city, employer_name, pw_source_name_9089); median imputation (pw_amount_9089); mode-fill of "nan"/"None" strings in pw_soc_code
- **Date handling:** pd.to_datetime on decision_date; derived year/month/day
- **Text normalization:** str.upper() on cities/employers; job titles lowercased, split on '-', 'ii', '/', 'sr.'->'senior'; state name standardization via 

## 7. Visualizations Used
| Chart | What it shows |
|---|---|
| Countplot: year x case_status | Visa applications per year by status - upward trend, 2016 highest |
| Countplot: top-10 employer cities x year | Top employer cities over time |
| Bar chart: top-10 employers | Applications per employer (with count labels) |
| Pie chart: top-10 economic sectors | IT dominates (~49,311 apps, 47%+ of top-10) |
| Bar chart: top-10 job titles | Software engineer most applications (18,582 vs 12,054 systems analyst) |
| Countplot: top-7 countries x case_status | Citizenship countries by approval/denial |
| Countplot: application_type | Type counts with labels |
| Countplot: foreign_worker_info_education | Education level counts |

## 8. ML Models Used
**None.** EDA + preprocessing only. Only sklearn usage is LabelEncoder. No model, split, or metrics.

## 9. Key Findings
- "7.2% of the visa application were denied" (Certified 92.80%, Denied 7.20%)
- Year-wise status trend is upward; 2016 highest
- case_no and case_number are the same concept with complementary missingness
- Top employer cities: NEW YORK, COLLEGE STATION, SANTA CLARA, SAN JOSE, REDMOND
- **IT** is by far the dominant economic sector
- "software engineer applies most visa application" (18,582 after normalization)
- Final frame: 356,168 rows x 9 label-encoded features with binary target - ready for modeling (not included)

## 10. Missing / Incomplete / Unclear
- **No markdown cells** - no problem statement, headings, or prose; all notes are inline comments
- **No modeling section** - stops after target/feature preparation
- Empty insight cells (employer city, top employers) with no written findings
- Final code cell empty and unexecuted; execution-count gaps (reruns/deletions)
- Hard-coded casenumber merge split at index 135,269 (fragile assumption)
- `pw_amount_9089` (wage) cleaned + median-imputed but then **excluded** by the 9-column positional selection with no rationale
- Some nulls left unaddressed; comment "#internal homework: deal with missing value treatement" suggests unfinished work
- Typos in comments ("visulaisation", "preparatrion", "categroical"); several plots lack titles
