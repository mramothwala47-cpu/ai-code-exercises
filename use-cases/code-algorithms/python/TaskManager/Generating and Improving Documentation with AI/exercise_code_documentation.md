# 1. Code Documentation Exercise

## Original Code

**File:** `task_manager.py`

```python
def get_statistics(self):
    tasks = self.storage.get_all_tasks()
    total = len(tasks)

    # Count by status
    status_counts = {status.value: 0 for status in TaskStatus}
    for task in tasks:
        status_counts[task.status.value] += 1

    # Count by priority
    priority_counts = {priority.name: 0 for priority in TaskPriority}
    for task in tasks:
        priority_counts[task.priority.name] += 1

    # Count overdue
    overdue_count = len([task for task in tasks if task.is_overdue()])

    # Count completed in last 7 days
    seven_days_ago = datetime.now() - timedelta(days=7)
    completed_recently = len([
        task for task in tasks
        if task.completed_at and task.completed_at >= seven_days_ago
    ])

    return {
        "total": total,
        "by_status": status_counts,
        "by_priority": priority_counts,
        "overdue": overdue_count,
        "completed_last_week": completed_recently
    }
```

# Prompt 1: Comprehensive Function Documentation
## AI Prompt Used
> Please create comprehension code comments for this Python function following Python docstring conventions. The documention should include:
>
> 1. A clear description of what the function does.
> 2. All parameters with types and descriptions.
> 3. Return value with type and description.
> 4. Any exceptions or errors that might be thrown.
> 5. Example usage.
> 6. Any important notes or edge cases developers should be aware of.

## Generated Documentation
```python
def get_statistics(self):
    """
    Generate summary statistics for all stored tasks.

    This method retrieves every task from storage and calculates useful
    statistics, including the total number of tasks, the number of tasks
    grouped by status and priority, the number of overdue tasks, and the
    number of tasks completed within the last seven days.

    Parameters
    ----------
    self : TaskManager
        The current TaskManager instance.

    Returns
    -------
    dict
        A dictionary containing:

        - total (int):
          Total number of tasks.

        - by_status (dict):
          Number of tasks grouped by status.

        - by_priority (dict):
          Number of tasks grouped by priority.

        - overdue (int):
          Number of overdue tasks.

        - completed_last_week (int):
          Number of tasks completed within the previous seven days.

    Raises
    ------
    No exceptions are intentionally raised. However, errors may occur if
    the task storage cannot be accessed or task objects contain invalid data.

    Example
    -------
    >>> manager = TaskManager()
    >>> stats = manager.get_statistics()
    >>> print(stats["total"])

    Notes
    -----
    - Tasks without due dates are never counted as overdue.
    - Only tasks with a completion date within the last seven days are
      included in the completed_last_week count.
    - Statistics always reflect the current state of task storage.
    """
```

# Prompt 2: Intent and Logic Explanation
## AI Prompt Used
> I need help documenting the intent and logic behind this code
### High-Level Purpose
The 'get_statistics()' method provides a summary of all tasks stored in the application. It is intended to give users or developers a quick overview of task activity by calculating totals, grouping tasks according to their status and priority, identifying overdue tasks, and tracking recently completed work.

### Step-bystep Logic
1. Retrieve every stored task.
2. Count the total number of tasks.
3. Create a dictionary to count each task status.
4. Loop through every task and increment its corresponding status count.
5. Create another dictionary to count task priorities.
6. Loop through every task and increment its priority count.
7. Identify overdue tasks by calling each task's 'is_overdue()' method.
8. Calculate the date seven days before today.
9. Count every task completed after that date.
10. Return all calculated statistics inside a single dictionary.

### Assumptions and Edge Cases
- The storage layer successfully returns a list of valid Task objects.
- Every task has a valid status and priority.
- Tasks without due dates are not overdue.
- Tasks that have never been completed are excluded from the recent completion count.
- If there are no tasks, all counts remain zero.

### Suggested Inline Comments

```python
# Retrieve every task from storage.
tasks = self.storage.get_all_tasks()

# Calculate the total number of tasks.
total = len(tasks)
```
# Count tasks grouped by their current status.
# Count tasks grouped by their priority level.
# Count tasks whose due dates have already passed.
# Determined how many tasks were completed during the last seven days.
# Return all calculated statistics in one dictionary.

### Potential Improvements
- Reduce multiple loops by camculating all statistics during a single iteration.
- Add optional filtering by project, tag, or date range.
- Return the statistics as a dedicated Statistics object instead of a dictionary.
- Add type hints for improved readability and IDE support.
- Include percentages alongside raw counts.


# FInal Combined Documentation.
```python
def get_statistics(self):
    """
    Generate summary statistics for every task managed by the TaskManager.

    The method retrieves all tasks from storage and calculates overall
    statistics, including total tasks, counts by status and priority,
    overdue tasks, and tasks completed within the last seven days.

    Returns
    -------
    dict
        Dictionary containing:

        - total (int)
        - by_status (dict[str, int])
        - by_priority (dict[str, int])
        - overdue (int)
        - completed_last_week (int)

    Example
    -------
    >>> manager = TaskManager()
    >>> statistics = manager.get_statistics()

    Notes
    -----
    - Tasks without due dates are excluded from overdue calculations.
    - Only completed tasks with a completion date during the previous
      seven days are included in the completed_last_week count.
    - The method assumes all task objects contain valid status and
      priority values.
    """

    # Retrieve every task from storage.
    tasks = self.storage.get_all_tasks()

    # Count the total number of tasks.
    total = len(tasks)

    # Count tasks grouped by status.

    # Count tasks grouped by priority.

    # Count overdue tasks.

    # Count tasks completed within the last week.

    # Return all statistics as a dictionary.
```

# Reflection
## Which parts of the documentation were most challenging for the AI?
The AI could describe the overall purpose of the function very well, but it could not confidently determine whether the function could raise expectations because that depends on the implementation of the storage layer and task objects. It also could not determine the intended business rules beyond what was visible in the code.

## What additional information did you need to provide in your prompts?
The AI performed better when instructed to follow Python docstring conventions and include parameter descriptions, return values, examples, edge cases, and implementation notes. Providing the complete function rather than a code snippet also improved the quality of the documentation.

## How would you use this approach in your own projects?
I would use AI to generate an initial version of documentation whenever I create new functionx or classes. I would then review the generated documentation to ensure it accurately reflects the code's behavior before committing it to the project. This approach would save time while maintaining consistent, high-quality documentation.
