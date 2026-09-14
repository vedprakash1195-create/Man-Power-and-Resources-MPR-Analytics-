# Man Power and Resources (MPR) Analytics – Power BI / SQL

## 📊 Project Overview

An interactive MPR (Man Power and Resources) Analytics Dashboard developed using Microsoft Power BI, SQL Server and Excel data to analyze workforce trends, manpower deployment, and resource utilization across departments.

## 🎯 Objectives

- Analyze total manpower strength across departments/locations
- Track manpower utilization vs allocation
- Identify vacant positions and staffing gaps
- Analyze resource distribution by department, role, and shift
- Clean and transform raw data, identify anomalies and missing values
- Track key manpower KPIs for data-driven decision-making

## 📌 Key KPIs

- Total Sanctioned Manpower
- Total Deployed Manpower
- Vacancy Count & Vacancy Rate (%)
- Manpower Utilization Rate (%)
- Department-wise Headcount
- Contract vs Permanent Staff Ratio

## 📈 Dashboard Analysis

The dashboard includes:

- Manpower Allocation by Department
- Manpower Allocation by Location/Site
- Vacancy Analysis by Role
- Resource Utilization Trend (Month-wise)
- Staff Category Breakdown (Permanent / Contract / Trainee)
- Shift-wise Manpower Distribution

## 🗄️ SQL Analysis

SQL Server was used to clean, transform, and calculate the core manpower KPIs before visualizing them in Power BI.

**Sample Queries:**

```sql
-- Total Sanctioned vs Deployed Manpower
SELECT 
    Department,
    SUM(Sanctioned_Strength) AS Total_Sanctioned,
    SUM(Deployed_Strength) AS Total_Deployed,
    SUM(Sanctioned_Strength) - SUM(Deployed_Strength) AS Vacancy_Count
FROM Manpower_Data
GROUP BY Department;

-- Vacancy Rate by Department
SELECT 
    Department,
    ROUND((SUM(Sanctioned_Strength) - SUM(Deployed_Strength)) * 100.0 
        / NULLIF(SUM(Sanctioned_Strength), 0), 1) AS Vacancy_Rate
FROM Manpower_Data
GROUP BY Department
ORDER BY Vacancy_Rate DESC;

-- Staff Category Distribution
SELECT 
    Staff_Category,
    COUNT(*) AS Total_Staff,
    ROUND(COUNT(*) * 100.0 / (SELECT COUNT(*) FROM Manpower_Data), 1) AS Percentage
FROM Manpower_Data
GROUP BY Staff_Category;

-- Identifying Missing/Anomalous Records
SELECT *
FROM Manpower_Data
WHERE Department IS NULL 
   OR Sanctioned_Strength IS NULL 
   OR Deployed_Strength < 0;

-- Month-wise Manpower Utilization Trend
SELECT 
    FORMAT(Report_Date, 'MMM-yyyy') AS Month,
    SUM(Deployed_Strength) AS Total_Deployed,
    SUM(Sanctioned_Strength) AS Total_Sanctioned,
    ROUND(SUM(Deployed_Strength) * 100.0 / NULLIF(SUM(Sanctioned_Strength), 0), 1) AS Utilization_Rate
FROM Manpower_Data
GROUP BY FORMAT(Report_Date, 'MMM-yyyy')
ORDER BY MIN(Report_Date);
```

These cleaned and aggregated query results were connected to Power BI for interactive visualization and dashboard reporting.

## 🛠️ Tools & Technologies

- Power BI
- SQL Server
- DAX
- Microsoft Excel
- Data Cleaning & Transformation
- Data Visualization

## 💡 Key Insights

- Certain departments consistently show higher vacancy rates compared to others, indicating staffing gaps.
- Manpower utilization fluctuates month-to-month, highlighting seasonal or project-based demand.
- A significant portion of the workforce falls under contract staffing, impacting long-term resource planning.
- Data anomalies (missing or negative values) were identified and cleaned before analysis, improving report accuracy.

## 👨‍💻 Author

Ved Prakash
