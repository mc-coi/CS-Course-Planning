# Day 3: Planning Phase – Design & Architecture

**Session Goal:** Create a detailed plan for your project including pseudocode, class design, and file structure.

---

## Today's Focus

Real software development starts with planning, not coding. Today you'll take your brainstorm from Day 2 and turn it into a blueprint. You'll design your classes, plan your functions, sketch your file structure, and write pseudocode. This plan is your guide for the next 20 days of building.

---

## Work Session Agenda

**Minutes 0-5:** **Planning Standup**
- Teacher: why planning matters (saves time, prevents rework, clarifies thinking)
- Quick demo: show one planning example from a past project

**Minutes 5-50:** **Individual Planning Work**
- Use the **Planning Template** (below) to design your project
- Create a document (Google Doc, .txt, or Markdown) with:
  - Class and function design
  - File structure diagram
  - Pseudocode for core features
  - Data models (what does your data look like?)
- Encourage: use diagrams, boxes, arrows — visual planning is powerful

**Minutes 50-55:** **Wrap-up & Save**
- Save planning document to your project folder
- Bring it to Day 4 check-in

---

## Planning Template

Use this structure for your detailed plan.

### 1. Project Overview (Revisit from Day 2)
```
PROJECT NAME:
TARGET USER:
CORE FEATURES (5-7):
1.
2.
...
```

### 2. Data Model
Describe the structure of your data.

```
MAIN DATA TYPES / CLASSES:

Class: Student
  - name: str
  - student_id: int
  - gpa: float
  - courses: list[str]
  - Methods:
    - get_avg_gpa()
    - add_course(course_name)
    - ...

Class: Course
  - course_code: str
  - title: str
  - students: list[str]
  - Methods:
    - enroll_student(student_id)
    - ...
```

### 3. File Structure
Diagram your project folders and files.

```
my_project/
├── main.py
├── data/
│   ├── students.json
│   └── courses.json
├── src/
│   ├── student.py
│   ├── course.py
│   └── system.py
├── README.md
└── tests/
    └── test_students.py
```

### 4. Function / Method Design
For each class and main module, list the functions/methods.

```
module: src/student.py

Class Student:
  __init__(name, student_id, gpa, courses=[])
    Purpose: Initialize a student object
    Parameters: name (str), student_id (int), gpa (float), courses (list)
    Returns: none

  add_course(course_name)
    Purpose: Add a course to this student's course list
    Parameters: course_name (str)
    Returns: none
    Side effects: Updates self.courses

  get_info()
    Purpose: Return formatted student info as a string
    Parameters: none
    Returns: str
```

### 5. Pseudocode for Core Features
Write step-by-step logic for your most important features.

```
FEATURE: Load student data from JSON

load_students(filename):
  1. Open file at filename
  2. Parse JSON content
  3. For each student object in JSON:
     a. Create a Student object
     b. Add to students list
  4. Return students list
  5. Handle errors: file not found, invalid JSON
```

### 6. Key Questions & Unknowns
List things you need to learn or clarify.

```
- How do I read/write JSON files? (Look at Unit 4)
- What does the input CSV look like? (Get sample file from teacher)
- Should I use matplotlib or a different library? (Research alternatives)
```

---

## Planning Example: Student Information System

Here's what a complete plan might look like:

```
PROJECT NAME: Student Information System
TARGET USER: School administrators, teachers
CORE FEATURES:
1. Create, read, update, delete student records
2. Search students by name or ID
3. Sort students by GPA or name
4. Save/load from JSON file
5. Display formatted student reports

=== DATA MODEL ===

Class: Student
  - name: str (e.g., "Alice Smith")
  - student_id: int (e.g., 12345)
  - gpa: float (e.g., 3.85)
  - courses: list[str] (e.g., ["Math 101", "Physics 201"])
  - email: str
  Methods:
    - get_summary() -> str
    - add_course(course: str) -> None
    - update_gpa(new_gpa: float) -> None

Class: StudentSystem
  - students: list[Student]
  Methods:
    - add_student(student: Student) -> None
    - remove_student(student_id: int) -> bool
    - find_by_id(student_id: int) -> Student | None
    - find_by_name(name: str) -> list[Student]
    - sort_by_gpa() -> list[Student]
    - load_from_json(filename: str) -> None
    - save_to_json(filename: str) -> None

=== FILE STRUCTURE ===

student_system/
├── main.py (entry point, menu loop)
├── student.py (Student class)
├── system.py (StudentSystem class, file I/O)
├── utils.py (helper functions, validation)
├── data/
│   └── students.json (persistent data)
├── README.md
└── tests/
    └── sample_data.json
```

---

## Planning Checklist

- [ ] Data model defined (classes, attributes, methods)
- [ ] File structure sketched
- [ ] 5-7 core functions/methods designed
- [ ] Pseudocode written for 2-3 hardest features
- [ ] Key unknowns listed
- [ ] Plan saved and ready for Day 4 review

---

## Reflection / Exit Ticket

1. What part of your plan are you most confident about?
2. What part do you need to learn more about before you start building?
3. Do you have any blockers or questions for the teacher check-in tomorrow?

---

## Progress Checklist

- [ ] Planning document completed
- [ ] Class/function design finalized
- [ ] File structure diagram created
- [ ] Pseudocode written for core features
- [ ] Plan saved to project folder
