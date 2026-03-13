# Unit 7: Capstone Project
> Plan, design, build, and present a complete programming project that demonstrates all semester skills.

##  Unit Overview
- **Duration:** 6 days / 2 weeks
- **Key Concepts:** Project planning, system design, implementation, testing, refactoring, documentation, and presentation
- **Big Idea:** Real programs are planned, designed, built in phases, tested, and refined
- **TN Standard:** 9-12.CCI.5 — Create a significant programming project

##  Learning Targets
- I can plan a project with clear requirements and user stories
- I can design system architecture and data structures
- I can implement features incrementally
- I can test and debug my code
- I can refactor code for clarity and efficiency
- I can document code with docstrings and comments
- I can present my project professionally

---

# Day 1: Project Planning
**Learning Target:** I can define project scope, requirements, and create user stories.

### Key Concepts
**Project planning:** Define what you're building before coding
**Requirements:** What the software must do
**User stories:** Feature descriptions from user perspective: "As a [user], I want [feature] so that [benefit]"

### Project Planning Guide
```
1. BRAINSTORM
   - What problem does this solve?
   - Who are the users?
   - What features are essential?

2. SCOPE
   - What's in scope (must have)?
   - What's nice-to-have?
   - What's out of scope (won't do)?

3. REQUIREMENTS
   - Functional: What system does
   - Non-functional: Performance, usability

4. USER STORIES
   Example:
   - "As a student, I want to track my assignments so that I don't miss deadlines"
   - "As a teacher, I want to view class grades so that I can generate reports"

5. ACCEPTANCE CRITERIA
   How to know when a story is done?
   - Task is complete when...
```

### Project Ideas
- Task management app
- Expense tracker
- Quiz generator
- Weather app
- Movie database
- Health tracker
- Study timer
- Grade calculator
- Inventory system
- Personal website backend

### Guided Practice
Choose a project idea and create planning document.

### Practice Problems
**Problem 1 — Beginner:** Write 3 user stories for a simple app.

**Problem 2 — Intermediate:** Create requirements document for project.

**Problem 3 — Challenge:** Create detailed project plan with timeline.

<details>
<summary>✅ Sample Answers</summary>

```
# Project: Task Manager App

USER STORIES:
1. As a student, I want to add tasks to my to-do list so that I don't forget assignments.
   Acceptance: Can create task with title, due date, priority

2. As a student, I want to mark tasks complete so that I can track progress.
   Acceptance: Completed tasks show as done

3. As a student, I want to view tasks by priority so that I focus on important work first.
   Acceptance: Can filter by priority level

REQUIREMENTS:
- Store tasks in file or database
- Support add, delete, update, view operations
- Filter and sort capabilities
- Simple command-line or GUI interface
```
</details>

---

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

# Day 3: Implementation Phase 1 — Core Features
**Learning Target:** I can implement core data structures and classes.

### Key Concepts
**Incremental development:** Build and test one feature at a time
**Core features:** Essential functionality
**Testing as you go:** Test each feature before moving on

### Implementation Checklist
```
1. SET UP PROJECT
   - Create file structure
   - Define main modules
   - Set up testing framework

2. IMPLEMENT DATA CLASSES
   - Define core classes
   - Initialize attributes
   - Implement basic methods

3. IMPLEMENT CORE LOGIC
   - Main functionality
   - Data validation
   - Error handling

4. TEST CORE FEATURES
   - Unit tests
   - Manual testing
   - Bug fixes
```

### Example: Task Manager Phase 1
```python
# task.py
class Task:
    def __init__(self, name, due_date=None, priority="medium"):
        self.name = name
        self.due_date = due_date
        self.priority = priority
        self.completed = False

    def mark_complete(self):
        self.completed = True

    def __str__(self):
        status = "✓" if self.completed else "○"
        return f"{status} {self.name} (Due: {self.due_date}, Priority: {self.priority})"

# task_manager.py
class TaskManager:
    def __init__(self):
        self.tasks = []

    def add_task(self, task):
        self.tasks.append(task)

    def remove_task(self, task_name):
        self.tasks = [t for t in self.tasks if t.name != task_name]

    def get_tasks(self):
        return self.tasks

    def mark_complete(self, task_name):
        for task in self.tasks:
            if task.name == task_name:
                task.mark_complete()
```

### Guided Practice
Implement core classes for your project.

