# Exercise Part 4 - Reflection and Presentation

## Slide 1: Application Overview

Good day everyone.

The application I explored is a **Python Task Management System**. It is a command-line application that allows users to create, update, organize, and complete tasks.

The application follows a layered architecture where each file has a specific responsibility:

- `cli.py` handles user interaction.
- `task_manager.py` contains the business logic.
- `models.py` defines the Task object.
- `storage.py` manages saving and loading tasks using a JSON file.

This separation makes the application easier to understand and maintain.

## Slide 2: Three Key Features

### 1. Task Creation

When a user creates a task, the CLI collects the input and passes it to the `TaskManager`.

The `TaskManager` validates the information, creates a `Task` object, and stores it using the storage component.

### 2. Task Prioritization

The application uses the `TaskPriority` enum to represent four priority levels:

- Low
- Medium
- High
- Urgent

The priority is converted into an enum before being stored and converted back when tasks are loaded from the JSON file.

### 3. Task Completion

When a task is marked as complete:

- The CLI receives the command.
- The `TaskManager` updates the task.
- The `Task` object changes its status to **DONE**.
- The completion time is recorded.
- The updated task is saved back to `tasks.json`.

## Slide 3: Interesting Design Pattern

One design approach I found interesting was **Separation of Concerns**.

Each file has a single responsibility:

- The CLI handles user interaction.
- The Task Manager contains the application logic.
- The Model represents the data.
- The Storage component manages persistence.

This makes the code modular and easier to maintain.

## Slide 4: Challenges and How AI Helped

The most challenging part for me was understanding how data moved between different files.

Initially, I focused on individual functions instead of following the complete flow of the application.

Using structured AI prompts helped me:

- Identify the important files.
- Follow the execution flow.
- Understand how data is stored and retrieved.
- Recognize why the application was designed with separate layers.

The prompts encouraged me to explore the code step by step instead of trying to understand everything at once.

## Slide 5: Conclusion

This exercise helped me understand that reading an unfamiliar codebase is not about memorizing every line of code.

Instead, it is about identifying the main components, understanding how they interact, and tracing how data flows through the application.

Using AI as a learning tool made the exploration process more structured and helped me build confidence when working with an existing codebase.

Thank you.
