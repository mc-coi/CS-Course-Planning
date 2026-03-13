# Day 6: Project Day — Student Grade Book
**Learning Target:** I can design and build a complete program using lists, dictionaries, and tuples.

### Project Overview
Build an interactive student gradebook that:
1. Stores student information (name, grade, GPA)
2. Adds new students
3. Updates grades
4. Calculates class statistics
5. Displays reports

### Requirements
- Use a list of dictionaries to store student data (or a dictionary of tuples)
- User menu with options: Add, Update, View All, Calculate Average, Exit
- Display students sorted by grade or name
- Calculate class average GPA
- Use appropriate data structures for each piece of information

### Scaffold & Starter Code
```python
# Student Grade Book Project

# Data structure: list of dictionaries
students = [
    {"name": "Alice", "grade": 95, "gpa": 3.9},
    {"name": "Bob", "grade": 87, "gpa": 3.5},
]

def add_student(name, grade, gpa):
    """Add a new student to the gradebook."""
    students.append({"name": name, "grade": grade, "gpa": gpa})

def view_all_students():
    """Display all students."""
    for i, student in enumerate(students, 1):
        print(f"{i}. {student['name']} - Grade: {student['grade']}, GPA: {student['gpa']}")

def calculate_class_average():
    """Calculate average grade and GPA."""
    if not students:
        print("No students yet.")
        return
    avg_grade = sum(s["grade"] for s in students) / len(students)
    avg_gpa = sum(s["gpa"] for s in students) / len(students)
    print(f"Class Average Grade: {avg_grade:.2f}")
    print(f"Class Average GPA: {avg_gpa:.2f}")

def main():
    while True:
        print("\n--- Student Gradebook ---")
        print("1. Add Student")
        print("2. View All Students")
        print("3. Calculate Class Average")
        print("4. Exit")
        choice = input("Select option: ")

        if choice == "1":
            name = input("Name: ")
            grade = int(input("Grade: "))
            gpa = float(input("GPA: "))
            add_student(name, grade, gpa)
            print("Student added!")
        elif choice == "2":
            view_all_students()
        elif choice == "3":
            calculate_class_average()
        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Invalid option.")

if __name__ == "__main__":
    main()
```

### Enhancement Ideas
- Sort students by grade or GPA
- Find highest/lowest grade
- Remove a student
- Search for a student by name
- Save/load from a file (Unit 4)
- Add multiple grades per student (nested data structures)

---
