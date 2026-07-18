# Part 3 - Test-Driven Development (Practice)
**File Used:** `task_priority.py`
**Function Modified:** `calculate_task_score()`


# Exercise 3.1: TDD for a New Feature

## 1. New Feature

The new feature to be added is:

> Tasks assigned to the current user should receive an additional **+12** score boost.


## 2. AI Guided Conversation

### AI Question 1

**What do you think the first test should be and why?**

### My Answer
The first test should verify that a task assigned to the current user receives an additional 12 points. I chose this because the new behaviour should be tested before changing the implementation.


### AI Feedback
Good choice.

In Test-Driven Development, the first step is to write a test that describes the new behaviour. The test should fail because the feature has not yet been implemented.

### AI Question 2

**Now that you've written the test, what is the minimum code you would add to make it pass?**

### My Answer
I would add a simple condition that checks whether the task is assigned to the current user. If it is, I would add 12 points to the score.


### AI Feedback
Excellent.

Only add the smallest amount of code required to satisfy the test. Avoid adding additional features at this stage.

### AI Question 3

**Now that the test passes, what test should you write next?**

### My Answer
I would test that tasks not assigned to the current user do not receive the 12-point bonus.

### AI Feedback
Correct.

Testing both positive and negative scenarios helps ensure the new feature behaves correctly.

### AI Question 4

**When should you refactor instead of adding more functionality?**

### My Answer
After all the tests pass and there is duplicated or unnecessary code, I should refactor without changing the behaviour of the program.

### AI Feedback
Correct.

The TDD cycle is:

- Red
- Green
- Refactor

Only refactor after the tests pass.


# 3. Follow the TDD Process

## Step 1 – Write a Failing Test (Red)

```python
from datetime import datetime, timedelta

from models import Task, TaskPriority
from task_priority import calculate_task_score

def test_current_user_receives_bonus():

    task = Task("Complete Assignment")

    task.priority = TaskPriority.MEDIUM

    task.updated_at = datetime.now() - timedelta(days=2)

    # New feature
    task.assigned_to_current_user = True

    score = calculate_task_score(task)

    assert score == 32
```

### Result

❌ Failed

The function does not yet add the +12 score boost.


## Step 2 – Implement the Minimum Code (Green)
The smallest change required is:

```python
if getattr(task, "assigned_to_current_user", False):
    score += 12
```

This code checks whether the task is assigned to the current user.

If it is, the score increases by 12.


## Step 3 – Run the Test Again
### Result

✅ Passed

The new feature now behaves correctly.


## Step 4 – Refactor
No major refactoring is required because the code remains short and readable.

The implementation follows the existing scoring style.

## Step 5 – Write the Next Test
The next test should verify that tasks **not** assigned to the current user do not receive the bonus.

```python
def test_task_not_assigned_to_current_user():

    task = Task("Prepare Presentation")

    task.priority = TaskPriority.MEDIUM

    task.updated_at = datetime.now() - timedelta(days=2)

    task.assigned_to_current_user = False

    score = calculate_task_score(task)

    assert score == 20
```



# Exercise 3.2: TDD for Bug Fix

## 1. Bug Description
The "days since update" calculation is incorrect.

The function should correctly determine how many days have passed since the task was last updated before deciding whether to award the recent-update bonus.


## 2. AI Guided Conversation
### AI Question 1

**What test would you write to reproduce the bug?**

### My Answer
I would create a task that was updated several days ago and verify that it does not receive the +5 recent update bonus.

### AI Feedback
Good.

Your test clearly reproduces the behaviour that needs to be fixed.

### AI Question 2

**Does your test actually demonstrate the bug?**

### My Answer
Yes.

If the calculation is incorrect, the task could incorrectly receive the recent update bonus.

### AI Feedback
Correct.

A good bug test should fail before the code is corrected.

### AI Question 3

**What is the smallest change you can make to fix the problem?**

### My Answer
I would calculate the number of days using the `.days` attribute and then apply the existing comparison.

### AI Feedback
Excellent.

A minimal fix reduces the chance of introducing new bugs.

### AI Question 4

**What additional tests would you add to prevent regression?**

### My Answer
I would add tests for:

- Tasks updated today
- Tasks updated yesterday
- Tasks updated several days ago
- Newly created tasks

### AI Feedback
Excellent.

Regression tests help ensure future changes do not break the corrected behaviour.


# 3. Write a Test That Demonstrates the Bug

```python
from datetime import datetime, timedelta

from models import Task
from task_priority import calculate_task_score

def test_old_task_receives_no_recent_update_bonus():

    task = Task("Finish Report")

    task.updated_at = datetime.now() - timedelta(days=3)

    score = calculate_task_score(task)

    assert score == 20
```

### Result

❌ Failed

The task incorrectly receives the recent update bonus.


# 4. Implement the Bug Fix

The corrected calculation is:

```python
days_since_update = (datetime.now() - task.updated_at).days

if days_since_update < 1:
    score += 5
```


# 5. Run the Test Again

### Result

✅ Passed

The task updated three days ago no longer receives the recent-update bonus.


# 6. Additional Regression Tests

| Test | Expected Result |
|------|------------------|
| Updated today | +5 bonus applied |
| Updated 12 hours ago | +5 bonus applied |
| Updated exactly one day ago | No bonus |
| Updated three days ago | No bonus |
| Updated seven days ago | No bonus |


# Summary
This demonstrated the complete TDD workflow.

For the new feature, I first wrote a failing test, implemented the minimum code needed to make it pass, confirmed that the test succeeded, considered whether refactoring was necessary, and identified the next test to write.

For the bug fix, I created a test that reproduced the issue, implemented the smallest possible correction, reran the test to verify the fix, and planned additional regression tests to ensure the bug does not reappear in future updates.

These exercises reinforced the **Red → Green → Refactor** cycle and highlighted the importance of writing tests before changing the implementation.
