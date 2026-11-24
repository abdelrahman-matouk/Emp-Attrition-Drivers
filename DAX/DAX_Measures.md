# DAX measures

The measures below are documented from the definitions supplied by the project author. Names and expressions are retained as supplied, except formatting/line breaks.

## Workforce and attrition

```DAX
Total_Emps :=
DISTINCTCOUNT(Employee[EmployeeID])

Active Employees :=
CALCULATE(
    COUNT(Employee[EmployeeID]),
    Employee[Attrition] = "No"
)

No of Attrition :=
CALCULATE(
    COUNT(Employee[EmployeeID]),
    Employee[Attrition] = "Yes"
)

Attrition Rate % :=
DIVIDE(
    CALCULATE(
        COUNT(Employee[EmployeeID]),
        Employee[Attrition] = "Yes"
    ),
    COUNT(Employee[EmployeeID]),
    0
)

Not Evaluated Employees :=
CALCULATE(
    COUNTROWS(Employee),
    FILTER(
        Employee,
        ISBLANK(RELATED(Latest_PerformanceRating[PerformanceID]))
    )
)
```

## Demographics, compensation, and tenure

```DAX
Avg Salary of Attrited Employees :=
CALCULATE(
    AVERAGE(Employee[Monthly_Salary]),
    Employee[Attrition] = "Yes"
)

Avg Salary :=
CALCULATE(
    AVERAGE(Employee[Salary]),
    Employee[Attrition] = "No"
)

Avg Age :=
CALCULATE(
    AVERAGE(Employee[Age]),
    Employee[Attrition] = "No"
)

Avg Age of Attrited Employees :=
CALCULATE(
    AVERAGE(Employee[Age]),
    Employee[Attrition] = "Yes"
)

Avg Tenure :=
CALCULATE(
    AVERAGE(Employee[YearsAtCompany]),
    Employee[Attrition] = "No"
)

Avg Tenure of Attrited Employees :=
CALCULATE(
    AVERAGE(Employee[YearsAtCompany]),
    Employee[Attrition] = "Yes"
)

Avg Years Since Last Promotion for Attrited :=
CALCULATE(
    AVERAGE(Employee[YearsSinceLastPromotion]),
    Employee[Attrition] = "Yes"
)

Avg Years in Current Role for Attrited :=
CALCULATE(
    AVERAGE(Employee[YearsInMostRecentRole]),
    Employee[Attrition] = "Yes"
)
```

## Overtime

```DAX
Attritions-With OverTime :=
CALCULATE(
    COUNT(Employee[OverTime]),
    Employee[OverTime] = "Yes",
    Employee[Attrition] = "Yes"
)

Overtim_No :=
CALCULATE(
    COUNT(Employee[OverTime]),
    Employee[OverTime] = "Yes"
)
```

## Performance and satisfaction

```DAX
Avg_Self-Rating :=
CALCULATE(
    AVERAGE(Latest_PerformanceRating[SelfRating]),
    Employee[Attrition] = "Yes"
)

Avg_Manger-Rating :=
CALCULATE(
    AVERAGE(Latest_PerformanceRating[ManagerRating]),
    Employee[Attrition] = "Yes"
)

[Avg Job_Satisfaction ] :=
AVERAGE(Latest_PerformanceRating[JobSatisfaction])

[Avg Worklife_Balance ] :=
AVERAGE(Latest_PerformanceRating[WorkLifeBalance])
```

## Onboarding

```DAX
Onboarding Attrition Count :=
CALCULATE(
    [No of Attrition],
    Employee[YearsAtCompany Group] = "0-2"
)

Onboarding Attrition Rate % :=
CALCULATE(
    [Attrition Rate %],
    Employee[YearsAtCompany Group] = "0-2"
)
```

## Satisfaction and attrition segments

```DAX
Attrition% for low UnSatisfied Emps :=
CALCULATE(
    [Attrition Rate %],
    Latest_PerformanceRating[JobSatisfaction] IN {1, 2}
)

Attrition% for High Satisfied Emps :=
CALCULATE(
    [Attrition Rate %],
    Latest_PerformanceRating[JobSatisfaction] IN {4, 5}
)

Active LowSatisfied Emps :=
CALCULATE(
    [Total_Emps],
    Employee[Attrition] = "No",
    Latest_PerformanceRating[JobSatisfaction] IN {1, 2}
)

Attrited LowSatisfied Emps :=
CALCULATE(
    [Total_Emps],
    Employee[Attrition] = "Yes",
    Latest_PerformanceRating[JobSatisfaction] IN {1, 2}
)

Attrited High_Satisfied Emps :=
CALCULATE(
    [Total_Emps],
    Employee[Attrition] = "Yes",
    Latest_PerformanceRating[JobSatisfaction] IN {4, 5}
)
```

## Validation notes before publishing
1. `Avg Salary of Attrited Employees` averages `Employee[Monthly_Salary]`, while `Avg Salary` averages `Employee[Salary]`. Confirm whether these columns represent the same unit/definition before comparing them.
2. `Overtim_No` filters `OverTime = "Yes"` despite its name. Confirm whether the name or filter is incorrect.
3. `Active LowSatisfied Emps` was supplied twice with the same expression; it is listed once here.
4. `Avg_Self-Rating` and `Avg_Manger-Rating` are filtered to employees with `Attrition = "Yes"`.
5. `Not Evaluated Employees` identifies employees with no related `Latest_PerformanceRating` row; it does not necessarily prove they were never evaluated historically.
6. The satisfaction attrition rates should be checked against the dashboard's displayed values and intended denominator/filter context before presenting them as a conclusion.

These definitions are transcribed from the author's supplied measures. They have not been independently recalculated or rewritten.
