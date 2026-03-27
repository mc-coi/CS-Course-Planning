# Unit 7: Capstone Project

> Apply everything you've learned to build a complete, real-world application from scratch.

## Unit Overview

- **Duration:** 25 days / 5 weeks
- **Big Idea:** Real software development is iterative — plan, build, test, refine, and present
- **TN Standards:** All course standards applied (9-12.CCI.1 through 9-12.CCI.5)

## Learning Targets

- I can plan a software project using pseudocode and class diagrams
- I can apply OOP design to structure a real program
- I can implement file I/O for data persistence
- I can use APIs or external libraries in a working application
- I can apply sorting and searching to real data
- I can handle errors and edge cases with exception handling
- I can write clean, documented, readable code
- I can present and explain my work to an audience

## Project Options

### Option 1: Data Analyzer
**Overview:** Build a command-line tool that reads a CSV or JSON dataset, computes statistics, and generates visualizations.

**Tech Stack:**
- Python (pandas for data handling is optional but recommended)
- matplotlib or similar for charts
- File I/O (Unit 4)

**Core Features (you must implement):**
1. Load data from CSV or JSON file
2. Compute summary statistics (mean, median, min, max, count)
3. Filter or search data by field
4. Generate at least 2 different chart types (bar, line, scatter, histogram)
5. Export results to a new file

**Example Extensions:**
- Data validation and error handling
- User menu system
- Multi-file comparison
- Trend analysis or prediction

**Why Choose This:** Great for learning data structures, file I/O, and visualization. Real-world application.

---

### Option 2: API-Powered App
**Overview:** Build a command-line or GUI app that fetches live data from a public API, processes it with object-oriented design, and displays results.

**Tech Stack:**
- Python (requests library for HTTP)
- OOP (Unit 2)
- File I/O for caching/storage (Unit 4)

**Core Features (you must implement):**
1. Fetch data from a public API (e.g., weather, news, crypto, NBA stats)
2. Parse JSON responses and extract relevant fields
3. Use OOP to model data (e.g., Weather class, NewsArticle class)
4. Implement at least 3 different searches/queries
5. Cache results or save user history to file
6. Display formatted output

**Example Extensions:**
- Filter, sort, or compare results
- User preferences stored in JSON
- Rate limiting or error handling for failed requests
- Web scraping as an alternative source

**Why Choose This:** Learn how real apps get their data, practice HTTP requests and JSON parsing, build something immediately useful.

---

### Option 3: Student Information System
**Overview:** A CRUD application for managing student records with search, sort, and file persistence.

**Tech Stack:**
- Python
- OOP (Unit 2) — Student, Course, Classroom classes
- File I/O for persistence (Unit 4) — JSON storage
- Sorting and searching (Unit 6)

**Core Features (you must implement):**
1. Create, read, update, delete student records
2. Each student has: name, ID, GPA, courses, contact info
3. Search students by name or ID
4. Sort students by name, ID, or GPA
5. Save/load data from JSON file
6. Bulk operations (e.g., add students to a course)

**Example Extensions:**
- Grade calculation and reporting
- Course enrollment management
- Data import/export to CSV
- GUI using tkinter
- Validation and error handling

**Why Choose This:** Powerful database-like application, practice full CRUD and OOP design, real-world information system.

---

### Option 4: Algorithm Visualizer
**Overview:** Text-based visualization of sorting algorithms with performance benchmarking.

**Tech Stack:**
- Python
- Sorting algorithms and complexity (Unit 6)
- File I/O for results (Unit 4)

**Core Features (you must implement):**
1. Implement at least 3 sorting algorithms (bubble, selection, insertion, merge, quick)
2. Generate random datasets of varying sizes
3. Visualize sorting steps in the terminal (show array state after each swap)
4. Benchmark: time each algorithm on datasets of 100, 500, 1000, 5000 elements
5. Generate a report with timing data and comparison charts (matplotlib)
6. Analyze: which algorithm is fastest? How does size affect time?

**Example Extensions:**
- Searching algorithm visualization
- Step-through mode (pause between swaps)
- Comparison with Python's built-in sort
- Statistical analysis of performance
- GUI visualization (pygame or tkinter)

**Why Choose This:** Deep dive into algorithms and complexity, performance analysis, build understanding of "why" certain algorithms are better.

---

### Option 5: Custom Project (Teacher Approved)
**Overview:** Propose your own project that applies 4+ concepts from Units 1–6.

**Requirements:**
- Must include: OOP (Unit 2) + File I/O (Unit 4) + At least 1 more concept (functions, sorting, APIs, etc.)
- Scope should be comparable to Options 1–4 (achievable in 25 days)
- Requires teacher approval by **Day 2**

**Pitch Template:**
- What is the project?
- Who is the user?
- What problem does it solve?
- Which Units' concepts will you use?
- Why is this a good capstone?

**Why Choose This:** Build something you're passionate about; learn ownership and direction-setting.

---

## Project Rubric

All projects must include:

1. **Working Code** — Runs without errors, core features function as specified
2. **Code Quality** — Clear variable/function names, comments, proper structure, error handling
3. **Documentation** — README file, docstrings, in-code comments
4. **Testing** — Evidence of testing (manual test cases, screenshots, or written test results)
5. **Presentation** — 5–7 minute demo or slides explaining your project and process

### Detailed Rubric

**Code Functionality (25 points)**
- 25: All required features work perfectly; edge cases handled
- 20: All required features work; minor edge case issues
- 15: Most required features work; some bugs
- 10: Some features missing or broken
- 5: Major features missing
- 0: Code doesn't run

**Code Quality & Design (25 points)**
- 25: Excellent OOP design, clear naming, minimal duplication, good error handling
- 20: Good OOP design, mostly clear naming, some error handling
- 15: Fair OOP design, some unclear naming, basic error handling
- 10: Poor design or organization
- 5: Minimal structure or organization
- 0: No meaningful structure

**Documentation & Comments (15 points)**
- 15: Excellent README, docstrings on all functions, comments explain "why"
- 12: Good README, docstrings on most functions, adequate comments
- 9: Adequate README, docstrings on some functions, basic comments
- 6: Poor README, few docstrings, minimal comments
- 3: Almost no documentation
- 0: No documentation

**Testing & Debugging (15 points)**
- 15: Comprehensive testing, handles errors gracefully, edge cases tested
- 12: Good testing, most errors handled, some edge cases tested
- 9: Basic testing, some error handling
- 6: Minimal testing, limited error handling
- 3: Very little testing
- 0: No evidence of testing

**Presentation (10 points)**
- 10: Clear, engaging, explains code and process, great Q&A
- 8: Clear, explains features and process, good Q&A
- 6: Adequate presentation, some explanation
- 4: Unclear or rushed presentation
- 2: Very unclear presentation
- 0: No presentation

**Total: 100 points**

---

# Day 1: Capstone Introduction — Project Options and Requirements

**Session Goal:** Understand the capstone project scope, explore project options, and understand the rubric and expectations for success.

---

## Today's Focus

The capstone is your chance to apply everything you've learned in Units 1–6 to build a real, complete application. Today you'll learn about your options, the requirements, and what success looks like. By the end of class, you'll be excited and ready to start planning your project.

---

## Work Session Agenda

**Minutes 0-10:** **Opening: What is a Capstone?**
- Teacher introduction: capstone as applied learning, real software development
- Demo of a previous student project (3-5 minutes, if available)
- Quick Q&A about scope and expectations

**Minutes 10-40:** **Project Options Presentation**
- Teacher walks through each of the 5 project options (see above)
- For each option: show scope, tech stack required, example features, and why it's a good capstone choice
- Emphasize: **You will choose ONE project to work on for the next 25 days.**

**Minutes 40-55:** **Rubric and Expectations**
- Review the Project Rubric (see above)
- Walk through: code quality, features, documentation, presentation
- Show examples of "excellent," "good," and "needs work"
- Clarify deliverables: working code + README + presentation

---

## Reflection / Exit Ticket

1. Which project option are you most interested in? Why?
2. What is one technical skill from Units 1–6 you want to get really good at during this capstone?

