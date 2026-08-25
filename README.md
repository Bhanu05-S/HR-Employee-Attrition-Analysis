# HR-Employee-Attrition-Analysis
An end-to-end HR analytics project using **MySQL, Python and Power BI** to analyze employee attrition, identify workforce segments with higher turnover, and generate data-driven retention recommendations.

---

## 📌 Project Overview

Employee attrition can create significant recruitment, training and productivity costs for organizations.

The objective of this project is to analyze employee characteristics and workforce patterns to identify **factors associated with employee attrition** and provide actionable insights for HR and management.

The analysis covers:

* Overall employee attrition
* Department-level attrition
* Job-role attrition
* Overtime and attrition
* Job satisfaction
* Age groups
* Years at company
* Income and attrition
* High-risk departments and job roles
* Combined workforce segments

The project follows an end-to-end analytics workflow:

**Dataset → Data Validation → SQL Analysis → Python EDA → Power BI → Business Insights → Recommendations**

---

## 🎯 Business Problem

Organizations need to understand:

1. How large is the current workforce?
2. How many employees have left?
3. Which departments have higher attrition?
4. Which job roles show higher turnover?
5. Is overtime associated with higher attrition?
6. Which age groups have higher attrition?
7. Does tenure appear to be associated with attrition?
8. Is job satisfaction associated with employee turnover?
9. Which workforce segments require further investigation?
10. What actions could HR consider to improve retention?

---

## 🎯 Project Objective

The objective is to use SQL, Python and Power BI to:

* Validate the HR dataset
* Calculate workforce KPIs
* Analyze attrition patterns
* Segment employees into meaningful groups
* Identify high-risk workforce segments
* Visualize findings through an interactive Power BI dashboard
* Translate analytical findings into business recommendations

---

## 🗂️ Dataset

The project uses the **IBM HR Analytics Employee Attrition & Performance** dataset.

The dataset contains:

* **1,470 employees**
* **35 columns**

Important fields include:

* EmployeeNumber
* Age
* Attrition
* Department
* JobRole
* JobSatisfaction
* MonthlyIncome
* OverTime
* YearsAtCompany
* YearsSinceLastPromotion
* PerformanceRating
* Gender

The project documentation identifies this as a fictional/synthetic HR analytics dataset.

---

## 🛠️ Tools & Technologies

### SQL

* MySQL
* SELECT
* WHERE
* GROUP BY
* HAVING
* CASE
* Aggregate functions
* Conditional aggregation
* KPI calculations

### Python

* Pandas
* NumPy
* Matplotlib
* Seaborn
* Exploratory Data Analysis

### Power BI

* DAX
* KPI cards
* Bar charts
* Column charts
* Slicers
* Interactive dashboard
* Workforce segmentation

The project instructions specifically use Pandas, NumPy, Matplotlib, Seaborn, Power BI and DAX.

---

## 🔄 Project Workflow

```text
HR Dataset
    ↓
Data Validation
    ↓
MySQL Analysis
    ↓
Python Exploratory Data Analysis
    ↓
Power BI Dashboard
    ↓
Business Insights
    ↓
Recommendations
```

---

# 1️⃣ Data Validation

Before performing analysis, the dataset was checked for data-quality issues.

### Duplicate check

EmployeeNumber was checked for duplicate employee records.

Expected result:

```text
No duplicate employees
```

### NULL-value check

Important fields checked included:

* EmployeeNumber
* Age
* Attrition
* Department
* JobRole
* MonthlyIncome
* YearsAtCompany

The project documentation expects these checks to return zero missing values.

### Categorical validation

Distinct values were checked for:

* Attrition
* Department
* JobRole

This helps prevent inconsistent categories from affecting SQL and Power BI results.

---

# 2️⃣ SQL Analysis

The SQL analysis was divided into workforce KPIs and business-focused attrition analysis.

## Overall Workforce KPIs

```sql
SELECT
    COUNT(*) AS total_employees,
    SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) AS employees_left,
    ROUND(
        SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END)
        * 100.0 / COUNT(*),
        2
    ) AS attrition_rate,
    ROUND(AVG(Age), 2) AS average_age,
    ROUND(AVG(MonthlyIncome), 2) AS average_monthly_income,
    ROUND(AVG(YearsAtCompany), 2) AS average_years_at_company
FROM employee_data;
```

This query demonstrates conditional aggregation, KPI calculation and aggregate functions.

---

# 3️⃣ Python Exploratory Data Analysis

Python was used to independently validate and explore the dataset.

The notebook workflow includes:

1. Import Libraries
2. Load Dataset
3. Data Overview
4. Data Quality Checks
5. Data Cleaning
6. Exploratory Data Analysis
7. Attrition Analysis
8. Visualization
9. Key Findings
10. Business Recommendations

The project uses Pandas for analysis and Matplotlib/Seaborn for visualization.

### Python validation

```python
df.shape
```

Expected:

```text
(1470, 35)
```

Duplicate validation:

```python
df.duplicated().sum()
```

Expected:

```text
0
```

---

# 4️⃣ Power BI Dashboard

The Power BI dashboard is designed around three pages.

## Page 1 — Executive Overview

The dashboard includes KPI cards for:

* Total Employees
* Employees Left
* Attrition Rate
* Average Monthly Income
* Average Years at Company

Additional visuals:

* Attrition by Department
* Attrition by Job Role
* Attrition by Overtime

Slicers:

* Department
* JobRole
* Gender
* OverTime

The project instructions define these as the main Executive Overview components.

