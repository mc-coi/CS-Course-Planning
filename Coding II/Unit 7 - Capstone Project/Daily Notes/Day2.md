# Day 2: Architecture & Design Patterns
**Learning Target:** I can design system architecture and choose appropriate design patterns.

### Key Concepts
**Architecture:** How components connect
**Design patterns:** Reusable solutions to common problems

Common patterns:
- **MVC (Model-View-Controller):** Separate data, display, logic
- **Factory pattern:** Create objects flexibly
- **Singleton pattern:** Only one instance of a class

### Design Document Template
```
1. SYSTEM COMPONENTS
   - What classes/modules needed?
   - How do they interact?

2. DATA STRUCTURES
   - What data storage needed?
   - Database or file format?

3. CLASS HIERARCHY
   - Parent/child relationships
   - Inheritance structure

4. ALGORITHMS
   - Complex logic needed?
   - Any special algorithms?

5. ERROR HANDLING
   - What can fail?
   - How to recover?

6. EXTERNAL DEPENDENCIES
   - Libraries needed?
   - APIs or services?
```

### Example Architecture
```
Task Manager App:

Classes:
- Task (name, due_date, priority, completed)
- TaskManager (list of tasks, add/remove/update)
- TaskUI (display tasks, get user input)
- TaskStorage (save/load from file)

Data: JSON file with task list
Flow: UI → TaskManager → TaskStorage
```

### Guided Practice
Design architecture for your project.

### Practice Problems
**Problem 1 — Beginner:** List classes needed for your project.

**Problem 2 — Intermediate:** Create class diagram (text or visual).

**Problem 3 — Challenge:** Design using MVC pattern.

<details>
<summary>✅ Sample Answers</summary>

```
MVC Pattern for Task Manager:

MODEL (Data):
- Task class
- TaskList class (container)
- File I/O operations

VIEW (Display):
- Display menu
- Display tasks
- Show messages

CONTROLLER (Logic):
- Handle user commands
- Call model operations
- Update view
```
</details>

---

---
