# Exercise Part 2 - Deepen Understanding Through Guided Questions

**Task Priorization System**

# 1. Initial Understanding of the Task Prioritization System
I explored how task priorities are implemented in the Task Manager application
From my initial review, I understood that task priorities are represented using the 'TaskPriority' enum in 'models.py'. The application supports four priority levels.

- LOW (1)
- MEDIUM (2)
- HIGH (3)
- URGENT (4)
When a user creates a task through the CLI, they provide a priority value, which is passed to the 'TaskManager'. The 'TaskManager' converts this value into a 'TaskPriority' enum before creating the task. The priority is then stored as part of the 'Task' object and saved to 'tasks.json'.

The main files involved appear to be:
- 'cli.py'
- 'task_manager.py'
- 'models.py'
- 'storage.py'

I believe the code works by receiving the user's priority value, validating it, converting it into an enum, and saving it with the task. When tasks are loaded again, the priority is converted back into a 'TaskPriority' enum.

# 2. Guided Questions
## Question 1
Where in the application is the user's numeric priority converted into a 'TaskPriority' enum, and why do you think this conversion happens there instead of in the CLI?

## Question 2
Trace the priority value from the moment the user enters it until it is written to `tasks.json`.
Which methods and files are involved?

## Question 3
Look at the `TaskEncoder'  and `TaskDecoder` classes in `storage.py`.
How is the priority converted when saving tasks, and how is it restored when tasks are loaded?

## Question 4
What happens if a user enters an invalid priority value?
Which part of the application prevents invalid data from being stored?

## Question 5
If you wanted to add a new priority level called **CRITICAL**, which files would need to be updated?

---

# 3. Answers After Exploring the Code
## Answer 1
The priority is converted into a `TaskPriority` enum inside the `create_task()` method in `task_manager.py` using:
```python
priority = TaskPriority(priority_value)
```
Keeping this conversion in the business logic allows the `TaskManager` to validate and process data consistently, regardless of where the input comes from.
---

## Answer 2
The priority moves through the application in the following order:
'''
User Input
      │
      ▼
cli.py
      │
      ▼
TaskManager.create_task()
      │
      ▼
Task()
      │
      ▼
TaskStorage.add_task()
      │
      ▼
tasks.json
``'
Each layer has a specific responsibility, which makes the application easier to maintain.

## Answer 3
When saving tasks, the `TaskEncoder` converts the enum into its numeric value before writing it to JSON.
When loading tasks, the `TaskDecoder` reads the numeric value from `tasks.json` and converts it back into a `TaskPriority` enum.
This allows the application to use enums internally while storing simple values in the JSON file.

## Answer 4
The CLI only accepts values from 1 to 4 by defining valid choices for the priority argument.
In addition, `TaskManager` converts the value into a `TaskPriority` enum. If an invalid value somehow reaches this point, it will not be accepted as a valid enum value, preventing incorrect data from being stored.

## Answer 5
Adding a new priority level would require changes to:
- `models.py` to define the new enum value.
- `cli.py` to allow users to select the new priority.
- `cli.py` to update the priority display symbols.
- Any logic that filters or displays priorities if necessary.

# 4. Code Understanding Journal
## 4.1. Initial Understanding vs. What I discovered.
Initially, i thought task priorities were simply integers that were passed throughout the application. After examining the code more closely, I discovered that the applicationconverts these integers into 'TaskPriority' enums before storing them in the 'Task' object. The enum is only converted back into an integer when the task is saved to 'task.json'.
The storage layer would continue to function because it already supports encoding and decoding enum values.

## 4.2. Key Insights the Guided Questions Helped Me Uncover
- The 'TaskManager' is responsible for converting and validating priority values.
- The application separates user input , business logic, data models, and storage into different modules.
- 'TaskEncoder' and 'TaskDecoder' manage the conversion between Python objects and JSON data.
- The layered design makes the code easier to understand and maintain.

## 4.3. Misconceptions That Were Clarified
I originally believed that the priority remained an integer throughout the application. I learned that it is actually stored as a 'TaskPriority' enum while the application is running.
I also assumed that validation occurred only in the CLI. After exploring the code , I found that the 'TaskManager' also validates the priority by converting it into a 'TaskPriority' enum before creating a task.
