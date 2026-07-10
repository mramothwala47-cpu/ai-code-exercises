# Exercise Part 2 - Deepen Understanding Through Guided QUestions

**Task Priorization System**

# 1. Initial Understanding
Before examining the code in detail, my understanding was:
- Each task has a priority level.
- The priority is selected what creating a task.
- Priority can be updated after the task has been created.
- Tasks can also be filtere by priority when listing them.

I expected the priority values to simply be stored as numbers.

# 2. Prompt Used
My approach so far:
- I have searched for keywords like "priority", "TaskPriority", "update_task_priority", and "get_tasks_by_priority".
- I looked in cli.py, task_manager.py, models.py, and storage.py.
- I think the feature is handled by the CLI, business logic, date model, and storage components.

Project Structure:
TaskManager/
- cli.py
- task_manager.py
- models.py
- storage.py
- tests/
- README.md

 Based on my research, these files appear relevant:
 - cli.py
 - task_manager.py
 - models.py
 - storage.py

Can you help me:
1. Evaluate my search approach and suggest improvements.
2. Identify which files contain the prioritization feature.
3. Suggest better search terms.
4. Explain how the feature us divided across the codebase.
5. Recommend a step-by-step investigation process.

AI Guided Questions:
After using the prompt, the AI suggested the following questions to guide my investigation:
## 1. Where is task priority first defined?
I found that the task task priority is defined in **models,py** using the 'TaskPriority' enum

'''python
class TaskPriority(Enum):
    LOW = 1
    MEDIUM = 2
    HIGH = 3
    URGENT = 4
'''

## 2. How does the user choose a priority?
The user specifies the priority through the command line.

```python

create_parser.add_argument(
    "--priority",
    type=int,
    choices=[1,2,3,4](

This ensures only valid priority values can be entered.

## 3. How is the numeric priority converted into a Python object?

Inside 'task_manager.py`, the integer is converted into a `TaskPriority` enum.

```python
priority = TaskPriority(priority_value)
```

---

## 4. Where is the priority stored?
The priority is stored inside the `Task` object.

```python
self.priority = priority
```

## 5. How is the priority updated?

The CLI calls:

```python
update_task_priority()
```

which then updates the task through the storage layer.

```python
return self.storage.update_task(
    task_id,
    priority=new_priority
)
```

## 6. How are tasks filtered by priority?

The filtering happens in `storage.py`.

```python
def get_tasks_by_priority(self, priority):
    return [
        task
        for task in self.tasks.values()
        if task.priority == priority
    ]
```

## 7. How is priority stored and retrieved?

Tasks are stored in **tasks.json**.

Before saving:

- the priority enum is converted into an integer.

When loading:

- the integer is converted back into a `TaskPriority` enum.

# 3. Journal Reflection

## 3.1. Initial Understanding vs What I Discovered
Initially, I believed that task priorities were simply numbers stored with each task.
After exploring the code, I discovered that the application uses the 'TaskPriority' enum to represent priorities internally. Numeric values are only used for user input and JSON storage, while the application itself works with enum objects.

## 3.2. Key Insights the Guided Questions Helped Uncover:
- The prioritization feature is spread across multiple file rather than existing in one location
- The CLI validates user input before passing it to the business logic.
- The "TaskManager" coverts user input into enum object.
- The 'Task' model stores the priority.
- 'TaskStorage' is responsible for saving and loading the priority.
- Custom JSON encoding and decoding preserve enum values when writing to and reading from 'task.json'.

## 3.3. Misconceptions That Were Clarified
I originally thought priorities were stored and used only as integers.

After examining the code, I learned that integers are only used when interacting with the user or storing data in JSON. Inside the application, priorities are represented using the 'TaskPriority' enum, making the code easier to read, safer, and more maintainable.

This conversion is handled by `TaskEncoder' and `TaskDecoder`.

