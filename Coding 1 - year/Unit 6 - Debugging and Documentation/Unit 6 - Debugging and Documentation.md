# Unit 6: Debugging and Documentation
> Master error handling, debugging strategies, and code documentation to write robust, maintainable Python programs.

## Unit Overview
- **Duration:** 25 days / 5 weeks (Traditional Schedule, 55-minute periods)
- **Days:** 121–145
- **Key Concepts:** Error types and tracebacks, debugging strategies, testing and edge cases, exception handling, code documentation, and file I/O operations
- **Big Idea:** Writing code is only half the battle—the real skill is finding and fixing bugs, testing thoroughly, documenting clearly, and handling errors gracefully. These practices transform code from "it works sometimes" to "it works reliably."

---

## Learning Targets

By the end of Unit 6, you will be able to:

1. I can identify and classify syntax, runtime, and logic errors
2. I can read and interpret Python tracebacks to locate errors
3. I can recognize common syntax errors and fix them
4. I can recognize common runtime errors (ZeroDivisionError, TypeError, NameError, IndexError) and fix them
5. I can use print() statements strategically to debug programs
6. I can apply rubber duck debugging to solve problems systematically
7. I can identify and fix off-by-one errors and infinite loops
8. I can debug functions by tracing parameter and return value issues
9. I can explain what testing is and why it matters
10. I can identify edge cases in a problem
11. I can write test cases with expected vs. actual output
12. I can use try/except blocks to handle errors gracefully
13. I can write clear comments that explain the "why" not just the "what"
14. I can write docstrings for functions
15. I can follow Python naming conventions for readability
16. I can open and read files in Python
17. I can write data to files and append to existing files
18. I can process file data (splitting lines, parsing CSV-style data)
19. I can use context managers (with statement) for safe file operations
20. I can design and implement a complete program with debugging, testing, and documentation

---

## Weekly Breakdown

### Week 25: Error Types & Reading Tracebacks (Days 121–125)
Understanding what goes wrong: Three types of errors, how to read tracebacks, common syntax errors, common runtime errors, and lab practice.

### Week 26: Debugging Strategies (Days 126–130)
Finding and fixing bugs: Print debugging, rubber duck debugging, debugging loops and functions, and challenge labs.

### Week 27: Testing & Edge Cases (Days 131–135)
Building reliable code: Manual testing, identifying edge cases, writing test cases, try/except basics, and hands-on labs.

### Week 28: Documentation & File I/O (Days 136–140)
Making code maintainable: Comments and docstrings, reading from files, writing to files, processing data, and file-based programs.

### Week 29: Review & Assessment (Days 141–145)
Bringing it together: Mini-projects, review sessions, and unit assessment.

---

# WEEK 25: ERROR TYPES & READING TRACEBACKS

# Day 121: Three Error Types—Syntax, Runtime, Logic Errors

**Learning Target:** I can identify and classify syntax, runtime, and logic errors.

### Key Concepts

There are three main types of errors you'll encounter as a programmer:

**1. Syntax Errors** occur when you violate Python's grammar rules. The code cannot run at all—Python stops before execution and tells you exactly what's wrong. These are the easiest to fix because Python points them out immediately.

**2. Runtime Errors** (also called exceptions) occur while the program is running. The code is syntactically correct, but something happens during execution that Python can't handle—like dividing by zero, accessing a list index that doesn't exist, or trying to do math with a string. The program crashes.

**3. Logic Errors** are the trickiest. The code runs without crashing, but it produces the wrong answer. The code is syntactically correct and doesn't crash, but the algorithm or condition is flawed. You have to figure out what's wrong by thinking through the logic carefully.

Understanding these three categories helps you approach debugging systematically: Is the code even syntactically valid? Does it crash when it runs? If not, does it give you the right answer?

### Code Examples

```python
# SYNTAX ERROR — Python won't even run this
print("Hello  # Missing closing quote
if x > 5  # Missing colon

# RUNTIME ERROR — Code starts but crashes
x = 10
print(x / 0)  # ZeroDivisionError: division by zero

items = [1, 2, 3]
print(items[5])  # IndexError: list index out of range

# LOGIC ERROR — Code runs fine but gives wrong answer
# Program: Calculate the area of a rectangle
length = 5
width = 3
area = length + width  # BUG: should be length * width
print(area)  # Prints 8, but area should be 15
```

### Guided Practice

For each of these code snippets, identify whether it's a syntax error, runtime error, or logic error:

1. `total = 10 + "5"` — What type of error?
2. `print("Hello")` with an extra space before `print` — What type?
3. A program that calculates age but subtracts birth year from current year when it should add — What type?

### Practice Problems

**Problem 1 — Beginner:** Write three Python snippets: one with a syntax error, one with a runtime error, and one with a logic error.

**Problem 2 — Intermediate:** Identify all three error types in this program and explain what's wrong with each:
```python
if score > 100  # Error 1: ?
    print(Grade: A")  # Error 2: ?
    passing = score > 50 and score < 50  # Error 3: ?
```

**Problem 3 — Challenge:** Write a program that calculates the average of three test scores. Intentionally include a logic error (the program runs but gives wrong results), then identify and fix it.

<details>
<summary>💡 Hints</summary>

- Problem 1: Syntax errors involve typos in code structure. Runtime errors happen during execution. Logic errors produce wrong answers.
- Problem 2: Look for missing colons, quote mismatches, and illogical conditions.
- Problem 3: Think about what operation should combine three numbers into an average.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
# Syntax Error
print(Hello")  # Missing opening quote

# Runtime Error
x = 10
y = 0
print(x / y)  # ZeroDivisionError

# Logic Error
age = 2026 - 1995  # Calculates 31, but should add 1
print(age)
```

**Problem 2:**
- Error 1: Missing colon after if statement (syntax)
- Error 2: Mixing quotes—starts with " and ends with ' (syntax)
- Error 3: Condition `score > 50 and score < 50` is always False (logic)

**Problem 3:**
```python
# Buggy version (logic error)
score1 = 85
score2 = 90
score3 = 78
average = (score1 + score2 + score3) / 2  # BUG: dividing by 2 instead of 3

# Fixed version
average = (score1 + score2 + score3) / 3  # Correct!
print(f"Average: {average}")
```

</details>

---

# Day 122: Reading Python Tracebacks

**Learning Target:** I can read and interpret Python tracebacks to locate errors.

### Key Concepts

When your program crashes, Python gives you a **traceback**—a detailed message that tells you what went wrong and where. Learning to read tracebacks is one of your most valuable debugging skills because they give you clues to the problem.

A traceback has several parts:
1. **The file and line number** where the error occurred
2. **The problematic code** on that line
3. **The error type** (e.g., ValueError, TypeError, NameError)
4. **The error message** that explains what went wrong

The key is to start at the **bottom of the traceback** and work upward. The last line tells you the error type and message. The lines above show the chain of function calls that led to the error.

When you see a traceback, ask:
- What is the error type?
- What line caused it?
- What was the code trying to do?
- Why did it fail?

### Code Examples

```python
# Example 1: Traceback reading
# If you run this code:
number = int(input("Enter a number: "))  # User enters "hello"
print(number * 2)

# You'd see:
# Traceback (most recent call last):
#   File "program.py", line 1, in <module>
#     number = int(input("Enter a number: "))
# ValueError: invalid literal for int() with base 10: 'hello'

# The error type is ValueError (tried to convert non-numeric string to int)

# Example 2: NameError traceback
print(student_name)  # Variable doesn't exist

# Traceback:
# NameError: name 'student_name' is not defined

# Example 3: IndexError traceback
grades = [85, 90, 78]
print(grades[5])  # Index 5 doesn't exist

# Traceback:
# IndexError: list index out of range
```

### Guided Practice

Given this traceback, answer the questions:
```
Traceback (most recent call last):
  File "calculator.py", line 5, in <module>
    result = 10 / divisor
ZeroDivisionError: division by zero
```

1. What is the error type?
2. What line caused the error?
3. What was the code trying to do?
4. How would you fix it?

### Practice Problems

**Problem 1 — Beginner:** Write code that produces a NameError, run it, and copy the traceback. Then explain what each part of the traceback means.

**Problem 2 — Intermediate:** Identify the error type from these tracebacks:
   a) `ValueError: invalid literal for int()`
   b) `TypeError: unsupported operand type(s) for +: 'int' and 'str'`
   c) `IndexError: list index out of range`

**Problem 3 — Challenge:** Read this traceback and identify the bug:
```
Traceback (most recent call last):
  File "program.py", line 7, in <module>
    average = total / count
ZeroDivisionError: division by zero
```
Write corrected code that checks if count is zero before dividing.

<details>
<summary>💡 Hints</summary>

- Problem 1: Run code with an undefined variable to see the traceback.
- Problem 2: Match error types to their descriptions.
- Problem 3: The error happens when dividing by zero—check if count is 0 first.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
print(undefined_variable)  # Produces NameError
```

Traceback parts:
- "Traceback (most recent call last):" — Python is about to tell us the error
- "File 'program.py', line X" — Where the error happened
- "NameError: name 'undefined_variable' is not defined" — What went wrong

**Problem 2:**
- a) ValueError — Cannot convert string to int
- b) TypeError — Trying to add incompatible types
- c) IndexError — List index is out of bounds

**Problem 3:**
```python
total = 0
count = 0  # Problem: count stays 0

# Fixed version
if count == 0:
    print("Cannot calculate average with zero items")
else:
    average = total / count
    print(f"Average: {average}")
```

