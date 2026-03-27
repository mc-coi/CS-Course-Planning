# Coding II — Full Year Course Materials

A complete, standards-aligned Python programming course for high school students. Built for a full academic year (36 weeks) meeting 5 days per week (180 total class sessions), covering Python intermediate concepts from data structures through capstone project development with expanded depth, practice, and project time.

---

## Course Overview

| | |
|---|---|
| **Language** | Python 3 |
| **Duration** | 36 weeks · 5 days/week · 55 min/session |
| **Total Sessions** | 180 class days |
| **Standards** | Tennessee Coding II Standards |
| **Units** | 7 |

---

## Folder Structure

Each unit folder contains the same set of materials:

```
Unit N - [Name]/
├── Daily Lesson Plans/
│   ├── Word/                   Daily lesson plan .docx files
│   └── PDF/                    Daily lesson plan .pdf files
├── Daily Notes/                Complete daily study guides (Day1.md … DayN.md)
├── ReferenceGuide.md           Key terms, syntax, common mistakes
├── UnitPractice.md             Practice problems for the unit
├── UnitAssessment.md           Formal assessment with answer key
└── Unit N - [Name].md          Full unit overview and all daily content combined
```

The root folder also contains `TN_Coding_II_Trad_Full_Year_Standards_Alignment.pdf` — a full-year standards mapping document.

---

## Getting Started — Installing Python

Before students can write code, they need Python and a code editor. Here's how to get set up:

### On a Windows Machine
1. **Install Python** — Open the Microsoft Store, search for "Python," and install it (free).
2. **Install Visual Studio Code** — Open the Microsoft Store, search for "Visual Studio Code," and install it (free).
3. **Install the Python Extension in VS Code** — Open VS Code, click Extensions (`Ctrl+Shift+X`), search "Python," and install the official Microsoft extension.

