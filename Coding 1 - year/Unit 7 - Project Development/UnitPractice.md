# Unit 7 Practice Problems: Project Design and Implementation

## Overview

These 15 practice problems range from beginner to advanced. They're complete, independent projects that use the skills from Units 1–6.

**Difficulty Levels:**
- **Tier 1 (Beginner):** Problems 1–3 (simple MVP)
- **Tier 2 (Intermediate):** Problems 4–10 (multiple features, data structures)
- **Tier 3 (Advanced):** Problems 11–15 (complex features, robust error handling)

---

## Tier 1: Beginner Projects

### P1: Temperature Converter

**Problem:** Write a program that converts between Celsius and Fahrenheit repeatedly.

**Core Features:**
1. Ask user if they want C→F or F→C
2. Get the temperature value
3. Convert and display result
4. Ask if they want another conversion (loop until "no")

**Requirements:**
- Use functions for each major task
- Validate input (user types non-numeric)
- Handle edge cases (absolute zero, very large numbers)

**Bonus:** Save conversion history to a file

**Formulas:**
- C to F: `(C × 9/5) + 32`
- F to C: `(F - 32) × 5/9`

---

### P2: Multiplication Table Generator

**Problem:** Create a program that generates and displays multiplication tables.

**Core Features:**
1. Ask user for a number (1–12)
2. Display the full multiplication table (1×N through 12×N)
3. Save the table to a file
4. Option to generate another table

**Requirements:**
- Format output nicely (aligned columns)
- Validate input (1-12 only)
- Save to file with clear formatting

**Example Output:**
```
Multiplication Table for 7:
1 x 7 = 7
2 x 7 = 14
...
12 x 7 = 84
```

---

### P3: Coin Flip Simulator

**Problem:** Simulate coin flips and track results.

**Core Features:**
1. Ask how many flips to simulate
2. Simulate each flip (use `random.choice(["Heads", "Tails"])`)
3. Count heads and tails
4. Display results with percentages

**Requirements:**
- Import `random` module
- Validate input (positive integer)
- Calculate percentages accurately
- Display results clearly

**Stretch:** Save results to file, compare multiple simulations

---

## Tier 2: Intermediate Projects

### P4: Grade Book Manager

**Problem:** Build a program to manage student grades across multiple students.

**Core Features:**
1. Store dictionary of student names → list of scores
2. Menu options:
   - Add a student
   - Add a score to a student
   - View a student's average
   - View class ranking (sorted by average)
   - List all students
3. Save/load data from file

**Requirements:**
- Use dictionaries and lists effectively
- Validate all input
- Calculate averages correctly
- Save and load from file (choose your format)

**Data Structure Hint:**
```python
gradebook = {
    "Alice": [92, 88, 95],
    "Bob": [78, 82, 80],
}
```

**Stretch:** Weighted averages (tests 50%, homework 30%, projects 20%)

---

### P5: Number Guessing Game

**Problem:** Create an interactive guessing game with scoring.

**Core Features:**
1. Randomly pick secret number (1–100)
2. Give hints: "too high", "too low", "correct!"
3. Count guesses
4. Rate player: Excellent (≤5), Good (≤10), Okay (≤15), Try again (16+)
5. Track all-time best score in file
6. Ask if they want to play again

**Requirements:**
- Use `random.randint()`
- Error handling for non-numeric input
- Save best score to file
- Clear messages at each step

**Stretch:** Difficulty levels (Easy: 1-50, Medium: 1-100, Hard: 1-1000)

---

### P6: Text Analyzer

**Problem:** Analyze a text file for statistics.

**Core Features:**
1. User selects a text file to analyze
2. Count:
   - Total words
   - Unique words
   - Sentences (roughly)
3. Find 5 most common words
4. Calculate average word length
5. Save results to file

**Requirements:**
- Open and read user-specified file
- Parse text (split into words, sentences)
- Use lists/dictionaries to track word frequencies
- Handle file not found gracefully

**Data Structure Hint:**
```python
# Count word frequencies
word_counts = {}
for word in words:
    word_counts[word] = word_counts.get(word, 0) + 1
```

**Stretch:** Ignore common words (the, a, an, etc.)

---

### P7: Simple To-Do List

**Problem:** Build a to-do list app with persistence.

**Core Features:**
1. Load tasks from `tasks.txt` on startup
2. Menu options:
   - Add task
   - Mark task complete
   - Delete task
   - View all tasks
3. Display completed tasks with [X], incomplete with [ ]
4. Save tasks to file on exit

**Requirements:**
- Store tasks as list of dictionaries (with completion status)
- Clear menu interface
- File I/O for persistence
- Handle file not found on startup

**Data Structure Hint:**
```python
tasks = [
    {"description": "Buy milk", "status": "incomplete"},
    {"description": "Finish homework", "status": "complete"},
]
```

