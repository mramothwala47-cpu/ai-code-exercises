# Part 1 - Understanding What to Test

**Language Chosen:** Python

**File:** 'task_priority.py'

**Functions Covered:**
- 'calculate_task_score()'
- 'sort_tasks_by_importance()'
- 'get_top_priority()'


# Exercise 1.1: Behaviour Analysis
## 1. Examine the 'calculate_task_score()' Fucntion

The 'calculate_task_score()' function calculates a numerical score for a task. This score determines how important a task is compared to others. The score is inflenced by several factors rather than only the task priority.

The factors include:
- Task priority
- Due date
- Task status
- Task tags
- How recently the task was updated

The higher the score the more improtant the task is considered.


## 2. AI Prompt Used
**Prompt**
```
> I'm learning how to test this function, and I want to understand what behaviors I should test.
>
> Rather than generating tests for me, please:
>
> 1. Ask me questions about what I think this function does.
> 2. After I answer, help identify any behaviors I missed.
> 3. Ask me what edge cases I think should be tested.
> 4. Help me identify additional edge cases I didn't think of.
> 5. Ask me which test I should write first and why.
```


## 3. AI Guided Conversation
### AI Question 1
**What should be tested first?**

### My Answer:
I think the function calculates an overall importance score for a task. It starts with the task's priority and then adjusts the score depending on whether the task is overdue, due soon, completed, under review, contain important tags, or has been updated recently.

### AI Feedback
Good observation.

The function also combines multiple business rules into one final score rather than relying on only one priority. Every rule either increases or decreases the overall score.


### AI Question 2
**Which behaviours do you think should be tested?**

### My Answer
I think these behaviours should be tested:

- Different priority levels shoukd produce different scores.
- Overdue tasks should receive additional points.
- Tasks due today should receive extra points.
- Completed tasks should lodr points.
- Tasks with important tags should receive bonus points.
- Recently updated tasks should receive bonus points.


### AI Feedback
Good job identifying the main behaviours.

One behaviour that was easy to overlook is that tasks with the status **REVIEW** receive a penalty that is smaller than completed tasks. This behavior should be tested.


### AI Question 3
**What edge cases do you thinl should be tested?**

### My Answer
Possible esge cases include:
- A task with no due date.
- A task with no tags.
- A task with Low priority.
- A completed task that is also overdue.
- A task updated a long time ago.

### AI Feedback
Those are good edge cases.

Additional edge cases include:
- A task with an unknown priority value.
- A task due exactly two days from now.
- A task due exactly seven days from now.
- A task containing multiple important tags.
- A task with an empty tag list.


### AI Question 4
**Which test would you write first and why?**

### My Answer
I would first test the priority calculation because it is the foundation of the scoring system. If priority scores are incorrect, every other calculation becomes unreliable.

### AI Feedback 
That is a good choice because priority is the starting poit for every score calculation before addtional rules are applied.


## Test Cases to Write
### Test Case 1
**Purpose**

Verify that each priority level produces the correct base score.

**Expected Result**
- LOW = 10
- MEDIUM = 20
- HIGH = 40
- URGENT = 6

### Test Case 2
**Purpose**

Verify that an overdue task receives an additional 35 points.

**Expected Result**
The calculated score increases by 35 points.

### Test Case 3
**Purpose**

Verify that a completed task loses 50 points.

**Expected Result**
The final score is reduced by 50.

### Test Case 4
**Purpose**

Verify that the tasks containing the tags **blocker**, **critical**, or **urgent** receive an additional 8 points.

**Expected Results**
The score increases by 8.

### Test Case 5
**Purpose**

Verify that tasks updated within the last day receive a bonus.

**Expected Result**
The score increases by 5.

### Test Case 6 (Edge Case)
**Purpose**

Verify that a task with no due date does not receive any due-date bonus.

**Expected Result**
The score depends only on priority, status, tags and update time.

### Test Case 7 (Edge Case)
**Purpose**

Verify that a task due exactly two days from now receives the correct bonus.

**Expected Result**
The score increases by 15.

### Test Case 8 (Edge Case)
**Purpose**

Verify that a task due exactly seven days from now receives the correct bonus.

**Expected Result**
The score increases by 10.



# Exercise 1.2: Test Planning
## 1. Functions Being Tested