---

## Page 2 — Attrition Drivers

This page focuses on characteristics associated with employee turnover.

Visuals include:

* Overtime vs Attrition
* Job Satisfaction vs Attrition
* Age Group vs Attrition
* Tenure Group vs Attrition
* Income Group vs Attrition

The project uses the following age groups:

* Under 25
* 25–34
* 35–44
* 45–54
* 55+

And tenure groups:

* 0–1 Years
* 2–5 Years
* 6–10 Years
* 10+ Years

These segmentation rules are defined in the project documentation and SQL files.

---

## Page 3 — Workforce Analysis

This page provides broader workforce analysis.

Visuals include:

* Employees by Department
* Employees by Job Role
* Average Income by Department
* Average Years at Company by Department
* Performance Rating vs Attrition
* Years Since Last Promotion vs Attrition

Slicers include:

* Department
* Job Role
* Gender
* Age Group
* OverTime

---

# 5️⃣ DAX Measures

The main Power BI measures are:

```DAX
Total Employees =
COUNTROWS('employee_data')
```

```DAX
Employees Left =
CALCULATE(
    COUNTROWS('employee_data'),
    'employee_data'[Attrition] = "Yes"
)
```

```DAX
Attrition Rate =
DIVIDE(
    [Employees Left],
    [Total Employees],
    0
)
```

```DAX
Average Monthly Income =
AVERAGE('employee_data'[MonthlyIncome])
```

```DAX
Average Years at Company =
AVERAGE('employee_data'[YearsAtCompany])
```

These measures form the basis of the dashboard KPI cards.

---

# 6️⃣ Key Findings

## Overall Attrition

The dataset contains:

* **1,470 employees**
* **237 employees who left**
* **16.12% overall attrition**

---

## Overtime

Employees working overtime showed substantially higher attrition than employees who did not work overtime.

This was one of the main business questions in the SQL and Python analysis.

**Interpretation:** Overtime is associated with higher employee attrition in this dataset.

---

## Department

Attrition varies across departments.

The analysis compares:

* Human Resources
* Research & Development
* Sales

The department-level SQL ranks departments by attrition rate.

---

## Job Role

Attrition varies considerably across job roles.

The SQL analysis specifically identifies roles whose attrition rate exceeds the overall **16.12% benchmark**.

---

## Age

Employees are grouped into five age categories.

The SQL analysis calculates attrition rates for each group and orders them from highest to lowest.

---

## Tenure

Employees are grouped according to:

* 0–1 Years
* 2–5 Years
* 6–10 Years
* 10+ Years

The analysis indicates that attrition varies considerably by tenure.

---

## Job Satisfaction

Job satisfaction is represented by four levels:

| Score | Level     |
| ----: | --------- |
|     1 | Low       |
|     2 | Medium    |
|     3 | High      |
|     4 | Very High |

Attrition is calculated for each satisfaction level.

---

# 7️⃣ Business Recommendations

### 1. Review overtime exposure

Investigate teams and roles with consistently high overtime exposure and review workload distribution.

### 2. Strengthen early-tenure retention

Introduce structured onboarding, mentoring and regular first-year employee check-ins.

### 3. Investigate high-risk job roles

Use job-role attrition rates to prioritize further HR investigation.

### 4. Monitor younger employee segments

Develop career-development and progression programs for early-career employees.

### 5. Monitor employee satisfaction

Use employee feedback and engagement programs to investigate low-satisfaction segments.

### 6. Use targeted retention strategies

Instead of applying one retention strategy to every employee, prioritize combinations of:

```text
High overtime
+
Short tenure
+
High-risk job role
+
Higher observed attrition
```

---

# 8️⃣ Important Analytical Limitation

This project identifies **associations**, not causal relationships.

For example:

> Employees working overtime have higher observed attrition.

It would be incorrect to conclude:

> Overtime causes employees to leave.

The dataset is observational, so causal conclusions cannot be established from these analyses alone. The original project instructions explicitly emphasize this distinction.

---

# 9️⃣ Repository Structure

```text
Employee-Attrition-Workforce-Analytics/
│
├── Dataset/
│   └── HR-Employee-Attrition.csv
│
├── SQL/
│   ├── 01_Data_Validation.sql
│   ├── 02_Attrition_Analysis.sql
│   └── 03_Business_Insights.sql
│
├── Python/
│   └── Employee_Attrition_Analysis.ipynb
│
├── PowerBI/
│   └── HR.pbix
│
├── Images/
│   ├── Dashboard_Overview.png
│   ├── Attrition_Drivers.png
│   └── Workforce_Analysis.png
│
└── README.md
```

This structure follows the portfolio organization specified in the project instructions.

---

# 🔟 Skills Demonstrated

### Technical Skills

* MySQL
* SQL aggregation
* GROUP BY
* HAVING
* CASE statements
* Conditional aggregation
* Data validation
* Data segmentation
* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Power BI
* DAX
* Dashboard development

### Analytical Skills

* Business problem definition
* KPI development
* Exploratory data analysis
* Workforce segmentation
* Pattern identification
* Insight generation
* Business recommendations
* Data storytelling

---

## 📌 Conclusion

This project demonstrates an end-to-end approach to HR analytics:

**SQL** was used to validate and analyze the workforce data.

**Python** was used for exploratory analysis and visualization.

**Power BI** was used to transform the analysis into an interactive management dashboard.

The final analysis highlights workforce segments with higher observed attrition and provides targeted areas for HR investigation and retention planning.
