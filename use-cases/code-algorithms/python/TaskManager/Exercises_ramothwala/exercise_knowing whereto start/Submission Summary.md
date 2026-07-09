# Submission Summary

## 1. Initial vs. Final Understanding
At first, i only knew that the project was a python Task Manager application. i was unfamiliar with the project structure, the purpose of the different files, and how the application stored and managed tasks.
I now understand that the project follows a modular structure:
- models.py defines the Task entity and related enums.
- storage.py handles saving and loading tasks from a JSON.file.
- task_manager.py contains the business logic
- cli.py provides the commandpline interface that users interact with.
I also understand how these componenets work together to create, update, delete, and display tasks.

## 2. Most Valuable Insights From Each Prompt
**Prompt 1 - Understanding Project Structure**
- Helped me identify the purpose of the main folders and files.
- Explained the overall architecture of the project.
- Shpwed where the application's entry points are located.
**Prompt 2 - Finding Feature Implementation**
- Helped me identify where a CSV export feature would most likely be implemented.
- Showed how to trace similar functionality across the codebase.
- Improved my ability to locate releveant files quickly.
**Prompt 3 - Understanding Domain Models**
- Explained the relationships between Task, TaskStatus, and TaskPriority.
- Helped me understand the business rules behind the application.
- Improved my understanding of the application's domain model.

## 3. Approach to Implementing the New Business Rule
To implement the rule that tasks overdue by more than seven days should automatically be marked as abandoned unless they are high priority, i would:
1. Modify models.py to support an **Abandoned** status.
2. Update the overdue checking logic in the Task model.
3. Add the business rule in task_manager.py.
4. Updtae cli.py so abandoned tasks are displayed correctly.
5. test the feature to ensure high-priority tasks are excluded from being abandoned automatically.

## 4. Strategies from Approaching Unfamiliar Code in the Future
- Start by understanding the overall project structure.
- Identify the main entry point and core components.
- Read the README and configuration files first.
- Use AI to explain unfamiliar code and concepts.
- Trace how data flows through the application.
- Test small sections of the code instead of trying to understand everything at once.
- Document key findings while exploring the codebase.
