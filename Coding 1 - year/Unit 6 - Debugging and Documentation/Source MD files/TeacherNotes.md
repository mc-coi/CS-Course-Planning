# Unit 6 - Debugging and Documentation: Teacher Misconception & Callout Guide

## Overview

Unit 6 is about recognizing and fixing errors—both the obvious (syntax errors that prevent code from running) and the subtle (logic errors that produce wrong answers). The biggest teaching challenges are: (1) students panic when they see error messages instead of using them as debugging guides; (2) they don't distinguish between syntax, runtime, and logic errors, so they approach all errors the same way; (3) they don't know how to systematically test their code, testing only "happy paths" (normal inputs) and missing edge cases; (4) they use print statements haphazardly instead of strategically for debugging; and (5) they write unclear comments and no docstrings, making their code hard to maintain. These misconceptions prevent students from debugging effectively on their own, forcing them to seek help for every error instead of developing independence.

---

## Misconceptions by Topic

### Three Error Types: Syntax, Runtime, Logic (Days 121–123)

**⚠️ Misconception:** "An error means my code is broken" OR "All errors are the same; I approach them the same way."

**What it looks like in code:**
```python
# SYNTAX ERROR (code won't run):
print("Hello   # Missing closing quote
if x > 5       # Missing colon

# RUNTIME ERROR (code crashes while running):
x = 10 / 0     # ZeroDivisionError
items = [1, 2]
print(items[5])  # IndexError: list index out of range

# LOGIC ERROR (code runs but gives wrong answer):
# Program: Calculate average of two numbers
total = 10 + 20
average = total / 2  # Forgot to add a third number, should be 3 not 2
print(average)  # Prints 15, but maybe should be different
```

**Why students think this:** They haven't internalized that errors are information. They see "error" as failure. They also don't see the progression: syntax → syntax valid → logic correct.

**How to address it:** **Teach the three categories explicitly:**

| Error Type | When | Example | How to Fix |
|---|---|---|---|
| **Syntax** | Before running | Missing quote, colon, parenthesis | Read error message; Python tells you where |
| **Runtime** | While running | ZeroDivisionError, IndexError, NameError | Read traceback; it shows what went wrong and where |
| **Logic** | Always runs correctly | Wrong formula, wrong condition | Trace through the logic; test with known inputs |

Show each error type:
```python
# SYNTAX: Python stops before running
print("Hello"  # SyntaxError: unterminated string literal

# RUNTIME: Runs, then crashes
result = 10 / int(input("Divisor: "))  # If input is 0, ZeroDivisionError

# LOGIC: Runs fine, wrong answer
age = 25
adult_threshold = 18
is_adult = age < adult_threshold  # BUG: should be >, not <
print(is_adult)  # Prints False, but age 25 should be adult
```

Key teaching move: "Errors are gifts. They tell you exactly what went wrong. Syntax errors are the easiest—Python points them out. Logic errors are the hardest—you have to think through the code yourself."

---

### Reading Tracebacks (Days 121–125)

**⚠️ Misconception:** "Error messages are confusing" OR "I don't know what the traceback is telling me."

**What it looks like in code:**
```python
# Student sees:
Traceback (most recent call last):
  File "program.py", line 5, in <module>
    result = 10 / int(items[5])
IndexError: list index out of range

# And they:
# 1. Panic
# 2. Ask for help without reading the message
# 3. Don't know to look at line 5
# 4. Don't understand "list index out of range"
```

**Why students think this:** Tracebacks use jargon ("Traceback," "module") and the formatting is dense. They don't know how to parse the information.

**How to address it:** **Teach traceback reading as a skill:**

**Structure of a traceback:**
1. **"Traceback (most recent call last):"** - This is a traceback; read from the bottom up usually.
2. **File path and line number** - Where the error happened.
3. **Code line** - What line caused the error.
4. **Error type and message** - What went wrong.

Show an example step-by-step:
```python
items = [1, 2, 3]

# This code has an error:
print(items[5])

# Traceback:
Traceback (most recent call last):
  File "program.py", line 3, in <module>
    print(items[5])
IndexError: list index out of range

# Read it:
# 1. Error type: IndexError
# 2. Line: 3 (print(items[5]))
# 3. Message: "list index out of range" (you're trying to access index 5, but the list only has indices 0, 1, 2)
```

Teach them the systematic approach:
1. **Read the error type** (e.g., "ZeroDivisionError"). Does it tell you what the problem is?
2. **Look at the line number**. Go to that line in your code. What's happening there?
3. **Read the message**. What does it say went wrong?
4. **Check the values**. What were the variables at the time?