### Practice Problems
**Problem 1 — Beginner:** Create main data classes.

**Problem 2 — Intermediate:** Implement core methods with error handling.

**Problem 3 — Challenge:** Write unit tests for core classes.

<details>
<summary>✅ Sample Answers</summary>

```python
# Unit test example
import unittest

class TestTask(unittest.TestCase):
    def setUp(self):
        self.task = Task("Test task", "2024-12-31", "high")

    def test_task_creation(self):
        self.assertEqual(self.task.name, "Test task")
        self.assertFalse(self.task.completed)

    def test_mark_complete(self):
        self.task.mark_complete()
        self.assertTrue(self.task.completed)

if __name__ == '__main__':
    unittest.main()
```
</details>

---

# Day 4: Implementation Phase 2 — Features & Polish
**Learning Target:** I can build additional features and handle edge cases.

### Key Concepts
**Feature implementation:** Adding functionality beyond core
**Edge cases:** Unusual inputs or situations
**Polish:** Making code robust and user-friendly

### Implementation Checklist
```
1. ADD FEATURES
   - Sorting/filtering
   - Search functionality
   - Advanced operations

2. ERROR HANDLING
   - Invalid inputs
   - File errors
   - API errors

3. USER EXPERIENCE
   - Clear messages
   - Input validation
   - Helpful feedback

4. TESTING
   - All features tested
   - Edge cases covered
   - Integration tests
```

### Example: Task Manager Phase 2
```python
class TaskManager:
    # ... existing code ...

    def get_tasks_by_priority(self, priority):
        return [t for t in self.tasks if t.priority == priority]

    def get_incomplete_tasks(self):
        return [t for t in self.tasks if not t.completed]

    def get_tasks_by_date(self):
        return sorted(self.tasks, key=lambda t: t.due_date or "")

    def search_tasks(self, keyword):
        return [t for t in self.tasks if keyword.lower() in t.name.lower()]

    def task_summary(self):
        total = len(self.tasks)
        completed = len([t for t in self.tasks if t.completed])
        incomplete = total - completed
        return {"total": total, "completed": completed, "incomplete": incomplete}
```

### Guided Practice
Add features and handle edge cases.

### Practice Problems
**Problem 1 — Beginner:** Add sorting feature.

**Problem 2 — Intermediate:** Add filtering and search.

**Problem 3 — Challenge:** Implement advanced features.

---

# Day 5: Refactoring & Documentation
**Learning Target:** I can improve code quality and write comprehensive documentation.

### Key Concepts
**Refactoring:** Improving code without changing behavior
**Documentation:** Docstrings, comments, README
**Code quality:** Readability, efficiency, maintainability

### Refactoring Checklist
```
1. CODE REVIEW
   - Is it readable?
   - Are there duplicates?
   - Can it be simpler?

2. OPTIMIZE
   - Remove unused code
   - Simplify logic
   - Improve efficiency

3. RENAME
   - Clear variable names
   - Consistent naming

4. EXTRACT
   - Break into smaller functions
   - Create helper methods

5. DOCUMENT
   - Add docstrings
   - Write comments
   - Create README
```

### Example: Well-Documented Code
```python
def get_tasks_by_priority(self, priority: str) -> list:
    """
    Retrieve all tasks with specified priority.

    Args:
        priority (str): Task priority level ('low', 'medium', 'high')

    Returns:
        list: List of Task objects matching priority

    Raises:
        ValueError: If priority not in valid values

    Example:
        >>> manager = TaskManager()
        >>> high_priority = manager.get_tasks_by_priority('high')
    """
    valid_priorities = ['low', 'medium', 'high']
    if priority not in valid_priorities:
        raise ValueError(f"Priority must be one of {valid_priorities}")

    # Filter tasks by priority
    return [t for t in self.tasks if t.priority == priority]
```

### Documentation Template
```
# Project Name

## Overview
Brief description

## Installation
```bash
pip install -r requirements.txt
```

## Usage
```python
# Example code showing how to use
```

## Features
- Feature 1
- Feature 2
- Feature 3

## Architecture
Description of how it works

## Testing
How to run tests

## Future Enhancements
Ideas for improvement
```

### Guided Practice
Refactor and document your project.

### Practice Problems
**Problem 1 — Beginner:** Add docstrings to all functions.

**Problem 2 — Intermediate:** Refactor for readability.

