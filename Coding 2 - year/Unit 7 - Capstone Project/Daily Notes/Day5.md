# Day 5: Sprint 1 Begins – Project Setup & Core Structure

**Session Goal:** Set up your project repository, create core classes/files, and establish a solid foundation for building.

---

## Today's Focus

Today you stop planning and start coding. You'll create your project folder structure, write the skeleton of your main classes, and set up any configuration or initialization code. This is less exciting than building features, but a solid foundation prevents headaches later. By end of day, your project should compile/run, even if it doesn't do much yet.

---

## Work Session Agenda

**Minutes 0-5:** **Standup: Sprint 1 Overview**
- What is a "sprint"? (2–3 week focused development cycle)
- Sprint 1 goal: foundation, structure, basic I/O
- Reminder: commit/save work frequently

**Minutes 5-50:** **Project Setup & Skeleton Code**

Follow these steps:

1. **Create project folder structure**
   - Make directories: `src/`, `data/`, `tests/`
   - Create files: `main.py`, and one file per class

2. **Write class skeletons** (empty methods, docstrings, just the shape)
   - Example: if you're building Student System, create `student.py` with `Student` class and empty methods
   - Each method should have a docstring, even if body is just `pass`

3. **Write `main.py` entry point**
   - Import your classes
   - Create a simple menu or startup code
   - Should run without errors (even if it does nothing interesting)

4. **Set up file I/O paths**
   - Decide where data files live (`data/students.json`, `data/records.csv`, etc.)
   - Create empty placeholder files if needed

5. **Test: Can you run `python main.py`?**
   - You should see some output or a menu, even if basic

**Minutes 50-55:** **Wrap-up & Save**
- Save all files
- Commit to Git if using version control
- Fill out progress tracker

---

## Code Skeleton Example (Student Information System)

```python
# student.py
class Student:
    """Represents a single student record."""

    def __init__(self, name, student_id, gpa, courses=None):
        """
        Initialize a Student.

        Args:
            name (str): Student's full name
            student_id (int): Unique student ID
            gpa (float): Current GPA
            courses (list): List of course codes (optional)
        """
        self.name = name
        self.student_id = student_id
        self.gpa = gpa
        self.courses = courses if courses else []

    def add_course(self, course_code):
        """
        Add a course to this student's enrollment.

        Args:
            course_code (str): Course code to add
        """
        pass

    def remove_course(self, course_code):
        """Remove a course from this student's enrollment."""
        pass

    def get_summary(self):
        """Return a formatted string with student info."""
        pass

    def __str__(self):
        """Return student info as a string."""
        pass


# system.py
class StudentSystem:
    """Manages a collection of students."""

    def __init__(self):
        """Initialize the student system with an empty list."""
        self.students = []

    def add_student(self, student):
        """Add a student to the system."""
        pass

    def remove_student(self, student_id):
        """Remove a student by ID."""
        pass

    def find_by_id(self, student_id):
        """Search for a student by ID."""
        pass

    def find_by_name(self, name):
        """Search for students by name (partial match)."""
        pass

    def load_from_json(self, filename):
        """Load students from a JSON file."""
        pass

    def save_to_json(self, filename):
        """Save students to a JSON file."""
        pass


# main.py
from student import Student
from system import StudentSystem

def main():
    """Main entry point."""
    system = StudentSystem()
    print("Welcome to Student Information System")
    print("1. Add student")
    print("2. View all students")
    print("3. Search by name")
    print("4. Exit")
    # TODO: implement menu loop

if __name__ == "__main__":
    main()
```

---

## Technical Tips & Resources

**From Unit 2 (OOP):**
- Remember: `__init__` runs when you create an object
- Use `self.attribute` to store data
- Use `def method(self):` for class methods
- Docstrings (`"""..."""`) go after `def`

**From Unit 4 (File I/O):**
- `import json` for JSON files
- `json.load(file)` to read, `json.dump(data, file)` to write
- `import csv` for CSV files
- Always use `with open(...) as file:` for safe file handling

**From Unit 3 (Functions):**
- Keep functions small and focused (one job each)
- Return values instead of printing (easier to test)

**Good practice:**
- Create empty files first, then fill in
- Run your code after each change to catch typos
- Use print statements for debugging

---

## Reflection / Exit Ticket

1. Did your project folder compile/run? What did you see?
2. What was the easiest part of setting up? Hardest?
3. What's the next feature you'll code in Sprint 1?

---

## Progress Checklist

- [ ] Project folder structure created
- [ ] All class skeletons written with docstrings
- [ ] `main.py` created and runs without errors
- [ ] File I/O paths planned (data/ folder set up)
- [ ] Code committed or saved
- [ ] Progress logged