Create a "common runtime errors" reference:

| Error | Cause | Fix |
|---|---|---|
| `ZeroDivisionError` | Dividing by 0 | Check if divisor != 0 before dividing |
| `IndexError` | List index out of range | Check if index < len(list) |
| `NameError` | Variable doesn't exist | Define the variable first |
| `TypeError` | Wrong type for operation | Convert types: int(), str(), etc. |
| `ValueError` | Invalid value | Validate input before using |

---

### Common Syntax Errors (Days 121–125)

**⚠️ Misconception:** "I don't know how to fix syntax errors" OR "Syntax errors are random."

**What it looks like in code:**
```python
# Missing colon:
if x > 5  # SyntaxError: expected ':'
    print("x is big")

# Indentation error:
if x > 5:
print("x is big")  # IndentationError: expected an indented block

# Mismatched quotes:
print("Hello world')  # SyntaxError: unterminated string

# Missing closing parenthesis:
print("Hello"  # SyntaxError

# Wrong operator in condition:
if x = 5:  # SyntaxError (or confusing NameError)
    print(x)
```

**Why students think this:** Syntax rules feel arbitrary. They don't realize that syntax errors follow patterns.

**How to address it:** **Create a "most common syntax errors" checklist:**

1. **Missing colon after `if`, `while`, `for`, `def`** - If you see a condition or loop, there's always a `:` at the end.
2. **Indentation error** - Lines inside a block must be indented (4 spaces or 1 tab). All lines in a block must match.
3. **Mismatched quotes** - Every `"` needs a closing `"`. Every `'` needs a closing `'`.
4. **Missing parenthesis** - `print(` needs `)`. Function calls need pairs.
5. **Missing closing bracket** - `[` needs `]`. `{` needs `}`.

Teach them: "When Python says 'syntax error,' look for these five things. Usually, you'll find the problem."

Show the fix pattern:
```python
# ERROR: Missing colon
if x > 5
    print("Big")

# FIX: Add colon
if x > 5:
    print("Big")

# ERROR: Indentation
if x > 5:
print("Big")  # Not indented

# FIX: Indent correctly
if x > 5:
    print("Big")  # Indented
```

---

### Logic Errors: Tracing & Testing (Days 126–135)

**⚠️ Misconception:** "I don't know how to find logic errors" OR "If the code runs without crashing, it's correct."

**What it looks like in code:**
```python
# LOGIC ERROR: Wrong condition
age = 15
if age >= 18:  # BUG: should be <=
    print("Minor")
else:
    print("Adult")
# Prints "Adult" for age 15, which is wrong

# LOGIC ERROR: Wrong formula
# Calculate area of rectangle
length = 5
width = 3
area = length + width  # BUG: should be * not +
print(area)  # Prints 8, but area should be 15

# LOGIC ERROR: Loop condition never reaches end
count = 0
while count < 5:
    print(count)
    count -= 1  # BUG: goes negative, loop runs forever
```

**Why students think this:** Logic errors don't produce error messages. The code looks correct. Finding them requires thinking through the logic, which is hard.

**How to address it:** **Teach systematic debugging:**

**Strategy 1: Trace by Hand**
"Walk through your code step-by-step with a real example. What should happen? What actually happens?"

```python
# Check: Is age 15 an adult or minor?
age = 15
if age >= 18:       # 15 >= 18? No, false
    print("Adult")  # This doesn't run
else:
    print("Minor")  # This runs

# Output: Minor ✓
# But if we expect "Adult" for 15, the condition is wrong
```

**Strategy 2: Print Debugging**
"Add print statements to see what values are really in your variables."

```python
age = 15
print(f"DEBUG: age = {age}")  # Check what age really is
if age >= 18:
    print("Adult")
else:
    print("Minor")

# If the output is unexpected, trace through the condition
```

**Strategy 3: Test with Known Values**
"Run your code with simple values where you know the answer."

```python
# Test the average function
def average(a, b):
    return (a + b) / 2

# Test: average of 10 and 20 should be 15
result = average(10, 20)
print(result)  # If it's not 15, there's a bug
```

Show the testing process:
```
Input: a=10, b=20
Expected: 15
Actual: 15
Status: PASS ✓

Input: a=5, b=5
Expected: 5
Actual: 5
Status: PASS ✓
```

---

### Edge Cases & Boundary Testing (Days 131–135)

