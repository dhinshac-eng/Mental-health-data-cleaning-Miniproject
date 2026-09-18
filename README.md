# Mental Health & Workplace Survey — Data Cleaning Mini-Project

## Overview
This project analyzes a workplace survey dataset examining the relationship
between employee mental health and workplace factors such as stress,
burnout, work hours, sleep, and job satisfaction. The workbook contains
**3,000 employee records** across **7 countries** and **6 departments**,
cleaned and enriched using Power Query.

## File Structure
The workbook (`Mental_Health_Data_Cleaning.xlsx`) contains two sheets:

| Sheet | Rows | Columns | Description |
|---|---|---|---|
| `mental_health_workplace_survey` | 3,000 | 25 | Raw/base survey data |
| `PowerQuery Analysis` | 3,000 | 31 | Cleaned data + 6 derived category columns built with Power Query |

No missing values were found in any column of the base dataset.

## Column Dictionary

### Identifiers & Demographics
| Column | Type | Description |
|---|---|---|
| `EmployeeID` | Integer | Unique employee identifier (3,000 unique values) |
| `Age` | Integer | Employee age (range: 22–59) |
| `Gender` | Text | Male, Female, Non-binary, Prefer not to say |
| `Country` | Text | UK, Germany, India, Australia, Brazil, USA, Canada |
| `JobRole` | Text | e.g. Software Engineer, Data Scientist, HR Specialist, Sales Associate, etc. (8 roles) |
| `Department` | Text | HR, IT, Support, Engineering, Marketing, Sales |
| `YearsAtCompany` | Integer | Tenure in years (0–20) |

### Work Patterns
| Column | Type | Description |
|---|---|---|
| `WorkHoursPerWeek` | Integer | Hours worked per week (30–59) |
| `RemoteWork` | Text | No, Hybrid, Yes |
| `CommuteTime` | Integer | One-way commute time in minutes (0–119) |
| `TeamSize` | Integer | Number of people on the employee's team (1–49) |
| `SalaryRange` | Text | Banded salary: `<40K`, `40K-60K`, `60K-80K`, `80K-100K`, `100K+` |

### Wellbeing & Mental Health Metrics (scored 1–10 unless noted)
| Column | Type | Description |
|---|---|---|
| `BurnoutLevel` | Float | Self-reported burnout severity |
| `JobSatisfaction` | Float | Self-reported job satisfaction |
| `StressLevel` | Float | Self-reported stress |
| `ProductivityScore` | Float | Self-reported productivity |
| `SleepHours` | Float | Average nightly sleep hours |
| `PhysicalActivityHrs` | Float | Weekly hours of physical activity |
| `ManagerSupportScore` | Float | Perceived support from manager |
| `WorkLifeBalanceScore` | Float | Perceived work-life balance |
| `CareerGrowthScore` | Float | Perceived career growth opportunity |
| `MentalHealthDaysOff` | Integer | Mental-health-related days off taken (0–9) |

### Support & Outcome Flags
| Column | Type | Description |
|---|---|---|
| `HasMentalHealthSupport` | Text | Whether employer offers mental health support (Yes/No) |
| `HasTherapyAccess` | Text | Whether employee has therapy access (Yes/No) |
| `BurnoutRisk` | Integer (0/1) | Binary flag: 1 = at risk of burnout, 0 = not |

### Derived Category Columns (Power Query Analysis sheet only)
These bucket the continuous scores into readable tiers:

| Column | Categories | Thresholds (based on source score) |
|---|---|---|
| `Stress Category` | Low / Moderate / High | Low: 1–3.99, Moderate: 4–6.99, High: 7–10 |
| `Burnout Category` | Low / Moderate / High | Low: 1–3.99, Moderate: 4–6.99, High: 7–10 |
| `Job Satisfaction Category` | Low / Moderate / High | Low: 1–3.99, Moderate: 4–6.99, High: 7–10 |
| `Work-Life Balance Category` | Poor / Moderate / Good | Poor: 1–3.99, Moderate: 4–6.99, Good: 7–10 |
| `Sleep Category` | Low / Moderate / Adequate | Low Sleep: 4–5.9, Moderate Sleep: 6–7.9, Adequate Sleep: 8–9 |
| `Work Hours Category` | Normal / Overtime / Extreme Overtime | Normal: 30–40 hrs, Overtime: 41–50 hrs, Extreme Overtime: 51–59 hrs |

## Data Cleaning Steps (Power Query)
1. Loaded the raw survey export into Power Query.
2. Verified data types for each column (integers, decimals, text).
3. Checked for and confirmed no missing/null values.
4. Standardized categorical text values (e.g., Yes/No, RemoteWork options).
5. Created six new calculated/binned columns to classify continuous scores
   (stress, burnout, job satisfaction, work-life balance, sleep, work hours)
   into Low/Moderate/High-style tiers for easier grouping and visualization.
6. Output the cleaned, enriched table to the `PowerQuery Analysis` sheet
   while preserving the original data on a separate sheet for reference.

## Suggested Uses
- Explore correlations between work hours, sleep, and burnout/stress levels.
- Compare mental health support availability against burnout risk across
  departments or countries.
- Build pivot tables/dashboards using the categorical tiers for quick
  visual summaries (e.g., % of employees in "High" burnout by department).
- Use `BurnoutRisk` as a target variable for a simple classification model.

## Notes
- All wellbeing/support scores are self-reported on a 1–10 scale (with two
  scores occasionally reaching 9.99 due to rounding in the source data).
- `EmployeeID` values are unique and can be used as a primary key when
  joining across sheets or exporting subsets.
