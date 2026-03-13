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

---
