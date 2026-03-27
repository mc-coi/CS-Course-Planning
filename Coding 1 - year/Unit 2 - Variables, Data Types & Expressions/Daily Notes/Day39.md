# Day 39: Mini-Project Work Day — Student Choice Calculator Program

**Learning Target:** I can design and build a complete calculator program of my choice using all Unit 2 concepts.

### Project Overview

**Your task:** Choose a real-world calculator program to build. This is your opportunity to apply everything you've learned in Unit 2 in a project YOU find interesting.

**Requirements:**
1. Program must accept user input (at least 2 inputs)
2. Must perform calculations using multiple operations
3. Must include at least one constant
4. Must use proper variable naming (snake_case)
5. Must validate at least one input
6. Must format output professionally (use f-strings with appropriate decimals)
7. Must be at least 20 lines of code
8. Must include comments explaining what your code does

**Project Ideas:**

1. **Personal Finance:**
   - Retirement calculator (how much to save for retirement)
   - Investment compound interest calculator
   - Budget tracker
   - Student loan payment calculator
   - Home mortgage calculator

2. **Health & Fitness:**
   - Calorie counter
   - Workout time calculator
   - Water intake calculator
   - Heart rate zone calculator
   - Protein intake calculator

3. **Travel:**
   - Trip cost splitter
   - Gas mileage and fuel cost calculator
   - Currency converter
   - Distance and time calculator
   - Luggage weight calculator

4. **School:**
   - GPA calculator
   - Study time tracker
   - Grade needed calculator (what grade do I need on the final?)
   - Quiz average calculator
   - Assignment point tracker

5. **Fun & Games:**
   - Dice game scorer
   - Sports statistics calculator
   - Video game level cost calculator
   - Party event cost calculator
   - Cooking recipe scaler

### Project Checklist

Before you start coding:
- [ ] Choose your calculator type
- [ ] Plan your inputs (what will user enter?)
- [ ] Plan your calculations (what math will you do?)
- [ ] Plan your output (what will you display?)
- [ ] Identify any constants you'll use
- [ ] Think about validation (what inputs might be invalid?)

### Guided Practice: Example Project

**Fitness Calorie Counter**
```python
# Calorie Counter Calculator
# This program helps track daily calorie intake

# Constants for different foods (calories per serving)
APPLE_CALORIES = 95
SANDWICH_CALORIES = 350
SODA_CALORIES = 140
PIZZA_SLICE_CALORIES = 285

DAILY_CALORIE_GOAL = 2000

# Get user input
print("=== Daily Calorie Tracker ===")
apples = int(input("How many apples? "))
sandwiches = int(input("How many sandwiches? "))
sodas = int(input("How many sodas? "))
pizza_slices = int(input("How many pizza slices? "))

# Calculate total calories
apple_total = apples * APPLE_CALORIES
sandwich_total = sandwiches * SANDWICH_CALORIES
soda_total = sodas * SODA_CALORIES
pizza_total = pizza_slices * PIZZA_SLICE_CALORIES

total_calories = apple_total + sandwich_total + soda_total + pizza_total
remaining = DAILY_CALORIE_GOAL - total_calories

# Display results
print(f"\n=== Daily Summary ===")
print(f"Apples: {apple_total} cal")
print(f"Sandwiches: {sandwich_total} cal")
print(f"Sodas: {soda_total} cal")
print(f"Pizza: {pizza_total} cal")
print(f"Total: {total_calories} cal")
print(f"Goal: {DAILY_CALORIE_GOAL} cal")
if remaining >= 0:
    print(f"Remaining: {remaining} cal")
else:
    print(f"Over goal by {-remaining} cal")
```

### Your Project Template

```python
# [Project Name and Description]
# [Your name]
# [Date]

# === CONSTANTS ===
# Define any constants here (e.g., tax rates, conversion factors)

# === MAIN PROGRAM ===
print("=== [Program Title] ===")

# Get user inputs
# Validate inputs
# Perform calculations
# Display results

print("Thank you for using [Program Name]!")
```

### Submission Checklist

When you're done, make sure:
- [ ] Your program runs without errors
- [ ] All inputs are validated
- [ ] Output is formatted professionally
- [ ] Code includes comments
- [ ] Variable names are descriptive (snake_case)
- [ ] Constants are used appropriately (UPPER_CASE)
- [ ] You tested with different inputs

### Grading Rubric

- **Functionality (40%):** Program runs, accepts inputs, performs calculations, produces output
- **Code Quality (30%):** Good naming, proper formatting, comments, constants used
- **Calculations (20%):** Correct math, proper rounding for money if applicable
- **Validation (10%):** Checks user input and handles errors gracefully

---

## Project Showcase

Share your project with classmates!
- Run your program for a peer
- Explain what it does
- Discuss your design choices
- Ask for feedback

