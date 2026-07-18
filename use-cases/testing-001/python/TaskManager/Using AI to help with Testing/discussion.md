# Discussion: Using AI to Help with Testing
**Project:** Python Task Manager


# 1. Test Plan Document (Part 1)

The testing plan focused on the three main functions in `task_priority.py`:

- `calculate_task_score()`
- `sort_tasks_by_importance()`
- `get_top_priority_tasks()`

### High-Priority Tests

- Verify base priority score calculation.
- Verify overdue task bonus.
- Verify completed task penalty.
- Verify tasks are sorted correctly.
- Verify only the highest-priority tasks are returned.

### Medium-Priority Tests

- Verify due today bonus.
- Verify due within two days bonus.
- Verify due within one week bonus.
- Verify review status penalty.
- Verify important tag bonus.
- Verify recently updated task bonus.

### Low-Priority Tests

- Empty task list.
- Tasks with identical scores.
- Limit greater than available tasks.
- Tasks without due dates.

### Types of Tests

- Unit Tests
  - Test each function individually.
  - Verify specific behaviours and edge cases.

- Integration Tests
  - Verify the three functions work correctly together.
  - Confirm the complete task-priority workflow.

### Expected Outcomes

- Correct score calculation.
- Correct task ordering.
- Correct number of top-priority tasks returned.
- Correct handling of edge cases.


# 2. Improved Unit Tests (Part 2)

The original unit tests were intentionally simple and only verified basic functionality.

After receiving AI guidance, the tests were improved by:

- Using more descriptive test names.
- Testing one behaviour at a time.
- Removing unrelated scoring factors.
- Using exact assertions instead of broad comparisons.
- Considering important edge cases.

### Improved Unit Tests Included

- High priority base score test.
- Due today bonus test.
- Additional planned tests for:
  - Overdue tasks.
  - Due within two days.
  - Due within one week.
  - No due date.
  - Important tags.
  - Completed tasks.

These improvements made the tests easier to understand, more reliable, and easier to maintain.


# 3. TDD Implementation and Tests (Part 3)

Two Test-Driven Development exercises were completed.

## New Feature

Feature added:

> Tasks assigned to the current user receive a +12 score boost.

The TDD process followed:

1. Wrote a failing test.
2. Implemented the minimum code required.
3. Confirmed the test passed.
4. Considered whether refactoring was necessary.
5. Planned the next test.


## Bug Fix

Bug addressed:

Incorrect calculation of "days since update."

The TDD process followed:

1. Wrote a failing test that reproduced the bug.
2. Implemented the minimal fix using the `.days` calculation.
3. Confirmed the test passed.
4. Added regression test ideas to prevent the bug from returning.

These exercises demonstrated the **Red → Green → Refactor** workflow.


# 4. Integration Test (Part 4)

The integration test verified that all three functions worked together correctly.

Workflow tested:

1. Calculate task scores using `calculate_task_score()`.
2. Sort tasks using `sort_tasks_by_importance()`.
3. Return the highest-priority tasks using `get_top_priority_tasks()`.

The test confirmed that:

- Scores were calculated correctly.
- Tasks were sorted correctly.
- Only the requested number of highest-priority tasks was returned.
- The overall workflow behaved as expected.


# 5. Reflection

Completing this exercise helped me understand that testing involves much more than simply checking whether code works. I learned that good tests should focus on specific behaviours, use clear assertions, and consider edge cases that might otherwise be overlooked.

Working with AI encouraged me to think through the testing process instead of relying on automatically generated tests. The guided questions helped me identify behaviours to test, plan my testing strategy, and improve the quality of my unit tests.

I also gained a better understanding of Test-Driven Development (TDD). Following the Red–Green–Refactor cycle showed me the importance of writing tests before implementing new features or fixing bugs. This approach helps ensure that new functionality is correctly implemented and reduces the likelihood of introducing errors.

Finally, I learned the difference between unit testing and integration testing. Unit tests verify individual functions in isolation, while integration tests confirm that multiple functions work together correctly as part of a complete workflow.

Overall, this exercise improved my understanding of software testing and demonstrated how AI can be used as a learning tool to strengthen testing skills rather than replace the developer's own thinking and problem-solving abilities.
