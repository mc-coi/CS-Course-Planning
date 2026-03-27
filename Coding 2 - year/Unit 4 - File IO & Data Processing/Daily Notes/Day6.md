# Day 6: Introduction to Exception Handling — try/except
**Learning Target:** I can use try/except blocks to handle runtime errors gracefully and prevent programs from crashing.

### Key Concepts

**Exception:** An error that occurs during program execution (e.g., dividing by zero, accessing a missing file).

**try block:** Code that might raise an exception.

**except block:** Code that runs if an exception occurs.

**Exception handling flow:** If an exception occurs in try, Python skips remaining code and jumps to except.

**Generic except:** Catching all exceptions (not recommended; be specific).

**Exception variable:** `except Exception as e:` captures the exception object to access error message.

**Graceful degradation:** Program continues running instead of crashing.

### Code Examples

```python
# Example 1: Basic try/except
try:
    number = int("hello")  # This will raise ValueError
except ValueError:
    print("Error: Could not convert to integer")

# Example 2: Exception with variable
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error occurred: {e}")

# Example 3: File handling with try/except
try:
    with open('missing_file.txt', 'r') as f:
        content = f.read()
except FileNotFoundError as e:
    print(f"File not found: {e}")

# Example 4: Multiple except blocks
try:
    user_input = input("Enter a number: ")
    number = int(user_input)
    result = 10 / number
except ValueError:
    print("Error: Please enter a valid integer")
except ZeroDivisionError:
    print("Error: Cannot divide by zero")

# Example 5: Generic Exception (less preferred)
try:
    x = int("abc")
except Exception as e:
    print(f"An error occurred: {type(e).__name__}: {e}")

# Example 6: Processing a list safely
numbers = ["1", "2", "abc", "4"]
for item in numbers:
    try:
        num = int(item)
        print(f"Successfully converted: {num}")
    except ValueError:
        print(f"Could not convert: {item}")

# Example 7: Accessing dictionary/list safely
data = {'name': 'Alice', 'age': 25}
try:
    print(data['city'])  # This key doesn't exist
except KeyError:
    print("Key not found in dictionary")

# Example 8: Safe list access
my_list = [1, 2, 3]
try:
    print(my_list[10])  # Index out of range
except IndexError:
    print("Index is out of range")

# Example 9: Nested try/except
try:
    with open('data.txt', 'r') as f:
        lines = f.readlines()
    for line in lines:
        try:
            value = int(line.strip())
            print(f"Value: {value}")
        except ValueError:
            print(f"Skipping non-integer line: {line.strip()}")
except FileNotFoundError:
    print("Data file not found")

# Example 10: Simple program using try/except
def divide_numbers(a, b):
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        print("Error: Cannot divide by zero")
        return None

print(divide_numbers(10, 2))   # Works fine
print(divide_numbers(10, 0))   # Handled gracefully
```

### Guided Practice

**Activity: User Input Validation**

1. Create a program that:
   - Asks the user for a number
   - Uses try/except to handle invalid input
   - If valid, calculates the square root
   - If invalid, displays a friendly error message and asks again

2. Handle these potential errors:
   - User enters non-numeric text (ValueError)
   - User enters a negative number for square root (ValueError when converting, or catch during calculation)

**Step-by-step code:**
```python
import math

while True:
    try:
        user_input = input("Enter a positive number (or 'q' to quit): ")

        if user_input.lower() == 'q':
            print("Goodbye!")
            break

        number = float(user_input)

        if number < 0:
            print("Error: Please enter a non-negative number")
            continue

        sqrt_value = math.sqrt(number)
        print(f"Square root of {number} is {sqrt_value:.2f}")

    except ValueError:
        print("Error: Please enter a valid number")
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that prompts for two numbers and divides them. Use try/except to handle division by zero.

**Problem 2 — Intermediate:** Write a program that reads a CSV line (Name,Age,Salary), parses it, and uses try/except to handle cases where Age or Salary are non-numeric.

**Problem 3 — Challenge:** Write a program that reads a file containing numbers (one per line), attempts to convert each to an integer, skips invalid lines, calculates the sum, and displays how many lines were valid vs. invalid.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use `try` to wrap the division operation.
- Catch `ZeroDivisionError`.
- Display a friendly error message.

**Problem 2:**
- Split the line by commas.
- Use separate try/except blocks (or nested) for Age and Salary conversions.
- Display which field caused the error.

**Problem 3:**
- Keep counters for valid and invalid lines.
- Use try/except in a loop reading lines.
- Sum only the valid numbers.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
try:
    a = float(input("Enter first number: "))
    b = float(input("Enter second number: "))
    result = a / b
    print(f"Result: {result}")
except ZeroDivisionError:
    print("Error: Cannot divide by zero")
except ValueError:
    print("Error: Please enter valid numbers")

# Problem 2
line = "Alice,thirty,50000"
try:
    parts = line.split(',')
    name = parts[0]
    age = int(parts[1])
    salary = float(parts[2])
    print(f"{name}: Age {age}, Salary ${salary:.2f}")
except ValueError as e:
    print(f"Error parsing line: {e}")

# Problem 3
data = """10
20
abc
30
xyz
40"""

valid_count = 0
invalid_count = 0
total = 0

for line in data.split('\n'):
    try:
        num = int(line.strip())
        total += num
        valid_count += 1
    except ValueError:
        invalid_count += 1

print(f"Valid: {valid_count}, Invalid: {invalid_count}, Sum: {total}")
```

</details>
