# Day 5: Exception Handling Advanced
**Learning Target:** I can write robust code with try/except/finally and multiple exception types.

### Key Concepts
Exception handling: `try`, `except`, `else`, `finally`, `raise`

Handle specific exceptions, not all errors generically.

### Code Examples
```python
# Basic try/except
try:
    num = int(input("Enter a number: "))
except ValueError:
    print("That's not a valid number!")

# Multiple exception types
try:
    file = open("data.txt", "r")
    data = file.read()
except FileNotFoundError:
    print("File not found!")
except IOError:
    print("Error reading file!")

# else and finally
try:
    num = int(input("Number: "))
except ValueError:
    print("Invalid input")
else:
    print(f"You entered {num}")
finally:
    print("Cleaning up...")

# Accessing exception info
try:
    1 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")

# Re-raising exceptions
try:
    file = open("data.txt", "r")
except FileNotFoundError:
    print("File not found!")
    raise  # Re-raise the exception
```

### Guided Practice
Write file operations with proper exception handling.

### Practice Problems
**Problem 1 — Beginner:** Write code that handles FileNotFoundError.

**Problem 2 — Intermediate:** Handle multiple exceptions in a calculator.

**Problem 3 — Challenge:** Create nested try/except with finally.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
try:
    a = int(input("Num 1: "))
    b = int(input("Num 2: "))
    result = a / b
except ValueError:
    print("Invalid number")
except ZeroDivisionError:
    print("Can't divide by zero")
```
</details>

---

---
