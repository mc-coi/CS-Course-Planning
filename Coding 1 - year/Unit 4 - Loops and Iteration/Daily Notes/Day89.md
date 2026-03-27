# Day 89: Mini-Project Start — Number Analyzer or Quiz Game

**Learning Target:** I can apply loops and lists to create an interactive, complete program with user input, data processing, and output.

### Key Concepts

This mini-project integrates all Unit 4 learning:
- Loops (while, for)
- Lists and list methods
- Input validation
- Data analysis
- Interactive programs

Choose one project to complete over Days 89–90.

### Project Options

**Option A: Number Analyzer**
A program that collects numbers from the user, then analyzes them statistically.

**Features:**
- Ask for numbers until user enters "done" or a sentinel value (e.g., -1)
- Store in a list
- Calculate: sum, average, count, highest, lowest, median
- Display results in a formatted report
- Option to sort and display all numbers

**Sample Run:**
```
=== NUMBER ANALYZER ===
Enter numbers (type 'done' to stop):
Number 1: 85
Number 2: 92
Number 3: 78
Number 4: 95
Number 5: done

=== ANALYSIS ===
Count: 4
Sum: 350
Average: 87.5
Highest: 95
Lowest: 78
Sorted: [78, 85, 92, 95]
```

---

**Option B: Quiz Game**
A program where the user answers questions, tracks score, and provides feedback.

**Features:**
- Define 5–10 quiz questions with answers
- Ask questions in random or sequential order
- Track correct/incorrect answers
- Calculate and display final score
- Option to play again
- Display detailed feedback

**Sample Run:**
```
=== QUIZ GAME ===
Question 1 of 5: What is the capital of France?
Your answer: Paris
Correct!

Question 2 of 5: What is 5 + 3?
Your answer: 7
Incorrect. The answer is 8.

...

=== RESULTS ===
Score: 4 / 5 (80%)
Correct: 4
Incorrect: 1
Play again? (yes/no): no
Thanks for playing!
```

---

### Guided Practice

**For Option A:**
- Write the input collection loop
- Test the list building with sample numbers
- Verify each calculation (sum, average, min, max)

**For Option B:**
- Create a list of question dictionaries (question, answer)
- Test asking and validating one question
- Test score tracking
- Test replay loop

### Implementation Steps

**Day 89 (Today): Planning & Setup**
1. Choose your project
2. Write pseudocode or flowchart
3. Define variables and data structures
4. Start coding input/list building

**Day 90: Complete & Test**
1. Finish core functionality
2. Add calculations/analysis
3. Format output nicely
4. Test edge cases
5. Peer review and feedback

### Starter Code Template

```python
# Mini-Project: [Option A or B]
# Name: ___________________
# Date: ___________________

# ===== INPUT =====
# Collect data from user
data = []
while True:
    # Get user input
    value = input("Enter value ('done' to stop): ")
    if value == "done":
        break
    # Add to list
    data.append(value)

# ===== PROCESSING =====
# Calculate results

# ===== OUTPUT =====
# Display results
print("\n=== RESULTS ===")
```

### Grading Criteria (for both options)

- **Functionality (40%):** Does the program run without errors? Do all features work?
- **Data Handling (20%):** Are lists used correctly? Are calculations accurate?
- **User Experience (20%):** Is the interface clear? Does it ask for input correctly?
- **Code Quality (10%):** Is code readable? Are variable names descriptive? Are comments present?
- **Completeness (10%):** Did you include all planned features?

---

## Mini-Project Checklist

Before submitting:
- [ ] Program runs without crashing
- [ ] All input validation works (only accepts valid input)
- [ ] Lists are used correctly (append, methods, loops)
- [ ] All calculations are accurate
- [ ] Output is formatted nicely (labels, alignment)
- [ ] Code is commented and readable
- [ ] Tested with multiple inputs
- [ ] Ready to share with peer reviewer

---
