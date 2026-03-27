# Day 69: Unit 3 Assessment

**Learning Target:** I can demonstrate mastery of conditional logic through written and coding assessments.

---

## Assessment Overview

**Format:**
- Part 1: Written Questions (20 minutes)
- Part 2: Code Tracing (15 minutes)
- Part 3: Code Writing (20 minutes)

**Grading:**
- Each part: 30-35 points
- Total: 100 points

---

## Part 1: Written Questions (30 points)

Answer in complete sentences unless otherwise noted.

**Question 1 (3 points):** Explain the difference between `=` and `==`.
- `=` is the assignment operator; assigns value to variable
- `==` is the comparison operator; returns True/False

**Question 2 (3 points):** When would you use `if` vs `elif` vs `else`?
- `if`: Initial condition to test
- `elif`: Additional condition if previous was False
- `else`: Catch all remaining cases

**Question 3 (3 points):** What does short-circuit evaluation mean?
- With `and`: if first is False, second not checked
- With `or`: if first is True, second not checked

**Question 4 (3 points):** What are truthy and falsy values?
- Falsy: False, 0, "", [], None
- Truthy: True, non-zero numbers, non-empty strings/lists

**Question 5 (3 points):** Explain the difference between `and` and `or`.
- `and`: Both conditions must be True
- `or`: At least one must be True

**Question 6 (3 points):** When should you use a nested conditional?
- When one decision depends on another
- When you need hierarchical logic

**Question 7 (3 points):** What is input validation and why does it matter?
- Checking that input meets requirements before using it
- Prevents crashes and incorrect calculations

**Question 8 (3 points):** What does a flag variable do?
- Tracks state (Boolean variable)
- Simplifies complex conditions

**Question 9 (3 points):** What does indentation do in Python?
- Defines code blocks
- Determines which code belongs to if/elif/else

**Question 10 (3 points):** Explain DeMorgan's Law.
- `not (A and B)` = `(not A) or (not B)`
- `not (A or B)` = `(not A) and (not B)`

---

## Part 2: Code Tracing (35 points)

Trace each program and predict output WITHOUT running code.

**Trace 1 (8 points):**
```python
x = 10
if x > 5:
    print("Big")
else:
    print("Small")
print("Done")
```
**Output:**
```
Big
Done
```

**Trace 2 (8 points):**
```python
score = 75
if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
else:
    print("F")
```
**Output:**
```
C
```

**Trace 3 (8 points):**
```python
x = 5
y = 3
if x > y and y > 0:
    print("Both true")
else:
    print("Not both")
```
**Output:**
```
Both true
```

**Trace 4 (11 points):**
```python
age = 20
has_license = True

if age >= 18:
    print("Adult")
    if has_license:
        print("Can drive")
else:
    print("Minor")
```
**Output:**
```
Adult
Can drive
```

---

## Part 3: Code Writing (35 points)

Write programs to solve these problems.

**Problem 1 (10 points) — Beginner:**

Write a program that asks for a test score and prints:
- "A" if score >= 90
- "B" if score >= 80
- "C" if score >= 70
- "D" if score >= 60
- "F" if score < 60

```python
score = int(input("Score: "))

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
elif score >= 60:
    print("D")
else:
    print("F")
```

**Requirements:**
- [ ] Accepts input
- [ ] Uses if/elif/else correctly
- [ ] Prints correct grade
- [ ] Works for all ranges

---

**Problem 2 (12 points) — Intermediate:**

Write a program that validates a password. A password is valid if:
- At least 8 characters long
- Contains at least one uppercase letter
- Contains at least one digit

If valid, print "✓ Valid password"
If invalid, print "✗ Invalid" and list what's wrong

```python
password = input("Password: ")

is_long = len(password) >= 8
has_upper = any(c.isupper() for c in password)
has_digit = any(c.isdigit() for c in password)

if is_long and has_upper and has_digit:
    print("✓ Valid password")
else:
    print("✗ Invalid")
    if not is_long:
        print("  - Too short (need 8+)")
    if not has_upper:
        print("  - Missing uppercase")
    if not has_digit:
        print("  - Missing digit")
```

**Requirements:**
- [ ] Accepts password input
- [ ] Checks all three conditions
- [ ] Provides specific feedback
- [ ] Validates correctly

---

**Problem 3 (13 points) — Challenge:**

Write a program that determines if someone can ride a roller coaster. They can ride if:
- At least 48 inches tall
- Age 8 or older
- No heart conditions

If they can't ride, explain why.

```python
height = int(input("Height (inches): "))
age = int(input("Age: "))
has_condition = input("Heart condition? (yes/no): ").lower()

tall_enough = height >= 48
old_enough = age >= 8
no_condition = has_condition != "yes"

if tall_enough and old_enough and no_condition:
    print("✓ You can ride!")
else:
    print("✗ You cannot ride")
    if not tall_enough:
        print("  - Too short (need 48\")")
    if not old_enough:
        print("  - Too young (need 8+)")
    if not no_condition:
        print("  - Medical restriction")
```

**Requirements:**
- [ ] Accepts three inputs
- [ ] Uses multiple conditions
- [ ] Determines eligibility correctly
- [ ] Explains why if denied
- [ ] Handles all cases

---

## Assessment Rubric

### Written Questions (30 points)
- Accuracy: 2-3 points each
- Completeness: Full explanations

### Code Tracing (35 points)
- Correct output: 7-11 points each
- Step-by-step accuracy

### Code Writing (35 points)
- **Functionality (15):** Works correctly, all cases
- **Code Quality (10):** Clear names, good indentation
- **Completeness (10):** Meets all requirements

---

## Test-Taking Strategies

1. **Read carefully:** Understand what each question asks
2. **Answer what's asked:** Don't add extra
3. **Show your work:** Write out condition evaluations
4. **Test your code:** Mentally run through examples
5. **Check syntax:** Colons, indentation, operators
6. **Manage time:** 20 min written, 15 min tracing, 20 min coding

---

## What to Review Before Assessment

- [ ] Truth tables (and/or/not)
- [ ] Comparison operators (all 6)
- [ ] if/elif/else structure
- [ ] Nested conditionals
- [ ] Input validation
- [ ] Common mistakes from Day 68
- [ ] Code tracing examples

---

## Assessment Day Checklist

**Before Assessment:**
- [ ] Get good sleep
- [ ] Eat breakfast
- [ ] Bring pencil and paper
- [ ] Clear mind, ready to focus

**During Assessment:**
- [ ] Read questions carefully
- [ ] Show your work
- [ ] Check for syntax errors
- [ ] Test mentally before writing

**After Assessment:**
- [ ] Review your answers
- [ ] Check all sections complete
- [ ] Submit on time

---

## Good Luck!

You've worked hard this unit. You understand conditionals thoroughly. Trust your learning and do your best!

---

*Remember: The goal is to show what you've learned, not to be perfect. Do your best and be honest about your understanding.*