The testing plan covers the following functions:

- `calculate_task_score()`
- `sort_tasks_by_importance()`
- `get_top_priority_tasks()`

## 2. AI Guided Planning Conversation
### AI Question 1

**What does `calculate_task_score()` do?**
### My Answer
It calculates an importance score for a task using priority, due date, status, tags and the last updated date.

### AI Feedback
Correct.

This function should primarily be tested using **unit tests** because it performs calculations independently.

### AI Question 2
**How would you test `sort_tasks_by_importance()`?**
### My Answer

I would create several tasks with different scores and verify that they are returned from the highest score to the lowest score.

### AI Feedback
Correct.

Also verify that tasks with identical scores are handled consistently.

### AI Question 3

**How would you test `get_top_priority_tasks()`?**
### My Answer

I would create more tasks than the specified limit and verify that only the highest-scoring tasks are returned.

### AI Feedback
Excellent.

Also test situations where:

- The limit is larger than the number of tasks.
- The task list is empty.

### AI Question 4

**What edge cases should be tested?**
### My Answer

- Empty task list.
- Tasks with identical scores.
- Tasks without due dates.
- Tasks with unknown priorities.
- Limits greater than the task count.

### AI Feedback
Those are appropriate edge cases for these functions.

## 3. Structured Test Plan

| Priority | Function | Test Type | Test Description | Expected Outcome |
|-----------|-----------|-----------|------------------|------------------|
| High | calculate_task_score() | Unit | Verify priority scoring | Correct base score |
| High | calculate_task_score() | Unit | Verify overdue bonus | +35 added |
| High | calculate_task_score() | Unit | Verify completed penalty | -50 applied |
| High | sort_tasks_by_importance() | Unit | Verify tasks are sorted highest to lowest | Correct order returned |
| High | get_top_priority_tasks() | Unit | Verify only top tasks are returned | Correct number returned |
| Medium | calculate_task_score() | Unit | Verify due today bonus | +20 added |
| Medium | calculate_task_score() | Unit | Verify due within two days bonus | +15 added |
| Medium | calculate_task_score() | Unit | Verify due within one week bonus | +10 added |
| Medium | calculate_task_score() | Unit | Verify review penalty | -15 applied |
| Medium | calculate_task_score() | Unit | Verify tag bonus | +8 added |
| Medium | calculate_task_score() | Unit | Verify recent update bonus | +5 added |
| Low | get_top_priority_tasks() | Unit | Empty task list | Empty list returned |
| Low | get_top_priority_tasks() | Unit | Limit greater than task count | All tasks returned |
| Low | sort_tasks_by_importance() | Unit | Tasks with identical scores | Stable sorted output |

### Priority of test cases
**High Priority Tests**
1. Base priority calculation.
2. Overdue task bonus.
3. Completed task penalty.
4. Sorting tasks correctly.
5. Returning only the highest-priority tasks.

**Medium Priority Tests**
1. Due today bonus.
2. Due within teo days bonus.
3. Due within seven days bonus.
4. Review status penealty.
5. Tag bonus.
6. Recently updated bonus.

**Low Priority Tests**
1. Empty task list.
2. Tasks with identical scores.
3. Limit larger than the available tasks.
4. Tasks without due dates.

### Test Dependencies

#### Unit Tests
These tests can be executed independently because each function performs a specific tasks.

Functions:
- `calculate_task_score()`
- `sort_tasks_by_importance()`
- `get_top_priority_tasks()`

#### Integration Tests
Integration testing should verify that:
1. `calculate_task_score()` calculates accurate scores.
2. `sort_tasks_by importance()` correctly prders tasks using those scores.
3. `get_top_priority_tasks()` returns the correct number of highest-scoring tasks.

### Expected Outcomes
| Test | Expected Outcome |
|------|------------------|
| Priority calculation | Correct score for each priority level |
| Due date bonuses | Appropriate bonus added |
| Completed task | Score reduced by 50 |
| Review task | Score reduced by 15 |
| Tag bonus | Score increased by 8 |
| Recent update | Score increased by 5 |
| Sorting | Tasks ordered from highest score to lowest score |
| Top priority tasks | Correct number of highest-scoring tasks returned |
| Empty list | Empty list returned without errors |
| Large limit | All available tasks returned |


