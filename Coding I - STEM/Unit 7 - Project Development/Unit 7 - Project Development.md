# Unit 7: Project Development
> Apply everything you've learned to build a complete, professional Python application.

## 📋 Unit Overview
- **Duration:** 6 days / 2 weeks (Days 49–54)
- **Key Concepts:** Project planning, incremental development, testing, debugging, documentation, presentation
- **Big Idea:** Real programming is solving real problems systematically — from defining the problem to writing, testing, documenting, and presenting working code
- **TN Standards Addressed:** Computational thinking, problem decomposition, program design, documentation, presentation of work

##  Learning Targets
- I can define a problem and write a clear project specification
- I can design a program structure before writing any code
- I can develop code incrementally, testing each piece as I go
- I can apply all prior skills (loops, functions, conditionals, lists, file I/O) in a cohesive project
- I can debug systematically using error messages and print tracing
- I can write complete documentation including docstrings and inline comments
- I can present my work and explain my design choices clearly
- I can reflect on my growth as a programmer throughout the course

---

# Day 1: Project Planning & Design

### Key Concepts

Great software starts on paper, not in the code editor. The **Software Development Process:**

| Phase | What You Do | Output |
|-------|------------|--------|
| **1. Define** | What problem are you solving? Who uses it? | Problem statement |
| **2. Plan** | What functions? What data? What input/output? | Project spec / pseudocode |
| **3. Code** | Write it — start with the smallest pieces | Working code |
| **4. Test** | Does it work? Edge cases? | Test results |
| **5. Refine** | Clean up, document, improve | Polished program |
| **6. Present** | Show your work, explain choices | Demo + walkthrough |

### Project Proposal Template

Fill this out **before** writing any code:

```
PROJECT TITLE: ___________________________

PROBLEM STATEMENT:
What problem does this program solve?
Who would use it?

INPUTS:
What data does the program take in?
(user input, files, etc.)

OUTPUTS:
What does the program produce?
(printed results, files, etc.)

FUNCTION LIST:
Function name         | What it does
--------------------- | ----------------------------
main()                | Ties everything together
get_input()           |
process_data()        |
display_results()     |

DATA STRUCTURES:
What variables/lists/dicts will you use?

TEST CASES:
Input → Expected Output
[normal case]  →
[edge case]    →
[error case]   →
```

### Pseudocode

Write the logic in plain English first — no Python syntax:

```
PROGRAM: Grade Calculator

1. Show welcome message
2. Ask for student's name
3. Loop until user types "done":
   a. Ask for a score
   b. Validate the score (must be 0-100)
   c. Add to scores list
4. Calculate average of all scores
5. Convert average to letter grade
6. Display full report
7. Ask if user wants to save report to file
   a. If yes, write report to file
```

### Breaking Problems into Functions

The key skill: look at your pseudocode and ask "what is each step doing?" — each step becomes a function.

```python
# From the pseudocode above:
def get_student_name():
    pass  # step 2

def get_scores():
    pass  # step 3 (loop with validation)

def calculate_average(scores):
    pass  # step 4

def letter_grade(average):
    pass  # step 5

def display_report(name, scores, average, grade):
    pass  # step 6

def save_report(filename, name, scores, average, grade):
    pass  # step 7

def main():
    name = get_student_name()
    scores = get_scores()
    avg = calculate_average(scores)
    grade = letter_grade(avg)
    display_report(name, scores, avg, grade)
    # ask about saving...
```

### Project Ideas by Category

**Productivity Tools**
- Grade tracker / GPA calculator
- Daily to-do list with file persistence
- Unit converter (length, weight, temperature)
- Simple budget tracker

**Games**
- Number guessing game with difficulty levels
- Hangman
- Rock-Paper-Scissors with win/loss tracking
- Quiz bowl (read questions from file)

**Data Programs**
- Weather data analyzer (read from CSV)
- Student grade report generator
- Word frequency counter / text analyzer
- Survey results processor