**⚠️ Misconception:** "If my code works for normal input, it's fine" OR "I don't need to test edge cases."

**What it looks like in code:**
```python
# Program: Calculate grade average
def average(scores):
    return sum(scores) / len(scores)

# Tests "normal" input:
result = average([80, 90, 85])
print(result)  # Works: 85

# But what about edge cases?
average([])  # ZeroDivisionError: division by zero
average([100])  # Should work: 100

# Program: Check if number is in range
def in_range(x, min_val, max_val):
    return min_val <= x <= max_val

# Tests normal case:
in_range(50, 0, 100)  # True

# Edge cases:
in_range(0, 0, 100)  # Should be True (boundary)
in_range(100, 0, 100)  # Should be True (boundary)
in_range(-1, 0, 100)  # Should be False (below range)
```

**Why students think this:** They test their code once with "normal" input and assume it works. They don't think about edge cases. They also don't realize that edge cases often reveal bugs.

**How to address it:** **Teach edge case thinking:**

**Common edge cases:**
- **Empty:** Empty list, empty string, 0 items
- **Zero:** Especially for division
- **Negatives:** Often forgotten
- **Boundaries:** Min/max values
- **Single item:** Off-by-one errors

Teach a testing process:
```
Test Case | Input | Expected | Actual | Status
---------|-------|----------|--------|-------
Normal | [80, 90] | 85 | 85 | PASS
Empty | [] | ERROR | ZeroDivisionError | FAIL
Single | [90] | 90 | 90 | PASS
```

Show how edge cases reveal bugs:
```python
def count_positives(numbers):
    count = 0
    for num in numbers:
        if num > 0:
            count += 1
    return count

# Normal test:
count_positives([1, 2, 3])  # 3 ✓

# Edge cases:
count_positives([])  # 0 ✓ (empty, returns 0)
count_positives([-1, -2])  # 0 ✓ (no positives)
count_positives([0])  # 0 ✓ (0 is not positive)
```

---

### Exception Handling with try/except (Days 127–135)

**⚠️ Misconception:** "I should avoid errors by writing perfect code" OR "try/except is for advanced programmers."

**What it looks like in code:**
```python
# No error handling:
age_str = input("Age: ")
age = int(age_str)  # ValueError if user types "abc"

# With error handling:
try:
    age = int(input("Age: "))
except ValueError:
    print("Please enter a valid number")

# Over-catching:
try:
    # 50 lines of code
except:  # Catches everything, hides bugs
    pass
```

**Why students think this:** They think errors are bad and should be prevented. They don't see try/except as a way to handle expected errors gracefully.

**How to address it:** **Teach try/except for expected errors:**

"Some errors are expected and expected. When a user types invalid input, `int()` raises a ValueError. Instead of crashing, you can catch that error and ask the user to try again."

Show the pattern:
```python
while True:
    try:
        age = int(input("Age: "))
        break  # Exit loop if conversion succeeds
    except ValueError:
        print("Invalid input. Please enter a number.")
```

Teach specific exception handling:
```python
# BAD: Catches everything
try:
    result = 10 / user_input
except:
    print("Error")

# GOOD: Catches only expected errors
try:
    result = 10 / int(user_input)
except ValueError:
    print("Please enter a number")
except ZeroDivisionError:
    print("Cannot divide by zero")
```

This is useful but not essential for Unit 6. Teach it as a tool for input validation.

---

### Comments That Explain Why (Days 136–140)

**⚠️ Misconception:** "Comments should explain what the code does" OR "I don't need comments if the code is clear."

**What it looks like in code:**
```python
# BAD: Says what code does (obvious)
x = 10  # Set x to 10
if x > 5:  # Check if x is greater than 5
    print(x)  # Print x

# GOOD: Explains why
years_to_save = 10  # Customer wants to save for 10 years
if years_to_save > 5:  # Long-term investments need different strategy
    print(years_to_save)

# Bad: Too many comments
result = a + b  # Add a and b
# Now result is a + b
# This line adds the two variables together

# Good: Meaningful comments at key points
# Apply a 10% discount if order total exceeds $100
discount = 0.1 if total > 100 else 0
final_price = total * (1 - discount)
```

**Why students think this:** They think comments are like captions. They don't understand that good comments explain the *why*, not the *what*.

**How to address it:** **Teach the comment rule:**

**"Comments explain *why*, not *what*. Code shows *what*."**

