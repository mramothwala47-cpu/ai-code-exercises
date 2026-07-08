# Exercise 2: Finding feature Implementation
## 1. Initial Search
I searched for file-related functionality by exploring the project files. i looked for code responsible for saving data and handling tasks

The files I examined were:
- storgae.py
- task_manager.py
- cli.py

From my investigation, i found that 'storage.py' handles saving and loading tasks, 'task_manager.py' manages the application's business logic, and 'cli.py' accepts user commands and cells that appropriate methods in 'task_manager.py'.

## 2. Form a Hypothesis
Based on my investigation, I believe the new **Task Export to CSV** feature should mainly be implmented in 'storage.py' because it already performs file operations.
I also think 'task_manager.py' would need a new method that calls the export functionality, while 'cli.py' would need a new command so that users can choose to export their tasks.

The terms that I used were:
- export
- csv
- file
- save
- write
- storage

The  existing components that might need to be modified:
- 'storage.py' - Add an 'export_to_csv()' function.
- 'task manager.py' - Add a method that calls the export funtion.
- 'cli.py' - Add a new command so users can export tasks.

 ## 3. Apply the Feature Location Prompt
 Based on my initial investigation, I believe the **Task Export to CSV** feature in this codebase, nut I am not sure where the code this feature lives.
 My approach so far:

- I've searched for keywords like **export**, **csv**, **file**, **save**, **write**, and **storage**.
- I looked in **storage.py**, **task_manager.py**, and **cli.py**, which seemed relevant.
- I think the feature might relate to **storage.py** because it already performs file operations, and **task_manager.py** because it manages task-related functionality.

### Project Structure
TaskManager/
- tests/
- README.md
- cli.py
- models.py
- storage.py
- task_list_merge.py
- task_manager.py
- task_parser.py
- task_priority.py
  
Based on my search, these files might be relevant:
- `storage.py'
- `task_manager.py'
- `cli.py'

Could you help me:

1. Evaluate my search approach and suggest improvements.
2. Identify which files most likely contain the implementation for this feature.
3. Suggest more effective search terms.
4. Explain what parts of the feature would likely be located in different files.
5. Recommend a step-by-step investigation process.

Also, what questions should I ask myself while exploring the code? What patterns should I look for to ensure I have found all the relevant parts?

After your guidance, could you give me a small challenge to test my understanding of navigating this feature's code?

## Comparison of AI Analysis with My Investigation

Before using AI, I believed that 'storage.py' would be the best place to implement the CSV export feature because it already handles saving and loading task data. I also thought that `task_manager.py` and `cli.py' would need to be updated.

After using AI, my understanding was confirmed. The AI explained that the project follows a layered structure:

- `cli.py' receives commands from the user.
- `task_manager.py' processes the request.
- `storage.py' performs file operations.

This helped me understand how the different components work together and where a new feature should be added.

## 4. Findings
### 4.1. Where the feature should be implemented
After exploring the code, I found that:
- 'storage.py' - this file is responsible for reading and writing task data. It already loads and saves tasks in a JSON file, making it the most appropriate place to implement the CSV export functionality.
- 'cli.py' - this file provides the command-line interface. A new command, such as 'export', should be added so users can export their tasks.
- 'task_manager.py' - this file contains the application's business logic. It manages operations such as creating, updating, and listing tasks. A new method should be added here to call the CSV export function in 'storage.py'.
### 4.2. Components Affected
- 'storage.py' | Add an 'export_to_csv()' function to create the CSV file.
- 'task_manager.py' | Add a method that calls the export function.
- 'cli.py' | Add a new command that allows users to export tasks.
### 4.3. Implementation Plan
1. Add an 'export_to_csv()' function to 'storage.py'.
2. Retrieve all tasks using 'get_all_tasks()'.
3. Write the task information into a CSV file.
4. Add an export method to 'task_manager.py'.
5. Add an 'export' command to 'cli.py'.
6. Test the feature to ensure the CSV file is created correctly and contains the expected task information.
