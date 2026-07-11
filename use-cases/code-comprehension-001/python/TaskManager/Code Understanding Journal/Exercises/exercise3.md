# Exercise Part 3 - Mapping Data Flow and State Management

# 1. Entry Points and Components Involved.
When a task is marked as complete, the following files and components are involved:
- 'cli.py' | Receives the user's command to update a task's status.
- 'task_manager.py' | Processes the request and applies the business logic for marking a task as complete.
- 'models.py' | Contains the 'Task' class and the 'mark_as_done()' method that chnages the task's state.
- 'storage.py' | Saves the updated task to persistent storage ('task.json').

# 2. Code Handling State Changes
## Snippet 1 - User Input ('cli.py')
```python
elif args.command == "status":
    if task_manager.update_task_status(args.task_id, args.status):
        print(f"Updated task status to {args.status}")
```

## Snippet 2 - Business Logic ('task_manager.py')

```python
def update_task_status(self, task_id, new_status_value):
    new_status = TaskStatus(new_status_value)

    if new_status == TaskStatus.DONE:
        task = self.storage.get_task(task_id)
        if task:
            task.mark_as_done()
            self.storage.save()
            return True
    else:
        return self.storage.update_task(task_id, status=new_status)
```

## Snippet 3 - State Change ('models.py')
```python
def mark_as_done(self):
    self.status = TaskStatus.DONE
    self.completed_at = datetime.now()
    self.updated_at = self.completed_at
```

## Snippet 4 - Persisting Changes ('storage.py)
```python
def save(self):
    with open(self.storage_path, "w") as f:
        json.dump(list(self.tasks.values()), f, cls=TaskEncoder, indent=2)
```

# 3. Prompt Used
Here iss what I know so far:
- The feature starts when a user enters the 'status' command in the command-line interface (CLI) to mark a task as complete.
- It seems to involve these components/files:
  1. 'cli.py' - Receives the user's command and passes it to the 'TaskManager'.
  2. 'task_manager.py' - handles the business logic for updating the task's status.
  3. 'models.py' - contains the 'Task' class and the 'mark_as_done()' method that updates the task's state.
  4. 'storage.py' - saves the updated task to 'tak.json'.

Here are key code snippets that show data handling:
### First Snippet - User Input ('cli.py')
```python
elif args.command == "status":
    if task_manager.update_task_status(args.task_id, args.status):
        print(f"Updated task status to {args.status}")
```

### Second Snippet - Data Processing ('task_manager.py')
```python
def update_task_status(self, task_id, new_status_value):
    new_status = TaskStatus(new_status_value)

    if new_status == TaskStatus.DONE:
        task = self.storage.get_task(task_id)
        if task:
            task.mark_as_done()
            self.storage.save()
            return True
    else:
        return self.storage.update_task(task_id, status=new_status)
```

### Third Snippet - State Change ('models.py')
```python
def mark_as_done(self):
    self.status = TaskStatus.DONE
    self.completed_at = datetime.now()
    self.updated_at = self.completed_at
```

# 4. Code Understanding Journal
## 4.1. Data Flow Diagram
User
  │
  ▼
CLI Command
(status <task_id> done)
  │
  ▼
cli.py
  │
  ▼
TaskManager.update_task_status()
  │
  ▼
Retrieve Task from Storage
  │
  ▼
Task.mark_as_done()
  │
  ▼
Update Task State
(status, completed_at, updated_at)
  │
  ▼
TaskStorage.save()
  │
  ▼
tasks.json

## 4.2. State Changes During Task Completion 
When a task is marked as complete, several state changes occur:
- The task status changes from its current value to 'DONE'.
- The 'completed_at' field is set to the current date and time.
- The 'updated_at' field is updated to reflect the modification time.
- The modified task is written back to 'task.json', ensuring the changes persist after the application closes.

## 4.3. Potential Points of Failure
Several issues could prevent a task from being marked as completed:
= The task ID provided by the user does not exist.
- An invalid status value is supplied.
- The task cannot be retrieved from storage.
- An error occurs while saving data to 'task.json', such as insufficient file permissions or disk write errors.
- The JSON file becomes corrupted, preventing tasks from loading correctly.

## 4.4. How the Application Persists Changes
The application stores all task information in a JSON file called 'tasks.json'.

When a task is updated:
1. The task object is modified in memory.
2. 'TaskStorage.save()', sarializes all task objects using 'TaskEncoder'.
3. Enums and 'datetime' objects are converted into JSON-compatible value.
4. The updated list of tasks is written back to 'tasks.json'.

When the application starts again:
- 'TaskStorage.load()` reads the JSON file.
- 'TaskDecoder` reconstructs each `Task` object.
- Enum values and dates are converted back into Python objects, restoring the application's state.
  
# Summary

Tracing the task completion feature showed how data flows through each layer of the application. The process begins with a user command in `cli.py`, moves through the business logic in `task_manager.py`, updates the task's state in `models.py`, and is finally persisted by `storage.py` in `tasks.json`.

This exploration highlighted the benefits of separating responsibilities across different modules. It also demonstrated how state changes are managed consistently and how persistent storage allows completed tasks to remain available between application sessions.
