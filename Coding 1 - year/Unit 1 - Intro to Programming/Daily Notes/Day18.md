# Day 18: Mini-Project — Build a Complete Program from Scratch
**Learning Target:** I can design, code, and test a complete beginner program from scratch.

### Key Concepts
This day is your chance to showcase everything you've learned. You'll:
1. Choose or be given a real-world problem
2. Follow the 5-step development process
3. Create a complete, working program
4. Test it thoroughly
5. Present clean, well-commented code

### Guided Practice - Choose ONE Project

**Project A: Personal Expense Calculator**
- Collect: expense name, amount, category
- Calculate: total expenses, average expense
- Display: formatted summary
- Requirements: 3+ inputs, 1+ calculation, clear output

**Project B: Grade Calculator**
- Collect: student name, 4 test scores
- Calculate: average, letter grade (90+=A, 80+=B, 70+=C, 60+=D, <60=F)
- Display: formatted grade report
- Requirements: string input, multiple numeric inputs, calculations, formatted output

**Project C: Trip Budget Planner**
- Collect: destination, days, daily budget
- Calculate: total budget, recommended daily spending by category (accommodation 40%, food 35%, activities 25%)
- Display: formatted budget breakdown
- Requirements: multiple inputs, multiple calculations, formatted output

**Project D: Time Tracker**
- Collect: task name, hours worked, hourly rate
- Calculate: total pay, projected weekly/monthly earnings
- Display: formatted payment details
- Requirements: inputs, calculations with proper order of operations, formatting

### Requirements for Any Project
- **Input:** At least 3 different inputs using `input()`
- **Variables:** At least 4 variables of mixed types
- **Calculations:** At least 2 mathematical operations
- **Comments:** At least 3 comments explaining your code
- **Output:** Clear, formatted output using f-strings
- **Testing:** Evidence that you tested with multiple inputs

### Sample Program Structure
```python
# ===== PROGRAM TITLE & PURPOSE =====
# This program [what it does]

# Step 1: Define & Plan (comments)
# Inputs: ...
# Calculation: ...
# Output: ...

# Step 3: Code
# Collect inputs
name = input("Name: ")
value1 = float(input("Value 1: "))
value2 = float(input("Value 2: "))

# Perform calculations
result = value1 + value2
average = result / 2

# Display results
print(f"\n=== RESULTS ===")
print(f"Name: {name}")
print(f"Total: {result:.2f}")
print(f"Average: {average:.2f}")

# Step 4: Testing notes:
# - Tested with: ...
# - Verified: ...
```

### Practice Problems (Pick 1 to complete)

**Option 1 (Beginner):** Create a simple interest calculator.
- Input: principal, rate (%), years
- Calculate: simple interest = principal × rate × years / 100, total = principal + interest
- Output: formatted statement showing starting amount, interest, and total

**Option 2 (Intermediate):** Create a restaurant bill calculator.
- Input: subtotal, tip percentage, tax rate
- Calculate: tax amount, tip amount, total
- Output: itemized receipt

**Option 3 (Challenge):** Create a home workout tracker.
- Input: name, exercises (count), minutes, calories burned
- Calculate: calories per minute, projected daily total (if 2 more workouts)
- Output: detailed workout summary with projections

### Submission Checklist
- [ ] Program runs without errors
- [ ] Has 3+ inputs
- [ ] Has 4+ variables
- [ ] Has 2+ calculations
- [ ] Has 3+ comments
- [ ] Uses f-strings for output
- [ ] Output is clear and labeled
- [ ] Tested with at least 2 different inputs

---
