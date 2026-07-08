# Exercise 3 - Understanding Domain Model
## 1. Extract Domain Model

### 1.1. Identifying the core entity classes
The main entity classes I identified are:
- **Task** - Represent an indiviual task in the Task Manager
- **TaskStatus** - An enumeration (Enum) that defines the possible states of a task.
- **TaskPriotity** - An enumeration (Enum) that defines the priority level of a task.

### 1.2. Looking for Business Logic related to task
The 'Task' class contains business logic that allows the application to:
- Create a new task.
- Update task information.
- Mark a task as completed.
- Check whether a task is overdue.

### 1.3. Any terminology or concepts that seem specific to this application
The application uses the following domain-specific terms:
- Task
- Task Status
- Task Priority
- Due Date
- Tags
- Completed At
- Overdue

## 2. Form Initial Understanding
### 2.1. Simple diagram of how I think the entities relate
                Task
                  |
      -------------------------
      |                       |
TaskStatus              TaskPriority
(TODO,                 (LOW,
IN_PROGRESS,           MEDIUM,
REVIEW,                HIGH,
DONE)                  URGENT)

### 2.2. Brief explanation of what I think each entity represents
**Task** - Represents a task created by the user. Each task has a tile, description, priority, status, due date, tags, and timestamps.
**TaskStatus** - Represents the current progress of a task. A task can be Todo, In Progress, Review, or Done.
**TaskPriority** - Represents how important a task is. A task can have a Low, Medium, High, or Urgent priority.

### 2.3. QUestions or confusion I have about the business logic.
- Why is every new task automatically assigned the **TODO** status?
- Why are **TaskStatus** and **TaskPriority** implemented as Enums instead of normal variables?
- How are overdue Tasks displayed to the user?

## 3. Apply the Domain Understanding Prompt

I would like you to act as a senior developer who deeply understands our codebase's domain model. I am a junior developer trying to make sense of the business logic and domain concepts in this application.
Here's what I have found in the codebase:
- 'Task'
- 'TaskStatus'
- 'TaskPriority'

Based on this code, my current understanding is:
- The system seems to be modelling a Task Manager application.
- I think 'Task' is related to both 'TaskStatus' and "TaskPriority' because every task has a status and a priority.
- The 'mark_as_done()' method appears to update the task when it has been completed.
- I am comfused about why 'TaskStatus' and 'TaskPriority' are implemented as Enums.

Could I:
1. Validate my understanding and correct any misconceptions?
2. Help me recognize the core domain concepts?
3. Explain the relationship between these entities in business terms?
4. Clarify any domain-specific terminology?
5. Connect these models to the application's features?

## 4. Test Your Knowledge
### 4.1. AI Questions
1. What is the purpose of the 'Task' entity?
- The 'task' entity represents an individual task and stores all information about that task, including its title, status, priority, due date, and tags.
2. Why does a task use 'TaskStatus'?
- 'TaskStatus' keeps track of the current progress of a task, such as Todo, In Progress, Review, or Done.
3. Why does a task use 'TaskPriority'?
- 'TaskPriority' indicates how important a task is and helps users organize their work based on urgency.
4. WHat happens when 'mark_as_done()' is called?
- The task status changes to **Done**, the completion date is recorded, and the updated time is refresded.
5. What makes a task overdue?
- A task is overdue when its due date has passed and its status is not **DONE**.

### 4.2. Revise the Entity Diagram Based on New Understanding
                   Task
-------------------------------------------------
ID
Title
Description
Status -----------------> TaskStatus
Priority ---------------> TaskPriority
Due Date
Created At
Updated At
Completed At
Tags

TaskStatus
-----------
TODO
IN_PROGRESS
REVIEW
DONE

TaskPriority
-------------
LOW
MEDIUM
HIGH
URGENT

### 4.3. Create a Glossary of Domain Terms Used in the Application
1. Task | A piece of work that the user wants to manage.
2. TaskStatus | The current stage of a task (Todo, In Progress, Review, Done).
3. TaskPriority | The importance level of a task (Low, Medium, High, Urgent).
4. Due Date | Teh date by which a task should be completed.
5. Tags | Labels used to organize tasks into categories.
6. Created At | The date and time when the task was created.
7. Updated At | The date and time when the task was last modified.
8. Completed At | The date and time when the task was marked as completed.
9. Overdue | A task whose due date has passed but has not been completed.