---

## Progress Checklist

- [ ] Attended Day 1 introduction
- [ ] Reviewed all 5 project options
- [ ] Understand the rubric and expectations
- [ ] Have a top 2–3 project choices in mind
- [ ] Exit ticket submitted

---

# Day 2: Project Selection and Brainstorming

**Session Goal:** Choose your capstone project (or pitch a custom one) and brainstorm initial ideas, features, and technical approach.

---

## Today's Focus

Today you commit to a project. Whether you're choosing from the five options or proposing something custom, this is the day you decide what you'll build for the next 24 days. By end of class, you'll have a project approved, a user in mind, and a rough list of features.

---

## Work Session Agenda

**Minutes 0-5:** **Standup: Decision Time**
- Teacher: reminder of approval timeline (custom projects need approval by end of today)
- Quick Q&A: "What if I'm stuck between two options?"

**Minutes 5-45:** **Individual Project Selection & Brainstorming**

For students choosing from Options 1-5:
1. Pick your project option
2. Fill out the **Project Brainstorm Template** (below)
3. Define your target user
4. List 5-7 core features you'll build
5. Note any libraries or tools you'll need

For students proposing a custom project:
1. Pitch your idea (what, who, why)
2. List which Units' concepts you'll apply
3. Get teacher feedback/approval
4. Fill out brainstorm template once approved

**Minutes 45-55:** **Share & Discuss**
- 2-3 volunteers share their project choice and target user
- Teacher feedback: is the scope right? Good fit?

---

## Project Brainstorm Template

```
PROJECT CHOICE: [Option 1/2/3/4/5, or Custom Project Name]

TARGET USER:
Who will use this app? (e.g., "Students wanting to learn Python", "School administrators managing enrollment")

PROBLEM IT SOLVES:
What need does it address?

CORE FEATURES (5-7):
1.
2.
3.
4.
5.

TECH STACK / LIBRARIES:
What languages, frameworks, libraries will you use?

WHY THIS PROJECT:
Why does this excite you? What will you learn?
```

---

## Technical Tips & Resources

**From Unit 2 (OOP):** If your project needs classes, review the class template in the Reference Guide.

**From Unit 4 (File I/O):** Make sure you understand how to read/write JSON and CSV files.

**From Unit 6 (Sorting & Searching):** If your project includes search or sort features, have those concepts ready.

---

## Reflection / Exit Ticket

1. What is your final project choice?
2. Who is your target user?
3. What's one feature you're most excited to build?

---

## Progress Checklist

- [ ] Chose a project option or got custom project approved
- [ ] Target user defined
- [ ] 5-7 core features listed
- [ ] Tech stack identified
- [ ] Brainstorm template completed
- [ ] Ready to start planning on Day 3

---

# Day 3: Planning Phase — Pseudocode and Class Design

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

---

# Day 4: Planning Check-in — Teacher Feedback Session

**Session Goal:** Present your plan to the teacher, get feedback, and refine before you start coding.

---

## Today's Focus

You've planned your project. Now get expert feedback. Meet with your teacher 1-on-1 or in small groups to discuss your design, identify potential issues early, and make sure you're ready to code. By end of class, your plan is solid and you're excited to build.

---

## Work Session Agenda

**Minutes 0-5:** **Standup: Feedback Protocol**
- Teacher: how to give and receive feedback (be specific, kind, focused on improvement)
- Schedule: how check-ins will work (1-on-1 or small group, 5-10 min each)

**Minutes 5-50:** **Individual Check-in Sessions**

Each student meets with teacher for 5-10 minutes:
1. Student briefly presents plan (1-2 min)
2. Teacher asks clarifying questions (2-3 min):
   - Is the scope right?
   - Do you have the skills to build this?
   - What's your biggest risk or blocker?
3. Teacher gives feedback (1-2 min):
   - Strengths of the plan
   - One thing to improve or clarify
4. Student takes notes

While waiting for your turn:
- Review your plan and notes
- Answer any unknowns from your "Key Questions" list
- Prepare a 2-minute summary of your project

**Minutes 50-55:** **Wrap-up & Next Steps**
- Make any final adjustments to your plan
- Confirm: you're ready to start coding tomorrow (Day 5)

---

## Teacher Feedback Form (For Teacher Notes)

```
STUDENT: ______________
PROJECT: ______________

Plan Strengths:
1.
2.

Questions / Concerns:
1.
2.

Recommendation:
[ ] Ready to code — no major issues
[ ] Ready to code — consider this adjustment:
[ ] Not ready yet — please revise:

Next Steps:
```

---

## What Makes a Good Plan?

Teacher will look for:

✓ **Clarity:** Can you explain your project in 1-2 sentences?

✓ **Scope:** Is it achievable in 20 days with intermediate skill?

✓ **Structure:** Do you have a clear data model and class design?

✓ **Learning:** Does it use concepts from Units 1-6?

✓ **Testability:** Will you be able to verify it works?

---

## Common Plan Improvements

**If your scope is too big:**
- Cut non-essential features
- Simplify data model
- Focus on core functionality first

**If your scope is too small:**
- Add an extension feature
- Include more complex search/sort
- Add data persistence or validation

**If your classes are unclear:**
- Write one pseudocode example
- Simplify method signatures
- Define inputs/outputs for each method

---

## Reflection / Exit Ticket

1. What feedback did your teacher give?
2. What's one change you'll make to your plan before coding?
3. Rate your confidence to start coding: 1 (low) to 5 (high). Why?

---

## Progress Checklist

- [ ] Met with teacher for feedback
- [ ] Addressed teacher feedback
- [ ] Plan is finalized and saved
- [ ] Ready to create project structure on Day 5

---

# Day 5: Sprint 1 — Project Setup and Core Structure

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
- Use descriptive class names (e.g., `Student`, not `S`)
- Each class should live in its own file
- Use `__init__` to initialize attributes
- Use docstrings on every class and method

**From Unit 4 (File I/O):**
- Plan your data structure before writing code
- Test with small sample files first
- Use `with open()` for safe file handling

**Common File I/O Pattern:**
```python
import json

def load_data(filename):
    """Load data from JSON file."""
    try:
        with open(filename, 'r') as f:
            return json.load(f)
    except FileNotFoundError:
        return []

def save_data(filename, data):
    """Save data to JSON file."""
    with open(filename, 'w') as f:
        json.dump(data, f, indent=2)
```

---

## Project Structure Template

```
my_project/
├── main.py                 # Entry point
├── README.md              # Project overview
├── src/
│   ├── student.py         # Student class
│   ├── course.py          # Course class
│   ├── system.py          # Main system/manager class
│   └── utils.py           # Helper functions
├── data/
│   ├── students.json      # Data file (initially empty)
│   └── courses.json       # Data file (initially empty)
└── tests/
    └── test_data.json     # Sample data for testing
```

---

## Reflection / Exit Ticket

1. Does your project structure match your plan from Day 3?
2. What's the first feature you'll implement in Sprint 1?
3. Any blockers or questions before Day 6?

---

## Progress Checklist

- [ ] Project folders created (src/, data/, tests/)
- [ ] Main classes skeleton written
- [ ] main.py created and imports classes
- [ ] Code runs without errors
- [ ] All files committed/saved
- [ ] Ready for feature building on Day 6

---

# Day 6: Sprint 1 — Building Core Features (Day 2)

**Session Goal:** Implement the first core features of your application. Build momentum.

---

## Today's Focus

Yesterday you built the skeleton. Today you put meat on the bones. You'll implement core features like loading data, creating records, or fetching API data. By end of day, your app does something real, even if it's not polished.

---

## Work Session Agenda

**Minutes 0-5:** **Sprint Standup**
- What did you accomplish yesterday?
- What are you building today?
- Any blockers?

**Minutes 5-50:** **Feature Implementation**

Pick 1-2 core features and implement them:
- Example: if you're building Student System, implement `add_student()` and `get_summary()` methods
- Example: if you're building Data Analyzer, implement CSV loading and statistics calculation
- Work through these steps:
  1. Write pseudocode (review your plan)
  2. Implement the method body
  3. Test it with sample data
  4. Fix bugs

