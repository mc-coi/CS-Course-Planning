# Day 64: Mini-Project Work Day

**Learning Target:** I can independently plan and build a complete conditional-based program of my choosing.

---

## Project Overview

Today you'll create your own program that demonstrates mastery of conditionals. You have flexibility in topic—choose something that interests you!

---

## Project Requirements

Your project must include:

**Core Requirements:**
- [ ] At least 3 inputs from user
- [ ] At least 5 decision branches (if/elif/else)
- [ ] At least 1 nested conditional
- [ ] At least 1 logical operator (and/or/not)
- [ ] Input validation or error handling
- [ ] Clear, formatted output
- [ ] At least 5 comments explaining logic
- [ ] No syntax errors

**Code Quality:**
- [ ] Descriptive variable names
- [ ] Consistent indentation
- [ ] Readable and organized
- [ ] Functions used (optional but encouraged)

---

## Project Ideas

### Game Projects
1. **Enhanced Rock-Paper-Scissors:** Multiple rounds, scoring, different strategies
2. **Dice Roller Game:** Roll dice, bet, determine winner
3. **Quiz Game:** Ask questions, score answers, provide feedback
4. **Card Game (simplified):** Deal cards, determine winner
5. **Coin Flip Game:** Heads/tails with betting

### Utility Projects
1. **Grade Calculator:** Accept grades, calculate GPA and letter grade with details
2. **Loan Calculator:** Determine if loan is approved based on criteria
3. **Schedule Planner:** Ask for tasks and priorities, organize output
4. **Expense Tracker:** Categorize spending and provide feedback
5. **Appointment Scheduler:** Book appointments with conflict checking

### Decision Projects
1. **Career Recommendation:** Ask about skills, recommend careers
2. **Movie Recommender:** Ask about preferences, recommend movies
3. **Restaurant Selector:** Based on budget/cuisine, recommend options
4. **College Admission Helper:** Check if student meets requirements
5. **Shopping Cart Discount Calculator:** Apply discounts based on amount/items

### Analysis Projects
1. **Triangle Validator:** Determine if sides form valid triangle, classify type
2. **Number Analyzer:** Check if prime, perfect, abundant, etc.
3. **Weather Advisor:** Suggest clothing based on temperature/conditions
4. **Fitness Goals:** Calculate BMI, give recommendations
5. **Water Intake Calculator:** Determine daily water needs based on activity

---

## Getting Started Checklist

**Step 1: Choose Your Project**
- [ ] Pick a topic from above, or design your own
- [ ] Write down the main goal (1 sentence)

**Step 2: Plan the Logic**
- [ ] List all inputs needed
- [ ] List all decision branches
- [ ] Sketch decision logic (flowchart or outline)

**Step 3: Build the Program**
- [ ] Write basic structure (inputs, conditionals, output)
- [ ] Test with valid inputs
- [ ] Add error handling
- [ ] Add comments
- [ ] Clean up formatting

**Step 4: Test Thoroughly**
- [ ] Test happy path (everything works)
- [ ] Test edge cases (min/max values)
- [ ] Test invalid input
- [ ] Verify all branches execute

**Step 5: Review & Polish**
- [ ] Check variable names are clear
- [ ] Check indentation is consistent
- [ ] Check comments explain logic
- [ ] Run one final time without errors

---

## Template to Get Started

```python
# PROJECT TITLE
# Description: What does your program do?

# [Your program here]

print("Program complete!")
```

---

## Example Projects (Choose One or Modify)

### Example 1: Movie Recommendation System
```python
print("=== Movie Recommender ===")

# Get preferences
genre = input("Preferred genre (action/comedy/drama): ").lower()
rating = input("Minimum rating (G/PG/PG-13/R): ").upper()
year = int(input("Prefer recent movies? (2020+)? (yes/no): "))

# Determine recommendation
if genre == "action":
    if rating in ["G", "PG"]:
        movie = "Top Gun"
    elif rating == "PG-13":
        movie = "Avengers"
    else:
        movie = "John Wick"
elif genre == "comedy":
    movie = "The Grand Budapest Hotel"
else:  # drama
    movie = "The Shawshank Redemption"

print(f"Recommended: {movie}")
```

### Example 2: Grade Improvement Advisor
```python
print("=== Grade Advisor ===")

current_grade = int(input("Current grade: "))
attendance = int(input("Attendance % (0-100): "))
participation = input("Participate in class? (yes/no): ").lower()

# Calculate advice
if current_grade >= 90:
    status = "Excellent"
    advice = "Keep up the great work!"
elif current_grade >= 80:
    status = "Good"
    if attendance < 80:
        advice = "Improve attendance"
    else:
        advice = "Study challenging topics"
elif current_grade >= 70:
    status = "Satisfactory"
    advice = "Attend tutoring sessions"
else:
    status = "Failing"
    advice = "Meet with teacher immediately"

print(f"Status: {status}")
print(f"Action: {advice}")
```

### Example 3: Gaming Console Selector
```python
print("=== Console Selector ===")

# Get preferences
budget = int(input("Budget ($): "))
games = input("Favorite game type (action/rpg/sports): ").lower()
online = input("Want online play? (yes/no): ").lower()

# Recommend console
if budget < 300:
    console = "Nintendo Switch"
elif budget < 400:
    if games == "action":
        console = "PlayStation 5"
    else:
        console = "Xbox Series X"
elif budget >= 400:
    console = "High-end PC"
else:
    console = "Unknown"

print(f"Recommended: {console}")
```

---

## Grading Rubric

| Criteria | Points | Notes |
|----------|--------|-------|
| Functionality | 40 | Works correctly; no errors |
| Requirements | 30 | Has all required components |
| Code Quality | 20 | Clear names; good indentation |
| Comments | 10 | Explains logic |

---

## Getting Help

If you're stuck:
1. **Review previous daily notes** for similar patterns
2. **Work with a partner** to talk through logic
3. **Draw a flowchart** to clarify decision flow
4. **Test incrementally** (build piece by piece)
5. **Use print() statements** to debug

---

## Reflection Questions (Answer Before Submitting)

1. What was the hardest part of your project?
2. Which conditional pattern did you use most?
3. What inputs did your program need to handle?
4. How would you improve your program?
5. What would you do if you had more time?

---

## Submission Checklist

Before turning in:
- [ ] Program runs without errors
- [ ] All features work as intended
- [ ] All requirements met
- [ ] Comments present
- [ ] Variable names are clear
- [ ] Indentation is consistent
- [ ] Test cases pass
- [ ] Reflection questions answered

---

## Bonus Challenges

If you finish early:
1. Add more decision branches
2. Add multiple rounds/loops (preview)
3. Save results to a file
4. Add difficulty levels
5. Combine with features from previous units

---

## Key Skills Demonstrated

By completing this project, you demonstrate:
- [ ] Understanding of conditional logic
- [ ] Ability to plan program structure
- [ ] Input/output handling
- [ ] Error handling
- [ ] Code organization and clarity
- [ ] Independent problem-solving
