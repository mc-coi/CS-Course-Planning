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