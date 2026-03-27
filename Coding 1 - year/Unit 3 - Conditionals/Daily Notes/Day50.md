# Day 50: Practice Lab — Boolean Expression Evaluator

**Learning Target:** I can evaluate complex Boolean expressions, combine operators correctly, and build interactive tools.

---

## Learning Summary (Week 10 Review)

This week you learned:
1. **Boolean expressions** evaluate to True or False
2. **Comparison operators** (==, !=, <, >, <=, >=) create Boolean results
3. **Logical operators** (and, or, not) combine expressions
4. **Chained comparisons** make code more Pythonic
5. **Boolean flags** simplify and clarify complex conditions

---

## Practice Lab: Boolean Expression Evaluator

### Project Overview

Build an interactive program that tests the user's understanding of Boolean logic. The program will:

1. Ask the user to evaluate Boolean expressions
2. Check their answer
3. Provide feedback (correct/incorrect)
4. Track score
5. Offer a menu of difficulty levels

### Requirements

**Minimum Requirements:**
- [ ] At least 10 Boolean expressions to evaluate (mix of all types)
- [ ] Accept user input (True/False answer)
- [ ] Give feedback ("Correct!" or "Incorrect! It was [answer]")
- [ ] Track and display final score
- [ ] Include at least:
  - 2 comparison operator questions
  - 2 logical operator (and/or/not) questions
  - 2 chained comparison questions
  - 2 compound condition questions
  - 2 flag/variable-based questions

**Code Quality:**
- [ ] Clear variable names
- [ ] Comments explaining logic
- [ ] Consistent indentation
- [ ] At least 4 comments total

**Stretch Goals (Optional):**
- [ ] Multiple difficulty levels
- [ ] Hints for wrong answers
- [ ] Show the working (step-by-step evaluation)
- [ ] Save high score

---

## Starter Code

```python
# Boolean Expression Evaluator
# ==============================

# Question 1: Simple comparison
q1 = "5 > 3"
answer1 = True  # CORRECT ANSWER

# Question 2: Logical and
q2 = "5 > 3 and 2 < 1"
answer2 = False

# Question 3: not operator
q3 = "not False"
answer3 = True

# Question 4: Chained comparison
q4 = "1 <= 5 <= 10"
answer4 = True

# Question 5: or operator
q5 = "10 == 10 or 5 == 3"
answer5 = True

# ... add more questions ...

# Main program
print("=== Boolean Expression Evaluator ===")
print()

# Question 1
print(f"Question 1: {q1}")
user_answer1 = input("True or False? ").strip().capitalize()
user_answer1 = user_answer1 == "True"

if user_answer1 == answer1:
    print("✓ Correct!")
    score = 1
else:
    print(f"✗ Incorrect. The answer is {answer1}")
    score = 0

# ... repeat for remaining questions ...

print()
print(f"Final Score: {score}/10")
```

---

## Example Questions to Include

### Comparison Operators
```python
q = "10 >= 10"       # True
q = "7 != 7"         # False
```

### Logical Operators
```python
q = "True and False"  # False
q = "True or False"   # True
q = "not True"        # False
```

### Chained Comparisons
```python
q = "1 <= 5 <= 10"    # True
q = "5 < 5 < 10"      # False
```

### Compound Conditions
```python
q = "(5 > 3) and (10 < 20)"    # True
q = "(5 > 10) or (5 == 5)"     # True
```

### With Variables
```python
# Set up: age = 17, has_license = True
q = "age >= 16 and has_license"  # True
```

---

## Testing Checklist

Before submitting, test:
- [ ] Program runs without errors
- [ ] All 10 questions are asked
- [ ] Score is calculated correctly
- [ ] Correct answers are marked correctly
- [ ] Incorrect answers show the right answer
- [ ] Final score displays properly
- [ ] Input is accepted case-insensitively (if possible)

---

## Sample Solution (Partial)

```python
# Boolean Expression Evaluator - Sample Solution
print("=== Boolean Expression Evaluator ===")
print("Evaluate each expression and enter True or False\n")

score = 0

# Question 1
print("Question 1: 5 > 3")
try:
    answer = input("True or False? ").strip().capitalize()
    user_answer = answer == "True"
    if user_answer == True:
        print("✓ Correct!\n")
        score += 1
    else:
        print("✗ Incorrect. The answer is True\n")
except:
    print("Please enter True or False\n")

# Question 2
print("Question 2: 5 > 3 and 2 < 1")
try:
    answer = input("True or False? ").strip().capitalize()
    user_answer = answer == "True"
    if user_answer == False:
        print("✓ Correct!\n")
        score += 1
    else:
        print("✗ Incorrect. The answer is False\n")
except:
    print("Please enter True or False\n")

# ... continue for questions 3-10 ...

# Final Score
print(f"=== Final Score: {score}/10 ===")
if score >= 8:
    print("Excellent!")
elif score >= 6:
    print("Good job!")
else:
    print("Review and try again!")
```

---

## Grading Rubric

| Criteria | Points | Notes |
|----------|--------|-------|
| Functionality | 40 | All questions work, scoring is correct |
| Code Quality | 30 | Clear names, good indentation, comments |
| Completeness | 20 | 10 diverse questions, all working |
| Testing | 10 | Tested thoroughly, handles inputs well |

---

## Challenge Extension

**If you finish early:**

1. **Add difficulty levels:** Easy (comparisons only), Medium (mixed), Hard (complex compound conditions)
2. **Add hints:** When a student gets a question wrong, provide a hint
3. **Show working:** Display step-by-step evaluation for complex expressions
4. **Save results:** Use a file to track attempts and high scores
5. **Time limit:** Give 30 seconds per question (use `time` module)

---

## Reflection Questions

After completing this lab, reflect:

1. Which type of expression was hardest to evaluate?
2. What mistakes did you make? How would you avoid them?
3. How could you improve this program?
4. What real-world uses do Boolean expressions have?

---

## Key Skills Demonstrated

By completing this lab, you can:
- [ ] Evaluate Boolean expressions correctly
- [ ] Combine operators (and, or, not)
- [ ] Read and understand complex conditions
- [ ] Write interactive programs with user input
- [ ] Track state with variables
- [ ] Provide user feedback
