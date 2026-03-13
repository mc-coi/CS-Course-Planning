#  Unit 7 Practice Bank (15 Problems)

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