# Methodology

## 1. Data preparation
Five source tables are used: Employee, EducationLevel, PerformanceRating, RatingLevel, and SatisfiedLevel. Power Query is used to prepare the data and create a latest-record table from the historical performance-rating records.

## 2. Latest available satisfaction/performance record
Because an employee may have multiple performance-rating records over time, `Latest_PerformanceRating` is used to select the latest available record per employee for analysis of satisfaction and ratings.

## 3. Satisfaction lookup roles
The `SatisfiedLevel` lookup is duplicated three times to create separate lookup tables for Job Satisfaction, Environment Satisfaction, and Relationship Satisfaction.

## 4. Data model and measures
The prepared tables are loaded into Power Pivot. DAX measures calculate workforce counts, attrition rates, averages, overtime counts, onboarding measures, and satisfaction/performance summaries.

## 5. Reporting
The dashboard contains five pages: Home, Overview, Attrition Drivers, Career Progression, and Satisfaction. PivotTables, charts, and filters support interactive exploration.

## Reproducibility
The macro-enabled Excel workbook is included as the primary executable project artifact. Exact Power Query M code, relationship key details, and complete slicer configuration should be captured from Excel before claiming that the project can be rebuilt from source files alone.
