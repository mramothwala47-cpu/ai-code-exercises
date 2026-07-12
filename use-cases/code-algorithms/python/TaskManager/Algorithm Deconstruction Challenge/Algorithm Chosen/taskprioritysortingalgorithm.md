# Prompt 1 - Understand an Algorithm Through Step-by-Step Analysis

## 1. My Current Understanding
### 1.1. What the function is trying to...
I think this algorithm is trying to determine which tasks should be worked on first by assigning each task a numerial score. Instead of only using the taask's priority level, it also considers factors such as due dates, completion status, tags, and when the task was last updated. Tasks with higher scores are considered more important and are displayed first.

### 1.2. The imputs seems to be
**Inputs**
- 'calculate_task_score(task)' accepts one 'Task' object.
- 'sort_tasks_by_importance(tasks)' accepts a list of Task objects.
- 'get_top_priority_tasks(tasks, limit=5)' accepts a list of tasks and an optional limit.
**Returns**
- 'calculate_task_score()' retirns an integer score.
- 'sort_tasks_by_importance()' returns a list of tasks sorted from highest to lowest score.
- 'get_top_priority_task()' returns only the highest-priority tasks according to the specified limit.

### 1.3. I am particularly confused about...
The most confusing part is why different numbers are added or subtracted from the score, such as:
- Why overdue tasks receive **+35**.
- Why completed tasks lose **50 points**.
- Why tags add **8 points**.
- Why recent updates add **5 points**.
At first glance these values seem arbitrary, but they are actually business rules used to influence how important each task becomes.

## 2. Breaking Down the Algorithm into key sections with their purposes.
| Section              | Purpose                                                                                   |
| -------------------- | ----------------------------------------------------------------------------------------- |
| Priority Weights     | Gives every task an initial score based on its priority level.                            |
| Due Date Calculation | Increases the score for tasks that need attention soon or are overdue.                    |
| Status Adjustment    | Lowers the score of completed or review tasks because they need less immediate attention. |
| Tag Check            | Gives extra importance to tasks marked as blocker, critical, or urgent.                   |
| Recent Update Check  | Slightly increases the score for recently modified tasks.                                 |
| Sorting              | Orders tasks from highest score to lowest score.                                          |
| Top Tasks            | Returns only the highest-ranked tasks if needed.                                          |

## 3. Walking through a simple example execution with concrete values
Suppose we have this task:
| Property | Value        |
| -------- | ------------ |
| Priority | HIGH         |
| Due Date | Tomorrow     |
| Status   | TODO         |
| Tags     | ["critical"] |
| Updated  | Today        |

### Step 1: Base Priority
HIGH has a weight of 4
Score = 4 × 10 = 40
Current score:
40
### Step 2: Due Date
The task is due tomorrow.
+15 points
Current score:
55
### Step 3: Status
Status is TODO.
No points are added or removed.
Current score:
55
### Step 4: Tags
The tasks contain the tag **critical**.
+8 points
Current score:
63
### Step 5: Recently Updated
The task was updated today.
+5 points
Final score:
68
### Step 6: Sorting
If another task scored **52**, this task task (68) would appear first because it has the higher importance score.

## 4. Explaing the core technique/pattern being used here
This algorithm uses a **weighted scoring system**.
Instead of checking only one condition (such as priority), it combines several factors into a single score.

The general process is:
```
Task
   │
   ▼
Priority Score
   │
   ▼
Due Date Adjustment
   │
   ▼
Status Adjustment
   │
   ▼
Tag Adjustment
   │
   ▼
Recent Update Adjustment
   │
   ▼
Final Score
   │
   ▼
Sort Highest → Lowest
```

This pattern makes it easy to compare tasks because every task ends with one final score.

## 5. Highlighting any non-obvious optimizations or tricks
### Optimization 1: Calculate each score only once
The algorithm creates this list:
```
task_scores = [(calculate_task_score(task), task) for task in tasks]
```
Instead of recalculating scores every time the tasks are compared during sorting, each, score is calculated once and stored with its task. This improves efficiency.

### Optimization 2: Dictionary Lookup
Instead of writing several 'if' statements for each priority level, the algorith uses a dictionary:

```
priority_weights.get(task.priority, 0)
```

Dictionary lookups are fast and make the code easier to maintain.

### Optimization 3: Python's 'any()' Sunction
Instead of looping manually through every tag, the algorithm uses:

```
any(tag in ["blocker", "critical", "urgent"] for tag in task.tags)
```

This stops checking as soon as it finds a matching tag, avoiding unnecessary work.

### Optimization 4: Reusing Functions
The algorithm is divided into three small functions:
- 'calculate_task_score()'
- 'sort_tasks_by_importance()'
- 'get_top_priority_tasks()'
Each function has one responsibility, making the code easier to understand, test, and reuse.

# Targeted Questions to Test My Understanding
## Underlying Principles
### Question 1
Why does the algorithm use a weighted scoring system instead of sorting only by task priority?

