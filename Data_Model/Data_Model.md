# Power Pivot data model

## Tables observed in the model diagram
- `Employee`
- `Latest_PerformanceRating`
- `RatingLevel`
- `Job Satisfaction`
- `Relationship Satisfaction`
- `Environment Satisfaction`
- `A` — measures table

## Model design
`Employee` stores employee-level attributes and the attrition flag. `Latest_PerformanceRating` stores the selected latest review record and its rating/satisfaction fields. Lookup tables provide readable labels for rating and satisfaction IDs/values.

The three satisfaction lookup tables are duplicated versions of `SatisfiedLevel`, assigned separate roles for job, environment, and relationship satisfaction.

## Relationship notes
The supplied Power Pivot diagram shows one-to-many relationships between the latest performance records and the employee / rating / satisfaction lookup tables. The exact key columns and filter direction should be confirmed from the relationship properties in Excel before publishing a formal relationship matrix.

## Why a latest-record table?
The employee table is employee-grain, while the original performance-rating table can contain multiple review records per employee. The latest-record table supports employee-level comparisons using one latest available review record per employee.

## Diagram
See the Power Pivot Diagram View screenshot captured during project review, if added by the author.
