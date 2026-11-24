# Power Query — Data preparation

## Source tables
The project identifies five source tables:
- `Employee`
- `EducationLevel`
- `PerformanceRating`
- `RatingLevel`
- `SatisfiedLevel`

## Latest performance record
The project creates `Latest_PerformanceRating` from `PerformanceRating` to use the latest recorded review/satisfaction row for each employee in the analysis.

The source `PerformanceRating` table can contain multiple records per employee over time. Using the latest available record avoids treating every historical review as a separate current employee state in the satisfaction/performance views.

**Interpretation:** latest available record means the most recent record present in the dataset; it does not guarantee a live/current employee sentiment.

## Satisfaction lookup queries
The original `SatisfiedLevel` lookup contains:

| SatisfactionID | SatisfactionLevel |
|---:|---|
| 1 | Very Dissatisfied |
| 2 | Dissatisfied |
| 3 | Neutral |
| 4 | Satisfied |
| 5 | Very Satisfied |

Three queries were created by **duplicating** the original query:
- `Job Satisfaction`
- `Environment Satisfaction`
- `Relationship Satisfaction`

Each duplicated lookup is used for a different satisfaction field in `Latest_PerformanceRating`.

## Reproducibility note
The original workbook contains the Power Query connections/queries. The exact M expressions and applied-step names should be exported from Excel's Power Query Advanced Editor before they are documented verbatim. This file describes the confirmed transformation design without inventing unverified M code.