## Edge Cases
### Question 2
What score adjustment happens if a task has **no due sate** and **no special tags**? How would that affect its position in the sorted list?

## Performance Characteristics
### Question 3
Why does the algorith calculate every task's score before sorting instead of calling 'calculate_task_score()' repeatedly during the sort? How does this improve performance?



# Prompt 2 - Decipher Code with Unclear Intent or Poor Documentation
## This code appears in...
This code appears in the task management application where tasks need to be ranked according to their importance. It is likely used before displaying tasks to users so that the most important ones appear first.
## It seems to be called when...
- The application needs to sort a list of tasks.
- The application needs to display the highest-priority tasks.
- The application needs to determine which task require immediate attention.
## The variable names suggest it might be...
The names suggest that the algorithm calculates an overall importance score for each task rather than relying on priority alone. It combines several factors into one value and then sorts tasks based on that score.

# 1. Suggesting Better Names for Functions and Variables
| Current Name           | Suggested Name               | Reason                                                                            |
| ---------------------- | ---------------------------- | --------------------------------------------------------------------------------- |
| `calculate_task_score` | `calculate_importance_score` | Makes it clearer that the score represents overall importance, not just priority. |
| `score`                | `importance_score`           | More descriptive of what the value represents.                                    |
| `priority_weights`     | `priority_score_weights`     | Indicates these values contribute to the final score.                             |
| `task_scores`          | `scored_tasks`               | Better describes a list of tasks paired with scores.                              |
| `sorted_tasks`         | `ranked_tasks`               | Shows that tasks are ranked by importance.                                        |
| `limit`                | `maximum_tasks`              | Makes the parameter's purpose clearer.                                            |
| `days_until_due`       | `remaining_days`             | Easier to understand at a glance.                                                 |

# 2. Programming Patterns and Techniques Used
## Weighted Scoring
The algorithm combines multiple task attributes into one numerical score. This makes it easy to compare tasks objectively.

## Separated of Responsibilities
The algorithm is divided into three functions:
- `calculate_task_score()` calculates the score.
- `sort_tasks_by_importance()` sorts the tasks.
- `get_top_priority_tasks()` returns only the requested number of tasks.

Each function performs one specific responsibility.

## Dictionary Lookup
Instead of several 'if' statements, a dictionary stores the priority weights.

```python
priority_weights.get(task.priority, 0)
```
This makes the code easier to maintain and read.

## List Comprehension
The algorithm creates a list containing both scores and tasks.

```python
task_scores = [(calculate_task_score(task), task) for task in tasks]
```

## Built-in Python Functions

The algorith uses:
- 'sorted()' for sorting.
- 'any()' for checking whether a task contains important tags.
- '.get()' for safely retrieving dictionary values.

# 3. Pseudocode Showing the Underlying Intent
For every task

    Start with a score of zero

    Add points based on priority

    If the task has a due date
        Add more points if it is overdue
        Otherwise add points if it is due soon

    If the task is completed
        Subtract many points

    If the task is in review
        Subtract some points

    If the task has important tags
        Add extra points

    If the task was updated recently
        Add a small bonus

Return the final score

Repeat this for every task

Sort all tasks from highest score to lowest score

Return the sorted list

If only the top tasks are needed
    Return the first N tasks
This pseudocode focuses on the logic without Python syntax, amking the algorithm earier to understand.

# 4. Drafting Documentation comments that would make this code understandable
```python
def calculate_task_score(task):
    """
    Calculates an overall importance score for a task.

    The score is determined using:
    - Task priority
    - Due date urgency
    - Task status
    - Important tags
    - Recent activity

    Higher scores indicate tasks that should receive attention first.
    """
```

```python
def sort_tasks_by_importance(tasks):
    """
    Calculates an importance score for every task and
    returns the tasks sorted from highest to lowest score.
    """
```

```python
def get_top_priority_tasks(tasks, limit=5):
    """
    Returns the highest-ranked tasks.

    By default, the function returns the top five tasks,
    but a different limit can be specified.
    """
```
# Questions to validate My Understanding
1. If I removed the due date calculations, how would the order of tasks change?
2. Why are completed tasks given a large negative score instead of simply being removed from the list?
3. If two tasks have the same priority, what other factor determine which task appears first?
4. Where else in the application is 'calulate_task_score()' called, and does its behavior match my understanding of its purpose?

# Small, Safe Experiments to Verify the Behavior
## Experiment 1: Change the Priority
Create two identical tasks, but assign one a **LOW** priority and the other an **URGENT** priority. Check whether the urgent task receives a higher score and appears first.
## Experiment 2: Change the Due Date
Keep every property the same except the due date. Compare a task due next week with one that is already overdue and observe how the scores change.
# Experiment 3: Change the Status
Change a task's status from **TODO** to **DONE** and verify that its scores decreases significantly and that it moves lower in the sorted list.
# Experiment 4: Add and Remove Tags
Create two identical tasks. Add the **critical** tag to one of them and compare their scores to confirm that important tags increase the task's rankung.



