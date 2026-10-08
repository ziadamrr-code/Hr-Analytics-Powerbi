# HR Analytics Dashboard (Power BI)

An interactive 3-page Power BI dashboard analyzing **100 employees** across **5 departments** and **3 locations**: headcount, payroll, salaries, workforce profile, and the change in performance between 2019 and 2020.

## Dashboard

### Overview
![Overview](overview.png)

### Performance
![Performance](performance.png)

### Staff & Salary
![Staff and Salary](staff-salary.png)

## Business Questions

1. How is the workforce distributed across departments, locations, gender, and education?
2. How much is the total payroll, and where does it go?
3. How did employee performance change from 2019 to 2020, and where was the change largest?
4. What do salaries look like across job titles, and who earns the most and the least?
5. What is the age and tenure profile of each location?

## Data

- Source: one Excel workbook with **5 sheets** (Sales, Marketing, IT, HR, Finance), one per department
- **100 employees**, 13 original columns: employee ID, name, gender, job title, department, location, hire date, birth date, education, salary, performance score 2019, performance score 2020
- The dataset is in **Arabic**, and the dashboard uses the original Arabic field values

## Data Preparation (Power Query)

- **Appended the 5 department sheets** into one table
- Set correct data types (dates, currency, percentages, text)
- Filled missing department values in the HR sheet
- **Standardized spelling** of city names (e.g. two different spellings of Cairo and Alexandria)
- Added calculated **Age** and **Tenure** columns from birth and hire dates, measured as of **31 Dec 2020** to match the performance data period

## Data Model & DAX Measures

A dedicated measures table keeps all KPIs in one place:

| Measure | Definition |
|---|---|
| Total Employees | `COUNT` of employee IDs |
| Total Payroll | `SUM` of salary |
| Avg / Min / Max Salary | `AVERAGE` / `MIN` / `MAX` of salary |
| Avg Age, Avg Tenure | `AVERAGE` of the calculated columns (as of 31 Dec 2020) |
| Male Count, Female Count, Female Ratio % | `CALCULATE` with a gender filter, and `DIVIDE` |
| Avg Performance 2019 / 2020 | `AVERAGE` of the performance scores |
| Performance Change % | `DIVIDE(Avg 2020 - Avg 2019, Avg 2019)` |

## Key Findings

| Metric | Value |
|---|---|
| Employees | **100** (50 male, 50 female) |
| Total payroll | **1,317,162** |
| Average salary | **13,172** (min 1,428, max 35,000) |
| Average age / tenure | **46 years** / **10 years** (as of 31 Dec 2020) |
| Avg performance 2019 → 2020 | **81.8% → 71.2%** (**-13.0%**) |

**Headcount:** Sales 37, HR 23, Marketing 18, IT 12, Finance 10. Alexandria 46, Cairo 36, Tanta 18.

**Performance change by location**

| Location | 2019 | 2020 | Change |
|---|---|---|---|
| Alexandria | 81.7% | 65.8% | **-19.5%** |
| Tanta | 81.8% | 73.1% | -10.7% |
| Cairo | 82.0% | 77.2% | -5.8% |

### Observations

- **Performance declined broadly.** 66 of 100 employees scored lower in 2020, 29 scored higher, and 5 were unchanged.
- **Alexandria drove the decline.** It has the largest location (46 employees) and the steepest drop, more than three times Cairo's.
- **Sales is the biggest payroll block.** The Sales department holds about 39% of total payroll, and Sales reps alone account for about 36%.
- **Gender balance is even** (50/50), and average salary is close between women (13,289) and men (13,055).
- **Education:** the 4 employees with a master's degree average about 24.5K, roughly double the bachelor's (12.4K) and diploma (13.2K) groups. The master's group is very small, so this should be read with care.

## Data Notes

- In the IT sheet, **6 employee IDs appear twice**, each time with different names but identical job, salary, and performance scores. The rows were kept as provided, so they are included in the headcount of 100.
- **Age and Tenure** are calculated as of **31 Dec 2020** (not today's date), so the values stay fixed and match the 2019-2020 performance period.
- **3 employees** have hire dates that imply they were hired before the age of 18. The dates were kept as provided.

## Tools

Power BI (Power Query, DAX, data modeling, slicers, page navigation) and Excel as the data source.

## Files

| File | Description |
|---|---|
| `Final_Project_power_bi.pbix` | The Power BI report |
| `overview.png`, `performance.png`, `staff-salary.png` | Dashboard screenshots |

## Author

**Ziad Amr** - [LinkedIn](www.linkedin.com/in/ziadamrr) 