</details>

---

# Day 123: Common Syntax Errors

**Learning Target:** I can recognize common syntax errors and fix them.

### Key Concepts

Syntax errors prevent your code from running at all. Python catches these immediately. Learning to recognize the most common syntax errors helps you fix them quickly. Common patterns include:

- **Missing colons** after if, elif, else, for, while, def, class
- **Mismatched or missing quotes** around strings
- **Mismatched parentheses, brackets, or braces**
- **Indentation errors** (too much, too little, or inconsistent)
- **Using keywords as variable names** (if, while, print, etc.)

The good news is that Python's error messages are usually pretty clear about what's wrong.

### Code Examples

```python
# SYNTAX ERROR 1: Missing colon after if
if x > 5
    print("x is greater than 5")

# Fixed:
if x > 5:
    print("x is greater than 5")

# SYNTAX ERROR 2: Mismatched quotes
print("Hello, world!)  # Starts with " but ends with )

# Fixed:
print("Hello, world!")

# SYNTAX ERROR 3: Indentation error
for i in range(5):
print(i)  # Not indented!

# Fixed:
for i in range(5):
    print(i)  # Properly indented

# SYNTAX ERROR 4: Missing parenthesis
print("Hello"  # Missing closing )

# Fixed:
print("Hello")

# SYNTAX ERROR 5: Using a keyword as a variable
class = "10th Grade"  # 'class' is a Python keyword

# Fixed:
grade_level = "10th Grade"
```

### Guided Practice

Fix these syntax errors:
1. `for x in range(10)`
2. `print('Hello")`
3. `if score > 100`

### Practice Problems

**Problem 1 — Beginner:** Write and run code with each of these syntax errors, note the error message, then fix it:
   - Missing colon after if
   - Mismatched quotes
   - Missing parenthesis

**Problem 2 — Intermediate:** Identify and fix all syntax errors in this code:
```python
name = input("What's your name?
if name = "Alex"
    print("Hello Alex"
```

**Problem 3 — Challenge:** Write a function with intentional syntax errors, exchange with a partner, and have them identify and fix all errors.

<details>
<summary>💡 Hints</summary>

- Problem 1: Run each buggy code to see the error message.
- Problem 2: Look for missing quotes, colons, and parentheses.
- Problem 3: Common function syntax errors include missing `def`, colon, or correct indentation.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
# Error 1: Missing colon
if x > 5:  # Fixed
    print("x is big")

# Error 2: Mismatched quotes
print("Hello")  # Fixed

