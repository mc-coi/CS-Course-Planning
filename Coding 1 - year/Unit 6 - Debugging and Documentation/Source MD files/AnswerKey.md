# Unit 6 Answer Key — 25 Problems

## Beginner Problems

---

## Problem 1: Identify Error Types

Identify the error type (syntax, runtime, logic) for each:
- a) `print("hello"` (missing closing parenthesis)
- b) `result = 10 / 0` (dividing by zero)
- c) `average = (85 + 90) / 2` but should be 3 scores (only 2)

### Solution
```python
# a) Missing closing parenthesis - SYNTAX ERROR
# Python can't parse this, gives SyntaxError

# b) Division by zero - RUNTIME ERROR
# Code looks valid, but fails during execution with ZeroDivisionError

# c) Logic error - LOGIC ERROR
# Code runs and produces output, but wrong average (87.5 instead of 84.33)
```

### Expected Output
```
a) Syntax Error
b) Runtime Error (ZeroDivisionError)
c) Logic Error
```

### Common Mistakes
- Confusing runtime and logic errors
- Not understanding syntax errors prevent execution

---

## Problem 2: Produce and Explain NameError

Write and run code that produces a NameError, then explain what the error message means.

### Solution
```python
# This code produces a NameError
print(undefined_variable)

# Error message: NameError: name 'undefined_variable' is not defined
# Explanation: The variable 'undefined_variable' doesn't exist.
# We're trying to use a variable that was never created with an assignment.
```

### Expected Output
```
NameError: name 'undefined_variable' is not defined
```

### Common Mistakes
- Not understanding that the error indicates a missing variable
- Using wrong variable names in code

---

## Problem 3: Fix Average Calculation

Fix this code to calculate average properly:
```python
scores = [85, 90, 78]
average = (85 + 90 + 78) / 2
print(average)
```

### Solution
```python
# Fixed version - divide by 3 (number of scores), not 2
scores = [85, 90, 78]
average = (85 + 90 + 78) / 3
print(average)
```

### Expected Output
```
84.33333333333333
```

### Common Mistakes
- Only fixing the denominator without understanding why
- Using the list variable but then hardcoding values

---

## Problem 4: Try/Except for Invalid Input

Write a function that adds two numbers. Add a try/except block to handle invalid input.

### Solution
```python
# Define function with error handling
def add_numbers(a, b):
    try:
        a = float(a)
        b = float(b)
        return a + b
    except ValueError:
        return "Invalid input"

# Test it
print(add_numbers(5, 10))      # 15.0
print(add_numbers("abc", 10))  # Invalid input
```

### Expected Output
```
15.0
Invalid input
```

### Common Mistakes
- Not converting input to appropriate type inside try block
- Not catching the specific exception (ValueError)

---

## Problem 5: Test Plan for len()

Create a test plan for the `len()` function with 4 test cases.

### Solution
```python
# Test plan for len() function
test_cases = [
    ([], 0),                    # Test 1: Empty list
    ([1], 1),                   # Test 2: Single element
    ([1, 2, 3], 3),             # Test 3: Multiple elements
    ("hello", 5),               # Test 4: String length
]

# Run tests
for test_input, expected in test_cases:
    result = len(test_input)
    status = "PASS" if result == expected else "FAIL"
    print(f"len({test_input}) = {result}, expected {expected}: {status}")
```

### Expected Output
```
len([]) = 0, expected 0: PASS
len([1]) = 1, expected 1: PASS
len([1, 2, 3]) = 3, expected 3: PASS
len(hello) = 5, expected 5: PASS
```

### Common Mistakes
- Not testing edge cases (empty list)
- Not testing different data types

---

## Problem 6: Read File Line by Line

Write a program that reads a file and prints each line.

### Solution
```python
# Read and print file contents
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())  # .strip() removes newline characters
```

### Expected Output
```
(Contents of data.txt, one line per output)
```

