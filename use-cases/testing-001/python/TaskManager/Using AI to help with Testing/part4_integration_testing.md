# Exercise: Using AI to Help with Testing

# Part 4: Integration Testing
**File Used:** `task_priority.py`

**Functions Tested:**
- `calculate_task_score()`
- `sort_tasks_by_importance()`
- `get_top_priority_tasks()`



# Exercise 4.1: Testing the Full Workflow

## 1. AI Guided Conversation

### AI Question 1

**What scenarios should an integration test verify?**

### My Answer
The integration test should verify that all three functions work together correctly. It should confirm that task scores are calculated correctly, tasks are sorted from highest to lowest priority, and only the requested number of top-priority tasks is returned.


### AI Feedback
Excellent.

An integration test should focus on how the functions interact rather than testing each function individually.


### AI Question 2

**How would you design test data that exercises the entire workflow?**

### My Answer
I would create several tasks with different priorities, due dates, and statuses so that each task receives a different score. This would make it easier to verify that the sorting and selection of top tasks works correctly.


### AI Feedback
Good approach.

Including tasks with different properties helps verify that each scoring rule contributes to the final ordering.


### AI Question 3

**What assertions would verify the correct behaviour?**

### My Answer
I would verify that:
- Each task receives the correct score.
- The tasks are sorted from the highest score to the lowest score.
- The correct number of tasks is returned.
- The highest-priority task appears first in the results.


### AI Feedback
Correct.

Assertions should verify both the calculated results and the overall workflow.


### AI Question 4

**How would you structure the test to make it readable and maintainable?**

### My Answer
I would separate the test into three sections:

1. Arrange – Create the test tasks.
2. Act – Run the workflow.
3. Assert – Verify the results.

This structure makes the test easier to read and maintain.


### AI Feedback
Excellent.

Using the Arrange–Act–Assert pattern is considered good testing practice because it clearly separates setup, execution, and verification.


# 2. Integration Test

```python
from datetime import datetime, timedelta

from models import Task, TaskPriority
from task_priority import (
    calculate_task_score,
    sort_tasks_by_importance,
    get_top_priority_tasks
)

def test_task_priority_workflow():

    # -------------------------
    # Arrange
    # -------------------------

    task1 = Task("Complete Project")
    task1.priority = TaskPriority.URGENT
    task1.updated_at = datetime.now() - timedelta(days=2)

    task2 = Task("Study for Exam")
    task2.priority = TaskPriority.HIGH
    task2.updated_at = datetime.now() - timedelta(days=2)

    task3 = Task("Organize Notes")
    task3.priority = TaskPriority.MEDIUM
    task3.updated_at = datetime.now() - timedelta(days=2)

    tasks = [task3, task1, task2]

    # -------------------------
    # Act
    # -------------------------

    scores = [calculate_task_score(task) for task in tasks]

    sorted_tasks = sort_tasks_by_importance(tasks)

    top_tasks = get_top_priority_tasks(tasks, limit=2)

    # -------------------------
    # Assert
    # -------------------------

    assert len(scores) == 3

    assert sorted_tasks[0] == task1

    assert sorted_tasks[1] == task2

    assert sorted_tasks[2] == task3

    assert len(top_tasks) == 2

    assert top_tasks[0] == task1

    assert top_tasks[1] == task2
```


# 3. Expected Results

| Step | Expected Outcome |
|------|------------------|
| calculate_task_score() | Calculates the correct score for every task |
| sort_tasks_by_importance() | Returns tasks ordered from highest score to lowest score |
| get_top_priority_tasks() | Returns only the specified number of highest-priority tasks |


# 4. Workflow Verification

The integration test verifies the following workflow:

### Step 1

Each task receives an importance score using `calculate_task_score()`.

**Expected Outcome**

Every task has a score based on its priority and other task properties.

### Step 2

The scored tasks are passed to `sort_tasks_by_importance()`.

**Expected Outcome**

Tasks are sorted from the highest score to the lowest score.

### Step 3

The sorted list is passed to `get_top_priority_tasks()`.

**Expected Outcome**

Only the requested number of highest-scoring tasks is returned.


# 5. Assertions Used

1. Verify that scores are calculated for all tasks.
2. Verify that the task with the highest score appears first.
3. Verify that tasks are correctly sorted from highest to lowest score.
4. Verify that only the requested number of tasks is returned.
5. Verify that the returned tasks are the highest-priority tasks.


# 6. Why This Is an Integration Test

This is an integration test because it verifies that multiple functions work together correctly instead of testing each function in isolation.

The test confirms that:

- `calculate_task_score()` correctly calculates task scores.
- `sort_tasks_by_importance()` correctly orders tasks using those scores.
- `get_top_priority_tasks()` correctly selects the highest-priority tasks from the sorted list.

Testing the complete workflow provides confidence that the task prioritization system functions correctly as a whole.


# Summary

This exercise demonstrated how to test the complete task-priority workflow by integrating three related functions. Rather than testing each function individually, the integration test verified that scores were calculated correctly, tasks were sorted in the correct order, and the highest-priority tasks were successfully returned. Following the Arrange–Act–Assert structure made the test easy to read, understand, and maintain while ensuring that the overall workflow behaved as expected.
