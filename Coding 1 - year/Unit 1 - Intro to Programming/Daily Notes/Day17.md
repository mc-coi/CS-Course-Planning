# Day 17: Debugging Intro — Syntax Errors & Reading Error Messages
**Learning Target:** I can identify and fix common syntax errors and type errors in Python.

### Key Concepts
Debugging is the process of finding and fixing errors in code. There are three main types of errors:

**Syntax Errors** - Breaking the rules of Python (code won't run):
- Misspelled keywords: `prin("Hello")` instead of `print("Hello")`
- Missing parentheses: `print "Hello"` instead of `print("Hello")`
- Missing quotes: `print(Hello)` instead of `print("Hello")`
- Missing colons or incorrect operators

**Type Errors** - Using the wrong data type:
- Trying to add a string and number: `"5" + 3`
- Trying to multiply a string by a float: `"hello" * 2.5`
- Not converting input: `age = input("Age: "); print(age + 10)`

**Logic Errors** - Code runs but produces wrong results:
- Incorrect formula: area = length + width instead of length × width
- Wrong order of operations
- Variable initialized to wrong value

**Reading error messages:**
When Python finds an error, it prints a message showing:
- The line number where the error occurred
- The type of error (SyntaxError, TypeError, etc.)
- A description of what went wrong

Example:
```
  File "program.py", line 3
    print("Hello"
           ^
SyntaxError: unexpected EOF while parsing
```

This means: Line 3 has a syntax error—probably a missing closing parenthesis.

### Code Examples
```python
# Syntax Error Examples

# Error: Missing closing parenthesis
# print("Hello"
# Fix:
print("Hello")

# Error: Misspelled function
# Print("Hello")
# Fix:
print("Hello")

# Error: Missing quotes
# print(Hello)
# Fix:
print("Hello")

# Type Error Example
# age = input("Age: ")
# print(age + 10)  # Can't add string to int!
# Fix:
age = int(input("Age: "))
print(age + 10)

# Logic Error Example
# length = 5
# width = 3
# area = length + width  # Should be multiplication!
# Fix:
area = length * width
```

### Guided Practice
Debug the following programs:
1. A program with syntax errors
2. A program with type errors
3. A program with logic errors

Identify the error, explain what's wrong, and write the fix.

### Practice Problems

**Problem 1 — Beginner:** Debug this code:
```python
name = input(What is your name? )
age = int(input("Age: ")
print("Hello, " name + "!")
```

**Problem 2 — Intermediate:** Debug this code:
```python
score1 = int(input("Score 1: "))
score2 = input("Score 2: ")
average = (score1 + score2) / 2
print(f"Average: {average}")
```

**Problem 3 — Challenge:** Debug this code:
```python
principal = float(input("Principal: "))
rate = float(input("Rate: "))
years = input("Years: ")
total = principal * (1 + rate / 100) ** years
print(f"Total: ${total.2f}")
```

<details>
<summary>💡 Hints</summary>

- Problem 1: Look for missing quotes and parentheses
- Problem 2: Check that all variables are the same type before using them in math
- Problem 3: Look for data type issues and formatting issues
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Fixed
name = input("What is your name? ")
age = int(input("Age: "))
print("Hello, " + name + "!")

# Problem 2 Fixed
score1 = int(input("Score 1: "))
score2 = int(input("Score 2: "))  # Convert to int!
average = (score1 + score2) / 2
print(f"Average: {average}")

# Problem 3 Fixed
principal = float(input("Principal: "))
rate = float(input("Rate: "))
years = int(input("Years: "))  # Convert to int!
total = principal * (1 + rate / 100) ** years
print(f"Total: ${total:.2f}")  # Use colon notation
```

</details>

---