### Common Mistakes
- Not using with statement (doesn't close file properly)
- Not stripping newline characters (extra blank lines appear)

---

## Problem 7: Write Numbers to File

Write a program that writes 5 numbers to a file, each on a separate line.

### Solution
```python
# Write numbers to file
with open("numbers.txt", "w") as file:
    for i in range(1, 6):
        file.write(f"{i}\n")

print("File written successfully")
```

### Expected Output
```
File written successfully
(And numbers.txt contains: 1, 2, 3, 4, 5 on separate lines)
```

### Common Mistakes
- Forgetting the "\n" for newlines
- Not using with statement
- Using "a" (append) instead of "w" (write)

---

## Problem 8: Fix Indentation Error

Fix this indentation error:
```python
for i in range(5):
print(i)
```

### Solution
```python
# Fixed - print statement must be indented
for i in range(5):
    print(i)
```

### Expected Output
```
0
1
2
3
4
```

### Common Mistakes
- Not understanding that indentation is required
- Using spaces instead of consistent indentation

---

## Problem 9: Identify Logic Error

Identify the logic error: `if score > 90 and score < 80:`

### Solution
```python
# Logic error: No number can be both > 90 AND < 80
# This condition is always False
# Should be either: if score > 90 OR score < 80
# Or more likely: if score >= 80 and score < 90
```

### Expected Output
```
Logic error: Impossible condition (always False)
```

### Common Mistakes
- Not recognizing impossible conditions
- Using AND when OR is needed (or vice versa)

---

## Problem 10: Add Comments to Code

Add comments to this code:
```python
name = input("Name: ")
age = int(input("Age: "))
print(f"Hello {name}, you are {age}")
```

### Solution
```python
# Get user's name
name = input("Name: ")

# Get user's age and convert to integer
age = int(input("Age: "))

# Display greeting with name and age
print(f"Hello {name}, you are {age}")
```

### Expected Output
```
Name: Alice
Age: 25
Hello Alice, you are 25
```

### Common Mistakes
- Comments that don't add value
- Too many comments on simple operations

---

## Intermediate Problems

---

## Problem 11: Debug List Sum Program

Debug this program that should sum a list of numbers:
```python
numbers = [5, 10, 15, 20]
total = 0
for num in numbers
    total = total + num
print(f"Total: {total}")
```

### Solution
```python
# Fixed: Added missing colon after for statement
numbers = [5, 10, 15, 20]
total = 0
for num in numbers:  # Added colon here
    total = total + num
print(f"Total: {total}")
```

### Expected Output
```
Total: 50
```

### Common Mistakes
- Missing colon after for statement
- Indentation issues

---

## Problem 12: Read CSV and Filter

Write a program that reads a CSV file (name,score) and prints only students with score > 80.

### Solution
```python
# Read CSV file and filter results
with open("scores.csv", "r") as file:
    for line in file:
        parts = line.strip().split(",")
        name, score = parts
        if int(score) > 80:
            print(name)
```

### Expected Output
```
(Student names with scores > 80)
```

### Common Mistakes
- Not converting score to int before comparing
- Not handling the newline character
- Not splitting on comma

---

## Problem 13: Write Test Cases

Write test cases for a function that checks if a password is strong (8+ characters).

### Solution
```python
# Function to test
def is_strong_password(password):
    return len(password) >= 8

# Test cases
test_cases = [
    ("abc", False),        # Too short
    ("password", True),    # Exactly 8 chars
    ("1234567", False),    # 7 chars
    ("12345678", True),    # 8 chars
    ("verylongpassword", True),  # Long password
]

# Run tests
for password, expected in test_cases:
    result = is_strong_password(password)
    status = "PASS" if result == expected else "FAIL"
    print(f"'{password}': {status}")
```

### Expected Output
```
'abc': PASS
'password': PASS
'1234567': PASS
'12345678': PASS
'verylongpassword': PASS
```

### Common Mistakes
- Not testing edge cases (exactly 8 characters)
- Not testing both True and False cases

---

## Problem 14: Add Docstring

Add a docstring to this function:
```python
def calculate_area(length, width):
    return length * width
```

### Solution
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

### Expected Output
```
(Function works the same, but now has documentation)
```

### Common Mistakes
- Not using triple quotes
- Not explaining what the function does
- Not documenting parameters and return value

---

## Problem 15: Handle Division by Zero

Fix this program to handle division by zero:
```python
num1 = float(input("Number 1: "))
num2 = float(input("Number 2: "))
result = num1 / num2
print(result)
```

### Solution
```python
# Fixed with try/except
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

### Expected Output
```
Number 1: 10
Number 2: 0
Cannot divide by zero
```

### Common Mistakes
- Only catching the exception without preventing the error
- Not checking before dividing

---

## Problem 16: Find Maximum in File

Write a program that reads a file of numbers and finds the maximum.

### Solution
```python
# Read numbers from file and find maximum
with open("numbers.txt", "r") as file:
    numbers = [float(line.strip()) for line in file]
    if numbers:
        print(f"Maximum: {max(numbers)}")
```

### Expected Output
```
Maximum: (largest number in file)
```

### Common Mistakes
- Not checking if list is empty before calling max()
- Not converting strings to float

---

## Problem 17: Identify and Fix Errors

Identify and fix all errors in this program:
```python
def get_grade(score)
    if score >= 90
        return "A"
    return "F"
```

### Solution
```python
# Fixed: Added colons after function definition and if statement
def get_grade(score):  # Fixed: Added colon
    if score >= 90:    # Fixed: Added colon
        return "A"
    return "F"
```

### Expected Output
```
(Program now runs correctly)
```

### Common Mistakes
- Missing colons on function definition and if statement
- Not recognizing both errors

---

## Problem 18: Use Print Debugging

Write a program that uses print debugging to trace a loop problem.

### Solution
```python
# Program with print debugging
result = 0
for i in range(5):
    print(f"DEBUG: i = {i}")
    result = result + i
    print(f"DEBUG: result = {result}")

print(f"Final result: {result}")
```

### Expected Output
```
DEBUG: i = 0
DEBUG: result = 0
DEBUG: i = 1
DEBUG: result = 1
DEBUG: i = 2
DEBUG: result = 3
DEBUG: i = 3
DEBUG: result = 6
DEBUG: i = 4
DEBUG: result = 10
Final result: 10
```

### Common Mistakes
- Not printing at key points
- Not using meaningful debug labels
- Forgetting to remove debug statements

---

## Problem 19: Create Edge Cases

Create edge cases for a function that removes duplicates from a list.

### Solution
```python
# Function to test
def remove_duplicates(items):
    seen = []
    result = []
    for item in items:
        if item not in seen:
            result.append(item)
            seen.append(item)
    return result

# Edge cases
edge_cases = [
    ([],),                      # Empty list
    ([1],),                     # Single item
    ([1, 1, 1],),               # All duplicates
    ([1, 2, 3],),               # No duplicates
    ([1, 2, 1, 2],),            # Multiple duplicates
]

# Test edge cases
for case in edge_cases:
    result = remove_duplicates(case[0])
    print(f"Input: {case[0]}, Output: {result}")
```

### Expected Output
```
Input: [], Output: []
Input: [1], Output: [1]
Input: [1, 1, 1], Output: [1]
Input: [1, 2, 3], Output: [1, 2, 3]
Input: [1, 2, 1, 2], Output: [1, 2]
```

### Common Mistakes
- Not testing empty list
- Not testing all duplicates
- Not preserving order

---

## Problem 20: Append Without Overwriting

Write a program that appends a new entry to a file without overwriting existing content.

### Solution
```python
# Append mode adds to end of file without overwriting
with open("journal.txt", "a") as file:  # "a" mode appends
    entry = input("New entry: ")
    file.write(entry + "\n")

print("Entry saved")
```

### Expected Output
```
New entry: My first entry
Entry saved
(And the entry is added to the file)
```

### Common Mistakes
- Using "w" mode (overwrites)
- Forgetting newline character
- Not using with statement

---

## Challenge Problems

---

## Problem 21: Debug Syntax and Runtime Errors

Debug a program with both syntax and runtime errors:
```python
def calculate_average(scores)
    total = sum(scores)
    average = total / len(scores)
    return average

print(calculate_average([85, 90, 78]))
```

### Solution
```python
# Fixed: Added colon and handle empty list case
def calculate_average(scores):  # Added colon
    if len(scores) == 0:  # Handle empty list
        return 0
    total = sum(scores)
    average = total / len(scores)
    return average

print(calculate_average([85, 90, 78]))
```

### Expected Output
```
84.33333333333333
```

### Common Mistakes
- Not adding the colon
- Not handling empty list edge case

---

## Problem 22: Read CSV, Calculate Statistics, Write Report

Write a program that reads a CSV file with student data (name,grade,score), calculates statistics (average score), and writes a summary to a file.

### Solution
```python
# Read CSV, calculate stats, write report
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
    avg = sum(scores) / len(scores)

    with open("summary.txt", "w") as file:
        file.write(f"Class average: {avg:.2f}\n")
```

### Expected Output
```
(summary.txt created with class average)
```

### Common Mistakes
- Not parsing CSV correctly
- Not handling empty file
- Not formatting output

---

## Problem 23: Complete Test Plan

Create a complete test plan for a function that calculates BMI. Include at least 8 test cases covering normal and edge cases.

### Solution
```python
def calculate_bmi(weight, height):
    return (weight / (height ** 2)) * 703

# Test plan with 8 cases
test_cases = [
    (150, 70, 21.52),        # Normal weight
    (200, 70, 28.70),        # Overweight
    (100, 70, 14.35),        # Underweight
    (0.1, 70, 0.00),         # Very small
    (500, 70, 71.76),        # Very large
    (150, 1, 107700.00),     # Very short (unrealistic)
    (150, 100, 1.50),        # Very tall (unrealistic)
    (150.5, 70.5, 20.96),    # Decimal values
]

# Run all tests
for weight, height, expected in test_cases:
    result = calculate_bmi(weight, height)
    status = "PASS" if abs(result - expected) < 0.01 else "FAIL"
    print(f"BMI({weight}, {height}) = {result:.2f}, expected {expected:.2f}: {status}")
```

### Expected Output
```
BMI(150, 70) = 21.52, expected 21.52: PASS
(All tests PASS)
```

### Common Mistakes
- Not testing edge cases
- Not testing decimal values
- Not considering unrealistic inputs

---

## Problem 24: Journal Program

Write a "journal" program that:
- Appends user entries to a file
- Displays all previous entries
- Handles all errors gracefully

### Solution
```python
import os

# Main loop
while True:
    print("1) Add entry")
    print("2) Read entries")
    print("3) Exit")
    choice = input("Choose: ")

    if choice == "1":
        # Add entry
        try:
            entry = input("New entry: ")
            with open("journal.txt", "a") as file:
                file.write(entry + "\n")
            print("Entry saved")
        except IOError:
            print("Error saving entry")

    elif choice == "2":
        # Read entries
        try:
            with open("journal.txt", "r") as file:
                print("\nAll entries:")
                print(file.read())
        except FileNotFoundError:
            print("No journal yet")

    elif choice == "3":
        break
    else:
        print("Invalid choice")
```

### Expected Output
```
1) Add entry
2) Read entries
3) Exit
Choose: 1
New entry: Today was great!
Entry saved
1) Add entry
2) Read entries
3) Exit
Choose: 2

All entries:
Today was great!
1) Add entry
2) Read entries
3) Exit
Choose: 3
```

### Common Mistakes
- Not handling file not found errors
- Using "w" instead of "a" (overwrites entries)
- Not displaying a menu

---

## Problem 25: Debug and Improve Program

Debug and improve this program:
```python
def process_data(filename):
    with open(filename) as file:
        for line in file:
            data = line.split(",")
            print(f"Name: {data[0]}, Score: {data[1]}")

process_data("data.csv")
```

### Solution
```python
def process_data(filename):
    """Process CSV file and display data."""
    try:
        with open(filename, "r") as file:
            for line in file:
                data = line.strip().split(",")  # strip() removes newline
                if len(data) >= 2:  # Check data has enough fields
                    name = data[0]
                    score = data[1]
                    print(f"Name: {name}, Score: {score}")
    except FileNotFoundError:
        print(f"File {filename} not found")
    except Exception as e:
        print(f"Error processing file: {e}")

process_data("data.csv")
```

### Expected Output
```
Name: Alice, Score: 85
Name: Bob, Score: 92
(Or appropriate error messages)
```

### Common Mistakes
- Not stripping newline characters
- Not checking if data has enough fields
- Not handling FileNotFoundError
- Not adding docstring

---
