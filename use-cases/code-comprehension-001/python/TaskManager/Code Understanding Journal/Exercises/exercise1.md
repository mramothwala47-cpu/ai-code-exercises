# Exercise Part 1 - Understanding a Specific Feature

**Task Creation** and **Task Status Updates**

# 1. Files related to Task Creation and Status Updates
The following files(purpose) are involved in creating tasks and updating their status:
- 'cli.py' | Handles user input from the command line and routes commands to the 'Taskmanager'.
- 'task_manager.py' | Contains the business logic for creating tasks and updating task status.
- 'models.py' | Defines the 'Task'class and task-related methods such as 'update()' and 'mark_as_done()' 
- 'storage.py' | handles saving, loading, updtating, and retrieving tasks from persistent storage ('tasks.json).

# 2. Relevant Code Snippets into the prompt
## Snippet 1 - Task Creation ('cli.py')
```python
if args.command == "create":
    tags = [tag.strip() for tag in args.tags.split(",")] if args.tags else []
    task_id = task_manager.create_task(
        args.title,
        args.description,
        args.priority,
        args.due,
        tags
    )
```

## Snippet 2 - Task Creation ('task_manager.py)
```python
def create_task(self, title, description="", priority_value=2,
               due_date_str=None, tags=None):
    priority = TaskPriority(priority_value)

    due_date = None
    if due_date_str:
        try:
            due_date = datetime.strptime(due_date_str, "%Y-%m-%d")
        except ValueError:
            print("Invalid date format.")
            return None

    task = Task(title, description, priority, due_date, tags)
    task_id = self.storage.add_task(task)
    return task_id
```

## Snippet 3 - Task Status Update ('task_manager.py')
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

# 3. Prompt Used
AI Explanation

This feature seems to handle creating new tasks, updating existing task statuses, and saving those changes.

Here are the key files that appear to be involved:
1. cli.py - Seems to receive user commands and call the TaskManager.
2. task_manager.py - Might be handling the business logic creating and updating tasks.
3. models.py - Contains the Task class and methods that manage task state.
4. storage.py - Handles storing and retrieving task data.

Here are the code snippets from parts I'm struggling to understand:
## Snippet 1 - Task Creation ('cli.py')
```python
if args.command == "create":
    tags = [tag.strip() for tag in args.tags.split(",")] if args.tags else []
    task_id = task_manager.create_task(
        args.title,
        args.description,
        args.priority,
        args.due,
        tags
    )
```

## Snippet 2 - Task Creation ('task_manager.py)
```python
def create_task(self, title, description="", priority_value=2,
               due_date_str=None, tags=None):
    priority = TaskPriority(priority_value)

    due_date = None
    if due_date_str:
        try:
            due_date = datetime.strptime(due_date_str, "%Y-%m-%d")
        except ValueError:
            print("Invalid date format.")
            return None

    task = Task(title, description, priority, due_date, tags)
    task_id = self.storage.add_task(task)
    return task_id
```

## Snippet 3 - Task Status Update ('task_manager.py')
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

Could you:
1. Explain in simple terms what this component actually does.
2. Walk me through the execution flow when a task is created or updated.
3. Clarify how these files interact with each other.
4. Identify any external dependencies or services this component relies on.
5. Explain any complex code blocks.
6. Provide a mental model I can use to think about this component.

i'm particularly confused about how data moves between the different files and when tasks are saved, so extra detail there would help.

Finaly, suggest three small code changes  could make to validate my understanding. Please give only the requirements and not the implementation.

# 4. Code Understanding Journal
## 4.1. Main Components Involved in Task Creation and Updates

The task creation and status update features involve four main components
- **'cli.py'** - Accecpts user commands and passes them to the 'TaskManager'.
- **'task_manager.py'** - Implements the business logic for creating and updating tasks.
- **'models.py'** - Defines the 'Task' class and methods that modify a task's state.
- **'storage.py'** - Saves, loads, updates, and retrieves tasks from 'tasks.json'.

## 4.2. Execution Flow When a Task Is Created or Updated
### Task Creation
1. The user enters a 'create' command in the terminal.
2. 'cli.py' reads the command-line arguments.
3. 'TaskManager.create_task()' validates the input and creates a 'Task' object.
4. The task is passed to 'TaskStorage.add_task()'.
5. 'storage.py' saves the task to 'tasks.json'.
6. The task ID is returned to the user.

### Task Status Update
1. The user enters a 'status' command.
2. 'cli.py' calls 'TaskManager.update_task_status()'.
3. The task status is updated.
4. If the new status is 'DONE', the'mark_as_done()' method records the completion date and time.
5. The updated task is saved to 'tasks.json'.

### 4.3. How Data Is Stored and Retrieved
The application stores tasks in a JSON file named 'tasks.json'.
- New tasks are saved using 'TaskStorage.add_task()'.
- Updates are written using 'TaskStorage,save()'.
- 'TaskEncoder' converts Python objects into JSON before saving.
- 'TaskStorage.load()' reads the JSON file when the application starts.
- 'TaskDecoder' converts the JSON data back into 'Task' objects.

### 4.4. Interesting Design Patterns Discovered
#### Separation of Concerns
Each file has a single responsibility:
- 'cli.py' handles user interaction.
- 'task_manager.py' contains business logic.
- 'models.py' defines the application's data model.
- 'storage.py' manages data persistences.

#### Layered Architecture
The application follows a layered structure:
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
``'

#### Object-Oriented Programming (OOP)
The `Task` class groups task data and related behaviour together. Methods such as `update()` and `mark_as_done()` allow the object to manage its own state, making the code easier to understand and maintain.
