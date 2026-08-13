# Student Performance - EDA Project

## 1. Project Overview
Two EDA notebooks analyzing student performance datasets. Notebook 2.0 analyzes a Kaggle exam-performance dataset (1000 students) focusing on how gender, ethnicity, parental education, lunch type and test-preparation affect test scores, with structured markdown, insights and visualizations. Notebook 5 analyzes the Portuguese secondary-education dataset (649 students) with univariate/bivariate/multivariate analysis, IQR outlier detection, and a train/test split (target: absences) - though encoding and scaling are left unfinished.

**Notebooks:**
- `2.0-Student Performance EDA  .ipynb` (structured; problem statement; insight-driven)
- `5. EDA-Student Performance.ipynb` (more exploratory; ends unfinished at "internal homework")

## 2. Datasets
**Notebook 2.0 - `stud.csv`:**
- Source: Kaggle (students-performance-in-exams dataset, URL stated)
- 1,000 rows x 8 columns: gender, race_ethnicity, parental_level_of_education, lunch, test_preparation_course, math_score, reading_score, writing_score
- No nulls, no duplicates
- Target: not explicitly declared; the three scores are treated as outputs (analysis centers on derived average/total_score)
- Domain: US-style exam performance (scores 0-100)

**Notebook 5 - `student-por.csv`:**
- Source: not stated (only a raw-cell column glossary; UCI/Kaggle link not given)
- 649 rows x 33 columns: school, sex, age, address, famsize, Pstatus, Medu, Fedu, Mjob, Fjob, reason, guardian, traveltime, studytime, failures, schoolsup, famsup, paid, activities, nursery, higher, internet, romantic, famrel, freetime, goout, Dalc, Walc, health, absences, G1, G2, G3
- Target: `absences` (per code comment "considering absences as the target variable")
- Domain: secondary-education student attributes (Portuguese students; grades 0-20)

## 3. Objective / Problem Statement
**Notebook 2.0 (quoted):**
> "This project understands how the student's performance (test scores) is affected by other variables such as Gender, Ethnicity, Parental level of education, Lunch and Test preparation course."

**Notebook 5:** No explicit problem statement found.

## 4. Technologies & Libraries
- Python 3 (Jupyter Notebook)
- pandas, numpy
- seaborn, matplotlib.pyplot (%matplotlib inline)
- warnings
- sklearn.model_selection.train_test_split (notebook 5 only)
- No other ML libraries

## 5. EDA Steps Performed
**Notebook 2.0:**
1. Problem statement + data collection (markdown)
2. Read CSV; head/shape; null, isna, duplicate checks; info, nunique, describe
3. Feature segregation: 5 categorical, 3 numerical
4. value_counts for gender and race_ethnicity
5. Feature engineering: total_score = sum of scores; average = total/3
6. Distribution plots of average (overall and by groups)
7. Correlation heatmap

**Notebook 5:**
1. Load CSV; full view, head/tail/shape/info/null check
2. Univariate: school counts + countplot, age histplot, address countplot, reason pie, activities pie, Walc/Dalc value_counts
3. Bivariate: Medu/Fedu countplots, studytime vs G3 and G2 barplots, internet vs G3 barplot
4. Multivariate: sex vs G3 with address hue
5. Boxplot of numeric columns; correlation matrix + heatmap
6. IQR outlier detection on age, absences (22 outlier indices detected, not removed)
7. X/y split (target = absences), train_test_split 25%, random_state=1 -> (486, 29) / (163, 29)
8. Ends with "#internal homework: #data encoding #scaling" - unfinished

## 6. Data Cleaning / Preprocessing
- Notebook 2.0: nulls (0) and duplicates (0) checked - none found; no imputation. No encoding/scaling/split.
- Notebook 5: nulls (0); IQR outlier detection only (not removed); train_test_split performed. **Encoding and scaling NOT done** (left as homework).
- G1, G2, G3 disappear from later outputs without visible drop code (notebook 5) - unexplained.

## 7. Visualizations Used
**Notebook 2.0:**
| Chart | What it shows |
|---|---|
| Histogram + KDE of average (bins=30) | Overall score distribution |
| Histograms of average by gender hue | Female vs male performance |
| 3-panel histograms of average by lunch | Standard lunch vs other |
| 3-panel histograms of average by parental_level_of_education | Parent education effect |
| 3-panel histograms of average by race_ethnicity | Ethnic group performance |
| Correlation heatmap (annotated) | Score inter-correlations |

**Notebook 5:**
| Chart | What it shows |
|---|---|
| Countplot of school | GP 423 vs MS 226 students |
| Histplot of age (bins=10, kde) | Age distribution (skewed; most 16-17) |
| Countplot of address | Urban majority |
| Pie charts: reason, activities | Reason to join course (course 285/649); 48.5% activities |
| Two-panel countplots Medu/Fedu | Mother/Father education distribution |
| Barplots: studytime vs G3/G2 | Study hours vs grades (1h->11, 2h->12 avg) |
| Barplot: internet vs G3 | Internet users score ~12 avg |
| Barplot: sex vs G3 (hue=address) | Urban males and females score higher |
| Boxplot of age, traveltime, studytime, absences, G1, G2, G3 | Outliers; median age 17 |
| Correlation heatmap (coolwarm) | Correlation matrix |

## 8. ML Models Used
**None.** Neither notebook trains a model. Notebook 5 only uses train_test_split. No metrics exist.

## 9. Key Findings
**Notebook 2.0:**
- Score means all close (66-69); std close (14.6-15.19); math min is 0
- "Female student tend to perform well than male students"
- "Standard Lunch help students perform well in exams" (regardless of gender)
- "In general parent's education don't help student perform well in exam" (small effect for males with associate's/master's parents; no effect on females)
- "Students of group A and group B tends to perform poorly in exam" (race_ethnicity)

**Notebook 5:**
- GP has more students than MS; majority age 16-17; mostly urban
- Most common reason: "to join the course"; 48.5% in activities; 45 students have regular weekend alcohol consumption
- Study time: 1h/day -> ~11 avg, 2h -> ~12 avg final grade
- Internet users score ~12 avg
- Urban males and females get higher average marks
- Mothers more educated in higher education than fathers
- Median age 17; outliers exist in some columns

## 10. Missing / Incomplete / Unclear
- Notebook 5 has no problem statement, dataset source, or formal conclusions
- Target choice (`absences`) seems arbitrary; G1/G2/G3 dropped from features without visible code
- Outlier indices detected but never removed or used
- **No encoding, scaling, or model** in either notebook
- Notebook 2.0 ends with an empty cell and no conclusions/summary section
- Heatmap/figures lack titles; notebook 2.0 has subplot-position inconsistency (`plt.subplot(141)` in 1x3 layout)
- Notebook 5: many redundant df.columns prints; several comments-only cells; typos ("45 studentes", "praticipating", "noth urban")