**Utilities**
- Password strength checker
- Simple contact book with file storage
- Grocery list manager
- Simple note-taking app

---

# Day 2: Development Session 1 — Build the Foundation

### Key Concepts

**Bottom-Up Development:** Start with the helper functions (the smallest, most isolated pieces) and build upward to `main()`.

**Why bottom-up?**
- Each piece is easy to test in isolation
- Bugs are easier to find when the scope is small
- You build confidence as each piece works

**Development order:**
1. Write and test the simplest function first
2. Test it immediately (don't wait!)
3. Add the next layer
4. Integrate gradually

### Development Session Strategy

**Hour breakdown for today:**
- 10 min: Review your project spec and plan
- 5 min: Identify which function to build first (the most basic, no dependencies)
- 30 min: Write 2–3 foundational functions
- 10 min: Test each function individually
- 5 min: Note what's left, plan tomorrow

### Unit Testing Your Functions

Before connecting everything, test each function alone:

```python
# ── Testing functions in isolation ─────────────────────────

def calculate_average(scores):
    """Return the mean of a list of scores."""
    if not scores:
        return 0.0
    return sum(scores) / len(scores)

def letter_grade(average):
    """Convert average to letter grade."""
    if average >= 90: return "A"
    if average >= 80: return "B"
    if average >= 70: return "C"
    if average >= 60: return "D"
    return "F"

# ── Test each function BEFORE connecting them ──────────────
print("Testing calculate_average:")
print(calculate_average([90, 85, 92]))   # Expected: 89.0
print(calculate_average([70, 70, 70]))   # Expected: 70.0
print(calculate_average([]))             # Expected: 0.0

print("\nTesting letter_grade:")
print(letter_grade(95))   # Expected: A
print(letter_grade(83))   # Expected: B
print(letter_grade(55))   # Expected: F

# ── Add a simple test runner ───────────────────────────────
def test_calculate_average():
    assert calculate_average([100, 90, 80]) == 90.0, "Test 1 failed"
    assert calculate_average([70, 70]) == 70.0, "Test 2 failed"
    assert calculate_average([]) == 0.0, "Test 3 failed"
    print("calculate_average: All tests passed ✓")

test_calculate_average()
```

### Common Development Pitfalls

| Pitfall | How to Avoid |
|---------|-------------|
| Writing everything at once | Write one function at a time |
| Never testing until the end | Test after every function |
| No error handling | Add `try/except` from the start |
| Unclear function names | Name says what it does: `get_user_age()` |
| Forgetting edge cases | Always test: empty input, 0, very large numbers |
| Copy-pasting code | Extract repeated code into a function |

---

# Day 3: Development Session 2 — Integration

### Key Concepts

**Integration:** Connecting your tested helper functions into a working program.

**Integration testing:** Testing how the pieces work *together* (vs. unit testing — testing each piece alone).

### Integration Checklist

Before integrating two functions:
- [ ] Both functions work correctly on their own
- [ ] The output type of function A matches what function B expects
- [ ] Edge cases have been handled

### Code Examples — Full Integration

```python
"""
grade_tracker.py
A complete grade tracking application.
Demonstrates full integration of functions built across multiple sessions.
"""

import os

# ── HELPER FUNCTIONS (built and tested individually) ───────

def get_student_name():
    """Prompt for and return the student's name."""
    name = input("Student name: ").strip()
    while not name:
        print("Name cannot be empty.")
        name = input("Student name: ").strip()
    return name

def get_scores():
    """Collect scores from user until 'done' is entered.

    Returns:
        list of float: Valid scores in range 0-100.
    """
    scores = []
    print("Enter scores one at a time. Type 'done' when finished.")
    while True:
        entry = input(f"Score {len(scores)+1} (or 'done'): ").strip()
        if entry.lower() == "done":
            if not scores:
                print("Please enter at least one score.")
                continue
            break
        try:
            score = float(entry)
            if 0 <= score <= 100:
                scores.append(score)
            else:
                print("Score must be between 0 and 100.")
        except ValueError:
            print("Please enter a number.")
    return scores

def calculate_average(scores):
    """Return the arithmetic mean of a list of scores."""
    if not scores:
        return 0.0
    return sum(scores) / len(scores)

def letter_grade(average):
    """Convert a numeric average to a letter grade (A-F)."""
    if average >= 90: return "A"
    if average >= 80: return "B"
    if average >= 70: return "C"
    if average >= 60: return "D"
    return "F"

def display_report(name, scores, average, grade):
    """Print a formatted grade report to the console."""
    border = "=" * 40
    print(f"\n{border}")
    print(f"  Grade Report: {name}")
    print(border)
    print(f"  Scores:   {[round(s, 1) for s in scores]}")
    print(f"  Average:  {average:.1f}")
    print(f"  Grade:    {grade}")
    status = "PASSING" if average >= 70 else "FAILING"
    print(f"  Status:   {status}")
    print(border)

def save_report(filename, name, scores, average, grade):
    """Save the grade report to a text file.

    Args:
        filename (str): Output file path.
        name, scores, average, grade: Report data.
    """
    try:
        with open(filename, "w") as f:
            f.write(f"Grade Report: {name}\n")
            f.write(f"Scores: {scores}\n")
            f.write(f"Average: {average:.1f}\n")
            f.write(f"Grade: {grade}\n")
        print(f"Report saved to '{filename}'")
    except IOError as e:
        print(f"Could not save file: {e}")

# ── MAIN (integration point) ───────────────────────────────

def main():
    """Run the grade tracking program."""
    print("=" * 40)
    print("   Welcome to Grade Tracker")
    print("=" * 40 + "\n")

    name = get_student_name()
    scores = get_scores()
    average = calculate_average(scores)
    grade = letter_grade(average)

    display_report(name, scores, average, grade)

    save_choice = input("\nSave report to file? (y/n): ").lower()
    if save_choice == "y":
        filename = f"{name.replace(' ', '_')}_report.txt"
        save_report(filename, name, scores, average, grade)

    print("\nThanks for using Grade Tracker!")

main()
```

### Integration Debugging Strategy

When integrated code doesn't work:
1. **Check the pipeline:** Trace data flowing from function to function — is it the right type?
2. **Print at connection points:** `print(f"After get_scores, got: {scores}")` between calls
3. **Isolate which function is failing:** Comment out later steps to narrow it down
4. **Check edge cases in integration:** Does `letter_grade` handle the `0.0` returned by `calculate_average([])`?

---

# Day 4: Development Session 3 — Polish & Documentation

### Key Concepts

**Refactoring:** Improving code structure without changing behavior.

Signs your code needs refactoring:
- A function is longer than ~20 lines — can it be split?
- The same code appears in multiple places — extract it to a function
- Variable names are unclear (`x`, `temp`, `stuff`)
- A function does more than one thing

**Code polish checklist:**
- [ ] All functions have docstrings
- [ ] Variable names are descriptive
- [ ] No duplicate code
- [ ] Error handling for all user inputs
- [ ] Edge cases tested (empty input, 0, large values)
- [ ] Code is consistently indented
- [ ] Comments explain *why*, not *what*

### Code Examples — Before and After Refactoring

```python
# ── BEFORE: messy, undocumented ────────────────────────────
def f(x):
    t = 0
    for i in x:
        t += i
    a = t / len(x)
    if a >= 90:
        g = "A"
    elif a >= 80:
        g = "B"
    elif a >= 70:
        g = "C"
    elif a >= 60:
        g = "D"
    else:
        g = "F"
    print("Avg:", a, "Grade:", g)

# ── AFTER: clean, modular, documented ──────────────────────
def calculate_average(scores):
    """Return the mean of a non-empty list of numbers."""
    return sum(scores) / len(scores)

def assign_letter_grade(average):
    """Convert numeric average to letter grade A through F."""
    if average >= 90: return "A"
    if average >= 80: return "B"
    if average >= 70: return "C"
    if average >= 60: return "D"
    return "F"

def print_grade_summary(scores):
    """Calculate and display average and letter grade for scores."""
    if not scores:
        print("No scores to analyze.")
        return
    avg = calculate_average(scores)
    grade = assign_letter_grade(avg)
    print(f"Average: {avg:.1f}  |  Grade: {grade}")

# ── What improved: ─────────────────────────────────────────
# 1. Split one function into three (single responsibility)
# 2. Meaningful names: f → print_grade_summary
# 3. Descriptive variable names: t → total (via sum()), a → avg, g → grade
# 4. Docstrings added
# 5. Edge case handled (empty list)
```

### Final Polish Checklist

Work through your entire project and check each item:

**Function Quality**
- [ ] Every function has a clear, descriptive name
- [ ] Every function has a docstring
- [ ] Every function does exactly one job
- [ ] No function is longer than ~20 lines

**Error Handling**
- [ ] All user inputs are validated
- [ ] File operations use `try/except`
- [ ] Division checks for zero
- [ ] List access checks length first

**Code Style**
- [ ] Consistent indentation (4 spaces)
- [ ] Blank lines between functions
- [ ] Module-level docstring at top of file
- [ ] No commented-out dead code left in

**Testing**
- [ ] Each function tested individually
- [ ] Edge cases tested (empty, 0, max values)
- [ ] Full program run-through on normal input
- [ ] Full program run-through on bad input

---

# Day 5: Presentations

### How to Present Your Project

A great 5-minute presentation has this structure:

| Section | Time | What to Cover |
|---------|------|--------------|
| **Introduction** | 30 sec | Name your program, state the problem it solves |
| **Demo** | 2 min | Run it live — show normal input, then an edge case |
| **Code Walkthrough** | 1.5 min | Explain 1–2 interesting functions (not line by line) |
| **Challenges** | 45 sec | What was the hardest part? How did you solve it? |
| **Questions** | 30 sec | Invite 1–2 questions |

### Presentation Tips

**Do:**
- Open your code in the editor before you start
- Have your test inputs ready (write them down)
- Speak to the audience, not the screen
- Say "when I call X it does Y" — show the connection
- Be ready for "what happens if the user types nothing?"

**Don't:**
- Read the code line by line (explain the logic instead)
- Say "I didn't get to implement..." (focus on what works)
- Apologize for imperfections (own your work!)
- Rush — it's okay to pause and think

### Sample Presentation Script

```
"Hi, I built a Grade Tracker. The problem: keeping track
of your scores throughout the year is tedious — my program
lets you enter scores, calculates your average, and saves
a report to a file.

Let me show you a demo... [runs program]
I'll enter three scores: 88, 92, 79. The program calculates
the average as 86.3 and assigns a B. Now watch what happens
when I type 'hello' instead of a number... [shows error handling]
It just asks again — no crash.

The most interesting function is get_scores(). It loops until
the user types 'done', but it validates every input with
try/except to catch bad data. Here's the key part... [shows code]

The hardest part was the file saving — I had to make sure it
handled the case where the file couldn't be written.

Any questions?"
```

### Presentation Prep Checklist
- [ ] Program runs without crashing on normal input
- [ ] I know what to type for my live demo
- [ ] I can explain 2 functions in plain English
- [ ] I know what was hardest and how I solved it
- [ ] I've practiced saying my presentation out loud at least once

---

# Day 6: Wrap-Up, Reflection & Course Celebration

### Course Reflection

You've completed Coding I. Let's look back at what you've learned:

**Unit 1 — Introduction:** You learned what programming is, what Python is, and how to write your very first lines of code. You went from `print("Hello, world!")` to writing interactive programs.

**Unit 2 — Variables & Data Types:** You learned to store data — numbers, text, decimals, booleans — and how to do math and string operations. You learned about `input()` and how to get data from users.

**Unit 3 — Conditionals:** You taught your programs to *decide* — using `if`, `elif`, and `else` to respond differently to different situations. Boolean logic became a tool, not a mystery.

**Unit 4 — Loops:** You made your programs *repeat* — `for` loops for counted repetition, `while` loops for conditional repetition. You solved problems that would take hours to do by hand.

**Unit 5 — Functions:** You learned to write code once and use it many times. You discovered how to pass information in (parameters), get information out (return values), and design programs in modular pieces.

**Unit 6 — Debugging & Documentation:** You learned to be a professional. You can find and fix bugs systematically, handle errors gracefully, read and write files, and document your code so others can understand it.

**Unit 7 — Project Development:** You combined everything to build a real program from scratch — starting with a plan, building incrementally, testing thoroughly, and presenting your work.

### Reflective Writing Prompts

Take 10 minutes to write (or discuss) your answers:

1. **What was your biggest "aha moment" in this course?** A time when something finally clicked.

2. **What is the concept or skill you're most proud of learning?** Why does it stand out?

3. **What was the most challenging part?** How did you push through it?

4. **Show your growth:** Find the first program you wrote and compare it to your final project. What's different about how you think about problems now?

5. **What do you want to build next?** If you had unlimited time, what program would you create?

6. **Advice to your Day-1 self:** What would you tell yourself at the beginning of this course?

### Skills Inventory — Check Off What You've Mastered

**Foundations**
- [ ] `print()`, `input()`, variables
- [ ] `int()`, `float()`, `str()`, `bool()` — type conversion
- [ ] Arithmetic operators: `+`, `-`, `*`, `/`, `//`, `%`, `**`
- [ ] String operations: concatenation, f-strings, `.upper()`, `.lower()`, `.strip()`

**Decisions**
- [ ] `if`, `elif`, `else`
- [ ] Comparison operators: `==`, `!=`, `<`, `>`, `<=`, `>=`
- [ ] Boolean operators: `and`, `or`, `not`
- [ ] Nested conditionals

**Repetition**
- [ ] `for` loops with `range()`
- [ ] `for` loops over lists/strings
- [ ] `while` loops with conditions
- [ ] `break` and `continue`
- [ ] Accumulator pattern

**Data Structures**
- [ ] Lists: create, access, append, remove, slice
- [ ] List methods: `.sort()`, `.reverse()`, `.index()`, `len()`
- [ ] Dictionaries: create, access, update, `.keys()`, `.values()`
- [ ] Tuples: create, unpack

**Functions**
- [ ] Define with `def`, call with `()`
- [ ] Parameters and arguments
- [ ] `return` values
- [ ] Variable scope (local vs. global)
- [ ] Default parameters
- [ ] Multiple return values

**Files & Errors**
- [ ] `with open()` — read and write
- [ ] File modes: `"r"`, `"w"`, `"a"`
- [ ] `try/except` for error handling
- [ ] Specific exception types
- [ ] Docstrings and comments

**Projects**
- [ ] Planning and pseudocode
- [ ] Incremental development
- [ ] Unit testing
- [ ] Debugging with print statements
- [ ] Code refactoring

---

##  Unit 7 Practice Bank (15 Problems)

These are full-program challenges that use all your skills. Each one is a complete mini-project.

### Tier 1 — Beginner Programs

**P1. Temperature Converter**
Write a complete program that:
- Asks the user if they want to convert C→F or F→C
- Gets the temperature
- Converts and displays the result
- Asks if they want to do another conversion (loop until "no")

**P2. Multiplication Table Generator**
Write a complete program that:
- Asks the user for a number (1–12)
- Prints the full multiplication table for that number (1×N through 12×N)
- Saves the table to `times_table.txt`

**P3. Simple Coin Flip Tracker**
Write a complete program that:
- Asks how many times to flip a coin
- Simulates each flip (use `random.choice(["Heads", "Tails"])`)
- Counts heads and tails
- Displays the results and percentages

### Tier 2 — Intermediate Programs

**P4. Grade Book**
Write a complete grade book program that:
- Stores a dictionary of student names → list of scores
- Lets the user: add a student, add a score for a student, view a student's average, or view the class ranking
- Saves/loads data from `gradebook.txt`

<details>
<summary>💡 Hint for P4 — Data structure</summary>

```python
gradebook = {
    "Alice": [92, 88, 95],
    "Bob": [78, 82, 80],
}

# To add a score:
gradebook["Alice"].append(90)

# To get average:
avg = sum(gradebook["Alice"]) / len(gradebook["Alice"])
```
</details>

**P5. Number Guessing Game**
Write a complete guessing game that:
- Randomly picks a secret number (1–100)
- Gives hints: "too high", "too low", "correct!"
- Counts guesses and rates the player (excellent/good/okay)
- Asks if they want to play again
- Tracks all-time best score in `high_scores.txt`

**P6. Text Analyzer**
Write a complete program that:
- Reads a text file the user names
- Counts total words, unique words, and sentences
- Finds the 5 most common words
- Reports average word length
- Saves results to `analysis.txt`

**P7. Simple To-Do List**
Write a to-do list application that:
- Loads existing tasks from `tasks.txt` on startup
- Lets user: add task, mark complete, delete task, view all tasks
- Saves tasks to file on exit
- Shows completed tasks differently (with [X] marker)

### Tier 3 — Challenge Programs

**P8. Expense Tracker**
Write a complete expense tracking program with:
- `add_expense(expenses, category, amount, description)` — add to list
- `total_by_category(expenses)` — returns dict of category→total
- `monthly_summary(expenses)` — displays all categories and totals
- `save_expenses(filename, expenses)` / `load_expenses(filename)` — persistence
- `main()` — menu-driven interface

**P9. Quiz Application**
Write a quiz program that:
- Reads questions from `quiz_data.txt` in format `Question|AnswerA|AnswerB|AnswerC|AnswerD|CorrectLetter`
- Presents questions one at a time with random ordering of choices
- Tracks score, time taken, and which questions were missed
- Generates a detailed results file

**P10. Mini Text Adventure**
Write a simple text adventure game where:
- The player is in a house with 4 rooms (North, South, East, West)
- Each room has a description and possibly an item
- Player can: move (n/s/e/w), pick up items, view inventory, use items
- Uses a dictionary for rooms and a list for inventory
- Reads room data from a file

**P11. Password Manager**
Write a password manager (educational only) that:
- Stores service name + password pairs
- Lets user: add entry, retrieve entry, list all services, delete entry
- Saves to `vault.txt` (encrypt passwords by shifting each character by 13)
- Uses `try/except` for all file operations

**P12. Student Report Card Generator**
Write a complete report card program that:
- Reads student data from `students.csv` (name, scores for each subject)
- Calculates average for each subject and overall GPA
- Assigns letter grades
- Writes individual report cards to separate `.txt` files
- Writes a class summary to `class_summary.txt`

**P13. Hangman Game**
Write a complete Hangman game that:
- Loads word list from `words.txt` (one word per line)
- Draws the hangman figure using text art at each stage
- Tracks letters guessed, remaining tries
- Lets player choose difficulty (easy: 8 tries, medium: 6, hard: 4)
- Saves win/loss history

**P14. Survey Analyzer**
Write a program that:
- Reads survey responses from a CSV file (one response per row)
- Calculates statistics for numeric questions (mean, median, mode)
- Counts responses for multiple-choice questions
- Generates a formatted report with all results
- Visualizes distribution as a simple bar chart using `*` characters

**P15. Complete Grade Tracker (Full Feature)**
Build the most complete version of the grade tracker with:
- Multiple students and multiple subjects
- Weighted averages (tests 50%, homework 30%, projects 20%)
- Letter grade and GPA calculation
- Progress tracking over time (load/save history)
- Report generation per student, per class, and overall
- Full error handling, docstrings, and clean code

<details>
<summary>💡 Hint for P15 — Data structure</summary>

```python
# One approach:
students = {
    "Alice": {
        "tests": [92, 88, 95],
        "homework": [100, 85, 90, 95],
        "projects": [88, 92]
    },
    "Bob": {
        "tests": [78, 82],
        "homework": [70, 75, 80],
        "projects": [85]
    }
}

def weighted_average(student_data):
    test_avg = sum(student_data["tests"]) / len(student_data["tests"])
    hw_avg = sum(student_data["homework"]) / len(student_data["homework"])
    proj_avg = sum(student_data["projects"]) / len(student_data["projects"])
    return test_avg * 0.5 + hw_avg * 0.3 + proj_avg * 0.2
```
</details>

---

## Development Checklists

### Project Planning Checklist (Before Coding)
- [ ] Problem statement written (1–2 sentences)
- [ ] Inputs identified (what data does the program take in?)
- [ ] Outputs identified (what does it produce?)
- [ ] Function list written (at least 4–5 functions)
- [ ] Data structures decided (lists? dicts? what variables?)
- [ ] Test cases written (normal, edge, error cases)

### During Development Checklist
- [ ] Building bottom-up (helper functions first)
- [ ] Testing each function before moving on
- [ ] Handling errors with `try/except`
- [ ] Using meaningful variable names
- [ ] Adding docstrings as I write functions
- [ ] Committing working code at checkpoints

### Pre-Submission / Pre-Presentation Checklist
- [ ] Program runs without errors on normal input
- [ ] Program handles bad input gracefully (no crashes)
- [ ] Every function has a docstring
- [ ] Variable names are clear and descriptive
- [ ] No commented-out dead code
- [ ] Code is consistently indented
- [ ] I've tested at least 3 edge cases
- [ ] I can explain every function in plain English

---

## Common Project Pitfalls

| Pitfall | Why It Happens | How to Avoid |
|---------|---------------|-------------|
| Starting to code without planning | Excited to get started | Spend 15 min on the proposal first |
| Writing everything at once | Feels faster | Build one function, test it, repeat |
| Never testing until the end | Avoidance | Test every function the moment it's written |
| Functions that do too much | No design phase | Each function = one job; max ~15 lines |
| No error handling | Forgot / didn't think about it | Every `input()` and `open()` needs protection |
| Confusing variable names | `temp`, `stuff`, `x` | Name the data: `student_score`, `file_path` |
| Copy-pasting instead of functions | Seems easier in the moment | If you copy-paste, that's a new function needed |
| Giving up when stuck | Frustration | Debug systematically: isolate, trace, search |
| Missing docstrings | Added last (or never) | Write docstrings as you write functions |

---

## Assessment Prep — Q&A

**Q1: What are the six phases of the software development process?**
Define (understand the problem), Plan (design functions and data structures), Code (write it), Test (check for correctness), Refine (improve and document), Present (show your work).

**Q2: What is pseudocode and why is it useful?**
Pseudocode is logic written in plain English (no Python syntax). It helps you think through the structure of a program before getting stuck on syntax details.

**Q3: What does "bottom-up development" mean?**
Writing and testing the simplest, most isolated helper functions first, then connecting them upward to `main()`. This makes each piece easy to verify before building on top of it.

**Q4: What is the difference between unit testing and integration testing?**
Unit testing tests each function in isolation. Integration testing tests how multiple functions work together. Both are important.

**Q5: What is refactoring?**
Improving the structure, readability, and organization of code without changing what it does. Signs you need to refactor: duplicate code, functions that do too much, unclear variable names.

**Q6: What should a function's name communicate?**
The name should clearly describe what the function does, usually as a verb-noun combination: `calculate_average`, `get_user_input`, `save_to_file`, `is_valid_score`.

**Q7: What are three things to check before submitting a project?**
Any of: runs without crashing, handles invalid input, all functions have docstrings, variable names are descriptive, no dead code, edge cases tested, error handling added.

**Q8: What is the most important thing to do when your code isn't working?**
Stay systematic: read the error message carefully, add print statements to trace values, isolate which function is failing, check your assumptions about variable types. Don't randomly change things — diagnose before fixing.

**Q9: Why should you test edge cases?**
Programs often fail on unusual inputs: empty list, 0, very large numbers, spaces in text. Testing these reveals bugs that normal inputs would never expose.

**Q10: What makes code "professional quality"?**
It works correctly (including edge cases), handles errors gracefully, is readable (clear names, logical structure), is documented (docstrings + comments), and is maintainable (modular, no repetition).

---

## Vocabulary & Quick Reference

| Term | Definition |
|------|-----------|
| **Software Development Process** | The stages of planning, building, and refining a program |
| **Pseudocode** | Logic written in plain English, not code syntax |
| **Project specification** | Document describing inputs, outputs, and functions |
| **Bottom-up development** | Building helpers first, then connecting to main |
| **Unit testing** | Testing a single function in isolation |
| **Integration testing** | Testing how multiple functions work together |
| **Edge case** | Unusual input that might expose bugs (0, empty, max) |
| **Refactoring** | Improving code structure without changing behavior |
| **Single responsibility** | Each function does exactly one job |
| **Incremental development** | Building and testing small pieces at a time |
| **Bug** | An error causing incorrect behavior |
| **Debug** | The process of finding and fixing bugs |
| **Modular** | Code organized into small, reusable, single-purpose functions |
| **Code review** | Examining code for correctness, readability, and style |

### Course Concepts at a Glance

```python
# Everything you learned, in one program:

"""module docstring — what this file does"""

# Constants (Unit 2)
PASSING_SCORE = 70

def get_scores():
    """Collect valid scores from user. (Unit 5 + Unit 6)"""
    scores = []
    while True:                          # while loop (Unit 4)
        try:                             # error handling (Unit 6)
            entry = input("Score (or done): ")
            if entry.lower() == "done":  # conditionals (Unit 3)
                break                    # loop control (Unit 4)
            score = float(entry)         # type conversion (Unit 2)
            if 0 <= score <= 100:
                scores.append(score)     # list method (Unit 4)
            else:
                print("Must be 0–100")
        except ValueError:
            print("Enter a number")
    return scores                        # return value (Unit 5)

def analyze(scores):
    """Return stats dict. (Unit 5)"""
    if not scores:
        return {}
    return {                             # dictionary (Unit 4)
        "avg": sum(scores) / len(scores),
        "max": max(scores),
        "min": min(scores),
        "passing": sum(1 for s in scores if s >= PASSING_SCORE)
    }

def save_report(filename, stats):
    """Save stats to file. (Unit 6)"""
    try:                                 # file I/O (Unit 6)
        with open(filename, "w") as f:
            for key, val in stats.items():
                f.write(f"{key}: {val}\n")
    except IOError as e:
        print(f"Save failed: {e}")

def main():
    """Run the program. (Unit 7)"""
    scores = get_scores()                # function call (Unit 5)
    stats = analyze(scores)
    for k, v in stats.items():          # for loop (Unit 4)
        print(f"{k}: {v}")
    save_report("report.txt", stats)

main()
```

---

**Congratulations on completing Coding I!** 🎉

You started with `print("Hello, world!")` and ended with complete, modular, documented, error-handling programs. You can solve real problems, think algorithmically, and communicate your code to others.

This is just the beginning. Keep building, keep breaking things, keep fixing them — that's how every programmer grows.

**What's next?**

| Path | Topics to Explore |
|------|-----------------|
| **Object-Oriented Programming** | Classes, inheritance, polymorphism |
| **Data Science** | pandas, NumPy, Matplotlib, data analysis |
| **Web Development** | HTML/CSS, JavaScript, Django or Flask |
| **Game Development** | pygame, game logic, event handling |
| **Automation** | File management, web scraping, scripts |
| **Machine Learning** | scikit-learn, TensorFlow, data modeling |
| **Cybersecurity** | Networking basics, ethical hacking concepts |
| **App Development** | Mobile apps, APIs, databases |

*Keep coding. Stay curious. Make cool stuff.*