**Tips:**
- Start with easier features to build confidence
- Test as you go (don't wait until everything is done)
- Use print statements to debug
- Save frequently

**Minutes 50-55:** **Wrap-up & Document**
- Save all changes
- Update progress tracker
- Note what you'll build tomorrow

---

## Code Implementation Tips

**Test as you go:**
```python
# In main.py or a test script
student = Student("Alice", 12345, 3.85)
print(student.get_summary())  # Does it work?
```

**Use print for debugging:**
```python
def add_course(self, course_code):
    print(f"Adding course: {course_code}")  # Debug output
    self.courses.append(course_code)
    print(f"Courses now: {self.courses}")  # Verify
```

**Implement incrementally:**
- Get one method working
- Then move to the next
- Don't try to do everything at once

---

## Feature Checklist for Each Day

For each feature you implement:
- [ ] Code written
- [ ] Tested manually
- [ ] No syntax errors
- [ ] Docstring explains what it does
- [ ] Comments explain "why" if logic is complex

---

## Reflection / Exit Ticket

1. What feature(s) did you implement today?
2. Did it work as expected? Any surprises?
3. What's next?

---

## Progress Checklist

- [ ] 1-2 core features implemented
- [ ] Code tested and working
- [ ] All changes saved
- [ ] Ready for Day 7

---

# Day 7: Sprint 1 — Building Core Features (Day 3)

**Session Goal:** Continue implementing core features. Add more functionality.

---

## Today's Focus

Keep the momentum going. You've got 1-2 features working. Today you'll build 2-3 more. By end of sprint, you'll have all your core features sketched in and mostly working.

---

## Work Session Agenda

**Minutes 0-5:** **Quick Standup**
- Demo what you built yesterday
- Plan for today

**Minutes 5-50:** **Continue Feature Implementation**

Implement the next 2-3 features:
- Example: search, sort, delete
- Example: multiple data formats, filtering
- Example: API queries, data caching

**Test each feature before moving on.**

**Minutes 50-55:** **Wrap-up**
- Save and commit
- Note progress

---

## Testing Strategies

**Manual Testing:**
```python
# Test in main.py
system = StudentSystem()
system.add_student(Student("Alice", 1, 3.85))
system.add_student(Student("Bob", 2, 3.5))
results = system.find_by_name("Alice")
print(results)  # Should print Alice
```

**Test edge cases:**
- Empty list: Does search work on empty system?
- Duplicate: What if you add same student twice?
- Invalid data: What if name is empty string?

---

## Reflection / Exit Ticket

1. How many core features are now working?
2. What's the most complex feature so far?
3. Any features that need more work?

---

## Progress Checklist

- [ ] 2-3 more features implemented
- [ ] All features tested
- [ ] Code runs without errors
- [ ] Ready for Day 8

---

# Day 8: Sprint 1 — Building Core Features (Day 4)

**Session Goal:** Implement remaining core features. Complete Sprint 1.

---

## Today's Focus

This is the final day of Sprint 1. You've built 4-5 features. Today you'll finish the remaining core features and prepare for your first check-in tomorrow. Your app should now have all the core functionality, even if some features need refinement.

---

## Work Session Agenda

**Minutes 0-5:** **Standup**
- How many core features are done?
- What's left for Sprint 1?

**Minutes 5-50:** **Final Core Features**

Implement the last 1-3 core features:
- File I/O (loading/saving data)
- Complex search or sort
- Data persistence
- API integration

**Test thoroughly.** Sprint 1 wrap-up check-in is tomorrow.

**Minutes 50-55:** **Prepare for Tomorrow**
- Save all code
- Make sure everything runs
- Prepare a short demo of what works

---

## Demo Checklist for Tomorrow

Tomorrow you'll demo to a peer. Make sure:
- [ ] App runs without crashing
- [ ] 5+ core features work
- [ ] Data persists if that's part of the project
- [ ] You can explain each feature briefly

---

## Reflection / Exit Ticket

1. Are all core features implemented?
2. What feature are you most proud of?
3. What will you demo tomorrow?

---

## Progress Checklist

- [ ] All core features implemented
- [ ] All features tested
- [ ] Code saves/loads data correctly
- [ ] App runs start to finish without major crashes
- [ ] Ready for check-in demo on Day 9

---

# Day 9: Sprint 1 Check-in — Progress Demo and Blockers

**Session Goal:** Demo your Sprint 1 progress, get feedback, and identify any blockers before moving to Sprint 2.

---

## Today's Focus

You've been building for 4 days. Time to pause, show your work, and get feedback. Peer code review and teacher check-in help you catch bugs early and plan Sprint 2 better. By end of class, you know what's working, what needs fixing, and what to build next.

---

## Work Session Agenda

**Minutes 0-20:** **Peer Demo Pairs**

You and a partner each take 5 minutes to demo your project:
1. **Demo (3 min):** Run your app and show the 3-4 most important features working
2. **Feedback (2 min):** Partner asks one question or gives one compliment

Use the **Peer Code Review Form** (below).

**Minutes 20-40:** **Teacher Check-in (Individual, 2-3 min)**

Meet briefly with teacher:
1. Show that code runs
2. Ask about any blockers or questions
3. Get feedback on code quality so far

**Minutes 40-55:** **Plan Sprint 2**

- Review what you've built (you should have 5+ working features)
- What's left to build? (2 weeks of Sprint 2 ahead)
- Identify any bugs to fix
- List 3-5 features for Sprint 2

---

## Peer Code Review Form

```
REVIEWER: ______________
DEVELOPER: ______________
PROJECT: ______________

DEMO QUESTIONS:
1. What feature are you most proud of?
   ______

2. What's the trickiest part of your code?
   ______

3. What's your biggest challenge right now?
   ______

CODE OBSERVATIONS:
Are there clear class names?        [ ] Yes [ ] Somewhat [ ] No
Are methods well-documented?        [ ] Yes [ ] Somewhat [ ] No
Did the demo crash?                 [ ] No [ ] Minor glitch [ ] Major crash

FEEDBACK:
One thing that went well:
______

One question I have:
______

One suggestion:
______
```

---

## Sprint 1 Retrospective

Answer for yourself:
1. What went smoothly?
2. What was harder than expected?
3. What will you do differently in Sprint 2?

---

## Reflection / Exit Ticket

1. What did feedback reveal about your project?
2. What's one bug or issue you need to fix?
3. What's your #1 goal for Sprint 2?

---

## Progress Checklist

- [ ] Demo completed
- [ ] Feedback received
- [ ] Teacher check-in done
- [ ] Sprint 2 features planned
- [ ] Ready to start Sprint 2 on Day 10

---

# Day 10: Sprint 2 — Adding Features (Day 1)

**Session Goal:** Begin Sprint 2. Implement extended features that enhance core functionality.

---

## Today's Focus

Sprint 1 is done. Time to expand. Sprint 2 is about adding features, improving user experience, and deepening functionality. You've got 7 days to build significant features. Today you'll start with one complex, meaningful feature.

---

## Work Session Agenda

**Minutes 0-5:** **Sprint 2 Kickoff**
- Sprint 2 goal: depth and polish, not just adding features
- Features should be thoughtful, not just "stuff piled on"
- Examples: better error handling, filtering options, data validation

**Minutes 5-50:** **Complex Feature Implementation**

Pick one medium-to-complex feature and really build it out:
- Example: implement a full search system with filters and sorting
- Example: build a complete API integration with caching
- Example: create a reporting or visualization module

Work methodically:
1. Pseudocode the feature
2. Build it incrementally
3. Test thoroughly
4. Refactor for clarity

**Minutes 50-55:** **Wrap-up**
- Save and commit
- Document what you built

---

## Sprint 2 Feature Ideas

Depending on your project:

**Student System:**
- Bulk import students from CSV
- Grade calculation and reporting
- Course enrollment management
- Data validation (GPA must be 0-4, ID unique, etc.)

**Data Analyzer:**
- Advanced filtering (multiple criteria)
- Comparison between datasets
- Trend analysis
- Custom report generation

**API App:**
- Multiple API sources
- Data caching with timestamps
- User preference storage
- Advanced search/filter combinations

**Algorithm Visualizer:**
- Step-through mode (pause between swaps)
- Comparison of multiple algorithms side-by-side
- Performance benchmarking
- Data export to CSV

---

## Reflection / Exit Ticket

1. What feature did you implement?
2. Is it working well?
3. What's next?

---

## Progress Checklist

- [ ] One significant feature implemented
- [ ] Tested and working
- [ ] All changes saved
- [ ] Ready for Day 11

---

# Day 11: Sprint 2 — Adding Features (Day 2)

**Session Goal:** Continue Sprint 2. Build another significant feature. Improve code quality.

---

## Today's Focus

Momentum is good. Yesterday you built one complex feature. Today you'll build another, refining as you go. Pay attention to code quality: clear naming, good comments, proper structure.

---

## Work Session Agenda

**Minutes 0-5:** **Standup**
- Demo yesterday's feature
- Plan today

**Minutes 5-50:** **Feature Implementation + Refactoring**

1. Implement another feature (2-3 days' worth of work)
2. Refactor old code if needed (simplify, improve naming, add comments)
3. Test thoroughly

**Minutes 50-55:** **Wrap-up**
- Save and commit
- Note progress

---

## Code Quality Checklist

As you write code, ask:
- [ ] Is the variable name clear? (use `student_list`, not `sl`)
- [ ] Does the method do one thing? (if not, break it up)
- [ ] Are there docstrings? (on every class and public method)
- [ ] Would someone else understand this code?

---

## Reflection / Exit Ticket

1. How does your code quality feel?
2. What was hard about this feature?
3. What's your confidence level on remaining Sprint 2 features?

---

## Progress Checklist

- [ ] Second major feature implemented
- [ ] Code quality reviewed and improved
- [ ] All tests passing
- [ ] Ready for Day 12

---

# Day 12: Sprint 2 — Connecting Components

**Session Goal:** Integrate your features. Make sure different parts of your app work together smoothly.

---

## Today's Focus

You have individual features built. Now they need to work together. Today you'll connect the dots: make sure file I/O works with search, API results integrate with your data model, visualizations use calculated data, etc. By end of day, your app is a cohesive system, not just separate pieces.

---

## Work Session Agenda

**Minutes 0-5:** **Architecture Standup**
- Teacher: integration overview (how pieces talk to each other)
- Avoid: circular dependencies, repeated code, unclear data flow

**Minutes 5-50:** **Integration Work**

Review your app architecture:
1. Can you load data, then search it? Test it.
2. Can you fetch API data, save it, then visualize it? Test it.
3. Does the menu system reach all features?
4. Do all file paths work?

Build connectors/glue code:
- Main menu that calls feature functions correctly
- Data flows from one component to another
- No duplicate code

Test end-to-end:
- Start app
- Do a complete workflow (load data → search → save → exit)
- Make sure nothing breaks

**Minutes 50-55:** **Wrap-up**
- Save and commit
- Document the data flow if complex

---

## Data Flow Example (Student System)

```
main.py
  │
  ├─→ StudentSystem (manager)
  │     │
  │     ├─→ Student class (individual records)
  │     ├─→ load_from_json() ──→ data/students.json
  │     ├─→ find_by_name()
  │     ├─→ sort_by_gpa()
  │     └─→ save_to_json() ──→ data/students.json
  │
  └─→ Menu loop
        ├─→ calls system.add_student()
        ├─→ calls system.find_by_name()
        └─→ calls system.save_to_json()
```

---

## Integration Testing Checklist

- [ ] Load data → works
- [ ] Search loaded data → works
- [ ] Create new records → works
- [ ] Update records → works
- [ ] Delete records → works
- [ ] Save → works
- [ ] Reload from saved file → works
- [ ] Complete workflow → works without crashes

---

## Reflection / Exit Ticket

1. Do all parts of your app work together?
2. What integration issue took the longest to fix?
3. Is your app starting to feel "done" or is there still a lot of work?

---

## Progress Checklist

- [ ] Components integrated
- [ ] End-to-end workflow tested
- [ ] Menu system connects all features
- [ ] No major crashes
- [ ] Ready for peer review on Day 13

---

# Day 13: Sprint 2 Check-in — Peer Code Review

**Session Goal:** Review peers' code. Get feedback on yours. Share learning.

---

## Today's Focus

Today you're a code reviewer. You'll exchange projects with a peer and review their code quality, design, and structure. You'll give thoughtful feedback, and you'll receive the same. This is how real developers work. By end of class, you'll have specific feedback to improve your code.

---

## Work Session Agenda

**Minutes 0-5:** **Code Review Training**
- Teacher: what to look for in code review
  - Is it readable?
  - Is there duplication?
  - Are there obvious bugs?
  - Are class names clear?
  - Are docstrings present?
- Teacher: how to give kind, constructive feedback

**Minutes 5-40:** **Peer Code Review (Exchange Projects)**

1. You review Partner A's code (15 minutes):
   - Read through main classes
   - Look for clarity, organization, documentation
   - Fill out **Code Review Form** (below)
   - Note 3 strengths and 2 improvement areas

2. Partner A reviews your code (15 minutes):
   - Same process

**Minutes 40-50:** **Feedback Discussion (Paired)**
- Exchange feedback forms
- Discuss 2-3 key points
- Ask clarifying questions

**Minutes 50-55:** **Wrap-up & Plan Improvements**
- Note feedback
- Identify 2-3 things to improve in Sprint 2 Continued

---

## Peer Code Review Form

```
REVIEWER: ______________
AUTHOR: ______________

PROJECT OVERVIEW:
What does this project do?
______

STRENGTHS (3 things that are well done):
1.
2.
3.

AREAS FOR IMPROVEMENT (2 things that could be better):
1. Suggestion:
2. Suggestion:

CODE QUALITY:
Variable/function naming       [ ] Clear [ ] Mostly clear [ ] Confusing
Documentation (docstrings)     [ ] Complete [ ] Partial [ ] Minimal
Organization (classes/modules) [ ] Excellent [ ] Good [ ] Needs work
Comments (explain complex logic) [ ] Yes [ ] Some [ ] No

ARCHITECTURE QUESTION:
How do the main classes interact? Can you explain it?
______

ONE QUESTION FOR THE AUTHOR:
______
```

---

## Common Code Review Feedback

**Good feedback:**
- "This method does two things. Consider splitting it into `search()` and `filter()`."
- "The variable `x` is unclear. What about `student_count`?"
- "Great docstring! This clarifies what the method does."

**Feedback to avoid:**
- "Your code is bad." (Not helpful; not specific)
- "You should have done this differently." (How? Why?)

---

## Reflection / Exit Ticket

1. What feedback surprised you?
2. What's one piece of feedback you'll act on?
3. What's one piece of feedback you'll clarify with your reviewer?

---

## Progress Checklist

- [ ] Reviewed peer's code thoroughly
- [ ] Received feedback on own code
- [ ] Identified 2-3 improvements for next phase
- [ ] Ready to refine code on Day 14

---

# Day 14: Sprint 2 Continued — Refining Features

**Session Goal:** Act on code review feedback. Refine existing features for quality and clarity.

---

## Today's Focus

You got feedback yesterday. Today you act on it. Refactoring and improving code is just as important as adding new features. By end of day, your code is cleaner, more readable, and better organized.

---

## Work Session Agenda

**Minutes 0-5:** **Refactoring Standup**
- Review your feedback form
- Pick top 3 improvements to make

**Minutes 5-50:** **Refactoring & Improvement**

1. Rename unclear variables/functions
2. Break up methods that do too much
3. Add missing docstrings
4. Remove duplicate code
5. Simplify complex logic with comments

**Test after each change.** Refactoring should not break existing features.

**Minutes 50-55:** **Wrap-up**
- Save and commit
- Document improvements

---

## Refactoring Techniques

**Rename for clarity:**
```python
# Before
def f(s):
    return len(s)

# After
def count_students(students):
    """Return the number of students."""
    return len(students)
```

**Extract duplicated code:**
```python
# Before
class StudentSystem:
    def find_by_name(self, name):
        for s in self.students:
            if s.name.lower() == name.lower():
                return s
        return None

    def find_by_id(self, sid):
        for s in self.students:
            if s.student_id == sid:
                return s
        return None

# After
class StudentSystem:
    def _find_student(self, predicate):
        """Helper: find first student matching predicate."""
        for s in self.students:
            if predicate(s):
                return s
        return None

    def find_by_name(self, name):
        return self._find_student(lambda s: s.name.lower() == name.lower())

    def find_by_id(self, sid):
        return self._find_student(lambda s: s.student_id == sid)
```

---

## Reflection / Exit Ticket

1. What code quality improvements did you make?
2. Does your code feel better organized now?
3. Ready to expand features more on Day 15?

---

## Progress Checklist

- [ ] Reviewed feedback form
- [ ] Made 3+ code improvements
- [ ] All tests still pass
- [ ] Code is cleaner and more readable
- [ ] Ready for Day 15

---

# Day 15: Sprint 2 Continued — Expanding Features

**Session Goal:** Build additional features or expand on existing ones. Deepen functionality.

---

## Today's Focus

You've cleaned up your code. Now expand it. Add more sophisticated features: advanced filtering, complex calculations, multiple data sources, better error handling, etc. Your app is getting close to feature-complete.

---

## Work Session Agenda

**Minutes 0-5:** **Feature Expansion Standup**
- What features are still on your Sprint 2 list?
- Pick 1-2 to fully implement today

**Minutes 5-50:** **Feature Implementation**

Add depth to your app:
- More search options
- Better validation
- Additional algorithms
- More data sources or formats
- Better user experience

**Minutes 50-55:** **Wrap-up**
- Save and commit
- Test everything

---

## Feature Expansion Ideas

**Student System:**
- Bulk operations (add 10 students at once)
- Grade tracking and GPA auto-calculation
- Course prerequisites
- Student statistics report (avg GPA, enrollment by course)

**Data Analyzer:**
- Grouping data by field (stats by category)
- Outlier detection
- Data comparison (before/after, dataset A vs B)
- Export to multiple formats (JSON, CSV, HTML)

**API App:**
- Favorite/bookmark feature
- Search history
- Data comparison across multiple searches
- Notification alerts

---

## Reflection / Exit Ticket

1. What features did you add?
2. How much work remains?
3. On a scale of 1-5, how "done" does your app feel?

---

## Progress Checklist

- [ ] 1-2 expansion features implemented
- [ ] All code tested
- [ ] No new bugs introduced
- [ ] Ready for integration on Day 16

---

# Day 16: Sprint 2 Continued — Integration and Testing

**Session Goal:** Integrate new features, test thoroughly, ensure everything works together.

---

## Today's Focus

You've added a lot of features. Today is about making sure it all works together and finding/fixing bugs. By end of day, your app is solid and you're confident in its functionality.

---

## Work Session Agenda

**Minutes 0-5:** **Integration & Testing Standup**
- What features are complete?
- What needs testing?
- Are there known bugs?

**Minutes 5-50:** **Testing & Integration**

1. **End-to-end testing**
   - Start the app
   - Use every feature in realistic scenarios
   - Look for crashes, logic errors, unexpected behavior

2. **Edge case testing**
   - Empty data
   - Very large data
   - Invalid inputs
   - Boundary conditions

3. **Bug fixing**
   - Document bugs you find
   - Fix the critical ones
   - Note minor ones for later

4. **Integration verification**
   - Do all features work with each other?
   - Is data consistent across features?
   - Can you save and reload without data loss?

**Minutes 50-55:** **Wrap-up**
- Save and commit
- List remaining issues for Sprint 3

---

## Testing Checklist

For each feature:
- [ ] Works with valid input
- [ ] Handles invalid input gracefully
- [ ] Works with empty data
- [ ] Works with large data
- [ ] Integrates with other features
- [ ] Doesn't crash on edge cases

---

## Common Bugs to Look For

- File I/O: What if file doesn't exist? What if it's empty or corrupted?
- Search: What if no results? What if search term is empty?
- Sort: What if list is empty? What if items are missing a sort field?
- User input: What if user enters letters instead of numbers?

---

## Reflection / Exit Ticket

1. What bugs did you find and fix?
2. Is there a feature you're still worried about?
3. Are you ready for Sprint 3 (polish and testing)?

---

## Progress Checklist

- [ ] All features tested
- [ ] Critical bugs fixed
- [ ] Integration verified
- [ ] App is stable
- [ ] Ready for Sprint 3 on Day 17

---

# Day 17: Sprint 3 — Polish and Error Handling

**Session Goal:** Add comprehensive error handling and polish your code. Make your app robust.

---

## Today's Focus

Sprint 1 built features. Sprint 2 expanded them. Sprint 3 is about robustness and polish. Add error handling, validate inputs, provide user-friendly messages. By end of day, your app gracefully handles problems instead of crashing.

---

## Work Session Agenda

**Minutes 0-5:** **Standup: Sprint 3 Goals**
- Sprint 3 is the "final" sprint: quality over quantity
- Focus: error handling, documentation, testing
- Presentation is 5 days away

**Minutes 5-50:** **Error Handling & Validation**

1. Add try/except blocks where things can fail:
   - File I/O
   - API requests
   - Data parsing
   - User input

2. Validate input:
   - Is a number actually a number?
   - Is a file path valid?
   - Is the data in the expected format?

3. Provide good error messages:
   - Tell users what went wrong
   - Suggest how to fix it
   - Don't expose raw stack traces

4. Handle edge cases:
   - Empty lists
   - None values
   - Unexpected data types

**Minutes 50-55:** **Wrap-up**
- Save and commit
- Test error cases

---

## Error Handling Example

```python
def load_data(filename):
    """
    Load student data from JSON file.

    Args:
        filename (str): Path to JSON file

    Returns:
        list: List of student data, or empty list on error
    """
    try:
        with open(filename, 'r') as f:
            return json.load(f)
    except FileNotFoundError:
        print(f"Error: File '{filename}' not found.")
        print("Creating new empty data file.")
        return []
    except json.JSONDecodeError:
        print(f"Error: File '{filename}' is not valid JSON.")
        print("Starting with empty data.")
        return []
    except Exception as e:
        print(f"Unexpected error reading file: {e}")
        return []
```

---

## Input Validation Example

```python
def get_student_id(prompt):
    """Get a valid student ID from user (must be a positive integer)."""
    while True:
        try:
            user_input = input(prompt)
            student_id = int(user_input)
            if student_id <= 0:
                print("Student ID must be a positive number.")
                continue
            return student_id
        except ValueError:
            print(f"'{user_input}' is not a valid number. Please try again.")
```

---

## Error Handling Checklist

- [ ] File operations wrapped in try/except
- [ ] API requests handle timeouts and failures
- [ ] User input is validated before use
- [ ] Missing or invalid data doesn't crash the app
- [ ] Error messages are helpful (not generic)
- [ ] App continues running after an error (unless critical)

---

## Reflection / Exit Ticket

1. What error cases did you identify?
2. Which error handling was hardest to add?
3. Does your app feel more robust now?

---

## Progress Checklist

- [ ] Comprehensive error handling added
- [ ] User input validated
- [ ] Edge cases handled
- [ ] Helpful error messages provided
- [ ] App is robust and doesn't crash
- [ ] Ready for testing on Day 18

---

# Day 18: Sprint 3 — Testing and Debugging (Day 2)

**Session Goal:** Systematic testing and bug fixing. Document test results.

---

## Today's Focus

You've added error handling. Now systematically test your entire app. Create a list of test cases and verify each one. Document what you test. By end of day, you have confidence your app works as intended.

---

## Work Session Agenda

**Minutes 0-5:** **Testing Strategy Standup**
- Teacher: systematic testing approach
- Create a **Test Plan** (list of all features to test)
- For each feature, list the test cases

**Minutes 5-50:** **Systematic Testing**

1. **Create a Test Plan Document**
   ```
   Feature: Add Student
   - Test Case 1: Add a valid student → Check student appears in list
   - Test Case 2: Add duplicate ID → Check error message
   - Test Case 3: Add with missing info → Check validation error

   Feature: Search by Name
   - Test Case 1: Exact match → Should find student
   - Test Case 2: Partial match → Should find students
   - Test Case 3: No match → Should return empty, no crash
   ```

2. **Run each test case**
   - Note results (passed/failed)
   - If failed, fix the bug
   - Re-test

3. **Document findings**
   - What worked well?
   - What bugs did you find?
   - What's fixed?

**Minutes 50-55:** **Wrap-up**
- Save test plan
- Commit all fixes

---

## Test Plan Template

```
PROJECT: [Name]
DATE: [Date]
TESTER: [Name]

FEATURE: [Feature Name]

Test Case 1: [Description]
  Steps: [What you do]
  Expected: [What should happen]
  Actual: [What actually happened]
  Status: [ ] PASS [ ] FAIL
  Notes: [Any observations]

Test Case 2: [Description]
  Steps:
  Expected:
  Actual:
  Status: [ ] PASS [ ] FAIL
  Notes:

...
```

---

## Bug Reporting

When you find a bug, note:
1. What were you doing? (Steps to reproduce)
2. What did you expect?
3. What actually happened?
4. Is it critical (app crashes) or minor (display issue)?

---

## Reflection / Exit Ticket

1. How many test cases did you run?
2. How many bugs did you find and fix?
3. Do you feel confident your app works?

---

## Progress Checklist

- [ ] Test plan created
- [ ] All features tested
- [ ] Critical bugs fixed
- [ ] Test results documented
- [ ] Ready for Day 19

---

# Day 19: Sprint 3 — Testing and Debugging (Day 3)

**Session Goal:** Continue systematic testing. Fix remaining bugs. Verify stability.

---

## Today's Focus

Keep testing. You've tested main features. Now test interactions, stress test with large data, test boundary cases. By end of day, your app is as stable as you can make it.

---

## Work Session Agenda

**Minutes 0-5:** **Standup**
- What bugs remain from yesterday?
- What edge cases need testing today?

**Minutes 5-50:** **Advanced Testing**

1. **Stress testing** — large data, many operations
   - Can your app handle 1000 students?
   - Can it search large datasets quickly?
   - Does it run out of memory?

2. **Integration testing** — feature interactions
   - Add data, search, delete, save, reload
   - Do operations on different features interfere?

3. **Boundary testing** — extreme values
   - Highest/lowest grades
   - Longest names
   - Special characters in input

4. **Bug fixes**
   - Fix any bugs found

**Minutes 50-55:** **Wrap-up**
- Save and commit
- Update test results

---

## Stress Testing Example

```python
import time

# Test with large dataset
students = []
for i in range(1000):
    students.append(Student(f"Student {i}", i, 3.5 + (i % 10) * 0.01))

system = StudentSystem()
for student in students:
    system.add_student(student)

# Time a search operation
start = time.time()
results = system.find_by_name("Student 500")
elapsed = time.time() - start

print(f"Found {len(results)} students in {elapsed:.4f} seconds")

# Save and reload time
start = time.time()
system.save_to_json("test_1000.json")
system2 = StudentSystem()
system2.load_from_json("test_1000.json")
elapsed = time.time() - start
print(f"Save/load 1000 students in {elapsed:.4f} seconds")
```

---

## Reflection / Exit Ticket

1. How does your app handle stress/large data?
2. Any remaining bugs?
3. Are you ready to document on Day 20?

---

## Progress Checklist

- [ ] Stress tested with large data
- [ ] Integration tested
- [ ] Boundary cases tested
- [ ] Remaining bugs fixed
- [ ] App is stable
- [ ] Ready for documentation on Day 20

---

# Day 20: Sprint 3 — Documentation (Docstrings, Comments, README)

**Session Goal:** Write comprehensive documentation for your project. Make it understandable to others.

---

## Today's Focus

Your code works. Now document it. Write a great README, add docstrings to every function, add clarifying comments. By end of day, someone else (or future you) can understand and use your code.

---

## Work Session Agenda

**Minutes 0-5:** **Documentation Standup**
- Teacher: what makes good documentation
- Standard: README, docstrings, inline comments

**Minutes 5-50:** **Write Documentation**

1. **README.md**
   - Project overview
   - How to install and run
   - Features list
   - How to use (with examples)
   - Project structure
   - Technical notes

2. **Docstrings**
   - Every class: brief description + attributes
   - Every method/function: purpose, args, returns
   - Use Google/NumPy docstring style (consistent)

3. **Inline comments**
   - Comment "why", not "what"
   - Explain tricky logic
   - Warn about edge cases

4. **Code structure clarity**
   - Ensure files are organized logically
   - Group related functions
   - Use clear naming

**Minutes 50-55:** **Wrap-up**
- Save all documentation
- Commit

---

## README Template

```markdown
# Project Name

## Overview
[1-2 sentences: what does this project do?]

## Features
- Feature 1
- Feature 2
- Feature 3

## Installation
1. Clone or download the project
2. Install dependencies (if any): `pip install -r requirements.txt`
3. Place data files in the `data/` folder (if applicable)

## How to Run
```bash
python main.py
```

## How to Use
[Walk through typical workflow with examples]

Example:
```
$ python main.py
Welcome to Student Information System
1. Add student
2. View all students
3. Search by name
4. Exit

> 1
Enter name: Alice Smith
Enter ID: 12345
Enter GPA: 3.85
Student added!
```

## Project Structure
```
project/
├── main.py          # Entry point
├── student.py       # Student class
├── system.py        # StudentSystem class
├── data/
│   └── students.json
└── README.md
```

## Technical Notes
[Any important implementation details, design decisions, known limitations]

## Author
[Your name]
```

---

## Docstring Example

```python
class Student:
    """
    Represents a student record.

    Attributes:
        name (str): Student's full name
        student_id (int): Unique student ID
        gpa (float): Current GPA (0-4)
        courses (list): List of course codes
    """

    def add_course(self, course_code):
        """
        Add a course to this student's enrollment.

        Args:
            course_code (str): Course code (e.g., "CS101")

        Returns:
            bool: True if added successfully, False if already enrolled

        Raises:
            ValueError: If course_code is empty or invalid format
        """
        if not course_code or not isinstance(course_code, str):
            raise ValueError("Course code must be a non-empty string")

        if course_code in self.courses:
            return False

        self.courses.append(course_code)
        return True
```

---

## Documentation Checklist

- [ ] README.md completed
- [ ] Every class has a docstring
- [ ] Every public method has a docstring
- [ ] Docstrings include Args, Returns, Raises where applicable
- [ ] Tricky code has comments explaining "why"
- [ ] File structure is clear and organized
- [ ] Installation and usage instructions are clear

---

## Reflection / Exit Ticket

1. Does your README explain what the project does?
2. Are all functions well-documented?
3. Would someone else understand your code?

---

## Progress Checklist

- [ ] README written and complete
- [ ] All classes documented
- [ ] All public methods documented
- [ ] Inline comments added where needed
- [ ] Documentation is clear and comprehensive
- [ ] Ready for final polish on Day 21

---

# Day 21: Final Polish and Submission Prep

**Session Goal:** Final cleanup, last-minute fixes, prepare all materials for submission.

---

## Today's Focus

You're almost done. Today is final polish: fix last-minute bugs, ensure code is clean, make sure all files are in order, and prepare what you'll submit. By end of day, your project is submission-ready.

---

## Work Session Agenda

**Minutes 0-5:** **Final Checklist Standup**
- Teacher: submission requirements recap
- What does the submission folder need to contain?

**Minutes 5-50:** **Final Polish & Submission Prep**

1. **Code cleanup**
   - Remove debug print statements
   - Remove unused imports or variables
   - Ensure consistent indentation/style
   - Final review of error handling

2. **Test one more time**
   - Full run-through of app
   - No crashes, no obvious bugs

3. **File organization**
   - All files in project folder
   - Data files present (sample data for testing)
   - README in root directory
   - `main.py` is the entry point

4. **Submission checklist**
   - [ ] Code runs without errors
   - [ ] README.md is complete
   - [ ] All docstrings are present
   - [ ] Sample data files included
   - [ ] No debug code left
   - [ ] All files organized

5. **Create submission package**
   - Zip the project folder
   - Name it: `[YourName]_Capstone_[ProjectName].zip`
   - Or keep as folder if submitting digitally

**Minutes 50-55:** **Wrap-up & Prepare**
- Verify submission is complete
- Prepare presentation materials (choose demo approach)
- Practice your 2-minute intro

---

## Submission Checklist

Your submission must include:
- [ ] `main.py` — runs without errors
- [ ] All Python source files (organized in `src/` folder if possible)
- [ ] `README.md` — clear, complete, explains project and how to run it
- [ ] Sample data or sample input (so evaluator can test)
- [ ] Documentation — docstrings, comments
- [ ] (Optional) `requirements.txt` if you use external libraries

---

## Presentation Format Decision

Choose one for Days 23-24:

**Option A: Live Demo (Recommended)**
- Pro: Engaging, shows it really works
- Con: Risk of crash
- Structure: Intro (30s) → Demo features (5 min) → Q&A

**Option B: Slides + Code Walkthrough**
- Pro: Safe, can pause and explain
- Con: Less engaging
- Structure: Title slide → Screenshots/overview (2 min) → Code walkthrough (3 min) → Q&A

---

## Reflection / Exit Ticket

1. Is your submission complete and ready?
2. What feature are you most proud of?
3. What's your presentation approach: live demo or slides?

---

## Progress Checklist

- [ ] All code cleaned up
- [ ] Final tests passed
- [ ] README complete and clear
- [ ] All files organized and in submission folder
- [ ] Submission checklist verified
- [ ] Ready for presentation prep on Day 22

---

# Day 22: Presentation Preparation & Peer Feedback

**Session Goal:** Finalize presentation materials. Practice and get feedback. Be ready for showtime.

---

## Today's Focus

Tomorrow and the next day, you present. Today is dress rehearsal. You'll practice your demo, get feedback, and make last-minute improvements. By end of day, you'll feel confident and polished.

---

## Work Session Agenda

**Minutes 0-10:** **Presentation Expectations**
- Teacher: intro to capstone presentations (5–7 minutes, followed by Q&A)
- Format: live demo of working app (preferred) OR slides + code walkthrough
- What evaluators are looking for: clear communication, understanding of code, ability to answer questions
- Ground rules: kind, respectful feedback

**Minutes 10-50:** **Practice & Peer Feedback (8 min per student)**

For each student:
1. Student gives 5–7 minute presentation (demo or slides)
2. Peer observers fill out **Presentation Feedback Form** (see below)
3. Brief discussion (1 min): what worked? What could improve?
4. Student notes feedback for final polish

**Minutes 50-55:** **Final Adjustments**
- Note feedback
- Make quick improvements (clarify demo points, fix timing, practice tricky transitions)
- Rest and prepare for presentations tomorrow

---

## Presentation Feedback Form

**Presenter Name:** ________________
**Date:** ________________

### Clarity
Did you understand what the project does?
- [ ] Yes, very clear
- [ ] Mostly clear
- [ ] Confused

What was most clearly explained?
________________

What was confusing?
________________

### Content
Which features did the presenter demo?
- [ ]
- [ ]
- [ ]

Did the code work without crashing?
- [ ] Yes
- [ ] Mostly (minor glitch)
- [ ] No

### Communication
Did the presenter speak clearly and confidently?
- [ ] Yes
- [ ] Mostly
- [ ] Could improve

Did the presenter explain their design/architecture?
- [ ] Yes, clear explanation
- [ ] Somewhat
- [ ] Not really

### Strengths (What went well?)
1. ________________
2. ________________

### Suggestions (What could improve?)
1. ________________
2. ________________

### One Compliment
________________

---

## Presentation Formats

Choose what works best for you:

### Format 1: Live Demo (Recommended)
- Run your app on the projector
- Walk through features as you use them
- More engaging, shows it really works
- Risk: something might crash (have backup plan)

**Structure:**
1. Intro (30 sec): "I built X. Here's what it does."
2. Demo (4–5 min): Show key features
3. Q&A (1–2 min): Answer questions

**Demo script example:**
```
"Welcome. I built a Student Information System to help schools manage student records.
Let me show you how it works.

First, I'll add a student. [Type name, ID, GPA → student appears in list]
Now I'll search for that student. [Search → finds it]
I can also sort by GPA. [Sort → list reorganizes]
And I can save the data. [Save → file updates]
Finally, if I restart the app and load the data... [Restart, load → data is still there]

Any questions?"
```

### Format 2: Slides + Code Walkthrough
- Create 5-7 slides with screenshots/overview
- Walk through code structure
- Safer than live demo

**Structure:**
1. Title slide (project name, your name)
2. Overview slide (what it does, who uses it)
3. Features slide (list key features)
4. Architecture slide (class diagram or file structure)
5. Code walkthrough (show and explain 2-3 important methods)
6. Conclusion (what you learned)
7. Q&A

---

## Demo Troubleshooting

If something crashes during demo:
- Stay calm
- Say: "Let me reload that..."
- Have a backup plan (screenshot, video, or restart app)
- Move on — the crash shows you're testing realistic scenarios!

---

## Practice Tips

- Practice out loud at least 2 times
- Time yourself (should be 5-7 minutes)
- Don't memorize; know your talking points
- Be ready to answer: "What was the hardest part?" and "What would you add next?"

---

## Reflection / Exit Ticket

1. How did your practice presentation go?
2. What feedback will you act on?
3. How confident do you feel (1-5)?

---

## Progress Checklist

- [ ] Chose presentation format
- [ ] Practiced presentation
- [ ] Received peer feedback
- [ ] Made improvements
- [ ] Ready to present on Days 23-24

---

# Day 23: Project Presentations (Day 1)

**Session Goal:** Present your capstone project. Explain your work and answer questions.

---

## Today's Focus

Presentation time! You've built something real. Today you show it to the class and explain what you built, how it works, and what you learned. Be proud of your work.

---

## Work Session Agenda

**Minutes 0-5:** **Presentation Reminders**
- Order of presentations
- Ground rules: respectful, supportive audience
- Each presentation is 5-7 min + 1-2 min Q&A

**Minutes 5-55:** **Student Presentations (8 min per student, 6-7 presentations)**

For each student:
1. Introduce yourself and your project
2. Demo or walkthrough (5-7 min)
3. Answer questions from classmates and teacher (1-2 min)
4. Teacher provides verbal feedback

**Teacher evaluates using the Rubric (see Day 1).**

---

## What to Do If Something Goes Wrong

- **App crashes:** Have a backup or video
- **Technical issue:** Take a screenshot or walk through the code
- **Forgot what to say:** Look at your notes or ask for a moment
- **Nervous:** Breathe, remember you've practiced, and the class is rooting for you

---

## Audience Questions to Expect

- "What was the hardest part?"
- "Why did you design it that way?"
- "What would you add if you had more time?"
- "Did you use anything from Unit X?"
- "How long did this take?"

---

## Reflection / Exit Ticket

1. How did your presentation feel?
2. What questions did you get?
3. What's one thing you'd change about your project?

---

## Progress Checklist

- [ ] Presented your project
- [ ] Answered questions
- [ ] Received feedback
- [ ] Ready for Day 24

---

# Day 24: Project Presentations (Day 2)

**Session Goal:** Continue presentations. Celebrate everyone's work.

---

## Today's Focus

If you presented yesterday, today you're in the audience. If you present today, it's your turn to shine. Either way, it's a celebration of the work everyone has done over the past 25 days.

---

## Work Session Agenda

**Minutes 0-5:** **Standup**
- Remaining presentations
- Appreciation for Day 23 presenters

**Minutes 5-55:** **Continue Student Presentations**

Same format as Day 23: 8 min per student (demo + Q&A).

---

## Audience Participation

If you're watching:
- Listen actively
- Ask respectful questions
- Celebrate classmates' work
- Notice techniques you could use in the future

---

## Reflection / Exit Ticket

1. What projects impressed you?
2. What's one technique you saw that you want to learn?
3. How do you feel about your own project compared to others?

---

## Progress Checklist

- [ ] All presentations completed
- [ ] Everyone received feedback
- [ ] Work is celebrated
- [ ] Ready for wrap-up on Day 25

---

# Day 25: Course Wrap-up, Reflection, and Celebration

**Session Goal:** Reflect on the capstone and the entire Coding 2 course. Celebrate your growth.

---

## Today's Focus

Today is about reflection and celebration. You've spent 6 units and 25 days on this capstone. You've gone from planning to a finished project. Today you celebrate your growth and set goals for the future.

---

## Work Session Agenda

**Minutes 0-10:** **Course Reflection**
- Teacher: reflection on the capstone and the entire course
- Highlight growth from Unit 1 to Unit 7
- Celebrate achievements

**Minutes 10-30:** **Individual Reflection (Written)**

Each student completes the **Self-Assessment Form** (below).

**Minutes 30-45:** **Group Sharing**
- 3-4 volunteers share their biggest learning
- Discuss growth, challenges overcome, skills gained

**Minutes 45-55:** **Celebration & Looking Forward**
- Awards/recognition (best features, best code, most creative, etc.)
- Discuss future learning paths (advanced Python, web development, etc.)
- Final thoughts and goodbyes

---

## Self-Assessment Form

```
PROJECT NAME: ______________
YOUR NAME: ______________

LEARNING TARGETS (Rate 1-5, where 5 = excellent mastery)

I can plan a software project using pseudocode and class diagrams
Rating: ___  Comments:

I can apply OOP design to structure a real program
Rating: ___  Comments:

I can implement file I/O for data persistence
Rating: ___  Comments:

I can use APIs or external libraries in a working application
Rating: ___  Comments:

I can apply sorting and searching to real data
Rating: ___  Comments:

I can handle errors and edge cases with exception handling
Rating: ___  Comments:

I can write clean, documented, readable code
Rating: ___  Comments:

I can present and explain my work to an audience
Rating: ___  Comments:

REFLECTION QUESTIONS:

1. What was your biggest challenge during the capstone?

2. How did you overcome it?

3. What's the part of your project you're most proud of?

4. What would you do differently if you started over?

5. What's one skill you significantly improved on?

6. What's one concept you still want to learn more about?

7. How has your understanding of software development changed?

8. What's your next goal as a programmer?

FEEDBACK:

One thing the teacher did well:

One thing that could have been better:

Will you continue programming after this course?
[ ] Yes, definitely
[ ] Maybe
[ ] No
[ ] Unsure

If yes, what do you want to build next?
```

---

## Course Growth Reflection

Looking back:
- **Unit 1:** Functions and fundamentals
- **Unit 2:** Object-oriented programming
- **Unit 3:** Debugging and testing
- **Unit 4:** File I/O and data handling
- **Unit 5:** APIs and external libraries
- **Unit 6:** Algorithms and complexity
- **Unit 7:** Putting it all together — your capstone

You've learned to think like a programmer, design systems, and build real applications.

---

## Future Learning Paths

Depending on your interests:

**Web Development:**
- Django (Python web framework)
- Flask (lightweight Python framework)
- JavaScript, HTML, CSS

**Data Science:**
- Pandas, NumPy, Matplotlib
- Machine learning with scikit-learn or TensorFlow

**Game Development:**
- Pygame, Godot

**Mobile Development:**
- iOS (Swift), Android (Java/Kotlin), React Native

**Systems & Algorithms:**
- Advanced data structures
- Competitive programming
- Systems design

---

## Celebration Ideas

- Share best features or coolest code snippets
- Award recognition: Most Creative, Best Code Quality, Persistence Award, etc.
- Group photo
- Reflect on favorites from the course

---

## Reflection / Exit Ticket

1. What's one thing you'll take away from this course?
2. Will you keep programming? Why or why not?
3. Thanks to the teacher/classmates for one specific thing.

---

## Progress Checklist

- [ ] Completed self-assessment
- [ ] Participated in reflection
- [ ] Attended celebration
- [ ] Course complete!
- [ ] Ready for your next programming adventure

---

# Planning Templates

## Pseudocode Template

```
FEATURE NAME:

MAIN STEPS:
1. [First major step]
   a. [Sub-step]
   b. [Sub-step]
2. [Second major step]
   a. [Sub-step]
3. [Handle edge cases / errors]
   - What if [condition]?
   - What if [condition]?

EXAMPLE WALKTHROUGH:
If we run this with [sample input], the steps would be:
1. [What happens]
2. [What happens]
3. [What happens]
Result: [Expected output]
```

---

## Class Design Template

```
CLASS NAME: [Name]

PURPOSE: [One-sentence description]

ATTRIBUTES:
- name (type): description
- name (type): description

METHODS:
- method_name(parameters) -> return_type
  Purpose: [What it does]
  Parameters: [Describe each]
  Returns: [What it returns]

- method_name(parameters) -> return_type
  Purpose: [What it does]
  Parameters: [Describe each]
  Returns: [What it returns]

SPECIAL CONSIDERATIONS:
- [Any important notes about this class]
```

---

## File Structure Template

```
project_name/
├── main.py                 # Entry point
├── README.md              # Documentation
├── src/                   # Source code
│   ├── class1.py
│   ├── class2.py
│   └── utils.py
├── data/                  # Data files
│   ├── input_data.json
│   └── output_data.json
└── tests/                 # Test files
    └── test_data.json
```

---

## Sprint Planning Worksheet

### Sprint 1 (Days 5-9)
**Goal:** Build core features and foundation

Features to implement:
1. [ ]
2. [ ]
3. [ ]
4. [ ]
5. [ ]

Blockers/Questions:
-
-

Success criteria:
- [ ] All core features sketched in code
- [ ] App runs without crashing
- [ ] Basic data I/O works
- [ ] Can demo to peer

---

### Sprint 2 (Days 10-16)
**Goal:** Expand functionality and integrate features

Features to implement:
1. [ ]
2. [ ]
3. [ ]

Refinements/Fixes from Sprint 1:
1. [ ]
2. [ ]

Success criteria:
- [ ] All features integrated
- [ ] Code quality improved
- [ ] Testing in progress
- [ ] App is feature-complete

---

### Sprint 3 (Days 17-21)
**Goal:** Polish, document, and finalize

Tasks:
1. [ ] Comprehensive error handling
2. [ ] Full documentation
3. [ ] Final testing
4. [ ] Code cleanup

Success criteria:
- [ ] App is robust (handles errors gracefully)
- [ ] README is complete
- [ ] All code is documented
- [ ] Ready for submission

---

# Peer Review Form

```
CODE REVIEWER: ______________
CODE AUTHOR: ______________
DATE: ______________

OVERALL IMPRESSION:
What does this project do?
______

STRENGTHS (3 things done well):
1. ______
2. ______
3. ______

CODE QUALITY:
Variable/function naming (clear, descriptive)    [ ] Excellent [ ] Good [ ] Fair [ ] Poor
Organization (logical structure, files)         [ ] Excellent [ ] Good [ ] Fair [ ] Poor
Comments and docstrings                         [ ] Excellent [ ] Good [ ] Fair [ ] Poor
Error handling                                  [ ] Excellent [ ] Good [ ] Fair [ ] Poor

SPECIFIC FEEDBACK:

Question 1: [Ask about a specific design choice]
______

Suggestion 1: [Give one constructive suggestion]
______

Suggestion 2: [Give another suggestion]
______

WHAT CONFUSED YOU (If anything):
______

ONE THING TO IMPROVE BEFORE SUBMISSION:
______

FINAL THOUGHTS:
______
```
