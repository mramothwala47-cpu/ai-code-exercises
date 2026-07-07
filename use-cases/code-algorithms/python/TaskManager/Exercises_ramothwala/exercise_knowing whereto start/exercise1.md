# Execise 1: Understanding Project Structure
  ## 1. Explore the code base
  After opening the Task Manager project, I noticed that it is organized into several Python files rather then one large file. There is also a 'test' folder and a 'README.md' file.

  The files I found are:
  - cli.py
  - models.py
  - task_manager.py
  - task_priority.py
  - task_list_merge.py
  - test/
  - README.md

  ## 2. Form Initial Understanding
  Before using AI, i made the following assusmptions, or this is what I understood about how thise codebase is organized;
  - The project is written in Python because the fies end woth '.py'.
  - 'cli.py' problem handles user interaction.
  - 'models.py' probably defines the application's data.
  - 'storage.py' probably saves and loads data.
  - 'task_manager.py' probably contains the main application logic.

  ## 3. Apply the project Structure Prompt
  **Prompt 1::**
  I am a junior developer who just joined this project. i have read the README but still need help understanding the project structure and technology stack.

  Here is my current understanding of the project:
  - It seems to be a Python Task Manager application.
  - It appears to use Python, Git/GitHub, and Markdown.
  - The folder structure seems to follow a modular pattern.

  Project Structure:
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

  Key configuration files:
  I could not find a 'requirement.txt', 'package.json', or 'pom.xml' file.

  Could you:
  1. Validate my understanding and correct any misconceptions.
  2. Identify additional technologies, frameworks, and libraries used.
  3. Explain the purpose of each main file and dolder.
  4. Point out whwere the qpplication entry poimts are located.
  5. Suggect 3-5 questions I should ask my team to deepen my undertsnading.

  Comparing the AI's analysis with my own observations, is that looking at my inital observations were mostly correct. I correctly identified that the project was written in Python and that the files appeared to have different responsibilities. However, i was unsure how the files interacted and where the application started. The AI explained that the project follows a modular structure, where each file has a specific purpose. It also helped me understand the likely responsibilites of files such as cli.py, models.py, and storage.py. However, i still need to inspect the code further to confirm the application's entry point.

  ## 4. Documenting the findings
  ### Misconceptions
  Initially, i assumed that one file would control the entire appllication. After using AI, I learned that the project separates responsibilites across multiple files, making the code easier and undertand and maintain.
  ### Entry Points and Architecture.
  The project appears to follow a modular architecture. The exact entry point still needs to be confirmed by exploring the code, but 'cli.py' or 'task_manager.py' are likely candidates.
  ### Key Components
  - 'cli.py' - handles user interaction.
  - 'models.py' - defines the application's data model.
  - 'storage.py' - saves and retrieves task data.
  - 'task_manager.py'- contains the main business logic.
  - 'task_priority.py' - manages task prioties.
  - 'test/' - contains automated tests.
