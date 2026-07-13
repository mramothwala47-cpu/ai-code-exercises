# Exercise: README and User Guide Documentation
## Project Information
**Project Name:** Task Management System

**Description**
The Task Management System is a Python command-line application that allows users to create, organize, update, and track tasks. It supports task priorities, due dates, tags, task status management, and statistical reporting.
**Technologies Used**
- Python 3.11+
- Python Standard Library
- JSON for data storage
- argparse
- datetime
- uuid
**Main Project Files**
```
task-manager/
│
├── cli.py
├── task_manager.py
├── models.py
├── storage.py
├── tasks.json
└── tests/
```

# Prompt 1 - README.md
## AI Prompt Used
> Please create a comprehensive README.md file for my Task Management SYstem project.

# Task Management System
A simple command-line task management application built with Python. The application enables users to create, update, organize, and track tasks while storing information in a JSON file.

## Features
- Create new tasks
- Update task status
- Update task priority
- Set due dates
- Add and remove tags
- Delete tasks
- View task details
- List tasks by priority or status
- View overdue tasks
- Generate task statistics

## Requirements
- Python 3.11 or later
No external libraries are required.

## Installation
Clone the repository.

```bash
git clone <repository-url>

cd task-manager
```
No addtiional installation is necessary.

## Running the Application
Create a task.

```bash
python cli.py create "Finish Assignment"
```

List all tasks.
```bash
python cli.py list
```
Show task details.
```bash
python cli.py show <task_id>
```
View statistics.
```bash
python cli.py stats
```

## Project Structure
| File | Purpose |
|-------|----------|
| cli.py | Command-line interface |
| task_manager.py | Business logic |
| models.py | Task model and enums |
| storage.py | JSON storage and persistence |

## Configuration
The application stores tasks inside:
```
tasks.json
```
No additional configuration is required.

## Troubleshooting
### Invalid Date
Use dates in the format:
```
YYYY-MM-DD
```
Example
```
2026-07-15
```

### No Tasks Displayed
ENsure tasks have been created successfully.

Run

```bash
python cli.py list
```

## Contributing
Contributions are welcome.
1. Forsk the repository.
2. Create a feature branch.
3. Commit your changes.
4. Submit a Pull Request.

## License
This project is intended for educational purposes.



# Prompt 2 - Step-by-Step Guide
## AI Prompt Used
> Please create a step-by-by guide explaining how to create and manage a task.

# Step-by-STep Guide
## Creating and Managing Tasks
### Prerequisities
- Python 3.11 installed
- Project cloned locally

## Step 1
Open a terminal inside the project folder

## Step 2
Create a task.
```bash
python cli.py create "Complete AI Exercise"
```

Expected Result

A Task-ID is generated.

## Step 3
View your tasks.
```bash
python cli.py list
```

## Step 4
Update the task status.
```bash
python cli.py status <task_id> done
```

## Step 5
Update the task priority.
```bash
python cli.py priority <task_id> 4
```

## Step 6
Add a tag.
```bash
python cli.py tag <task_id> school
```

## Step 7
View task statistics.
```bash
python cli.py stats
```

## Common Mistakes
- Using an incorrect Task ID.
- Entering dates in the wrong format.
- Selecting an invalid prioriy outside 1-4.


## Troubleshooting
### "Task not found"
Verify the Task ID by running
```bash
python cli.py list
```

### "Invalid date format"
Use

```
YYYY-MM-DD
```

only.



# Prompt 3 - Frequently Asked Questions (FAQ)
## AI Prompt Used
> Please help me create a comprehensive FAQ for the Task Management System.

# Frequently Asked Questions
## What is the Task Management System?
A Python command-line application used to manage perdonal or work tasks.

## How do I create a task?
```bash
python cli.py create "Study Python"
```

## How do I see all tasks?
```bash
python cli.py list
```

## How do i change a task's priority?
```bash
python cli.py priority <task_id> 3
```

## How do I mark a taskas complete?
```bash
python cli.py status <task_id> done
```

## How do I delete a task?
```bash
python cli.py delete <task_id>
```

## How do I add tags?
```bash
python cli.py tag <task_id> urgent
```

## How do I remove a tag?
```bash
python cli.py untag <task_id> urgent
```

## How do I check overdue tasks?
```bash
python cli.py list --overdue
```
## Where are tasks stored?
All task information is stored in the 'task.json' file.

## What should I do if I receive an invalid date error?
Ensure all dates follow the format:
```
YYYY-MM-DD
```

# Reflection
## Which aspects of the project were most challenging to document?
The command-line interface contained many commands with differebt parameters. Ensuring every command was explained clearly while keeping the documentation concise required careful organization.

## How did you adjust your prompts?
I specified that the AI should generate a README, a beginner-friendly user guide, and an FAQ with installation instructions, usage examples, troubleshooting tips, and common questions. This resulted in more complete and structured documentation.

## What did you learn about document structure and organization?
I learned that effective documentation should be organizaed into clear sections,  use headings consistently, include priactical examples, and provide troubleshooting information so users can quickly find what they need.

## How would you incorporate this approach into your workflow?
I would use AI to generate the first draft of project documentation whenever I begin a new project. I would then review and refine the content to ensure it accurately reflects the project's functionality and remains up to date as the project evolves.