---

### P8–P10: (Additional Intermediate Projects)

**P8: Budget Tracker**
- Add expenses by category
- Calculate totals by category
- Display monthly summary
- Save/load expenses
- Show spending breakdown

**P9: Contact Book**
- Add, delete, update contacts
- Store name, phone, email
- Search for contacts
- Save/load from file
- Display all contacts

**P10: Quiz Application**
- Load questions from file
- Present one question at a time
- Track correct/incorrect
- Show final score
- Save results

---

## Tier 3: Advanced Projects

### P11: Password Strength Checker

**Problem:** Evaluate password strength and suggest improvements.

**Core Features:**
1. User enters password
2. Check:
   - Length (8+ strong)
   - Uppercase (yes/no)
   - Lowercase (yes/no)
   - Numbers (yes/no)
   - Special characters (yes/no)
3. Assign strength: Weak/Fair/Good/Strong
4. Give specific suggestions
5. Save password history (for testing, not in production!)

**Requirements:**
- Use `string` module for character types
- Provide specific feedback
- Educational, not a real password manager

---

### P12: Student Report Card Generator

**Problem:** Generate individual and class reports from student data.

**Core Features:**
1. Load student data from `students.csv`
2. For each student:
   - Calculate average for each subject
   - Calculate overall GPA
   - Assign letter grades
3. Generate individual `.txt` report files
4. Generate class summary with statistics

**Requirements:**
- Parse CSV file
- Use dictionaries to organize data
- Calculate statistics (average, GPA)
- Generate formatted reports

**Data Structure Hint:**
```python
students = {
    "Alice": {
        "math": [85, 92, 88],
        "english": [90, 88, 92],
        "science": [87, 85, 90]
    }
}
```

---

### P13: Hangman Game

**Problem:** Implement the classic Hangman game.

**Core Features:**
1. Load word list from file
2. Draw hangman figure at each wrong guess
3. Track letters guessed, remaining tries
4. Difficulty levels (easy: 8 tries, medium: 6, hard: 4)
5. Save win/loss history
6. Play multiple rounds

**Requirements:**
- ASCII art for hangman figure
- String operations to track guessed letters
- File I/O for word list and results
- Clear game state display

---

### P14: Survey Analyzer

**Problem:** Process and visualize survey responses.

**Core Features:**
1. Load survey data from CSV
2. For numeric questions: calculate mean, median, mode
3. For multiple-choice: count responses
4. Generate formatted report
5. Visualize distribution with ASCII bar chart

**Requirements:**
- Parse CSV
- Statistical calculations
- String-based visualization (using `*` or `#`)

**Example Output:**
```
Question: How satisfied are you? (1-5)
1 ████ 4 responses
2 ██████ 6 responses
3 ███████████ 11 responses
4 ████████████████ 16 responses
5 ██████ 6 responses
```

---

### P15: Inventory Management System (Comprehensive)

**Problem:** Build a complete inventory system for a small business.

**Core Features:**
1. Store inventory: item name, quantity, price per unit
2. Menu:
   - Add item
   - Remove item
   - Update quantity
   - Calculate total value
   - Generate inventory report
3. Save/load from file
4. Low-stock warnings (alert if quantity < threshold)
5. Search/filter items

**Requirements:**
- Complex data structures (list of dicts or nested dicts)
- Multiple file operations (save, load)
- Calculations (total value, reorder alerts)
- Robust error handling

**Data Structure Hint:**
```python
inventory = {
    "widget": {
        "quantity": 50,
        "price": 9.99,
        "min_stock": 10
    }
}
```

---

## Implementation Tips for All Problems

### General Approach

1. **Plan first:** Write pseudocode before coding
2. **Build incrementally:** One feature at a time
3. **Test as you go:** Don't wait until the end
4. **Error handling:** Every input and file operation needs it
5. **User experience:** Clear menus, friendly messages

### Code Quality Checklist

- [ ] All functions have docstrings
- [ ] Variable names are descriptive
- [ ] No code duplication (use functions)
- [ ] Error handling throughout
- [ ] Comments on complex logic
- [ ] Consistent indentation

### Testing Checklist

- [ ] Normal cases work
- [ ] Edge cases handled (empty, 0, max)
- [ ] Error cases don't crash (bad input, missing file)
- [ ] Menu works as expected
- [ ] Save/load works correctly

---

## Choosing Your Project

**Consider:**
1. **Interest:** Pick something YOU find interesting
2. **Scope:** Don't pick something too big (or too small)
3. **Skills:** Should stretch your skills, not be impossible
4. **Real-world use:** Imagine a real person using it

**Sweet spot:** Medium difficulty project that interests you!

---

**Good luck with your projects!** 🚀