### On a Chromebook (Also Works on Windows/Mac If You Can't Install Software)
Use **Kira Learning** — a free, browser-based Python IDE with no installation required.
- Main site: [app.kira-learning.com](https://app.kira-learning.com)
- Direct IDE link: [app.kira-learning.com/ide/](https://app.kira-learning.com/ide/)

---

## Units at a Glance

| Unit | Title | Days | Class Days | Standard |
|------|-------|------|------------|----------|
| 1 | Data Structures | 22 | 1–22 | 9-12.CCI.2 |
| 2 | Object-Oriented Programming | 30 | 23–52 | 9-12.CCI.1 |
| 3 | Advanced Functions & Algorithms | 27 | 53–79 | 9-12.CCI.3 |
| 4 | File I/O & Data Processing | 26 | 80–105 | 9-12.CCI.4 |
| 5 | Sorting, Searching & Recursion | 28 | 106–133 | 9-12.CCI.3 |
| 6 | APIs & External Libraries | 22 | 134–155 | 9-12.CCI.4/.5 |
| 7 | Capstone Project | 25 | 156–180 | 9-12.CCI.5 |

---

## Unit Descriptions

### Unit 1 — Data Structures (Days 1–22)
Students master Python's core collection types with expanded time for deep exploration and practice. Topics: lists (creation, indexing, slicing, methods, iteration), list comprehensions, nested lists and 2D arrays, tuples (immutable sequences, packing/unpacking), dictionaries (creation, methods, nested structures), sets and frozensets, and choosing appropriate data structures for given problems. Ends with a full student gradebook project.

**TN Standard 9-12.CCI.2:** Use and manipulate collection data structures

### Unit 2 — Object-Oriented Programming (Days 23–52)
Students learn to design and build programs around objects. Topics: classes and objects, `__init__` and `self`, instance vs class variables, `@classmethod` and `@staticmethod`, encapsulation with private attributes and `@property`, inheritance with `super()`, method overriding, polymorphism, duck typing, special/dunder methods (`__str__`, `__repr__`, `__len__`, `__eq__`, `__add__`, `__iter__`), abstract classes (`abc` module), composition vs inheritance, and design pattern introductions (Singleton, Factory). Ends with a multi-class OOP application project.

**TN Standard 9-12.CCI.1:** Use an object-oriented programming language with classes and objects

### Unit 3 — Advanced Functions & Algorithms (Days 53–79)
Students explore powerful function techniques and algorithm design. Topics: lambda functions, higher-order functions (`map`, `filter`, `zip`, `reduce`), advanced comprehensions, closures and scope (LEGB rule), custom decorators, generators and iterators (`yield`, generator expressions), recursion (base case, call stack, factorial, Fibonacci, tree traversal), recursive algorithms, and Big O notation. Ends with a functional programming mini-project or algorithm challenge set.

**TN Standard 9-12.CCI.3:** Design and implement algorithms

### Unit 4 — File I/O & Data Processing (Days 80–105)
Students work with real-world data from files and external sources. Topics: file reading and writing (modes, `with` statement), text file processing, CSV files (`csv` module, `DictReader`/`DictWriter`), JSON files (`json` module), exception handling (`try`/`except`/`else`/`finally`, raising exceptions), custom exceptions, data validation and cleaning, regular expressions (`re` module), working with directories (`os`, `pathlib`), and basic data analysis. Ends with a data analysis project that reads a CSV, computes statistics, and writes a report.

**TN Standard 9-12.CCI.4:** Use external data sources

### Unit 5 — Sorting, Searching & Recursion (Days 106–133)
Students master the algorithms that power real software. Topics: recursion deep dive, linear search (O(n)), binary search (O(log n), iterative + recursive), bubble sort (O(n²)), selection sort, insertion sort, merge sort (O(n log n), divide and conquer), quick sort (pivot, partition), Python's built-in `sorted()` with `key=` and lambda, algorithm comparison and selection, and performance benchmarking. Ends with an algorithm implementation and benchmarking project.

**TN Standard 9-12.CCI.3:** Implement and analyze algorithms

### Unit 6 — APIs & External Libraries (Days 134–155)
Students connect their programs to the world. Topics: what is an API? (REST, HTTP methods, status codes), the `requests` library (`GET`/`POST`, JSON responses, headers), API keys and authentication, working with multiple public APIs, the `random`, `datetime`, `math`, and `collections` modules, NumPy basics (arrays, vectorized operations), Matplotlib basics (line charts, bar charts, customization), and a data visualization project using live API data.

**TN Standards 9-12.CCI.4/.5:** Use external data sources and create significant projects

### Unit 7 — Capstone Project (Days 156–180)
Students apply everything from Units 1–6 to build and present a complete, substantial application. Students choose from four project options: Data Analyzer, API-Powered App, Student Information System, or Algorithm Visualizer (or propose a custom project). Work is organized into three sprints with check-ins, peer code review, and a teacher feedback session. Ends with class presentations and course reflection.

**TN Standard 9-12.CCI.5:** Create a significant programming project

---

## File Types Explained

### Daily Lesson Plans (Word & PDF)
One file per class session. Each 55-minute lesson plan follows a consistent format:
- **Objective** — what students will be able to do by the end
- **Warm-Up** — brief review or hook activity (5 min)
- **Direct Instruction** — new concept with code examples (15–20 min)
- **Guided Practice** — teacher-led coding activity (15 min)
- **Independent Practice** — student coding exercises (10–15 min)
- **Closure** — exit ticket or reflection (5 min)

Lesson plans are fully self-contained and can be run by a substitute with no additional context.

### Unit Assessments (Word and PDF)
Each unit includes a formal assessment document with:
- Multiple choice questions
- Short answer questions
- Coding challenges
- Complete answer key and grading rubric

Assessment types include: predict-the-output, write-the-code, identify-the-error, algorithm traces, and short answer.

### Daily Notes & Study Guides
One comprehensive markdown file per class day. Each guide includes:
- Learning target for the day
- Key concepts with bold vocabulary and explanations
- Annotated code examples
- Guided practice activity
- Three-tier practice problems (Beginner / Intermediate / Challenge)
- Hints and sample answers in collapsible `<details>` blocks

### Unit Overview Files
Each unit also has a combined `Unit N - [Name].md` that embeds all daily content, plus:
- Unit practice bank (15–20 problems)
- Common mistakes and fixes table
- Assessment prep Q&A
- Vocabulary and quick reference section

---

## Materials Count

| Material | Count |
|----------|-------|
| Daily notes .md files | 180 |
| Unit overview .md files | 7 |
| Unit reference guides | 7 |
| Unit practice banks | 7 |
| Unit assessments | 7 |
| Standards alignment document | 1 (.pdf) |
| **Total files** | **~215** |

---

## Standards Alignment

All materials are aligned to the **Tennessee Coding II** standards. The full mapping is in `TN_Coding_II_Trad_Full_Year_Standards_Alignment.pdf` at the root of this folder. Standards covered:

- **9-12.CCI.1:** Object-oriented programming with classes and objects
- **9-12.CCI.2:** Collection data structures (lists, tuples, dicts, sets)
- **9-12.CCI.3:** Algorithm design, recursion, sorting, and searching
- **9-12.CCI.4:** File I/O, external data sources, and libraries
- **9-12.CCI.5:** Significant programming project development

---

## How to Use These Materials

**For daily instruction:** Open the current `Word/Day N.docx` (or matching PDF). Each lesson is self-contained and designed for 55 minutes. Adapt pacing based on student needs.

**For student reference:** Share the unit's `.md` files via your LMS, email, or cloud storage. They render well in GitHub, VS Code Preview, and most Markdown viewers and make excellent homework-help and test-prep resources.

**For assessments:** Print the PDF version, or open the `.docx` to customize with your school name and preferences. The answer key is included in both formats.

**For sub plans:** The PDF lesson plans are fully self-contained. A substitute can run any lesson directly from the PDF with no additional context or coding experience.

**For differentiation:** The Beginner / Intermediate / Challenge problem tiers in every daily note allow you to meet students where they are. Scaffold with hints and starter code for struggling learners; use Challenge problems to extend advanced students.

---

## Student Learning Outcomes

By the end of Coding II (Traditional), students will be able to:

- Choose and use the right collection data structure for any problem
- Design and build multi-class object-oriented programs
- Apply functional programming patterns (lambdas, map/filter, comprehensions, generators)
- Analyze algorithm complexity using Big O notation
- Implement major sorting and searching algorithms from scratch
- Read, write, and process data from text files, CSV, and JSON
- Connect programs to live web APIs and visualize data with Matplotlib
- Plan, build, test, document, and present a complete software project
- Apply professional coding practices: error handling, documentation, refactoring

---

*Tennessee Coding II · Full Year (Traditional Schedule) · Course Materials*
