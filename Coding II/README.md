# Coding II — Full Semester Course Materials

A complete, standards-aligned Python programming course for high school students. Built for an 18-week semester meeting 3 days per week (54 total class sessions), covering Python intermediate concepts from data structures through capstone project development.

---

## Course Overview

| | |
|---|---|
| **Language** | Python 3 |
| **Duration** | 18 weeks · 3 days/week · 1 hour/session |
| **Total Sessions** | 54 class days |
| **Standards** | Tennessee Coding II Standards |
| **Units** | 7 |

---

## Folder Structure

Each unit folder contains the same set of materials:

```
Unit N - [Name]/
├── Daily Lesson Plans
    ├── Word/                   Daily lesson plan .docx files + unit assessment .docx
    ├── PDF/                    Daily lesson plan .pdf files + unit assessment .pdf
├── ReferenceGuide.md       Key terms, formulas, common mistakes
├── UnitPractice.md         15 practice problems based on unit topics
├── UnitAssessment.md       10 assessment prep questions with answers
└── Daily Notes/            Complete daily study guides (Markdown)
    ├── Day1.md through Day[N].md
```

The root folder also contains `TN_Coding_II_Full_Semester_Standards_Alignment.docx/.pdf` — a full-semester standards mapping document.

---

## Units at a Glance

| Unit | Title | Days | Class Days | Standard |
|------|-------|------|------------|----------|
| 1 | Data Structures | 6 | 1–6 | 9-12.CCI.2 |
| 2 | Object-Oriented Programming | 9 | 7–15 | 9-12.CCI.1 |
| 3 | Advanced Functions & Algorithms | 9 | 16–24 | 9-12.CCI.3 |
| 4 | File I/O & Data Processing | 9 | 25–33 | 9-12.CCI.4 |
| 5 | Sorting, Searching & Recursion | 9 | 34–42 | 9-12.CCI.3 |
| 6 | APIs & External Libraries | 6 | 43–48 | 9-12.CCI.4 |
| 7 | Capstone Project | 6 | 49–54 | 9-12.CCI.5 |

---

## Unit Descriptions

### Unit 1 — Data Structures (Days 1–6)
Students master Python's fundamental collection types. Topics: lists (indexing, slicing, methods), list comprehensions, nested lists, tuples (immutable sequences, packing/unpacking), dictionaries (key-value operations), sets (unique collections and operations), and choosing appropriate data structures. Ends with a student gradebook project.

**TN Standard 9-12.CCI.2:** Use and manipulate collection data structures

### Unit 2 — Object-Oriented Programming (Days 7–15)
Students learn to structure programs around objects combining data and behavior. Topics: classes and objects, `__init__` and `self`, instance methods, class vs instance variables, encapsulation with properties, inheritance and `super()`, polymorphism and method overriding, dunder methods (`__str__`, `__eq__`, `__len__`). Ends with a bank account system project.

**TN Standard 9-12.CCI.1:** Use an object-oriented programming language with classes and objects

### Unit 3 — Advanced Functions & Algorithms (Days 16–24)
Students explore powerful function techniques and algorithmic thinking. Topics: lambda functions, higher-order functions (map, filter, zip), list and dictionary comprehensions, recursion (base case, recursive case, memoization), pseudocode, Big O notation (O(1), O(n), O(n²), O(log n)), decorators and closures, functional programming patterns. Ends with a recursive calculator and algorithm showcase.

**TN Standard 9-12.CCI.3:** Design and implement algorithms

### Unit 4 — File I/O & Data Processing (Days 25–33)
Students work with external data from files and APIs. Topics: file operations (read, write, append with context managers), text processing, CSV files (reader/DictReader), JSON files (load/dump), exception handling (try/except/finally, multiple exceptions), custom exceptions, data cleaning and validation, basic statistics (mean, median, mode). Ends with a student data analyzer project.

**TN Standard 9-12.CCI.4:** Use external data sources

### Unit 5 — Sorting, Searching & Recursion (Days 34–42)
Students master classic algorithms. Topics: linear search (O(n)), binary search (O(log n)), bubble sort (O(n²)), selection sort, insertion sort, merge sort (O(n log n)), Python's built-in sorting, algorithm complexity comparison, benchmarking. Ends with a sort and search visualizer.

**TN Standard 9-12.CCI.3:** Implement and analyze algorithms

### Unit 6 — APIs & External Libraries (Days 43–48)
Students leverage existing tools and libraries. Topics: pip and package management, virtual environments, the requests library (HTTP requests, status codes, error handling), REST APIs and JSON data, data visualization with matplotlib, numpy basics (arrays, vectorized operations, statistics). Ends with an API data dashboard project.

**TN Standard 9-12.CCI.4:** Leverage existing tools and libraries

### Unit 7 — Capstone Project (Days 49–54)
Students plan, design, build, and present a complete project. Topics: project planning (requirements, user stories), system architecture and design patterns, incremental implementation with testing, refactoring and documentation, professional presentation skills, course reflection. Students build and present a significant programming project of their choice.

