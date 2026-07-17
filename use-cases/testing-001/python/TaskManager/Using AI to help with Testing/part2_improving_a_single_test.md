# Part 2 - Improving a Single Test
**Project:** Python Task Manager
**File Used:** `task_priority.py`
**Function Tested:** `calculate_task_score()`

# Exercise 2.1" Writing Your First Test
## 1. Basic Test
The first test is intentionally simple and focuses only on verifying the base priority calculation.
```python
from models import Task, TaskPriority
from task_priority import calculate_task_score

def test_high_priority_task():
    task = Task("Complete Assignment")
    task.priority = TaskPriority.HIGH

    score = calculate_task_score(task)

    assert score >= 40
```

## AI Guided Conversation
### AI Question 1

**What is your test trying to verify?**

### My Answer
The test checks that a task with HIGH priority receives a higher score than lower-priority tasks.

### AI Feedback
Correct.

However, notice that the test only checks that the score is greater than or equal to 40. It does not verify the exact behaviour of the function.

### AI Question 2

**Is your test checking behaviour or implementation details?**

### My Answer
The test is checking behaviour because it verifies the result returned by the function instead of checking how the function calculates the score internally.

### AI Feedback
Correct.

Good tests focus on observable behaviour rather than internal implementation.

### AI Question 3

**How could you make the purpose of the test clearer?**

### My Answer
I could use a more descriptive test name and verify the exact expected score instead of checking that it is simply greater than or equal to 40.

### AI Feedback
Excellent.

Descriptive test names make it easier to understand what is being tested.

### AI Question 4

**Which edge cases might your test be missing?**

### My Answer
The test does not check:

- Due dates
- Completed tasks
- Review status
- Important tags
- Recently updated tasks

### AI Feedback
Correct.

Your current test only verifies one behaviour.

### AI Question 5

**How could your assertions be more precise?**

### My Answer
Instead of checking whether the score is at least 40, I should verify the exact score expected under controlled conditions.

### AI Feedback
Excellent.

Precise assertions make tests more reliable and easier to debug.

# 3. Improved Test
```python
from models import Task, TaskPriority
from task_priority import calculate_task_score
from datetime import timedelta, datetime

def test_high_priority_base_score():
    task = Task("Complete Assignment")
    task.priority = TaskPriority.HIGH

    # Prevent extra score from recent update
    task.updated_at = datetime.now() - timedelta(days=2)

    score = calculate_task_score(task)

    assert score == 40
```

# 4. Improvements Made
### Improvement 1
The test name now clearly explains what behaviour is being tested.

### Improvement 2
The assertion now checks the exact expected score.

### Improvement 3
The updated_at value was changed so the task does not receive the +5 recent update bonus.

### Improvement 4
The test focuses on one behaviour only, making it easier to understand and maintain.



# Exercise 2.2.: Learning From Examples

## 1. Selected Behaviour
The due date calculation was selected for further testing.

## 2. Initial Test Idea (Pseudocode)

```text
Create a HIGH priority task.

Set the due date to today.

Calculate the score.

Check whether the due today bonus was added.
```

## 3. AI Guided Conversation

### AI Question 1

**What makes a good test for due date calculations?**

### AI Explanation
A good test should isolate the due date behaviour from all other scoring rules.

This means controlling:

- Priority
- Status
- Tags
- Updated date

so that only the due date affects the score.

### AI Example

```python
def test_due_today_bonus():
    task = Task("Submit Project")
    task.priority = TaskPriority.MEDIUM

    task.updated_at = datetime.now() - timedelta(days=2)
    task.due_date = datetime.now()

    score = calculate_task_score(task)

    assert score == 40
```

### Why This Example Is Better

- Only one behaviour is tested.
- Other scoring bonuses are removed.
- The expected result is clear.
- The assertion checks the exact score.

### AI Question 2

**How would you improve your original test?**

### My Answer
I would remove any unrelated scoring factors so that only the due date bonus affects the result.

### AI Feedback
Correct.

Good tests should isolate one behaviour whenever possible.

### AI Question 3

**Which edge cases should you also test?**

### My Answer
I should also test:

- Overdue tasks
- Tasks due tomorrow
- Tasks due exactly two days away
- Tasks due exactly seven days away
- Tasks with no due date

### AI Feedback
Excellent.

These edge cases verify every due date rule in the function.

### AI Question 4

**How can your assertions become more precise?**

### My Answer
Instead of checking whether the score increased, I should verify the exact score that should be returned.

### AI Feedback
Correct.

Exact assertions provide stronger confidence that the function behaves correctly.

## 4. Comprehensive Due Date Test

```python
from datetime import datetime, timedelta

from models import Task, TaskPriority
from task_priority import calculate_task_score

def test_due_today_bonus():
    task = Task("Submit Assignment")

    task.priority = TaskPriority.MEDIUM

    # Remove unrelated bonus
    task.updated_at = datetime.now() - timedelta(days=2)

    # Task due today
    task.due_date = datetime.now()

    score = calculate_task_score(task)

    # Base score = 20
    # Due today bonus = 20
    # Total = 40

    assert score == 40
```
