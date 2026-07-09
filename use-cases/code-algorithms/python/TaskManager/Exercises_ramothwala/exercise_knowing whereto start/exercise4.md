# Exercise 4 - Practical Application

## 1. Planning
### 1.1. Identifying which files I would need to modify.
Based on my understanding of the codebase, I would need to modify the following files:
- 'models.py'
- 'task_manager.py'
- 'storage.py'
- 'cli.py' (if the abandoned status needs to be displayed or managed through a command)
  
### 1.2. Outlining the changes that I would make to implement this rule
The new business rule states:
> **Tasks that are overdue for more than 7 days should be automatically marked as abandoned unless they are marked as high priority.**
To implement this rule, I would:
1. Update the 'Task' class in 'model.py' to support an **ABANDONED** task status.
2. Modify the overdue checking logic so that it determines whether a task has been overdue for more than seven days.
3. Ensure that tasks with a **HIGH** or **URGENT** priority are excluded from being marked as abandoned.
4. Add a method in 'task_manager.py' that checks all tasks and automatically updates qualifying tasks to the **ABANDONED** status.
5. Save the updated task information using the existing functionallity in 'storage.py'.
6. Update 'cli.py' if users need a way to view or manage abandoned tasks.

### 1.3. Questions I would ask my team before implementing.'
Before implementing the feature, I would ask my team:
- Should **URGENT** task also be excluded, or only **HIGH** priority tasks?
- When should the automatic check run (every time the application startys, whenever tasks are listed, or on a schedule?
- Should users be able to restore an abandoned task?
- Should abandoned tasks appear in statistics and reports?
- Should the abandoned status be displayed differently from other task status?

## 2. Reflection

### 2.1. How did AI prompts help understand where and how to implement this feature?
The AI prompts helped me understand the overall structure of the project identifying the responsibilities of each file. They also helped me recognize how the application separates the user interface, business logic, and data stoarge. this made it easier to determine where the new business rule should be implemented without changing unrelated parts of the application.

### 2.2. Aspects of the codebase I am still unsure about.
I am still unsure about:
- The complete flow of the application when it starts.
- Whether there are additional files that interact with the task model.
- How automated testing is implemented in the 'tests' folder.
- Whether there are existing design patterns used throughout the project that I should follow.

### 2.3. The next steps that deepen my understanding
To improve my understanding of the project, I would:
1. Explore the remaining Python files in the project.
2. Review the files in the 'tests' folder to understand how the application is tested.
3. Run the application locally to observe how each command works.
4. Continue using AI to help explain unfamiliar code while verifying my understanding by reading the source code.
