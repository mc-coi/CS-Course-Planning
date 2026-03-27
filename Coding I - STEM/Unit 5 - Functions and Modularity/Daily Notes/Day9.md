# Day 9: Unit 5 Project — Modular Application

### Project Options

**Option A — Grade Calculator**
Build a modular grade calculator with:
- `get_scores()` — collect scores from user until they type "done"
- `calculate_average(scores)` — return the average
- `letter_grade(average)` — return A/B/C/D/F
- `print_report(name, scores, average, grade)` — formatted output
- `main()` — orchestrates everything

**Option B — Modular Quiz Game**
Build a modular quiz with:
- `load_questions()` — return a list of question dictionaries
- `ask_question(q)` — display and return whether answered correctly
- `run_quiz(questions)` — loop through all questions
- `show_results(correct, total)` — display final score and grade
- `main()` — ties it together

**Option C — Simple Number Cruncher**
Build a modular stats program with:
- `get_numbers()` — collect numbers from user
- `calculate_sum(numbers)` — return total
- `calculate_average(numbers)` — return mean
- `find_outliers(numbers, threshold)` — return values far from average
- `print_stats(numbers)` — display all stats neatly
- `main()` — run everything

### Template to Get Started

```python
# ── Unit 5 Project: [YOUR TITLE HERE] ─────────────────────

def main():
    # This function runs the whole program
    # Step 1: Get input
    # Step 2: Process
    # Step 3: Display results
    pass

# Define your helper functions here:

def get_input():
    pass

def process_data(data):
    pass

def display_results(results):
    pass

# Run the program:
main()
```

### Evaluation Checklist
- [ ] At least 4 functions defined
- [ ] Each function has exactly one job
- [ ] At least one function uses parameters
- [ ] At least one function uses `return`
- [ ] `main()` ties everything together
- [ ] No global variables (use parameters/returns)
- [ ] Code is readable with clear variable names
- [ ] Program runs without errors

---