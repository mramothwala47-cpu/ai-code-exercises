# Exercise: Function Decomposition Challenge

## Selected Function

**Report Generation Function with Multiple Data Transformations (Python)**

The function selected for this exercise is `generate_sales_report()` from the provided `sales_report.py` project.


# AI Prompt Used

> I have a complex function that I'd like to refactor by breaking it down into smaller functions.
>
> Please:
>
> 1. Identify the distinct responsibilities in this function.
> 2. Suggest a decomposition strategy with smaller functions.
> 3. Show which parts of the original code would move to each new function.
> 4. Provide a refactored version where the main function delegates work to smaller helper functions.


# Responsibility Analysis
The AI identified that `generate_sales_report()` performs many different responsibilities, violating the **Single Responsibility Principle**.

The responsibilities include:

1. Input validation.
2. Date range validation and filtering.
3. Applying custom filters.
4. Handling empty datasets.
5. Calculating summary metrics.
6. Grouping sales data.
7. Building the report structure.
8. Creating detailed transaction reports.
9. Generating forecast information.
10. Building chart data.
11. Producing the requested output format (JSON, HTML, Excel, or PDF).


# Decomposition Plan

The large function can be broken into the following helper functions.

| Helper Function | Responsibility |
|-----------------|----------------|
| `validate_inputs()` | Validate report parameters and inputs |
| `filter_by_date_range()` | Filter sales using the selected date range |
| `apply_filters()` | Apply custom user filters |
| `calculate_summary_metrics()` | Calculate totals, averages, minimums, and maximums |
| `group_sales_data()` | Group sales by category, region, customer, or product |
| `build_summary_report()` | Build the report summary section |
| `build_detailed_report()` | Generate detailed transaction information |
| `build_forecast_report()` | Generate monthly sales forecasts |
| `generate_chart_data()` | Build chart information |
| `export_report()` | Produce JSON, HTML, Excel, or PDF output |



# Refactored Main Function

Instead of containing hundreds of lines of logic, the main function would become much simpler.

```python
def generate_sales_report(
    sales_data,
    report_type="summary",
    date_range=None,
    filters=None,
    grouping=None,
    include_charts=False,
    output_format="pdf"
):

    validate_inputs(sales_data, report_type, output_format)

    sales_data = filter_by_date_range(sales_data, date_range)
    sales_data = apply_filters(sales_data, filters)

    if not sales_data:
        return handle_empty_data(report_type, output_format)

    summary = calculate_summary_metrics(sales_data)

    grouped_data = None
    if grouping:
        grouped_data = group_sales_data(sales_data, grouping)

    report = build_summary_report(
        summary,
        report_type,
        date_range,
        filters,
        grouped_data,
        grouping
    )

    if report_type == "detailed":
        report["transactions"] = build_detailed_report(sales_data)

    elif report_type == "forecast":
        report["forecast"] = build_forecast_report(sales_data)

    if include_charts:
        report["charts"] = generate_chart_data(
            sales_data,
            grouped_data,
            grouping
        )

    return export_report(
        report,
        output_format,
        include_charts
    )
```



# Tests Performed

The existing unit tests in `test_sales_report.py` should be executed after refactoring.

Example command:

```bash
python -m unittest test_sales_report
```

Expected result:

- All existing tests pass successfully.
- The report output remains identical to the original implementation.
- Refactoring only changes the internal structure, not the functionality.



# Benefits of the Refactoring
The refactored version provides several improvements.

- Smaller and easier-to-read functions.
- Better separation of responsibilities.
- Simpler debugging because each helper function performs one task.
- Improved code reuse.
- Easier unit testing of individual functions.
- Easier future maintenance and extension.
- Better compliance with the Single Responsibility Principle.


# Reflection Questions

## 1. How did breaking down the function improve its readability and maintainability?
Breaking the function into smaller helper functions made the overall workflow much easier to understand. Each helper function performs one specific responsibility, making the code easier to read, debug, maintain, and test independently. The main function now clearly shows the overall process without exposing implementation details.


## 2. What was the most challenging part of decomposing the function?
The biggest challenge was identifying the logical boundaries between responsibilities. Some sections, such as grouping, forecasting, and chart generation, share related data, so care must be taken to separate them without changing the original behaviour.


## 3. Which extracted function would be most reusable in other contexts?
The following helper functions are highly reusable:

- `validate_inputs()`
- `filter_by_date_range()`
- `apply_filters()`
- `calculate_summary_metrics()`
- `group_sales_data()`

These functions could easily be reused in other reporting or analytics applications because they perform generic data-processing tasks rather than report-specific logic.



# Overall Learning
This demonstrated how AI can help identify opportunities for refactoring large functions into smaller, focused helper functions. Applying the Single Responsibility Principle improves rea ability, maintainability, and testability while preserving the original functionality. It also reinforced the importance of running automated tests after refactoring to ensure that no existing behaviour has changed.
