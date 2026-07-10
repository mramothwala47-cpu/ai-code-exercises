# Exercise Part 1 - Understanding a Specific Feature
## Feature Selected
**Task Creation** and **Task Status Updates**

# 1. Identifying the files that are related to Task Creation and Status Updates
The following files(purpose) are involved in creating tasks and updating their status:
- 'cli.py' | accepts user commands and calls the appropriate methods in the 'Task Manager' class.
- 'task_manager.py' | contains the business logic for creating tasks and updating task information.
- 'models.py' | defines the 'Task' object and methods such as 'update()' and ;mark_as_done()'
- 'storage.py' | handles saving, loading, updtating, and retrieving tasks from 'task.json'.

# 2. Relevant Code Snippets into the prompt
### Task Creation ('cli.py.)
'''python
if args.command -- "create":
    tags = [tag.strip() for tag in args.tags.split(",")] if args.tags else []
    task_id = task_manager.create_task(
        args.title,
        args.description,
        args.priority,
        args.due,
        tags
    )
'''

### Task Creation ('task_manager.py)

'''python
def create_task(self, title, description="", priority_value2,
              due_date_str=None, tags=None):
    priority = TaskPriority(priority_value)

  due_date = None
  if due_date_str:
      due_date = datetime.strptime(due_date_str, "%Y-%m-%d")

  task = Task(title, description, priority, due_date, tags)
  task_id = self.storage.add_task(task)
  return task_id
```

### Task Status Update ('cli.py)
```python
elif args.command == "status":
  if task_manager.update_task_status(args.task_id, args.status):
        print(f"Updated task status to {args.status}")
```

### Task Status Update (`task_manager.py`)

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

# 3. Prompt Used to Understand the Features
'''text
I am a junio developer trying to understand how task creation and task status updates work in this Python project.

The files involved appear to be:
- cli.py
- task_manager.py
- models.py
- storage.py

From what I understand:
- cli.py accepts the user's command-line input.
- task_manager.py contains the business logic.
- models.py defines the Task object.
- storage.py stores and retrieves task date.

-----

# 4. Main Components that are involved in the Task Creation and Updates
The feature os implemented using four main componenets.

### 'cli.py'
- Acts as the application's command-line interface.
- Receives user command.
- Passes user input to the 'TaskManager'.

### 'task_manager.py.'
- Contains the application's business logic.
- Creates new 'Task' objects.
- Updates task status, priority, due staes, amd tags.
- Validates user input before interacting with storage.

### 'models.py'
- Defines the 'Task' class
- Stores task attributes such as title, description, priority, status, due date, and tags.
- Includes methods like 'update()' and 'mark_as_done()' to modify task information.

### 'storage.py'
- Stores all tasks.
- Saves tasks to 'tasks.json'.
- Loads tasks from 'task.json'.
- Updates existing task information.

# 5. Execution Flow When a Task is Created or Updated
## Task Creation Flow
1. The user runs a command such as:
'''bash
python cli.py create "Finish Assignment"

2. 'cli,py' reads the command-line arguements.

3. 'cli.py' calls:
'''python
TaskManager.create_task()

4. 'TaskManager':
- Converts the priority value into a 'TaskPriority'.
- Converts the due date into a 'datetime; object.
- Creates a new 'Task' object.

5. The new task is passed to:
'''python
TaskStorage.add_task()

6. 'storage.py' saves the task to 'task.json'.

7. The task ID is returned and displayed to the user

## Task Status Update Flow
1. The user runs:
'''bash
python cli.py status <task_id> done

2. 'cli.py' calls:
'''python
TaskManager.update_task_status()

3. The new status is converted into a 'TaskStatus'.
4. If the status is 'DONE'. and the task's 'mark_as_done()' method is called.
5. If the staus is another value, the task is updated using:
'''python
storage.update_task()

6. The updated task is saved to 'tasks.json'

# 6. How rhe data is stored and retrieved
The application stores task information in a JSON file named:
- tasks.json

### Storing Data
- New tasks are added using 'add_task()'.
- Updated tasks are saved using 'save()'.
- The 'TaskEncoder' converts Python objects into JSON format before saving.

### Retrieving Data
- WHen the application starts, 'load()' reads the contents of 'task.json'.
- The 'TaskDecoder' converts the JSON data back into 'Task' objects.
- Tasks are then available for listing, updating, or deleting.
This allows task information to persist even after the application is closed.

# 7. Interesting Design Patterns Discovered
### Separation of Concerns

Each file has a specifc responsibility:
- 'cli.py' handles user interaction.
- 'task_manager.py' manages business logic.
- 'models.py'handles data persistence.
This separation makes the code easier to maintain and extend.

### Layered Architecture
The application follows a layered struture:

User
   │
   ▼
cli.py
   │
   ▼
task_manager.py
   │
   ▼
storage.py
   │
   ▼
tasks.json

Each layer communicates with the next layer, keeping responsibilities clearly separated.

### Object-Oriented Programming (OOP)

The application uses a "Task` class to represent tasks.

Methods such as "update()' and `mark_as_done()' keep task-related behaviour inside the class, improving code organization and readability.

# Summary

The task creation and status update features involve four key files: `cli.py`, `task_manager.py`, `models.py`, and `storage.py`. User commands are received by the CLI, processed by the `TaskManager`, represented as `Task` objects, and stored in `tasks.json` by the storage layer. The project follows good software engineering practices such as Separation of Concerns, Layered Architecture, and Object-Oriented Programming, making the code modular, maintainable, and easy to understand.
---