# Prompt 3: Understand Complex Logic and Control Flow
The algorithm begins by assigning a base score according to the task's priority.

# I am particularly unsure about
1. Why overdue tasks receive a much larger score increase than tasks due today or withon the next week.
2. Why completed tasks lose 50 points instead of simply being excluded from the sorted list.
3. How multiple adjustments combine together to produce the final importance score.

# 1. Visual Representative of the Control Flow
```
Start
  │
  ▼
Receive Task
  │
  ▼
Assign Base Score from Priority
  │
  ▼
Does the task have a due date?
 ├── No → Continue
 └── Yes
        │
        ▼
    Is it overdue?
      ├── Yes → +35
      └── No
            │
            ▼
      Due today?
      ├── Yes → +20
      └── No
            │
            ▼
      Due within 2 days?
      ├── Yes → +15
      └── No
            │
            ▼
      Due within 7 days?
      ├── Yes → +10
      └── No → No change
            │
            ▼
Check Task Status
 ├── DONE → -50
 ├── REVIEW → -15
 └── Other → No change
            │
            ▼
Contains important tags?
 ├── Yes → +8
 └── No
            │
            ▼
Recently updated?
 ├── Yes → +5
 └── No
            │
            ▼
Return Final Score
            │
            ▼
Repeat for Every Task
            │
            ▼
Sort Highest Score → Lowest Score
            │
            ▼
Return Top Tasks
```

# 2. Referencing the Code into More Understandable Segments
Instead of viewing the algorithm as one long function, it can be understood as five logical stages.
## Stage 1 - Assign Base Priority
```
Determine the starting score on the task's priority.
```
## Stage 2 - Evaluate Due Date
```
Increase the score if the task is overdue or approaching its due date.
```
## Stage 3 - Evalaute Ststus
```
Reduce the score for tasks that are already completed or currently under reviee.
```
## Stage 4 - Check Special Conditions
```
Increase the score if the task contains important tags or has been updated recently.
```
## Stage 5 - Sort the Tasks
```
Calculate every task's score, sort them from highest to lowest, and return either the full list or only the requested number of tasks.
```

# 3. Key Decision Points and Their Interdependence
## Decision Point 1 - Priority
The priority determines the starting score. Every task begins here before any additional adjustments are made.
## Decision Point 2 - Due Date
The due date modifies the base score. A task that is overdue or due soon becomes more important.
## Decision Point 3 - Status
 The task's status can significantly reduce its importance. Completed tasks receive a large penalty because they no longer require attention.
## Decision Point 4 - Tags
Tasks labelled as **blocker**, or **urgent** receive additional points because these tags indicate higher business importance.
## Decision Point 5 - Recent Updates
Recently updated tasks receive a small bonus, amking active tasks slightly more visible.
## How These Decisions Work Together
Each decision builds on the previous one rather than replacing it. The final score is the conbined result of every applicable adjustment.

# 4. Potential Logic Bugs or Edge Cases
## Edge Case 1 - Missing Due Date
If a task has no due date, no due-date bonus is added. This expected behaviour but means only the remaining factora determine its score.
## Edge Case 2 - Equal Scores
Two different tasks may end up with exectly the same score. The algorithm does not define how ties should be broken, so their final order depends on Python's sorting behaviour.
## Edge Case 3 - Unexpected Priority Values
If an invalid priority is supplied, the dictionary lookup returns '0'. The task still receives a score but starts with no priority contribution.
## Edge Case 4 - Empty Tag List
If a task had no tags, the 'any()' function simply returns 'False', so bo bonus is added

# Exercise to Test My Understanding
## Scenario 1
**Task**
- Priority: URGENT
- Due Date: Yesterday
- Status: TODO
- Tags; '["critical']'
- Updated: Today
### Predict
Before looking at the answer, predict whether this task would receive a very high, medium, or low score.
### What Actually Happens
The task receives:
- Hihj base score from URGENT priority.
- +35 because it is overdue.
- +8 because it has the 'critical' tag.
- +5 because it was updated today.
SInce there are no penalities, this task receives one of the hoghest possible scores and is likely to appear near the top of the sorted list.

## Scenario 2
**Task**
- Priority: HIGH
- Due Date: Tomorrow
- Status: Done
- Tags: None
- Updated: Last Week
### Predict
Would this task appear near the top or near the bottom of the sorted list?
### What Actually Happens
Although the task starts with a high priority and receives adue-date bonus, ut loses 50 points because its status is 'DONE'. This large penalty signficantly lowers its final score, causing it to appear much lower in the sorted list.

## Scenario 3
**Task**
- Priority: LOW
- Due Date: None
- Status: TODO
- Tags: None
- Updated: Two weeks ago
### Predict
How important do you think this task will be compared to the others?
### What Actually Happens
This task receives only the base score from its LOW priority. It gains no additional points because it has no due date, no important tags, and was not updated recently. As a rsult, it is likely to appear the bottom of the sorted list.