Show the difference:
```python
# BAD: What (obvious from code)
count = 0  # Initialize count to 0

# GOOD: Why (reasoning)
count = 0  # Will count the number of valid entries; reset for each file

# BAD: What (obvious)
if age >= 18:  # Check if age is 18 or more

# GOOD: Why (reasoning)
if age >= 18:  # Legal voting age in most US states
```

Enforce this: "Comments should explain decisions or non-obvious logic, not restate the code."

---

### Docstrings for Functions (Days 136–140)

**⚠️ Misconception:** "Docstrings are the same as comments" OR "I only need docstrings for public code."

**What it looks like in code:**
```python
# No docstring:
def calculate_tax(amount):
    return amount * 0.08

# Good docstring:
def calculate_tax(amount):
    """Calculate sales tax for a given amount.

    Args:
        amount (float): The purchase amount in dollars

    Returns:
        float: The sales tax (8% of amount)
    """
    return amount * 0.08
```

**Why students think this:** They haven't written reusable functions yet. Docstrings feel optional. They don't see the value.

**How to address it:** **Teach docstrings as part of function design:**

"Docstrings tell someone (including you later!) what a function does, what it expects, and what it returns. Good docstrings make functions reusable."

Simple format:
```python
def function_name(param1, param2):
    """Brief description of what function does.

    Args:
        param1: Description
        param2: Description

    Returns:
        Description of return value
    """
    pass
```

For Unit 6, require a simple one-line docstring at minimum. Don't enforce the full format.

---

### Naming Conventions & Readability (Days 136–140)

**⚠️ Misconception:** "Variable names don't matter" OR "Short names are better."

**What it looks like in code:**
```python
# BAD: Unclear names
a = 10
b = 20
c = a + b

# GOOD: Meaningful names
principal = 10
interest_rate = 20
total_amount = principal + interest_rate

# BAD: Inconsistent capitalization
myVariable = 10
myfunction = lambda x: x + 1
MyClass = object

# GOOD: Consistent (snake_case for variables)
my_variable = 10
my_function = lambda x: x + 1
my_class = object
```

**Why students think this:** They're focused on making the code work, not on communicating. Short names feel efficient.

**How to address it:** **Teach naming as communication:**

"Code is read much more often than it's written. Good names make code readable and maintainable."

Python conventions:
- **Variables and functions:** `snake_case` (lowercase with underscores)
- **Constants:** `UPPER_CASE` (uppercase with underscores)
- **Classes:** `PascalCase` (capitalize first letter of each word)

Show the improvement:
```python
# Before
d = 100
r = 0.05
t = 5
i = d * (r ** t)

# After
principal = 100
rate = 0.05
time = 5
interest = principal * (rate ** time)
```

Enforce this in code reviews: "Is this name clear? Would someone understand what this variable holds?"

---

## Whole-Class Warning Signs

Watch for these patterns—if you see them, **stop and re-teach**:

- **Ignoring error messages:** If students get an error and just change random things without reading the message, teach traceback reading.

- **Testing only happy paths:** If students test with one "normal" input and assume the code is correct, do a class exercise on edge cases.

- **Comments that restate code:** If comments just explain what code does, show the comment rule: explain why, not what.

- **No docstrings:** If functions have no documentation, require a one-line docstring for every function.

- **Using global variables for state:** If functions modify global variables instead of using parameters/returns, this cascades from Unit 5. Reinforce good design.

- **Poor variable names:** If code uses `x`, `temp`, `data` for everything, require meaningful names.

- **No error handling for user input:** If code crashes on invalid input, teach try/except for input validation.

---

## Questions That Reveal Understanding

Ask these to assess real vs. surface-level understanding:

