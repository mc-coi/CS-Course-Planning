# Unit 6 Practice Bank — 25 Problems by Difficulty

## Beginner Problems (Straightforward, foundational concepts)

**Problem 1:** Identify the error type (syntax, runtime, logic) for each:
   - a) `print("hello"` (missing closing parenthesis)
   - b) `result = 10 / 0` (dividing by zero)
   - c) `average = (85 + 90) / 2` but should be 3 scores (only 2)

**Problem 2:** Write and run code that produces a NameError, then explain what the error message means.

**Problem 3:** Fix this code to calculate average properly:
```python
scores = [85, 90, 78]
average = (85 + 90 + 78) / 2
print(average)
```

**Problem 4:** Write a function that adds two numbers. Add a try/except block to handle invalid input.

**Problem 5:** Create a test plan for the `len()` function with 4 test cases.

**Problem 6:** Write a program that reads a file and prints each line.

**Problem 7:** Write a program that writes 5 numbers to a file, each on a separate line.

**Problem 8:** Fix this indentation error:
```python
for i in range(5):
print(i)
```

**Problem 9:** Identify the logic error: `if score > 90 and score < 80:`

**Problem 10:** Add comments to this code:
```python
name = input("Name: ")
age = int(input("Age: "))
print(f"Hello {name}, you are {age}")
```

---

## Intermediate Problems (Multiple steps, combining concepts)

**Problem 11:** Debug this program that should sum a list of numbers:
```python
numbers = [5, 10, 15, 20]
total = 0
for num in numbers
    total = total + num
print(f"Total: {total}")
```

**Problem 12:** Write a program that reads a CSV file (name,score) and prints only students with score > 80.

**Problem 13:** Write test cases for a function that checks if a password is strong (8+ characters).

**Problem 14:** Add a docstring to this function:
```python
def calculate_area(length, width):
    return length * width
```

**Problem 15:** Fix this program to handle division by zero:
```python
num1 = float(input("Number 1: "))
num2 = float(input("Number 2: "))
result = num1 / num2
print(result)
```

**Problem 16:** Write a program that reads a file of numbers and finds the maximum.

**Problem 17:** Identify and fix all errors in this program:
```python
def get_grade(score)
    if score >= 90
        return "A"
    return "F"
```

**Problem 18:** Write a program that uses print debugging to trace a loop problem.

**Problem 19:** Create edge cases for a function that removes duplicates from a list.

**Problem 20:** Write a program that appends a new entry to a file without overwriting existing content.

---

## Challenge Problems (Complex, requires synthesis of multiple concepts)

**Problem 21:** Debug a program with both syntax and runtime errors:
```python
def calculate_average(scores)
    total = sum(scores)
    average = total / len(scores)
    return average

print(calculate_average([85, 90, 78]))
```

**Problem 22:** Write a program that reads a CSV file with student data (name,grade,score), calculates statistics (average score), and writes a summary to a file.

**Problem 23:** Create a complete test plan for a function that calculates BMI. Include at least 8 test cases covering normal and edge cases.

**Problem 24:** Write a "journal" program that:
   - Appends user entries to a file
   - Displays all previous entries
   - Handles all errors gracefully

**Problem 25:** Debug and improve this program:
```python
def process_data(filename):
    with open(filename) as file:
        for line in file:
            data = line.split(",")
            print(f"Name: {data[0]}, Score: {data[1]}")

process_data("data.csv")
```

---

## Problem Solutions

### Beginner Solutions

**Problem 1:**
- a) Syntax error (missing closing paren)
- b) Runtime error (ZeroDivisionError)
- c) Logic error (dividing by 2 instead of 3)

**Problem 2:**
```python
print(undefined_variable)
# NameError: name 'undefined_variable' is not defined
```

**Problem 3:**
```python
scores = [85, 90, 78]
average = (85 + 90 + 78) / 3  # Fixed: divide by 3, not 2
print(average)  # Prints 84.33...
```

**Problem 4:**
```python
def add_numbers(a, b):
    try:
        a = float(a)
        b = float(b)
        return a + b
    except ValueError:
        return "Invalid input"
```

**Problem 5:**
```
Test cases for len():
- len([]) → 0
- len([1]) → 1
- len([1, 2, 3]) → 3
- len("hello") → 5
```

**Problem 6:**
```python
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())
```