**Problem 3 — Challenge:** Write comprehensive README.

---

# Day 6: Presentations & Showcase
**Learning Target:** I can present my project professionally and reflect on learning.

### Presentation Guide
```
PRESENTATION STRUCTURE (5-10 minutes):

1. INTRODUCTION (30 sec)
   - Project name and purpose
   - Problem it solves

2. DEMO (3-4 min)
   - Show it working
   - Key features
   - Real example

3. TECHNICAL EXPLANATION (2-3 min)
   - How it works
   - Key classes/components
   - Interesting challenges

4. REFLECTION (1-2 min)
   - What you learned
   - Challenges overcome
   - Future improvements

5. Q&A (remaining time)
   - Be ready for questions
```

### Presentation Tips
- Practice beforehand
- Show working code (have backup video if demo fails)
- Explain clearly for all audiences
- Be confident
- Answer questions honestly

### Reflection Questions
```
1. What was the most challenging part?
2. What would you do differently?
3. What did you learn?
4. How could you improve it?
5. What new skills did you develop?
6. How could you expand this project?
```

### Guided Practice
Practice presentations with peers or instructor.

### Peer Feedback Guide
```
What went well:
- Clear explanation?
- Good demo?
- Interesting project?

What could improve:
- Pacing?
- Technical depth?
- Code quality?

Questions:
- What would you ask?
```

---

# Unit Practice Bank & Project Ideas

## Project Ideas
1. **Task/To-Do Manager** — Add, edit, delete, filter tasks; save to file
2. **Expense Tracker** — Track spending; categorize; generate reports
3. **Grade Calculator** — Calculate GPA, letter grades; generate transcripts
4. **Quiz Application** — Create quizzes; track scores; analyze performance
5. **Weather Dashboard** — Fetch from API; display forecasts; visualize data
6. **Contact Manager** — Store contacts; search; export/import
7. **Habit Tracker** — Track daily habits; visualize streaks
8. **Movie Database** — Search movies; rate; create watchlists
9. **Personal Finance** — Budget tracker; savings goals; reports
10. **Study Aid** — Flashcard app; spaced repetition algorithm
11. **Workout Planner** — Create routines; track progress; visualize improvements
12. **Meal Planner** — Plan meals; generate shopping lists; nutrition tracking
13. **Reading Tracker** — Track books; rate; create reading list
14. **Discord/Chat Bot** — Automated responses; fun commands
15. **Data Analysis Tool** — Process CSV; calculate stats; visualize

---

# Common Mistakes & How to Fix Them
| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Starting to code before planning | Scope creep, poor design | Spend time on planning first |
| No testing until the end | Many bugs to find and fix | Test as you go |
| Poor variable/function names | Code is hard to understand | Use clear, descriptive names |
| No documentation | Others (or you later) can't understand | Document as you code |
| Overcomplicating | Code is hard to maintain | Keep it simple |
| Not handling errors | Program crashes on bad input | Validate and handle errors |

---

# Semester Reflection

**Final Questions:**

1. What was your favorite unit? Why?
2. What concept was most challenging to understand?
3. What programming skill are you most proud of?
4. How has your problem-solving improved?
5. What would you like to learn next?
6. How would you describe programming to someone else?
7. What real-world applications interest you?
8. Would you take more programming classes? Why?

---

# Vocabulary & Quick Reference

**Key Terms:**
- **Requirements:** What software must do
- **User story:** Feature from user perspective
- **Architecture:** Structure of system components
- **Refactoring:** Improving code without changing behavior
- **Docstring:** Documentation in code
- **Unit test:** Test for single function/class
- **Integration test:** Test multiple components together
- **Deployment:** Making software available to users

**Project Phases:**
1. Planning (requirements, design)
2. Implementation (code features)
3. Testing (verify it works)
4. Refactoring (improve quality)
5. Documentation (explain it)
6. Presentation (show it)

---

# End of Course Celebration

You've completed Tennessee Coding II! You've learned:
- Data structures (lists, dicts, sets, tuples)
- Object-oriented programming
- Advanced functions and algorithms
- File I/O and data processing
- Sorting and searching algorithms
- External APIs and libraries
- Complete project development

You're ready to:
- Build real applications
- Continue learning
- Contribute to open source
- Take AP Computer Science Principles/AP CSA
- Career paths in software development

Congratulations on your hard work and dedication!
