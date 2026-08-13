# HR Analytics - Employees Engagement EDA

## 1. Project Overview
EDA of an HR employees-engagement dataset (Kaggle) covering 311 employees. The analysis explores salaries, performance scores, absences, recruitment sources, satisfaction, engagement surveys, and multivariate relationships, with the goal of obtaining actionable HR insights. Descriptive EDA only - no machine learning.

**Notebook:** `2. EDA-HR Analytics.ipynb`

## 2. Dataset
- **Source:** stated as "present in kaggle platform" (Employees Engagement dataset)
- **File:** `HRDataset_v14.csv`
- **Rows x Columns:** 311 rows x 36 columns
- **Domain:** HR Analytics - employee engagement, performance, satisfaction, attrition
- **Target variable:** none explicitly defined - descriptive EDA only; attrition-related columns (Termd, TermReason) explored via counts
- **Columns (36):** Employee_Name, EmpID, MarriedID, MaritalStatusID, GenderID, EmpStatusID, DeptID, PerfScoreID, FromDiversityJobFairID, Salary, Termd, PositionID, Position, State, Zip, DOB, Sex, MaritalDesc, CitizenDesc, HispanicLatino, RaceDesc, DateofHire, DateofTermination, TermReason, EmploymentStatus, Department, ManagerName, ManagerID, RecruitmentSource, PerformanceScore, EngagementSurvey, EmpSatisfaction, SpecialProjectsCount, LastPerformanceReview_Date, DaysLateLast30, Absences

## 3. Objective / Problem Statement (quoted from markdown)
> "HR Analytics - Employees Engagement... In this EDA project we will performing HR Analytics - Employees Engagement Analysis... we'll be performing different analysis and visualizations using the Employees Engagement Dataset to obtain some valuable insights"

Context: evaluating employee performance/efficiency is "the most difficult task" for HRs.

## 4. Technologies & Libraries
- Python 3 (Jupyter Notebook)
- pandas, numpy
- seaborn, matplotlib.pyplot
- warnings
- No scikit-learn or other ML/stats libraries

## 5. EDA Steps Performed
1. Load data; view df, columns, shape, dtypes, info()
2. Null check, fill, duplicate check
3. Top 10 highest salaries
4. Performance score inspection (unique values; PIP employees - 13)
5. Absences: value counts + normalized percentages
6. Married status counts; special projects count analysis (70 employees with none)
7. Bar chart: top-10 highest vs lowest salaries
8. Recruitment source analysis (uniques + horizontal bar)
9. Performance trend lineplot
10. Employee satisfaction (scale 1-5) value counts + stem plot
11. Multivariate: salary by department (boxplot), engagement by position (barplot), marital status by gender (countplot), avg engagement by department (groupby mean)
12. "Internal homework" Q&A: terminations by position/reason, median salary by sex, absences/engagement by department, special projects/absences by gender
13. Ends with an unfinished list of questions (max salary, min days late, earliest/latest dates...) - analysis stops there

## 6. Data Cleaning / Preprocessing
- Nulls: DateofTermination (207), ManagerID (8) - filled with the **string "0"** via `fillna("0")` (mixed-type imputation; note: wrong type for numeric ManagerID)
- Duplicates: 0 found; drop_duplicates run anyway (no effect)
- **No encoding, no scaling, no outlier removal, no feature engineering** found

## 7. Visualizations Used
| Chart | What it shows |
|---|---|
| Bar chart: top-10 highest (green) vs lowest (red) salaries | Highest salaries vary a lot (~138,888-250,000); lowest are close together (~45,046-46,430) |
| Horizontal bar: recruitment source | Indeed 87, LinkedIn 76, Google Search 49, Employee Referral 31, Diversity Job Fair 29, CareerBuilder 23, Website 13, Other 2, On-line Web application 1 |
| Line plot: performance trend | PerformanceScore counts: Fully Meets 243, Exceeds 37, Needs Improvement 18, PIP 13 |
| Stem plot: satisfaction ratings 1-5 | 3->108, 5->98, 4->94, 2->9, 1->2 |
| Boxplot: salary by department | Salary distributions with outliers (Executives paid highest; least in Production) |
| Barplot: engagement survey by position | Engagement scores across positions |
| Countplot: marital status x gender | "Most of the males are single" |

## 8. ML Models Used
**None.** No model imports, no train/test split, no metrics anywhere.

## 9. Key Findings
- 13 employees on PIP ("needs special attention")
- Highest absences = 20 leaves (by 4.5% of employees); most common satisfaction rating = 3
- 187 employees not married vs 124 married (notebook comment says "187 employees are marries" - see section 10)
- 70 employees have no special project
- Indeed is the most common recruitment source, then LinkedIn, Google Search
- Executives paid highest; least salary in Production; outliers present
- Executive Office has highest avg engagement (4.83): dept means Admin 4.39, Executive 4.83, IT/IS 4.15, Production 4.13, Sales 3.82, Software Eng 4.06
- Terminations highest for Production Technician I (52) and II (26); top reasons: "Another position" 20, "unhappy" 14, "more money" 11
- Median salary: F 62,066.5 vs M 63,353 (slightly higher for males)
- Production has by far the most absences (2,120 total); Sales lowest avg engagement

## 10. Missing / Incomplete / Unclear
- **No machine learning at all** despite notebook numbering implying an EDA module
- No conclusion/summary markdown; notebook ends on an unfinished list of questions
- Data-cleaning flaw: nulls replaced with string "0" (wrong type for numeric ManagerID)
- Redundant filler cells (df.columns printed 10+ times)
- Unlabeled/mislabeled charts (x-axis "Recruitment score" should be source; duplicate plt.ylabel; no titles)
- Some insights factually off (187 count is MarriedID==0 i.e. NOT married; "4.5 percent" vs ~6.4-7.4% shown)
- Numerous typos ("marries", "emloyees", "mdeian", "enagement", etc.)
- "Internal homework" sections mix questions into code cells with no narrative answers
- No correlation analysis / heatmap, no train/test split, no feature selection