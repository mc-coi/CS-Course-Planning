# Day 1: Capstone Project Introduction

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
- Teacher walks through each of the 5 project options (see below)
- For each option: show scope, tech stack required, example features, and why it's a good capstone choice
- Emphasize: **You will choose ONE project to work on for the next 25 days.**

**Minutes 40-55:** **Rubric and Expectations**
- Review the Project Rubric (see below)
- Walk through: code quality, features, documentation, presentation
- Show examples of "excellent," "good," and "needs work"
- Clarify deliverables: working code + README + presentation

---

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

## Project Requirements & Rubric

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
