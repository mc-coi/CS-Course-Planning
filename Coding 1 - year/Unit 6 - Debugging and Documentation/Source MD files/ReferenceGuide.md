# Unit 6 Reference Guide — Debugging & Documentation Quick Reference

## Error Types & Identification

### Syntax Errors
**When:** Before the program runs (Python can't even parse the code)
**Examples:** Missing colon, mismatched quotes, indentation error
**How to fix:** Read the error message—Python tells you exactly where

```python
if x > 5        # Missing colon ❌
if x > 5:       # Fixed ✓

print("hello    # Mismatched quotes ❌
print("hello")  # Fixed ✓
```

### Runtime Errors
**When:** While the program is running
**Examples:** ZeroDivisionError, TypeError, NameError, IndexError
**How to fix:** Read the traceback

| Error Type | Cause | Fix |
|---|---|---|
| `ZeroDivisionError` | Divide by zero | Check if denominator != 0 |
| `TypeError` | Wrong data type for operation | Convert types: `int()`, `float()`, `str()` |
| `NameError` | Variable doesn't exist | Define the variable first |
| `IndexError` | List index out of range | Check `len(list)` before accessing |
| `ValueError` | Invalid value for conversion | Validate input before converting |

### Logic Errors
**When:** Program runs but gives wrong answer
**Examples:** Wrong formula, missing variable, condition always false
**How to fix:** Trace through code logic; use print debugging

---

## Debugging Strategies

### Strategy 1: Print Debugging
```python
for i in range(5):
    print(f"DEBUG: i = {i}")  # Shows what's happening
    result = i * 2
    print(f"DEBUG: result = {result}")
    print(result)
```

### Strategy 2: Rubber Duck Debugging
1. Explain your code out loud
2. Explain what each line does
3. When you have to explain something, you'll often find the bug

### Strategy 3: Systematic Testing
1. Make a test plan
2. Run test cases
3. Compare expected vs. actual output
4. Fix any mismatches

---

## Testing & Edge Cases

### Common Edge Cases
- **Empty:** Empty list, empty string, no items
- **Zero:** Especially important for division
- **Negatives:** Often forgotten
- **Boundaries:** Min/max values
- **Single item:** Off-by-one errors

### Test Case Format
```
Input: (what you're testing)
Expected: (what should happen)
Actual: (what really happens)
Status: PASS or FAIL
```

---

## Exception Handling

### Basic Structure
```python
try:
    # Code that might fail
    result = 10 / user_input
except ZeroDivisionError:
    print("Cannot divide by zero")
except ValueError:
    print("Invalid input")
```

### Common Exceptions to Catch
```python
try:
    num = int(input("Number: "))  # ValueError if non-numeric
except ValueError:
    print("Please enter a number")

try:
    result = a / b  # ZeroDivisionError if b is 0
except ZeroDivisionError:
    print("Cannot divide by zero")

try:
    item = my_list[10]  # IndexError if index doesn't exist
except IndexError:
    print("Index out of range")
```

---

## Documentation

### Comments (Explain WHY, not WHAT)
```python
# BAD: Just restates the code
x = 10  # x is 10

# GOOD: Explains reasoning
# We use separate variables for clarity (could be one line)
price = 10
quantity = 5
total = price * quantity
```

### Docstrings (For Functions)
```python
def calculate_discount(price, percent):
    """
    Calculate final price after discount.

    Args:
        price: Original price (float)
        percent: Discount percentage (0-100)

    Returns:
        Final price after discount (float)
    """
    discount = price * (percent / 100)
    return price - discount
```

### Naming Conventions
```python
# Variables and functions: lowercase_with_underscores
student_name = "Alex"
calculate_average()

# Constants: UPPERCASE_WITH_UNDERSCORES
MAX_SCORE = 100
PI = 3.14159

# Classes: PascalCase
class StudentRecord:
    pass
```

---

## File I/O

### Reading Files
```python
# Method 1: Read entire file
with open("data.txt", "r") as file:
    content = file.read()

# Method 2: Read line by line (best for large files)
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())  # .strip() removes \n

# Method 3: Read all lines into list
with open("data.txt", "r") as file:
    lines = file.readlines()  # ["line1\n", "line2\n"]
```

### Writing Files
```python
# Write (overwrites existing file)
with open("output.txt", "w") as file:
    file.write("Hello\n")
    file.write("World\n")

# Append (adds to end of file)
with open("log.txt", "a") as file:
    file.write("New entry\n")
```

### Processing CSV Data
```python
with open("data.csv", "r") as file:
    for line in file:
        parts = line.strip().split(",")
        name, age, score = parts
        print(f"{name}: {score}")
```

### Error Handling with Files
```python
try:
    with open("data.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("File not found")
except IOError:
    print("Error reading file")
```

---

## Quick Troubleshooting

| Problem | Check |
|---------|-------|
| Syntax error | Missing colon? Mismatched quotes/brackets? Wrong indentation? |
| NameError | Is the variable defined? Typo in name? |
| IndexError | Is the index within list bounds? `print(len(list))` first |
| TypeError | Are you mixing int and string? Use `int()`, `float()`, `str()` |
| ZeroDivisionError | Is divisor zero? Check before dividing |
| Logic error | Print variables to trace execution; check conditions |

---

## Common Debugging Workflows

### Workflow 1: Read a Traceback
1. Start at the bottom line (error type and message)
2. Go up to find the line that caused it
3. Understand what that line was trying to do
4. Apply the fix

### Workflow 2: Debug a Loop
1. Print loop variable at start of each iteration
2. Print important values inside loop
3. Count how many iterations happen
4. Check for off-by-one errors

### Workflow 3: Debug a Function
1. Print input parameters
2. Print intermediate values
3. Print what's being returned
4. Check if return statement exists

---

## Unit 6 Key Vocabulary

- **Algorithm:** Step-by-step procedure to solve a problem
- **Debugging:** Process of finding and fixing errors
- **Edge case:** Unusual or extreme input that might cause errors
- **Exception:** Runtime error in a Python program
- **Logic error:** Code runs but produces wrong answer
- **Runtime error:** Error that occurs while program is executing
- **Syntax error:** Violation of Python grammar rules
- **Test case:** Input, expected output, and description
- **Traceback:** Error message showing where and what error occurred
- **try/except:** Block that catches and handles exceptions

---