# Error 3: Missing parenthesis
print("Done")  # Fixed
```

**Problem 2:**
```python
# Original (with errors):
name = input("What's your name?
if name = "Alex"
    print("Hello Alex"

# Fixed:
name = input("What's your name?")
if name == "Alex":
    print("Hello Alex")
```

**Problem 3:** Errors might include: `def` keyword missing, missing `:`, incorrect indentation, `=` instead of `==`.

</details>

---

# Day 124: Common Runtime Errors

**Learning Target:** I can recognize common runtime errors and fix them.

### Key Concepts

Runtime errors occur while your program is running. The syntax is correct, but something happens that Python can't handle. The four most common runtime errors are:

1. **ZeroDivisionError** — You tried to divide by zero
2. **TypeError** — You tried to do an operation with incompatible types (e.g., add int and string)
3. **NameError** — You tried to use a variable that doesn't exist (typo or never created)
4. **IndexError** — You tried to access a list index that doesn't exist

Each of these has a clear fix once you understand what caused it.

### Code Examples

```python
# RUNTIME ERROR 1: ZeroDivisionError
numerator = 10
denominator = 0
result = numerator / denominator  # ERROR

# Fixed: Check for zero before dividing
if denominator != 0:
    result = numerator / denominator
else:
    print("Cannot divide by zero")

# RUNTIME ERROR 2: TypeError
age = "17"
next_year_age = age + 1  # Can't add string and int

# Fixed: Convert to int first
age = int(input("Age: "))
next_year_age = age + 1
print(next_year_age)

# RUNTIME ERROR 3: NameError
print(student_score)  # Variable never defined

# Fixed: Define the variable first
student_score = 85
print(student_score)

# RUNTIME ERROR 4: IndexError
grades = [85, 90, 78, 92]
print(grades[4])  # Index 4 doesn't exist (only 0–3)

# Fixed: Check length or use valid index
if len(grades) > 4:
    print(grades[4])
else:
    print("Index out of range")
    print(grades[3])  # Use valid index
```

### Guided Practice

What runtime error would each of these cause?
1. `x = "5"; print(x * 2)` — What error type and why?
2. `scores = [10, 20]; print(scores[5])` — What error type and why?
3. `result = 100 / (5 - 5)` — What error type and why?

### Practice Problems

**Problem 1 — Beginner:** Write code that produces each of the four common runtime errors, then fix each one.

**Problem 2 — Intermediate:** Fix this code:
```python
user_input = input("Enter a number: ")
doubled = user_input * 2
print(f"Doubled: {doubled}")
```

**Problem 3 — Challenge:** Write a program that safely calculates the average of user-entered numbers, handling the case where the user enters non-numeric input or no numbers.

<details>
<summary>💡 Hints</summary>

- Problem 1: Divide by zero, concatenate string with int, use undefined variable, access invalid list index.
- Problem 2: The input is a string; convert to int before math.
- Problem 3: Use try/except to handle ValueError when converting input.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
# ZeroDivisionError
result = 10 / 0  # Fixed: if denom != 0: result = 10 / denom

# TypeError
x = "5" + 3  # Fixed: x = int("5") + 3

# NameError
print(undefined)  # Fixed: define it first

# IndexError
lst = [1, 2, 3]
print(lst[10])  # Fixed: print(lst[2]) or check len(lst)
```

**Problem 2:**
```python
user_input = int(input("Enter a number: "))  # Convert to int
doubled = user_input * 2
print(f"Doubled: {doubled}")
```

**Problem 3:**
```python
numbers = []
while True:
    try:
        num = float(input("Enter a number (or 'done'): "))
        numbers.append(num)
    except ValueError:
        if "done" in input("Enter a number (or 'done'): ").lower():
            break

if numbers:
    avg = sum(numbers) / len(numbers)
    print(f"Average: {avg}")
else:
    print("No numbers entered")
```

</details>

---

# Day 125: Practice Lab—Error Identification and Correction

**Learning Target:** I can identify and classify errors, read tracebacks, and apply fixes.

### Key Concepts

This lab brings together everything from Week 25. You'll work with code that has syntax, runtime, and logic errors. Your job is to:
1. Identify the error type
2. Read the traceback (if applicable)
3. Understand what went wrong
4. Apply the fix
5. Test to confirm it works

Real-world debugging is rarely about one error at a time. You'll practice finding multiple errors in a single program.

### Code Examples

```python
# Example buggy program (Calculate student grades)
student_name = input("Student name: ")
test1 = input("Test 1 score: ")
test2 = input("Test 2 score: "
test3 = input("Test 3 score: ")

average = (test1 + test2 + test3) / 3
print(f"{student_name}'s average: {average}")

# This has:
# 1. Syntax error (missing closing quote on line 3)
# 2. Runtime error (can't add strings; need int conversion)
# 3. Logic error? (Not necessarily, if we fix runtime error)
```

### Guided Practice

Debug this program that calculates the area of a circle:
```python
import math

radius = input("Radius: ")
area = math.pi * radius ** 2
print(f"Area: {area}")
```

Identify the error(s), explain why they occur, and fix them.

### Practice Problems

**Problem 1 — Beginner:** Fix this grade calculator:
```python
score1 = input("Score 1: ")
score2 = input("Score 2: ")
score3 = input("Score 3: ")
average = (score1 + score2 + score3) / 3
print(f"Average: {average}")
```

**Problem 2 — Intermediate:** Find and fix all errors in this program:
```python
items = ["apple", "banana", "cherry"]
item1 = items[0]
item2 = items[1]
item3 = items[5]  # Error?
item1_price = 0.50
item2_price = 0.75
item3_price = 0.60
total = item1_price item2_price item3_price
print(total)
```

**Problem 3 — Challenge:** Debug a "divide two numbers" program that handles edge cases:
```python
num1 = input("First number: ")
num2 = input("Second number: ")
result = num1 / num2
print(f"Result: {result}")
```

<details>
<summary>💡 Hints</summary>

- Problem 1: Input returns strings; convert to float/int before math.
- Problem 2: Index 5 doesn't exist (only 0–2). Also missing + operators.
- Problem 3: Handle both type conversion and zero division.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
score1 = float(input("Score 1: "))
score2 = float(input("Score 2: "))
score3 = float(input("Score 3: "))
average = (score1 + score2 + score3) / 3
print(f"Average: {average}")
```

**Problem 2:**
```python
items = ["apple", "banana", "cherry"]
item1 = items[0]
item2 = items[1]
item3 = items[2]  # Fixed: index 2, not 5
item1_price = 0.50
item2_price = 0.75
item3_price = 0.60
total = item1_price + item2_price + item3_price  # Fixed: add + operators
print(total)
```

**Problem 3:**
```python
try:
    num1 = float(input("First number: "))
    num2 = float(input("Second number: "))
    if num2 == 0:
        print("Cannot divide by zero")
    else:
        result = num1 / num2
        print(f"Result: {result}")
except ValueError:
    print("Please enter valid numbers")
```

</details>

---

# WEEK 26: DEBUGGING STRATEGIES

# Day 126: Print Debugging

**Learning Target:** I can use print() statements strategically to debug programs.

### Key Concepts

**Print debugging** is one of the most powerful tools you have. The idea is simple: add print statements to trace what your program is doing at each step. By printing out variable values, you can see where things go wrong.

Good debugging print statements show:
- **What variables contain at key points**
- **Whether conditions are true or false**
- **Which branch of an if/elif/else block is executing**
- **Loop iteration counts and values**

The key is being strategic: print just enough to understand what's happening, but not so much that you're overwhelmed with output.

### Code Examples

```python
# Example 1: Debugging a buggy loop
# This program should print multiples of 3 from 3 to 30
for i in range(1, 11):
    multiple = i * 3
    print(f"DEBUG: i = {i}, multiple = {multiple}")  # Strategic print
    if multiple > 15:
        print(multiple)

# Example 2: Debugging function issues
def calculate_discount(price, discount_percent):
    print(f"DEBUG: Entered with price={price}, discount_percent={discount_percent}")
    discount_amount = price * (discount_percent / 100)
    print(f"DEBUG: discount_amount = {discount_amount}")
    final_price = price - discount_amount
    print(f"DEBUG: final_price = {final_price}")
    return final_price

result = calculate_discount(100, 20)
print(f"Final result: {result}")

# Example 3: Debugging a list problem
scores = [85, 90, 78, 92, 88]
total = 0
for score in scores:
    print(f"DEBUG: Adding {score}, total was {total}")
    total = total + score
    print(f"DEBUG: total is now {total}")
print(f"Final total: {total}")
```

### Guided Practice

A program is supposed to find the sum of all even numbers in a list, but it's giving the wrong answer. Add print statements to debug:

```python
numbers = [2, 5, 8, 3, 10, 7, 4]
even_sum = 0
for num in numbers:
    if num % 2 == 0:
        even_sum = even_sum + num
print(f"Sum of even numbers: {even_sum}")
```

Add DEBUG print statements to trace what's happening.

### Practice Problems

**Problem 1 — Beginner:** Add print statements to this program to show the value of `x` at each step:
```python
x = 10
x = x + 5
x = x * 2
x = x - 3
print(f"Final x: {x}")
```

**Problem 2 — Intermediate:** Debug this program that calculates factorial by adding print statements:
```python
def factorial(n):
    result = 1
    for i in range(1, n + 1):
        result = result * i
    return result

print(factorial(5))  # Should be 120
```

**Problem 3 — Challenge:** A program that checks if a number is prime has a bug. Add print statements and fix it:
```python
def is_prime(num):
    for i in range(2, num):
        if num % i == 0:
            return False
    return True

print(is_prime(17))  # Should be True
print(is_prime(15))  # Should be False
```

<details>
<summary>💡 Hints</summary>

- Problem 1: Print x after each operation to see the values.
- Problem 2: Print `i` and `result` in each iteration.
- Problem 3: Print each divisor being tested and whether it divides evenly.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
x = 10
print(f"DEBUG: x = {x}")
x = x + 5
print(f"DEBUG: x = {x}")
x = x * 2
print(f"DEBUG: x = {x}")
x = x - 3
print(f"DEBUG: x = {x}")
print(f"Final x: {x}")
```

**Problem 2:**
```python
def factorial(n):
    result = 1
    for i in range(1, n + 1):
        print(f"DEBUG: i = {i}, result = {result}")
        result = result * i
        print(f"DEBUG: result = {result}")
    return result
```

**Problem 3:**
```python
def is_prime(num):
    for i in range(2, int(num ** 0.5) + 1):  # Only check up to sqrt(num)
        print(f"DEBUG: Checking if {num} is divisible by {i}")
        if num % i == 0:
            print(f"DEBUG: {num} is divisible by {i}, not prime")
            return False
    print(f"DEBUG: {num} is prime")
    return True
```

</details>

---

# Day 127: Rubber Duck Debugging and Systematic Problem Solving

**Learning Target:** I can apply rubber duck debugging to solve problems systematically.

### Key Concepts

**Rubber duck debugging** is a technique where you explain your code, line by line, to a rubber duck (or another person, or even yourself). Often, by the time you finish explaining, you realize what's wrong. It forces you to think through the logic carefully.

The process:
1. Get a rubber duck (or any object, or a person)
2. Explain what your code is supposed to do
3. Explain what each line does
4. Often, you'll catch the bug just by explaining it

This works because explaining forces precision. When you say "this adds numbers," you might realize you're actually concatenating strings instead.

### Code Examples

```python
# Example: Buggy program (calculates miles to kilometers)
miles = input("Miles: ")
kilometers = miles * 1.609
print(f"{miles} miles is {kilometers} kilometers")

# Rubber duck conversation:
# "This program converts miles to kilometers."
# "Line 1: Get miles from user."
# "Line 2: Multiply miles by 1.609."
# "Wait... miles is a STRING. I can't multiply a string by a number!"
# Bug found!

# Fixed:
miles = float(input("Miles: "))  # Convert to float!
kilometers = miles * 1.609
print(f"{miles} miles is {kilometers} kilometers")

# Another example: Loop problem
count = 0
for i in range(5):
    count = count + 1
    print(i)

# Rubber duck:
# "This loop prints 0 through 4 and counts iterations."
# "i goes from 0 to 4 (5 iterations)."
# "Each iteration, count increases by 1."
# "After the loop, count should be 5."
# "Looks correct!"
```

### Guided Practice

Use rubber duck debugging (explain to someone or a real duck!) on this program:
```python
def check_grade(score):
    if score >= 90:
        return "A"
    if score >= 80:
        return "B"
    if score >= 70:
        return "C"
    if score >= 60:
        return "D"
    return "F"

print(check_grade(85))  # Should print "B"
```

Explain line by line. Does it work correctly?

### Practice Problems

**Problem 1 — Beginner:** Use rubber duck debugging on this simple program. Explain it line by line:
```python
name = input("Your name: ")
greeting = "Hello, " + name
print(greeting)
```

**Problem 2 — Intermediate:** Use rubber duck debugging on this program and identify the bug:
```python
def double(x):
    x = x * 2
    return x

numbers = [1, 2, 3, 4, 5]
for num in numbers:
    print(num * 2)

# Missing: actually calling the function!
```

**Problem 3 — Challenge:** Use rubber duck debugging on this program. It has a subtle logic error:
```python
password = input("Enter password: ")
if password = "secret123":
    print("Access granted")
else:
    print("Access denied")
```

<details>
<summary>💡 Hints</summary>

- Problem 1: Trace through: input, concatenate, print.
- Problem 2: Notice the function `double()` is never called.
- Problem 3: Look for syntax errors and logic issues.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:** The program works correctly. It gets the user's name, concatenates it with "Hello, ", and prints the greeting.

**Problem 2:** The function `double()` is defined but never called. The loop prints `num * 2` directly instead of calling `double()`. It still works, but it's not using the function.

**Problem 3:**
- Bug 1 (syntax): `=` should be `==` (assignment vs. comparison)
- Fixed:
```python
password = input("Enter password: ")
if password == "secret123":
    print("Access granted")
else:
    print("Access denied")
```

</details>

---

# Day 128: Debugging Loops

**Learning Target:** I can identify and fix off-by-one errors and infinite loops.

### Key Concepts

Loops are tricky to debug because they repeat code multiple times. Two common loop problems are:

**Off-by-one errors** occur when your loop iterates one too many or one too few times. For example:
- `range(0, 5)` gives [0, 1, 2, 3, 4]—five items
- `range(1, 5)` gives [1, 2, 3, 4]—four items
- Off-by-one errors are especially common with list indexing

**Infinite loops** happen when the loop condition is always true and there's no `break` statement to exit. The program hangs and never finishes.

### Code Examples

```python
# OFF-BY-ONE ERROR 1: Loop stops too early
# Goal: Print 1 through 10
for i in range(1, 10):  # Bug: goes 1-9, not 1-10
    print(i)
# Fixed:
for i in range(1, 11):  # Now goes 1-10

# OFF-BY-ONE ERROR 2: List indexing
scores = [85, 90, 78, 92]
for i in range(1, len(scores)):  # Bug: starts at index 1, skips first score
    print(scores[i])
# Fixed:
for i in range(len(scores)):  # Starts at 0

# INFINITE LOOP: Condition never becomes false
count = 0
while count < 5:
    print(count)
    # Bug: count never increases!
# Fixed:
count = 0
while count < 5:
    print(count)
    count = count + 1  # Increment!

# INFINITE LOOP with input
while True:
    answer = input("Do you want to continue? (yes/no): ")
    if answer == "no":
        break  # Exit the loop
    print("Continuing...")
# This is OKAY if there's a break statement
```

### Guided Practice

Find the off-by-one error:
```python
# Goal: Print the first 5 numbers in a list
my_list = [10, 20, 30, 40, 50, 60, 70]
for i in range(6):
    print(my_list[i])
```

What does this actually print? How would you fix it?

### Practice Problems

**Problem 1 — Beginner:** Fix this off-by-one error:
```python
# Goal: Print numbers 1 through 5
for i in range(5):
    print(i)
```

**Problem 2 — Intermediate:** Identify and fix the infinite loop:
```python
password = input("Enter password: ")
while password != "correct":
    password = input("Wrong! Try again: ")
print("Access granted!")
```

This one actually works. Write a version that has an infinite loop.

**Problem 3 — Challenge:** Debug this program that should print only even numbers 2 through 20:
```python
for num in range(2, 20):
    if num % 2 == 0:
        print(num)
```

<details>
<summary>💡 Hints</summary>

- Problem 1: `range(5)` gives 0-4. Use `range(1, 6)` for 1-5.
- Problem 2: The loop shown is correct. For an infinite loop, remove the input line inside the loop.
- Problem 3: The code is actually correct! It prints 2, 4, 6, 8, 10, 12, 14, 16, 18.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
for i in range(1, 6):  # Fixed: range(1, 6) for 1-5
    print(i)
```

**Problem 2:**
```python
# Working version (your original)
password = input("Enter password: ")
while password != "correct":
    password = input("Wrong! Try again: ")
print("Access granted!")

# Infinite loop version:
password = input("Enter password: ")
while password != "correct":
    print("Wrong! Try again:")
    # Bug: never gets new password input!
```

**Problem 3:**
```python
# This code is already correct!
for num in range(2, 20):
    if num % 2 == 0:
        print(num)
# Prints: 2, 4, 6, 8, 10, 12, 14, 16, 18
```

</details>

---

# Day 129: Debugging Functions

**Learning Target:** I can debug functions by tracing parameter and return value issues.

### Key Concepts

Functions are great for organization, but they introduce new places where bugs can hide:
- **Parameters not passed correctly** — function expects three arguments but only two are provided
- **Wrong parameter values** — function receives the right number of arguments but in the wrong order or type
- **Return value issues** — function doesn't return anything (returns None), returns wrong value, or doesn't return at all
- **Variable scope issues** — using variables inside the function that don't exist

Debugging functions requires understanding:
1. What arguments are being passed in?
2. What happens inside the function?
3. What is being returned?

### Code Examples

```python
# FUNCTION ERROR 1: Wrong number of arguments
def greet(name, greeting):
    return f"{greeting}, {name}!"

print(greet("Alex"))  # Error: missing 'greeting' argument

# Fixed:
print(greet("Alex", "Hello"))

# FUNCTION ERROR 2: Wrong argument types
def add_numbers(a, b):
    return a + b

result = add_numbers("5", "3")  # Wrong: strings, not numbers
print(result)  # Prints "53", not 8

# Fixed:
result = add_numbers(5, 3)

# FUNCTION ERROR 3: No return statement
def calculate_tax(price):
    tax = price * 0.08
    # Bug: no return statement!

total = calculate_tax(100)
print(total)  # Prints None

# Fixed:
def calculate_tax(price):
    tax = price * 0.08
    return tax  # Return the value!

# FUNCTION ERROR 4: Scope issue
x = 10

def modify_x():
    x = 20  # Creates a local variable, doesn't change global x

modify_x()
print(x)  # Still 10, not 20
```

### Guided Practice

Debug this function. What's wrong with it?
```python
def calculate_average(scores):
    total = sum(scores)
    average = total / len(scores)
    print(f"Average: {average}")

result = calculate_average([85, 90, 78])
print(result)  # Prints None—why?
```

### Practice Problems

**Problem 1 — Beginner:** Fix this function:
```python
def double(x):
    x * 2  # Bug: no return statement!

result = double(5)
print(result)  # Should print 10, but prints None
```

**Problem 2 — Intermediate:** Find and fix all errors:
```python
def calculate_grade(score):
    if score > 90:
        grade = "A"
    elif score > 80:
        grade = "B"
    else:
        grade = "C"
    return grade

print(calculate_grade(85))  # Should work—does it?
```

Actually test it! Does it work or is there an error?

**Problem 3 — Challenge:** Write a function that calculates the cost of items with tax. Include debugging print statements:
```python
def item_total(price, quantity, tax_rate):
    # Your code here
    # Should return: price * quantity * (1 + tax_rate)
    pass

# Test:
result = item_total(10, 3, 0.08)
print(result)  # Should print 32.4
```

<details>
<summary>💡 Hints</summary>

- Problem 1: Add `return` before `x * 2`.
- Problem 2: Test it! The code is actually correct.
- Problem 3: Remember to return the calculated value.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
def double(x):
    return x * 2  # Fixed: added return

result = double(5)
print(result)  # Prints 10
```

**Problem 2:**
```python
# The function is correct as-is!
def calculate_grade(score):
    if score > 90:
        grade = "A"
    elif score > 80:
        grade = "B"
    else:
        grade = "C"
    return grade

print(calculate_grade(85))  # Prints B
```

**Problem 3:**
```python
def item_total(price, quantity, tax_rate):
    print(f"DEBUG: price={price}, qty={quantity}, tax={tax_rate}")
    subtotal = price * quantity
    print(f"DEBUG: subtotal={subtotal}")
    total = subtotal * (1 + tax_rate)
    print(f"DEBUG: total={total}")
    return total

result = item_total(10, 3, 0.08)
print(result)  # Prints 32.4
```

</details>

---

# Day 130: Practice Lab—Debug Challenge

**Learning Target:** I can apply print debugging, rubber duck debugging, and systematic approaches to fix broken programs.

### Key Concepts

This lab combines all the debugging strategies from Week 26. You'll work with more complex, broken programs that require:
- Print statements to trace execution
- Rubber duck reasoning to understand logic
- Knowledge of common loop and function bugs
- Systematic problem-solving

Real debugging is not always clean or linear. Sometimes you need multiple approaches.

### Code Examples

```python
# Example: Complex buggy program (student grades)
students = [
    {"name": "Alice", "scores": [85, 90, 78]},
    {"name": "Bob", "scores": [92, 88, 95]},
]

for student in students:
    name = student["name"]
    scores = student["scores"]
    total = sum(scores)
    average = total / len(scores)
    print(f"{name}: {average}")  # This might work—debug to check

# If it doesn't work, add print statements:
for student in students:
    name = student["name"]
    print(f"DEBUG: Processing {name}")
    scores = student["scores"]
    print(f"DEBUG: scores = {scores}")
    total = sum(scores)
    print(f"DEBUG: total = {total}")
    average = total / len(scores)
    print(f"DEBUG: average = {average}")
    print(f"{name}: {average}")
```

### Guided Practice

Debug this program that searches for a number in a list:
```python
def find_number(lst, target):
    for i in range(len(lst)):
        if lst[i] = target:  # Bug?
            return i
    return -1

print(find_number([10, 20, 30, 40], 30))  # Should print 2
```

### Practice Problems

**Problem 1 — Beginner:** A program calculates the sum of numbers in a list. Fix it:
```python
numbers = [5, 10, 15, 20]
total = 0
for num in numbers
    total = total + num
print(total)
```

**Problem 2 — Intermediate:** A program to find the maximum number in a list has a bug. Find and fix it:
```python
def find_max(lst):
    max_value = lst[0]
    for num in lst:
        if num > max_value:
            max_value = num
    return max_value

print(find_max([3, 7, 2, 9, 1]))  # Should print 9
```

Test this code. Does it work?

**Problem 3 — Challenge:** Debug this complex program:
```python
def calculate_statistics(numbers):
    if len(numbers) == 0:
        return None

    total = sum(numbers)
    average = total / len(numbers)

    min_value = numbers[0]
    max_value = numbers[0]

    for num in numbers:
        if num < min_value:
            min_value = num
        if num > max_value:
            max_value = num

    return {
        "average": average,
        "min": min_value,
        "max": max_value
    }

result = calculate_statistics([5, 12, 3, 8, 10])
print(result)
```

This program should return a dictionary with average, min, and max. Test it thoroughly and fix any bugs.

<details>
<summary>💡 Hints</summary>

- Problem 1: Look for syntax errors (missing colon).
- Problem 2: Test the code yourself. It likely works correctly.
- Problem 3: Trace through with print statements if needed.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
numbers = [5, 10, 15, 20]
total = 0
for num in numbers:  # Fixed: added colon
    total = total + num
print(total)  # Prints 50
```

**Problem 2:**
```python
# The code works correctly!
def find_max(lst):
    max_value = lst[0]
    for num in lst:
        if num > max_value:
            max_value = num
    return max_value

print(find_max([3, 7, 2, 9, 1]))  # Prints 9
```

**Problem 3:**
```python
# The code works correctly!
def calculate_statistics(numbers):
    if len(numbers) == 0:
        return None

    total = sum(numbers)
    average = total / len(numbers)

    min_value = numbers[0]
    max_value = numbers[0]

    for num in numbers:
        if num < min_value:
            min_value = num
        if num > max_value:
            max_value = num

    return {
        "average": average,
        "min": min_value,
        "max": max_value
    }

result = calculate_statistics([5, 12, 3, 8, 10])
print(result)  # Works correctly
```

</details>

---

# WEEK 27: TESTING & EDGE CASES

# Day 131: What is Testing? Manual Testing Strategies

**Learning Target:** I can explain what testing is and apply manual testing strategies.

### Key Concepts

**Testing** is the process of verifying that your code works as expected. It's different from debugging—debugging is fixing known problems, while testing is looking for problems you might not know exist.

Good testing involves:
1. **Defining expected behavior** — What should the program do?
2. **Planning test cases** — What inputs should I try?
3. **Running the program with those inputs**
4. **Comparing expected output to actual output**
5. **Documenting results**

Manual testing means you run the program with different inputs and check if the output is correct. This is simple but tedious. You'll later learn about automated testing, but manual testing is where you start.

### Code Examples

```python
# Example program: Calculate the absolute value
def absolute_value(x):
    if x < 0:
        return -x
    else:
        return x

# Testing plan:
# 1. Positive number: absolute_value(5) should return 5
# 2. Negative number: absolute_value(-5) should return 5
# 3. Zero: absolute_value(0) should return 0

print(absolute_value(5))   # Expected: 5, Actual: 5 ✓
print(absolute_value(-5))  # Expected: 5, Actual: 5 ✓
print(absolute_value(0))   # Expected: 0, Actual: 0 ✓

# Program PASSES all tests!

# Example 2: Test a grade calculator
def get_grade(score):
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    else:
        return "F"

# Test cases:
print(get_grade(95))   # Expected: A, Actual: A ✓
print(get_grade(85))   # Expected: B, Actual: B ✓
print(get_grade(75))   # Expected: C, Actual: C ✓
print(get_grade(60))   # Expected: F, Actual: F ✓
```

### Guided Practice

For this program, create a testing plan (list of test cases):

```python
def is_even(num):
    return num % 2 == 0

# What test cases would you run?
# 1. ?
# 2. ?
# 3. ?
```

### Practice Problems

**Problem 1 — Beginner:** Create a test plan for the `len()` function. What inputs would you test?

**Problem 2 — Intermediate:** Write a program that checks if a password is strong (at least 8 characters). Create a test plan with at least 4 test cases.

**Problem 3 — Challenge:** Write a program that calculates the day of the week (0 = Monday, 6 = Sunday). Create a comprehensive test plan.

<details>
<summary>💡 Hints</summary>

- Problem 1: Test empty list, single item, multiple items.
- Problem 2: Test short password, long password, exactly 8 characters, edge cases.
- Problem 3: Test all 7 days of the week, maybe some edge cases.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
Test cases for `len()`:
- len([]) should be 0
- len([1]) should be 1
- len([1, 2, 3]) should be 3
- len("hello") should be 5

**Problem 2:**
```python
def is_strong_password(password):
    return len(password) >= 8

# Test cases:
print(is_strong_password("abc"))        # Expected: False
print(is_strong_password("abcdefgh"))   # Expected: True
print(is_strong_password("abcdefg"))    # Expected: False (7 chars)
print(is_strong_password("abcdefgh123")) # Expected: True
```

**Problem 3:**
```python
def day_of_week(day_num):
    days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"]
    if 0 <= day_num <= 6:
        return days[day_num]
    return "Invalid"

# Test cases:
for i in range(7):
    print(f"Day {i}: {day_of_week(i)}")
```

</details>

---

# Day 132: Edge Cases

**Learning Target:** I can identify edge cases in a problem.

### Key Concepts

**Edge cases** are inputs that are at the extremes or unusual in some way. They often expose bugs that normal test cases miss. Common edge cases include:

- **Empty input** — empty list, empty string, no items
- **Zero** — especially problematic for division
- **Negative numbers** — often forgotten
- **Single item** — boundary condition
- **Very large numbers** — potential overflow or performance issues
- **Boundary values** — if range is 0-100, test 0 and 100

Edge cases are important because:
1. They often break programs that work with "normal" data
2. They test the boundaries of your logic
3. They prepare you for real-world data

### Code Examples

```python
# Example 1: Function that divides two numbers
def divide(a, b):
    return a / b

# Normal test cases: divide(10, 2) = 5
# Edge cases:
# - divide(10, 0)  — ZeroDivisionError!
# - divide(-10, 2) — should work, but is negative expected?
# - divide(0, 5)   — should return 0
# - divide(10.5, 2.5) — should work with floats

# Example 2: Find minimum in a list
def find_min(lst):
    min_val = lst[0]
    for item in lst:
        if item < min_val:
            min_val = item
    return min_val

# Normal case: find_min([3, 1, 4]) = 1
# Edge cases:
# - find_min([])           — IndexError! (empty list)
# - find_min([5])          — single item
# - find_min([-5, -10, 3]) — negative numbers
# - find_min([0])          — zero

# Example 3: Check if name is valid (not empty)
def is_valid_name(name):
    return len(name) > 0

# Normal case: is_valid_name("Alex") = True
# Edge cases:
# - is_valid_name("")      — empty string
# - is_valid_name(" ")     — space (technically not empty)
# - is_valid_name("A")     — single character
```

### Guided Practice

For this function, identify at least 5 edge cases:
```python
def get_nth_item(lst, n):
    return lst[n]
```

### Practice Problems

**Problem 1 — Beginner:** List edge cases for a function that calculates the average of test scores.

**Problem 2 — Intermediate:** For a function that checks if a number is prime, identify 5+ edge cases.

**Problem 3 — Challenge:** Write a function that removes duplicates from a list. Then list 6+ edge cases and test them.

<details>
<summary>💡 Hints</summary>

- Problem 1: Consider empty list, single score, zero, negative numbers.
- Problem 2: Consider 1, 2, negative numbers, zero, very large numbers.
- Problem 3: Empty list, single item, all duplicates, no duplicates, negative numbers.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
Edge cases for average of scores:
- Empty list (no scores)
- Single score
- All same scores
- Including a zero
- Including negative numbers (if possible)

**Problem 2:**
Edge cases for is_prime:
- 1 (not prime)
- 2 (only even prime)
- Negative numbers
- 0
- Very large numbers
- Perfect squares like 25, 49

**Problem 3:**
```python
def remove_duplicates(lst):
    return list(set(lst))

# Edge cases:
# 1. Empty list: remove_duplicates([]) → []
# 2. Single item: remove_duplicates([5]) → [5]
# 3. No duplicates: remove_duplicates([1, 2, 3]) → [1, 2, 3]
# 4. All duplicates: remove_duplicates([5, 5, 5]) → [5]
# 5. With zero: remove_duplicates([0, 1, 0]) → [0, 1]
# 6. With negative: remove_duplicates([-1, 1, -1]) → [-1, 1]
```

</details>

---

# Day 133: Writing Test Cases

**Learning Target:** I can write test cases with expected vs. actual output.

### Key Concepts

A **test case** includes:
1. **Input** — What are you testing with?
2. **Expected output** — What should happen?
3. **Actual output** — What really happened?
4. **Status** — Pass or fail?

A good test case is:
- **Specific** — Not vague
- **Reproducible** — You can run it again and get the same result
- **Independent** — Doesn't depend on other tests
- **Clear** — Someone else can understand what you're testing

Writing test cases systematically prevents bugs from slipping through.

### Code Examples

```python
# Example: Testing a function that checks if a year is a leap year
def is_leap_year(year):
    return (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0)

# Test cases:
test_cases = [
    # (input, expected_output, description)
    (2020, True, "Year divisible by 4 and not by 100"),
    (2021, False, "Year not divisible by 4"),
    (2000, True, "Year divisible by 400"),
    (1900, False, "Year divisible by 100 but not 400"),
]

# Run tests:
for year, expected, description in test_cases:
    actual = is_leap_year(year)
    status = "PASS" if actual == expected else "FAIL"
    print(f"{status}: {year} - {description}")
    print(f"  Expected: {expected}, Actual: {actual}")

# Example output:
# PASS: 2020 - Year divisible by 4 and not by 100
#   Expected: True, Actual: True
# PASS: 2021 - Year not divisible by 4
#   Expected: False, Actual: False
```

### Guided Practice

Write test cases for this function:
```python
def is_positive(num):
    return num > 0
```

Include at least 5 test cases with input, expected output, and description.

### Practice Problems

**Problem 1 — Beginner:** Write 5 test cases for `str.upper()`. Use the format above.

**Problem 2 — Intermediate:** Write 8+ test cases for a function that validates an email (starts with letter, contains @, ends with .com).

**Problem 3 — Challenge:** Write 10+ comprehensive test cases for a function that calculates the number of days until a birthday.

<details>
<summary>💡 Hints</summary>

- Problem 1: Test empty string, single char, multiple words, numbers, special characters.
- Problem 2: Include valid emails, missing @, missing domain, invalid characters.
- Problem 3: Today's date matches birthday, birthday passed, birthday in future, edge of year.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
test_cases = [
    ("hello", "HELLO", "Lowercase string"),
    ("HELLO", "HELLO", "Already uppercase"),
    ("HeLLo", "HELLO", "Mixed case"),
    ("", "", "Empty string"),
    ("123", "123", "Numbers"),
]
```

**Problem 2:**
```python
def is_valid_email(email):
    return email[0].isalpha() and "@" in email and email.endswith(".com")

test_cases = [
    ("alex@example.com", True, "Valid email"),
    ("1user@example.com", False, "Starts with number"),
    ("alex@.com", True, "Contains @"),  # Note: real validation is more complex
    ("user.com", False, "Missing @"),
]
```

**Problem 3:**
```python
# Test cases for days until birthday
# Include: past birthday this year, birthday today, birthday this year, birthday next year
```

</details>

---

# Day 134: try/except Basics

**Learning Target:** I can use try/except blocks to handle errors gracefully.

### Key Concepts

**Exception handling** lets you catch errors and handle them gracefully instead of crashing. The basic structure is:

```
try:
    (code that might cause an error)
except ErrorType:
    (code to run if that error happens)
```

Common errors to catch:
- `ValueError` — Invalid value for conversion (e.g., `int("hello")`)
- `ZeroDivisionError` — Division by zero
- `IndexError` — List index out of range
- `TypeError` — Wrong data type for operation
- `NameError` — Variable doesn't exist
- `KeyError` — Dictionary key doesn't exist

You can have multiple `except` blocks for different error types.

### Code Examples

```python
# Example 1: Catching ValueError
try:
    age = int(input("Age: "))
    print(f"You are {age} years old")
except ValueError:
    print("Please enter a valid number")

# Example 2: Catching ZeroDivisionError
try:
    num1 = int(input("First number: "))
    num2 = int(input("Second number: "))
    result = num1 / num2
    print(f"Result: {result}")
except ZeroDivisionError:
    print("Cannot divide by zero!")
except ValueError:
    print("Please enter valid numbers")

# Example 3: Catching IndexError
try:
    items = [10, 20, 30]
    print(items[5])
except IndexError:
    print("Index out of range")

# Example 4: Generic catch-all
try:
    # risky code
    pass
except:
    # This catches ANY error (not recommended)
    print("Something went wrong")

# Better: specify the error type
try:
    # risky code
    pass
except Exception as e:
    # This catches any exception and stores it in 'e'
    print(f"Error occurred: {e}")
```

### Guided Practice

Write a try/except block for a calculator that takes two numbers and an operation (+, -, *, /) and handles all errors.

### Practice Problems

**Problem 1 — Beginner:** Write code that asks for a number and prints it doubled. Use try/except to handle invalid input.

**Problem 2 — Intermediate:** Write code that gets an item from a list by index. Handle both IndexError (index out of range) and ValueError (invalid input).

**Problem 3 — Challenge:** Write a program that converts temperatures. Ask for Celsius, convert to Fahrenheit. Handle invalid input gracefully and allow retrying.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `int(input())` and catch ValueError.
- Problem 2: Try/except for ValueError when converting input, try/except for IndexError when accessing list.
- Problem 3: Use a loop and `try/except` to allow retrying on error.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
try:
    num = int(input("Enter a number: "))
    print(f"Doubled: {num * 2}")
except ValueError:
    print("Invalid input! Please enter a number.")
```

**Problem 2:**
```python
items = [10, 20, 30, 40]
try:
    index = int(input("Index: "))
    print(items[index])
except ValueError:
    print("Invalid index input!")
except IndexError:
    print("Index out of range!")
```

**Problem 3:**
```python
while True:
    try:
        celsius = float(input("Temperature in Celsius: "))
        fahrenheit = celsius * 9/5 + 32
        print(f"{celsius}°C = {fahrenheit}°F")
        break  # Success, exit loop
    except ValueError:
        print("Invalid input! Please enter a number.")
```

</details>

---

# Day 135: Practice Lab—Building Robust Programs

**Learning Target:** I can design and implement programs with thorough testing, edge case handling, and error handling.

### Key Concepts

This lab brings together testing, edge cases, and exception handling. You'll write a complete program that:
- Handles edge cases gracefully
- Uses try/except for error handling
- Has test cases that verify it works
- Is robust against bad input

A "robust" program is one that works reliably even when given unexpected input.

### Code Examples

```python
# Example: Robust grade calculator
def get_valid_score():
    while True:
        try:
            score = float(input("Enter score (0-100): "))
            if score < 0 or score > 100:
                print("Score must be between 0 and 100")
                continue
            return score
        except ValueError:
            print("Invalid input! Please enter a number.")

def calculate_letter_grade(score):
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"

# Main program
scores = []
while True:
    score = get_valid_score()
    scores.append(score)

    letter = calculate_letter_grade(score)
    print(f"Grade: {letter}")

    if input("Add another score? (yes/no): ").lower() != "yes":
        break

if scores:
    average = sum(scores) / len(scores)
    print(f"\nAverage: {average:.2f}")
else:
    print("No scores entered")
```

### Guided Practice

Design and write a program that:
1. Asks the user for a list of numbers
2. Calculates and displays the sum, average, and count
3. Handles edge cases (empty list, non-numeric input)
4. Uses try/except for error handling

### Practice Problems

**Problem 1 — Beginner:** Write a program that asks for two numbers and divides the first by the second. Handle division by zero gracefully.

**Problem 2 — Intermediate:** Write a "shopping list" program that:
   - Lets users add items and prices
   - Calculates total cost
   - Handles invalid prices
   - Has edge cases (no items, zero price)

**Problem 3 — Challenge:** Write a "student grade tracker" that:
   - Stores student names and multiple test scores
   - Calculates average per student
   - Handles all edge cases and errors
   - Provides a summary report
   - Allows viewing individual student grades

<details>
<summary>💡 Hints</summary>

- Problem 1: Use try/except with ZeroDivisionError.
- Problem 2: Use lists or dictionaries to store items.
- Problem 3: Use nested dictionaries or lists to organize data.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
try:
    num1 = float(input("First number: "))
    num2 = float(input("Second number: "))
    if num2 == 0:
        print("Cannot divide by zero!")
    else:
        result = num1 / num2
        print(f"Result: {result}")
except ValueError:
    print("Invalid number!")
```

**Problem 2:**
```python
items = {}
total_cost = 0

while True:
    try:
        item_name = input("Item name (or 'done'): ").strip()
        if item_name.lower() == "done":
            break
        price = float(input(f"Price of {item_name}: "))
        if price < 0:
            print("Price cannot be negative!")
            continue
        items[item_name] = price
        total_cost += price
    except ValueError:
        print("Invalid price! Enter a number.")

print(f"\nTotal cost: ${total_cost:.2f}")
print(f"Items: {', '.join(items.keys()) if items else 'None'}")
```

**Problem 3:**
```python
# Dictionary structure: {"name": {"scores": [85, 90], "average": 87.5}}
students = {}

while True:
    print("\n1. Add student")
    print("2. Add score")
    print("3. View student")
    print("4. Summary")
    print("5. Exit")

    choice = input("Choice: ")

    if choice == "1":
        name = input("Student name: ")
        students[name] = {"scores": [], "average": 0}
    elif choice == "2":
        name = input("Student name: ")
        if name in students:
            try:
                score = float(input("Score: "))
                students[name]["scores"].append(score)
                students[name]["average"] = sum(students[name]["scores"]) / len(students[name]["scores"])
            except ValueError:
                print("Invalid score!")
    # etc.
```

</details>

---

# WEEK 28: DOCUMENTATION & FILE I/O

# Day 136: Code Documentation

**Learning Target:** I can write clear comments, docstrings, and follow naming conventions.

### Key Concepts

**Documentation** helps others (and your future self) understand your code. Three types:

1. **Comments** (`#`) explain WHY you did something, not what you did. If the code is clear, you don't need comments. If it's complex, explain the reasoning.

2. **Docstrings** (triple quotes) describe what a function does, what parameters it takes, and what it returns. They go right after the function definition.

3. **Naming conventions** make code readable:
   - Variables and functions: `lowercase_with_underscores`
   - Constants: `UPPERCASE_WITH_UNDERSCORES`
   - Classes: `PascalCase`

### Code Examples

```python
# BAD: Comments just restate the code
x = 10  # x is 10
y = 20  # y is 20
z = x + y  # Add x and y

# GOOD: Comments explain why
# Using separate variables for readability (could have calculated inline)
price_per_item = 10
number_of_items = 20
total_cost = price_per_item * number_of_items

# Example: Docstring
def calculate_final_price(original_price, discount_percent):
    """
    Calculate the final price after applying a discount.

    Args:
        original_price: The original price (float)
        discount_percent: The discount percentage (0-100)

    Returns:
        The final price after discount (float)
    """
    discount_amount = original_price * (discount_percent / 100)
    return original_price - discount_amount

# Example: Good naming
# GOOD
student_name = "Alex"
student_gpa = 3.85
is_on_honor_roll = student_gpa >= 3.5

# BAD (unclear)
sn = "Alex"
gpa = 3.85
ohr = gpa >= 3.5
```

### Guided Practice

Rewrite this code with better comments and naming:
```python
# Calculate average
s1 = 85
s2 = 90
s3 = 78
a = (s1 + s2 + s3) / 3
print(a)
```

### Practice Problems

**Problem 1 — Beginner:** Add docstrings to three simple functions (e.g., `add()`, `subtract()`, `multiply()`).

**Problem 2 — Intermediate:** Write a program that calculates BMI. Include:
   - Clear variable names
   - Meaningful comments (explaining logic, not just what code does)
   - Docstrings for any functions

**Problem 3 — Challenge:** Take a piece of code from an earlier unit and improve its documentation: rename variables, add comments, and write docstrings.

<details>
<summary>💡 Hints</summary>

- Problem 1: Docstring format: description, Args, Returns.
- Problem 2: Use names like `weight_lbs` not `w`.
- Problem 3: Comments should explain "why", not "what".

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
def add(a, b):
    """Add two numbers and return the result."""
    return a + b

def subtract(a, b):
    """Subtract the second number from the first and return the result."""
    return a - b

def multiply(a, b):
    """Multiply two numbers and return the product."""
    return a * b
```

**Problem 2:**
```python
def calculate_bmi(weight_lbs, height_inches):
    """
    Calculate Body Mass Index.

    Args:
        weight_lbs: Weight in pounds
        height_inches: Height in inches

    Returns:
        BMI as a float
    """
    # Convert to metric units for BMI formula
    weight_kg = weight_lbs * 0.453592
    height_m = height_inches * 0.0254

    # BMI = weight(kg) / height(m)^2
    bmi = weight_kg / (height_m ** 2)
    return bmi

# Get user input
weight = float(input("Weight (lbs): "))
height = float(input("Height (inches): "))

# Calculate and display
bmi = calculate_bmi(weight, height)
print(f"Your BMI: {bmi:.1f}")
```

**Problem 3:** Depends on code chosen, but should include:
- Renamed variables for clarity
- Comments explaining complex logic
- Docstrings for functions

</details>

---

# Day 137: Reading from Files

**Learning Target:** I can open and read files in Python.

### Key Concepts

Working with files is essential for many programs. Basic steps to read a file:

1. **Open** the file using `open()`
2. **Read** the file's contents
3. **Close** the file

Python provides several ways to read:
- `read()` — Read entire file as one string
- `readline()` — Read one line at a time
- `readlines()` — Read all lines into a list
- **Context manager** (`with` statement) — Automatically closes file

The `with` statement is safer because it automatically closes the file even if an error occurs.

### Code Examples

```python
# Method 1: read() — entire file as one string
with open("data.txt", "r") as file:
    content = file.read()
    print(content)

# Method 2: readline() — one line at a time
with open("data.txt", "r") as file:
    line1 = file.readline()  # "First line\n"
    line2 = file.readline()  # "Second line\n"
    print(line1)
    print(line2)

# Method 3: readlines() — all lines in a list
with open("data.txt", "r") as file:
    lines = file.readlines()  # ["First\n", "Second\n", "Third\n"]
    for line in lines:
        print(line.strip())  # .strip() removes \n

# Method 4: Loop through file (most common)
with open("data.txt", "r") as file:
    for line in file:  # Automatically reads one line at a time
        print(line.strip())  # Remove newline

# Handling file not found
try:
    with open("missing.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("File not found!")
```

### Guided Practice

Create a file called `names.txt` with several names (one per line). Write a program that reads this file and prints each name.

### Practice Problems

**Problem 1 — Beginner:** Write a program that reads a file and prints how many lines it has.

**Problem 2 — Intermediate:** Write a program that reads a file of numbers (one per line) and calculates the sum and average.

**Problem 3 — Challenge:** Write a program that reads a CSV file (comma-separated values) with columns like `name,grade,score` and displays a formatted report.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `readlines()` or count as you loop.
- Problem 2: Convert each line to a number, accumulate sum.
- Problem 3: Use `line.split(",")` to parse CSV.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
try:
    with open("data.txt", "r") as file:
        lines = file.readlines()
        print(f"File has {len(lines)} lines")
except FileNotFoundError:
    print("File not found!")
```

**Problem 2:**
```python
try:
    with open("numbers.txt", "r") as file:
        numbers = []
        for line in file:
            numbers.append(float(line.strip()))

        if numbers:
            total = sum(numbers)
            average = total / len(numbers)
            print(f"Sum: {total}")
            print(f"Average: {average}")
except FileNotFoundError:
    print("File not found!")
except ValueError:
    print("File contains non-numeric values!")
```

**Problem 3:**
```python
try:
    with open("grades.csv", "r") as file:
        for line in file:
            parts = line.strip().split(",")
            if len(parts) == 3:
                name, grade, score = parts
                print(f"{name}: Grade {grade}, Score {score}")
except FileNotFoundError:
    print("File not found!")
```

</details>

---

# Day 138: Writing to Files

**Learning Target:** I can write data to files and append to existing files.

### Key Concepts

Writing to files is similar to reading, but uses different modes:
- `"w"` — Write (creates new file or overwrites existing)
- `"a"` — Append (adds to end of existing file)
- `"x"` — Exclusive creation (fails if file exists)

Methods:
- `write()` — Write a string
- `writelines()` — Write a list of strings

Always use `with` statement to ensure file closes properly.

### Code Examples

```python
# Write to a file (creates new or overwrites existing)
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("This is line 2\n")
    file.write("This is line 3\n")

# Write multiple lines
with open("output.txt", "w") as file:
    lines = ["Line 1\n", "Line 2\n", "Line 3\n"]
    file.writelines(lines)

# Append to existing file
with open("log.txt", "a") as file:
    file.write("New log entry\n")

# Write data in a loop
with open("squares.txt", "w") as file:
    for i in range(1, 6):
        file.write(f"{i} squared is {i**2}\n")

# Safe writing with error handling
try:
    with open("data.txt", "w") as file:
        file.write("Important data")
    print("File written successfully")
except IOError:
    print("Error writing to file!")
```

### Guided Practice

Write a program that asks the user for their name, age, and favorite hobby, then saves this information to a file.

### Practice Problems

**Problem 1 — Beginner:** Write a program that creates a file with the numbers 1-10, each on a separate line.

**Problem 2 — Intermediate:** Write a program that:
   - Reads a file of student names
   - Asks for each student's grade
   - Writes name and grade to a new file

**Problem 3 — Challenge:** Write a "journal" program that:
   - Lets users write entries
   - Saves entries to a file (appending, not overwriting)
   - Displays all previous entries

<details>
<summary>💡 Hints</summary>

- Problem 1: Loop from 1-10 and write each with `\n`.
- Problem 2: Read names, get grades via input(), write to file.
- Problem 3: Use "a" mode to append entries.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
with open("numbers.txt", "w") as file:
    for i in range(1, 11):
        file.write(f"{i}\n")
```

**Problem 2:**
```python
# First, read student names
with open("names.txt", "r") as file:
    names = [line.strip() for line in file]

# Then get grades and write
with open("grades.txt", "w") as file:
    for name in names:
        grade = input(f"Grade for {name}: ")
        file.write(f"{name}: {grade}\n")
```

**Problem 3:**
```python
while True:
    entry = input("Write journal entry (or 'done'): ")
    if entry.lower() == "done":
        break

    with open("journal.txt", "a") as file:
        file.write(entry + "\n")

    print("Entry saved!")

# Display all entries
print("\nAll entries:")
try:
    with open("journal.txt", "r") as file:
        print(file.read())
except FileNotFoundError:
    print("No journal yet")
```

</details>

---

# Day 139: Processing File Data

**Learning Target:** I can process file data, including splitting lines and parsing CSV-style data.

### Key Concepts

Reading files is step one. Processing the data is step two. Common tasks:
- **Split lines** by delimiters (commas, spaces, etc.)
- **Parse CSV** (comma-separated values) into structured data
- **Clean data** (strip whitespace, convert types)
- **Extract information** (find specific columns, calculate aggregates)

The `split()` method is essential for breaking strings into parts.

### Code Examples

```python
# Example 1: CSV file with student data
# File contents: name,age,grade
# Alex,17,A
# Bob,16,B
# Carol,17,A+

with open("students.csv", "r") as file:
    for line in file:
        parts = line.strip().split(",")
        name, age, grade = parts
        print(f"{name} ({age}) got {grade}")

# Example 2: Parse data and store in list of dictionaries
students = []
with open("students.csv", "r") as file:
    for line in file:
        parts = line.strip().split(",")
        student = {
            "name": parts[0],
            "age": int(parts[1]),
            "grade": parts[2]
        }
        students.append(student)

# Now we can process the data
for student in students:
    print(f"{student['name']}: {student['grade']}")

# Example 3: Processing space-separated data
# File contents:
# apple 0.50
# banana 0.75
# cherry 1.25

total_price = 0
with open("prices.txt", "r") as file:
    for line in file:
        parts = line.strip().split()
        item = parts[0]
        price = float(parts[1])
        total_price += price
        print(f"{item}: ${price}")

print(f"Total: ${total_price:.2f}")
```

### Guided Practice

Create a CSV file with columns: `product,quantity,price_per_unit`. Write a program that reads this file and calculates the total inventory value.

### Practice Problems

**Problem 1 — Beginner:** Write a program that reads a file where each line is `name score`, and prints the names of students who scored above 80.

**Problem 2 — Intermediate:** Write a program that reads a CSV file with `date,amount,description` and calculates total income.

**Problem 3 — Challenge:** Write a program that reads a CSV with student data and calculates statistics: average grade, highest score, number of students, etc.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `split()` to separate name and score.
- Problem 2: Convert amount to float, sum values.
- Problem 3: Store in list of dictionaries, calculate statistics.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
with open("scores.txt", "r") as file:
    for line in file:
        parts = line.strip().split()
        name = parts[0]
        score = int(parts[1])
        if score > 80:
            print(name)
```

**Problem 2:**
```python
with open("income.csv", "r") as file:
    total = 0
    for line in file:
        parts = line.strip().split(",")
        amount = float(parts[1])
        total += amount
    print(f"Total income: ${total:.2f}")
```

**Problem 3:**
```python
import statistics

students = []
with open("students.csv", "r") as file:
    for line in file:
        parts = line.strip().split(",")
        students.append({
            "name": parts[0],
            "score": float(parts[1])
        })

scores = [s["score"] for s in students]
print(f"Count: {len(students)}")
print(f"Average: {statistics.mean(scores):.2f}")
print(f"Max: {max(scores)}")
print(f"Min: {min(scores)}")
```

</details>

---

# Day 140: Practice Lab—File-Based Programs

**Learning Target:** I can write complete programs that read, process, and write file data.

### Key Concepts

This lab combines file I/O with real-world applications. You'll build programs that:
- Read data from files
- Process and analyze the data
- Handle errors gracefully
- Write results back to files

Real programs work with files constantly—logs, configuration, data analysis, reports.

### Code Examples

```python
# Example: Gradebook program
def add_grade(filename, student_name, grade):
    with open(filename, "a") as file:
        file.write(f"{student_name},{grade}\n")

def read_grades(filename):
    grades = {}
    try:
        with open(filename, "r") as file:
            for line in file:
                parts = line.strip().split(",")
                if len(parts) == 2:
                    grades[parts[0]] = float(parts[1])
    except FileNotFoundError:
        print(f"{filename} not found")
    return grades

def calculate_class_average(filename):
    grades = read_grades(filename)
    if grades:
        average = sum(grades.values()) / len(grades)
        return average
    return 0

# Main program
while True:
    print("1. Add grade")
    print("2. View all grades")
    print("3. Class average")
    print("4. Exit")

    choice = input("Choice: ")

    if choice == "1":
        name = input("Student name: ")
        try:
            grade = float(input("Grade: "))
            add_grade("grades.txt", name, grade)
        except ValueError:
            print("Invalid grade!")
    elif choice == "2":
        grades = read_grades("grades.txt")
        for name, grade in grades.items():
            print(f"{name}: {grade}")
    elif choice == "3":
        avg = calculate_class_average("grades.txt")
        print(f"Class average: {avg:.2f}")
    elif choice == "4":
        break
```

### Guided Practice

Write a program that maintains a "to-do list" in a file:
- Load tasks from file on startup
- Allow adding, viewing, and removing tasks
- Save changes back to file

### Practice Problems

**Problem 1 — Beginner:** Write a simple "contact list" program that:
   - Reads contacts from a file (name, phone)
   - Displays all contacts
   - Saves to file

**Problem 2 — Intermediate:** Write an "expense tracker" that:
   - Reads expenses from a CSV file
   - Calculates total spent
   - Allows adding new expenses
   - Saves updated list back to file

**Problem 3 — Challenge:** Write a complete "student grade management system" that:
   - Maintains student records in a file (name, multiple grades)
   - Calculates average per student
   - Allows adding students and grades
   - Generates a report
   - Handles all errors gracefully

<details>
<summary>💡 Hints</summary>

- Problem 1: Store name and phone separated by comma or space.
- Problem 2: CSV format; use float for amounts.
- Problem 3: Use dictionaries; save after each change.

</details>

<details>
<summary>✅ Sample Answers</summary>

**Problem 1:**
```python
def load_contacts(filename):
    contacts = {}
    try:
        with open(filename, "r") as file:
            for line in file:
                parts = line.strip().split(",")
                if len(parts) == 2:
                    contacts[parts[0]] = parts[1]
    except FileNotFoundError:
        pass
    return contacts

def save_contacts(filename, contacts):
    with open(filename, "w") as file:
        for name, phone in contacts.items():
            file.write(f"{name},{phone}\n")

contacts = load_contacts("contacts.txt")

while True:
    print("1. View", "2. Add", "3. Exit")
    choice = input("Choice: ")

    if choice == "1":
        for name, phone in contacts.items():
            print(f"{name}: {phone}")
    elif choice == "2":
        name = input("Name: ")
        phone = input("Phone: ")
        contacts[name] = phone
        save_contacts("contacts.txt", contacts)
    elif choice == "3":
        break
```

**Problem 2:** Similar structure with expenses.csv

**Problem 3:** Complete student grade system with full functionality.

</details>

---

# WEEK 29: REVIEW & ASSESSMENT

# Day 141: Mini-Project—Bug Hunt Challenge

**Learning Target:** I can apply all debugging and programming skills to solve a complex problem.

### Key Concepts

In this mini-project, you'll either:
1. Debug a deliberately broken program
2. Build a file-based program from scratch

Both options require:
- Understanding the problem
- Debugging systematically
- Testing thoroughly
- Documenting your code

### Guided Practice

**Option A: Bug Hunt Challenge**

You're given a broken program that should calculate student GPAs from a file. The program has:
- 2-3 syntax errors
- 2-3 runtime errors
- 1-2 logic errors

Your job:
1. Identify all errors
2. Explain what each error is
3. Fix each error
4. Test to ensure it works

**Option B: Build a Program**

Build a "journal analyzer" that:
1. Reads journal entries from a file
2. Counts words and entries
3. Finds longest/shortest entries
4. Saves a summary report
5. Handles all errors gracefully

### Practice Problems

**Problem 1 — Beginner:** Debug a provided program that calculates average test scores.

**Problem 2 — Intermediate:** Debug a more complex program that processes student data from a CSV file.

**Problem 3 — Challenge:** Build a complete "grade tracker" program that reads, processes, and writes student data with full error handling and testing.

<details>
<summary>💡 Hints</summary>

- Problem 1: Look for missing colons, type conversion issues, off-by-one errors.
- Problem 2: CSV parsing, missing return statements, logic errors in calculations.
- Problem 3: Plan the program first; test thoroughly.

</details>

---

# Day 142: Review—Error Types, Debugging Strategies

**Learning Target:** I can identify error types and apply appropriate debugging strategies.

### Key Concepts

Review of Weeks 25-26:
- **Three error types:** Syntax, runtime, logic
- **Reading tracebacks:** Error type, line number, message
- **Common errors:** ZeroDivisionError, TypeError, NameError, IndexError
- **Debugging strategies:** Print debugging, rubber duck debugging, systematic testing

### Guided Practice

Provide an unfamiliar program with errors. Students must:
1. Classify each error
2. Find the line causing it (using traceback)
3. Apply appropriate debugging strategy
4. Fix the error
5. Test the fix

### Practice Problems

**Problem 1 — Beginner:** Classify and fix 5 mixed errors from throughout the unit.

**Problem 2 — Intermediate:** Debug a program using only tracebacks (no looking at code).

**Problem 3 — Challenge:** Fix a program with multiple errors using only print debugging.

<details>
<summary>💡 Hints</summary>

- Problem 1: Review Week 25 & 26 materials.
- Problem 2: Read tracebacks carefully; they point to the problem.
- Problem 3: Strategic print statements; don't overwhelm with output.

</details>

---

# Day 143: Review—Testing, Documentation, File I/O

**Learning Target:** I can write test cases, document code clearly, and work with files.

### Key Concepts

Review of Weeks 27-28:
- **Testing:** Manual testing, edge cases, test cases
- **Exception handling:** try/except blocks
- **Documentation:** Comments, docstrings, naming conventions
- **File I/O:** Reading, writing, appending, processing data

### Guided Practice

Provide a program with:
- Missing documentation
- No error handling
- Untested edge cases

Students must:
1. Add comments and docstrings
2. Add try/except blocks
3. Identify and test edge cases
4. Add file I/O if needed

### Practice Problems

**Problem 1 — Beginner:** Add documentation to a simple program.

**Problem 2 — Intermediate:** Add error handling and test cases to a program.

**Problem 3 — Challenge:** Build a complete program with documentation, error handling, testing, and file I/O.

<details>
<summary>💡 Hints</summary>

- Problem 1: Focus on docstrings and clear variable names.
- Problem 2: Identify edge cases; add try/except.
- Problem 3: Plan everything before coding.

</details>

---

# Day 144: Unit 6 Assessment

**Learning Target:** I can demonstrate mastery of debugging, testing, documentation, and file I/O.

### Format

The Unit 6 Assessment consists of:
- **Part 1: Concept Questions** (5 questions, multiple choice or short answer)
- **Part 2: Bug Fixing** (3 programs with bugs to find and fix)
- **Part 3: File Processing** (Write a program that reads, processes, and writes data)
- **Part 4: Documentation** (Add documentation to provided code)

Total time: 55 minutes

### Assessment Topics

1. Error types (syntax, runtime, logic)
2. Reading and interpreting tracebacks
3. Common runtime errors and fixes
4. Debugging strategies
5. Testing and edge cases
6. Exception handling with try/except
7. Code documentation (comments, docstrings, naming)
8. File I/O (reading, writing, appending, processing)

---

# Day 145: Assessment Review and Reflection

**Learning Target:** I can reflect on my learning and identify areas of strength and growth.

### Activities

1. **Review Assessment Results** — Go through your assessment with the teacher/grader
2. **Error Analysis** — For each error, understand:
   - What went wrong?
   - Why did it go wrong?
   - What would you do differently?
3. **Reflection Questions:**
   - What was your strongest area in Unit 6?
   - What was most challenging?
   - What debugging strategy works best for you?
   - How will you apply these skills in Unit 7?
4. **Create a "Debugging Cheat Sheet"** — Your personal quick reference for common errors and fixes

### Guided Practice

In groups, discuss:
- The most common errors you encountered
- The most effective debugging technique
- Real-world applications of file I/O

---

## Unit Vocabulary Quick Reference

**Algorithm:** Step-by-step procedure to solve a problem
**Debugging:** Process of finding and fixing errors
**Edge case:** Unusual or extreme input that might cause errors
**Exception:** Runtime error in a Python program
**Logic error:** Code runs but produces wrong answer
**Runtime error:** Error that occurs while program is executing
**Syntax error:** Violation of Python grammar rules
**Test case:** Input, expected output, and description of what's being tested
**Traceback:** Error message showing where and what error occurred
**try/except:** Block that catches and handles exceptions

---

## Resources & Further Learning

- **Python Official Documentation:** docs.python.org
- **Real Python Tutorials:** realpython.com
- **GeeksforGeeks Python Guide:** geeksforgeeks.org/python
- **Stack Overflow:** stackoverflow.com (for searching error messages)

---

## Unit 6 Assessment Overview

See **UnitAssessment.md** for the full 15-question assessment.

See **UnitPractice.md** for 25 practice problems organized by difficulty.

See **ReferenceGuide.md** for quick syntax reference and key terms.