**Problem 7:**
```python
with open("numbers.txt", "w") as file:
    for i in range(1, 6):
        file.write(f"{i}\n")
```

**Problem 8:**
```python
for i in range(5):
    print(i)  # Fixed: added indentation
```

**Problem 9:**
Logic error: `if score > 90 and score < 80:` is always False (no number is both > 90 AND < 80)

**Problem 10:**
```python
# Get user's name
name = input("Name: ")
# Get user's age and convert to integer
age = int(input("Age: "))
# Display greeting with name and age
print(f"Hello {name}, you are {age}")
```

### Intermediate Solutions

**Problem 11:**
```python
numbers = [5, 10, 15, 20]
total = 0
for num in numbers:  # Fixed: added colon
    total = total + num
print(f"Total: {total}")
```

**Problem 12:**
```python
with open("scores.csv", "r") as file:
    for line in file:
        parts = line.strip().split(",")
        name, score = parts
        if int(score) > 80:
            print(name)
```

**Problem 13:**
```python
def is_strong_password(password):
    return len(password) >= 8

test_cases = [
    ("abc", False),
    ("password", True),
    ("1234567", False),
    ("12345678", True),
]
```

**Problem 14:**
```python
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.

    Args:
        length: Rectangle length
        width: Rectangle width

    Returns:
        Area (length × width)
    """
    return length * width
```

**Problem 15:**
```python
try:
    num1 = float(input("Number 1: "))
    num2 = float(input("Number 2: "))
    if num2 == 0:
        print("Cannot divide by zero")
    else:
        result = num1 / num2
        print(result)
except ValueError:
    print("Invalid input")
```

**Problem 16:**
```python
with open("numbers.txt", "r") as file:
    numbers = [float(line.strip()) for line in file]
    if numbers:
        print(f"Maximum: {max(numbers)}")
```

**Problem 17:**
```python
def get_grade(score):  # Fixed: added colon
    if score >= 90:    # Fixed: added colon
        return "A"
    return "F"
```

**Problem 18:**
```python
for i in range(5):
    print(f"DEBUG: i = {i}")
    result = i * 2
    print(f"DEBUG: result = {result}")
    print(result)
```

**Problem 19:**
Edge cases:
- Empty list
- Single item
- All duplicates
- No duplicates
- Negative numbers
- Zeros

**Problem 20:**
```python
with open("journal.txt", "a") as file:  # "a" mode appends
    entry = input("New entry: ")
    file.write(entry + "\n")
```

### Challenge Solutions

**Problem 21:**
```python
def calculate_average(scores):  # Fixed: added colon
    total = sum(scores)
    average = total / len(scores)
    return average

print(calculate_average([85, 90, 78]))  # Prints 84.33...
```

**Problem 22:**
```python
import statistics

students = []
with open("grades.csv", "r") as file:
    for line in file:
        parts = line.strip().split(",")
        students.append({
            "name": parts[0],
            "score": float(parts[2])
        })

if students:
    scores = [s["score"] for s in students]
    avg = statistics.mean(scores)

    with open("summary.txt", "w") as file:
        file.write(f"Class average: {avg:.2f}\n")
```

**Problem 23:**
```
Test cases for BMI calculation:
1. Normal weight → valid result
2. Overweight → valid result
3. Zero weight → should handle gracefully
4. Negative weight → should reject
5. Zero height → ZeroDivisionError
6. Very large numbers → valid result
7. Very small numbers (decimal) → valid result
8. Non-numeric input → ValueError
```

**Problem 24:**
```python
while True:
    entry = input("Journal entry (or 'done'): ")
    if entry.lower() == "done":
        break

    try:
        with open("journal.txt", "a") as file:
            file.write(entry + "\n")
        print("Entry saved")
    except IOError:
        print("Error saving entry")

print("\nAll entries:")
try:
    with open("journal.txt", "r") as file:
        print(file.read())
except FileNotFoundError:
    print("No journal yet")
```

**Problem 25:**
```python
def process_data(filename):
    """Process CSV file and display data."""
    try:
        with open(filename, "r") as file:
            for line in file:
                data = line.strip().split(",")
                if len(data) >= 2:
                    name = data[0]
                    score = data[1]
                    print(f"Name: {name}, Score: {score}")
    except FileNotFoundError:
        print(f"File {filename} not found")
    except Exception as e:
        print(f"Error processing file: {e}")

process_data("data.csv")
```

---