**TN Standard 9-12.CCI.5:** Create a significant programming project

---

## File Types Explained

### Daily Lesson Plans (Word & PDF)
One file per class session. Each lesson plan follows a consistent 60-minute format:
- **Objective** — what students will be able to do by the end
- **Warm-Up** — brief review or hook activity (5-10 min)
- **Direct Instruction** — new concept with code examples (15-20 min)
- **Guided Practice** — teacher-led coding activity (15 min)
- **Independent Practice** — student coding exercises (15 min)
- **Closure** — exit ticket or reflection (5 min)

Lesson plans are designed for teachers unfamiliar with content—they're fully self-contained and can be run by a substitute.

### Unit Assessments (Word and PDF)
Each unit includes a 20–25 question assessment in two formats:
- **.docx / .pdf** — printable version for traditional testing

Assessment question types include multiple choice, true/false, predict-the-output, write-the-code, identify-the-error, and short answer questions.

### Markdown Study Guides (.md)
One comprehensive study guide per day per unit. Each guide includes:
- Unit overview and learning targets
- Day-by-day key concepts with annotated code examples
- Guided practice activities
- Practice problems at three tiers (Beginner / Intermediate / Challenge)
- Hint and answer collapsibles (`<details>` blocks)
- 15-problem unit practice bank
- Common mistakes and fixes
- 10 assessment prep Q&A pairs
- Vocabulary and quick reference section

These are designed for student self-study, review, and reference. They render well in GitHub, VS Code, and most Markdown viewers.

---

## Materials Count

| Material | Count |
|----------|-------|
| Daily lesson plan .docx files | 54 |
| Daily lesson plan .pdf files | 54 |
| Unit assessment .docx files | 7 |
| Unit assessment .pdf files | 7 |
| Daily notes .md files | 54 |
| Unit overview .md files | 7 |
| Unit reference/practice/assessment files | 21 |
| Standards alignment document | 1 (.docx + .pdf) |
| **Total files** | **~220** |

---

## Standards Alignment

All materials are aligned to the **Tennessee Coding II** standards. The full mapping is in `TN_Coding_II_Full_Semester_Standards_Alignment.docx/.pdf` at the root of this folder. Standards covered:

- **9-12.CCI.1:** Object-oriented programming
- **9-12.CCI.2:** Collection data structures
- **9-12.CCI.3:** Algorithm design and analysis
- **9-12.CCI.4:** External data and libraries
- **9-12.CCI.5:** Significant programming projects

---

## How to Use These Materials

### For Daily Instruction
1. Open the `Word/Day N.docx` (or matching PDF) for the current class session
2. Each lesson is self-contained and designed for 60 minutes
3. Follow the sections: Warm-Up → Direct Instruction → Guided Practice → Independent Practice → Closure
4. Adapt activities based on student needs and pacing

### For Assessments
1. Use the Word version to customize if desired (add school name, adjust instructions, etc.)
2. Print the PDF version for students
3. Answer key is included in both formats

### For Student Reference
1. Share the unit's `.md` files with students via learning management system, email, or cloud storage
2. Students can use for homework help, test prep, and review
3. Render beautifully in GitHub, Google Docs (via export), or Markdown viewers

### For Sub Plans
1. The PDF lesson plans are fully self-contained
2. A substitute can run any lesson directly from the PDF
3. No additional context or preparation needed

### For Differentiation
- Markdown files include Beginner/Intermediate/Challenge problems
- Lesson plans can be modified to spend more/less time on sections
- Practice problems offer scaffolding at multiple levels

---

## Key Features

✓ **Complete Coverage** — All 54 days planned, aligned to TN standards
✓ **Multiple Formats** — Docx, PDF, and Markdown for flexibility
✓ **Ready to Use** — No additional prep needed
✓ **Scaffolded Problems** — Beginner/Intermediate/Challenge tier
✓ **Comprehensive References** — Quick guides, common mistakes, vocabulary
✓ **Assessment Support** — Practice problems + assessment prep Q&A
✓ **Professional Lesson Plans** — Detailed, timed, structured
✓ **Capstone Project** — Semester culmination with real deliverables

---

## Student Learning Outcomes

By the end of Coding II, students will be able to:

- Use lists, tuples, dictionaries, and sets appropriately
- Design and implement object-oriented programs
- Write lambda functions and higher-order functions
- Analyze algorithm complexity and choose appropriate algorithms
- Read/write files and process external data (CSV, JSON)
- Use external libraries (requests, matplotlib, numpy)
- Plan, design, build, and present complete projects
- Apply professional software development practices

---

## Suggested Extensions

- **Challenge Units:** Add advanced topics (decorators, metaclasses, async)
- **Industry Tools:** Introduce Git, GitHub, continuous integration
- **Web Development:** Add Flask/Django units
- **Data Science:** Expand pandas, machine learning topics
- **Game Development:** Introduce pygame or similar library
- **Competitions:** Prepare for programming competitions
- **Open Source:** Contribute to real projects

---

*Tennessee Coding II · Full Semester Materials · Standards-Aligned · Ready to Teach*
