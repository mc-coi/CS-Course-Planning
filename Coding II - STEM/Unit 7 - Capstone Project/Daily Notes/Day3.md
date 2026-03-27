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

---