1. **"I got a traceback. How do I figure out what went wrong?"**
   - Good answer: "Read the error type (bottom line), look at the line number, go to that line in my code, and see what value caused the problem."
   - Surface answer: "I don't know" or "Ask the teacher." (Doesn't know how to read tracebacks.)

2. **"What's the difference between a syntax error and a runtime error?"**
   - Good answer: "Syntax errors prevent the code from running (Python can't parse it). Runtime errors happen while the program is running (like dividing by zero)."
   - Surface answer: "One is bad syntax?" (Right idea, doesn't explain when each happens.)

3. **"My code runs but gives the wrong answer. How do I find the bug?"**
   - Good answer: "Trace through the code with a simple example. Use print statements to see what values variables have. Compare expected vs. actual output."
   - Surface answer: "I don't know" or "Rewrite it?" (Doesn't know debugging strategy.)

4. **"Should I test my code with lots of different inputs?"**
   - Good answer: "Yes. Test normal cases, empty cases, boundary values, and negative values. Edge cases often reveal bugs."
   - Surface answer: "I test it once?" (Doesn't understand the need for multiple test cases.)

5. **"What should a comment explain?"**
   - Good answer: "Comments explain *why* the code does something, not what it does. The code itself shows what it does."
   - Surface answer: "What the code does?" (Wrong—that's restating the code.)

6. **"Do I need a docstring if my function name is clear?"**
   - Good answer: "Yes. Docstrings explain what parameters the function expects and what it returns. This helps anyone using the function."
   - Surface answer: "No, if it's obvious." (Doesn't understand that docstrings document the interface.)

---

## Common Student Questions & How to Answer Them

### Q1: "What does this error message mean?"

**Good answer:** "Read the bottom line—that's the error type. Read the line number and go to that line. That's where the error happened. Read the message—it tells you what went wrong. Does the error type match what you see?"

**Why this works:** It gives them a systematic approach to reading any traceback.

---

### Q2: "How do I fix this logic error?"

**Good answer:** "Run the code with a simple test case where you know the answer. Trace through the code step-by-step. Does the output match what you expected? If not, which line has the bug? Print the values to see what they really are."

**Why this works:** It teaches a debugging strategy that works for any logic error.

---

### Q3: "What should I test for?"

**Good answer:** "Test normal cases, empty cases (empty list, empty string), zero, negative numbers, and boundary values. If any of these break your code, there's a bug you need to fix."

**Why this works:** It gives them a test checklist for common edge cases.

---

### Q4: "Can I use try/except to ignore errors?"

**Good answer:** "You can, but don't. Only catch expected errors (like invalid user input). Catching everything hides bugs. Use try/except to handle errors gracefully, not to ignore them."

**Why this works:** It shows the purpose of try/except (graceful handling) and warns against misuse.

---

### Q5: "How many comments should I write?"

**Good answer:** "Write comments for non-obvious logic, key decisions, and why you're doing something. Don't comment every line—that's noise. Aim for 2–5 meaningful comments per function."

**Why this works:** It gives them a balance between no comments and over-commenting.

---

## Analogies That Work

### Analogy 1: Error Messages as Diagnostic Tools

**When to use:** When teaching students to read and use error messages.

**The analogy:** "Error messages are like your car's check-engine light. Instead of panicking, you take the car to a mechanic, who plugs in a reader and sees 'Oxygen sensor malfunction.' That tells them exactly what to fix. Error messages work the same way. They tell you exactly what went wrong and where. Read them, and they'll guide you to the fix."

**Why it works:** It removes the fear of errors and frames them as helpful information.

---

### Analogy 2: Testing as Quality Assurance

**When to use:** When teaching systematic testing and edge cases.

**The analogy:** "Testing is like taste-testing a recipe. You don't just try it once and assume it's perfect. You test it with different ingredient quantities, with the stove at different temperatures, with different variations. If any version tastes bad, you know there's a problem. Code testing works the same way: try many inputs to find bugs."

**Why it works:** It shows testing as a verification process, not busywork.

---

### Analogy 3: Comments as Notes to Your Future Self

**When to use:** When teaching why comments are important.

**The analogy:** "Comments are notes you leave for your future self. Imagine you write code today, then come back to it in six months. You've forgotten why you made a certain decision. Good comments explain the *why* so you can understand your own reasoning later. Bad comments just explain the code, which you can read anyway."

**Why it works:** It makes comments feel personal and purposeful, not bureaucratic.

---

## Summary of Teaching Priorities

In order of importance (most cascading-confusion first):

1. **Reading tracebacks** – Essential for independent debugging. Prevents panic and random fixes.
2. **Three error types (syntax, runtime, logic)** – Different approaches for each. Syntax is easy (read message); runtime requires tracing; logic is hardest.
3. **Systematic testing with edge cases** – Prevents "works on my computer" syndrome.
4. **Print debugging** – A tool for understanding what's happening inside your code.
5. **Comments explain why** – Builds sustainable code; prevents confusion later.
6. **Meaningful variable names** – Makes code readable and self-documenting.
7. **Docstrings for functions** – Documents the interface; makes code reusable.
8. **try/except for expected errors** – Handles input validation gracefully.

Focus the most energy on items 1–4 in the first two weeks. Mastery here builds debugging independence, which is critical for Unit 7 (projects).

