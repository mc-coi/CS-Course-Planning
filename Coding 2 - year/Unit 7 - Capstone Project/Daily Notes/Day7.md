# Day 7: Sprint 1 – Building Core Features (Part 2)

**Session Goal:** Complete 2–3 more core features. Connect components; start seeing your app come together.

---

## Today's Focus

You've built one feature; now build on that momentum. Today you'll implement additional core features and start connecting them together. Your app is starting to feel less like a skeleton and more like a real application.

---

## Work Session Agenda

**Minutes 0-5:** **Standup**
- Report: Which feature did you finish yesterday?
- Teacher: tips for today's focus feature (e.g., "Search functions use list comprehension from Unit 6")
- Students: set target for 2 features today

**Minutes 5-50:** **Focused Coding**
- Work on second and third core features
- Connect them to your main menu or workflow
- Test the full flow end-to-end (e.g., add student → save to file → load from file)
- Pair programming encouraged: work with a classmate if both are on the same project

**Minutes 50-55:** **Wrap-up**
- Verify your app runs through a basic scenario
- Commit work
- Update progress tracker

---

## Feature Integration Checklist

When you finish a feature, make sure it integrates:

- [ ] Feature works in isolation (passes basic test)
- [ ] Feature is called from `main.py` or relevant module
- [ ] Feature doesn't break other features you've built
- [ ] Error handling is in place (try/except)
- [ ] You can explain what the code does

---

## Example: Connecting Add Student + Save to File

```python
# system.py
def add_student(self, student):
    """Add a student to the system."""
    if not isinstance(student, Student):
        raise TypeError("Must be a Student object")
    self.students.append(student)
    print(f"Added {student.name}")

# main.py
def main():
    system = StudentSystem()
    system.load_from_json("data/students.json")  # Load existing data

    while True:
        print("\n1. Add Student")
        print("2. View All")
        print("3. Save & Exit")
        choice = input("Pick: ")

        if choice == "1":
            name = input("Name: ")
            sid = int(input("Student ID: "))
            gpa = float(input("GPA: "))
            student = Student(name, sid, gpa)
            system.add_student(student)

        elif choice == "2":
            for s in system.students:
                print(s.get_summary())

        elif choice == "3":
            system.save_to_json("data/students.json")
            print("Saved. Goodbye!")
            break
```

---

## Unit Reminders

**From Unit 6 (Search & Sort):**
```python
# Search: list comprehension
results = [s for s in system.students if name.lower() in s.name.lower()]

# Sort: key parameter
sorted_students = sorted(system.students, key=lambda s: s.gpa, reverse=True)
```

**From Unit 2 (OOP):**
```python
# Type checking
if not isinstance(obj, ClassName):
    raise TypeError("Expected ClassName")
```

**From Unit 4 (File I/O):**
```python
# Safe file handling
try:
    with open(filename) as f:
        data = json.load(f)
except FileNotFoundError:
    print(f"File {filename} not found")
    data = []
```

---

## Reflection / Exit Ticket

1. How many core features have you completed so far?
2. What was surprising or challenging today?
3. What feature will you tackle on Day 8?

---

## Progress Checklist

- [ ] Second core feature implemented
- [ ] Third core feature implemented
- [ ] Features integrated with main menu/flow
- [ ] Basic testing done (add → save → load)
- [ ] Code committed/saved
