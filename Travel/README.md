# Travel Package - EDA & Preprocessing Project

## 1. Project Overview
EDA and preprocessing of a travel/tourism package customer dataset (4,888 customers). The notebook performs univariate/bivariate/multivariate analysis, data cleaning (typo fix, row dropping), feature engineering, and prepares train/test splits with a ColumnTransformer pipeline (one-hot encoding + scaling) for a binary classification task on whether a customer takes a product/package (`ProdTaken`). **No model is trained - the notebook stops after preprocessing.**

**Notebook:** `4. EDA-Travel.ipynb`

## 2. Dataset
- **File:** `Travel.csv`
- **Rows x Columns:** 4,888 rows x 20 columns; after cleaning 4,128 rows x 20 columns (760 rows dropped)
- **Domain:** Travel/tourism customer data (demographics, pitch/contact info, satisfaction, income)
- **Target variable:** `ProdTaken` (binary 0/1 - product/package taken; ~19.3% positive - imbalanced)
- **Columns:** CustomerID, ProdTaken, Age, TypeofContact, CityTier, DurationOfPitch, Occupation, Gender, NumberOfPersonVisiting, NumberOfFollowups, ProductPitched, PreferredPropertyStar, MaritalStatus, NumberOfTrips, Passport, PitchSatisfactionScore, OwnCar, NumberOfChildrenVisiting, Designation, MonthlyIncome
- **Note:** Dataset source (e.g., Kaggle name) is **not stated** in the notebook.

## 3. Objective / Problem Statement
**Not stated.** The notebook has zero markdown cells. The implied objective (from code) is binary classification of `ProdTaken`, with EDA, feature engineering, and train/test split + preprocessing performed - but no model or evaluation.

## 4. Technologies & Libraries
- Python 3 (Jupyter Notebook)
- pandas, numpy
- matplotlib.pyplot, seaborn
- mpl_toolkits.mplot3d (Axes3D - 3D scatter)
- sklearn.model_selection.train_test_split
- sklearn.preprocessing.OneHotEncoder, StandardScaler
- sklearn.compose.ColumnTransformer
- warnings

## 5. EDA Steps Performed
1. Load CSV; view df, shape (4888x20), head, info, dtypes, columns
2. Gender typo fix: `'Fe Male'` -> `'Female'`
3. Null analysis: isnull().sum() + percentage; **dropna(axis=0)** (4888 -> 4128)
4. Split columns into cats (12) and nums (8)
5. Univariate: countplot of ProdTaken; countplots of all 12 categorical columns; histplots (kde) of all 8 numeric columns; histogram of Age
6. Insight comment: "30-40 age group are travelling more"
7. CityTier average of 1.66 "doesn't make sense" -> converted discrete numeric columns to object dtype (treated as categorical)
8. Bivariate: scatterplot Age vs DurationOfPitch (hue=ProdTaken); crosstab MaritalStatus x ProdTaken + stacked bar; barplot ProductPitched vs PitchSatisfactionScore; lineplot NumberOfFollowups vs PitchSatisfactionScore
9. Multivariate: violinplot (ProdTaken vs Age, hue=OwnCar); swarmplot (Gender vs Age, hue=ProdTaken); 3D scatter (Age, MonthlyIncome, DurationOfPitch, colored by ProdTaken)
10. Correlation heatmap of numeric columns
11. Feature engineering: dropped CustomerID; created TotalVisiting = NumberOfPersonVisiting + NumberOfChildrenVisiting
12. train_test_split (80/20, random_state=1); ColumnTransformer (OneHotEncoder drop='first' + StandardScaler), fit_transform on train / transform on test

## 6. Data Cleaning / Preprocessing
- Typo fix: 'Fe Male' -> 'Female'
- Null handling: all null rows dropped (760 rows, ~15.5% of data - no imputation, no discussion)
- Type conversion: 12 discrete/categorical columns cast to object dtype
- Dropped column: CustomerID
- Feature engineering: TotalVisiting = persons visiting + children visiting
- Encoding: OneHotEncoder(drop='first') on 11 categorical features via ColumnTransformer
- Scaling: StandardScaler on 8 numeric features via ColumnTransformer
- Split: train_test_split(0.2, random_state=1)

## 7. Visualizations Used
| Chart | What it shows |
|---|---|
| Countplot ProdTaken (viridis) | Class imbalance in target (more 0s) |
| 12 countplots (categorical columns) | Distribution of each categorical feature |
| 8 histplots with KDE (numeric columns) | Numeric feature distributions |
| Histogram of Age (30 bins) | Age distribution - "30-40 age group travelling more" |
| Countplot TypeofContact | Self Enquiry (2918) vs Company Invited |
| Scatterplot Age vs DurationOfPitch (hue=ProdTaken) | Age-pitch duration relationship by target |
| Stacked bar MaritalStatus x ProdTaken | Single customers take product most (36.4%), Divorced least (13.3%) |
| Barplot ProductPitched vs PitchSatisfactionScore | Mean satisfaction by product |
| Lineplot NumberOfFollowups vs PitchSatisfactionScore | Satisfaction vs follow-ups trend |
| Violinplot ProdTaken vs Age (hue=OwnCar) | Age distribution by target and car ownership |
| Swarmplot Gender vs Age (hue=ProdTaken) | Age spread by gender and target |
| 3D scatter Age x MonthlyIncome x DurationOfPitch (c=ProdTaken) | 3D feature relationship vs target |
| Correlation heatmap (annotated) | Numeric feature correlations |

## 8. ML Models Used
**None.** No model is trained. Only train_test_split + ColumnTransformer preprocessing (OneHotEncoder + StandardScaler). No evaluation metrics.

## 9. Key Findings
- **"30-40 age group are travelling more"** (only explicit insight in notebook)
- ProdTaken is imbalanced (mean 0.193)
- Single customers take the product most often (36.4%); Divorced lowest (13.3%)
- TypeofContact mostly "Self Enquiry"; Gender mostly Male (2463); Occupation mostly Salaried (1999); ProductPitched mostly Basic (1615); Designation mostly Executive (1615)
- CityTier average of 1.66 "doesn't make sense" -> treated as categorical
- "All the categorical data should be converted to numbers" for model building

## 10. Missing / Incomplete / Unclear
- **No markdown cells at all** - no narrative, no problem statement, no conclusions
- **No ML modeling** - stops after transforming X_test; final cell empty and unexecuted
- No evaluation metrics or model results
- `preprocessor.transform(X_test)` output printed but not assigned/stored
- Dropping 760 rows (~15.5%) without discussion
- Execution-count gaps (reruns/deletions); some plots lack titles
- Correlation heatmap values not interpreted; scatter/heatmap cells show axes objects but no annotations