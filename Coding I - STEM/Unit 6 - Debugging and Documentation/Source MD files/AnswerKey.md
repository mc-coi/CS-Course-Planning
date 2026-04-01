# Unit 6: Debugging and Documentation - Answer Key

---

## Problem 1: Classify Errors

### Solution
```python
# a) SYNTAX ERROR - missing colon
# for i in range(5)     # <- Missing colon at end
#     print(i)

# FIXED:
for i in range(5):
    print(i)

print()

# b) RUNTIME ERROR - division by zero
# x = 0
# print(10 / x)  # <- Crashes when executed

x = 1  # Fix by using non-zero
print(10 / x)

print()

# c) LOGIC ERROR - using = instead of +=
# total = 0
# for i in range(1, 6):
#     total = i   # <- Should be total += i

total = 0
for i in range(1, 6):
    total += i   # Now correctly sums

print(f"Sum 1-5: {total}")
```

### Expected Output
```
0
1
2
3
4

10.0

Sum 1-5: 15
```

### Common Mistakes
- Not distinguishing between the three error types
- Thinking syntax errors can be caught at runtime
- Not understanding that logic errors run without crashing

---

## Problem 2: Write Numbers to File

### Solution
```python
# Write numbers 1-20 to file, one per line
with open("numbers.txt", "w") as f:
    for i in range(1, 21):
        f.write(str(i) + "\n")

print("Successfully wrote 1-20 to numbers.txt")

# Verify by reading it back
with open("numbers.txt", "r") as f:
    content = f.read()
    print("\nFile contents:")
    print(content)
```

### Expected Output
```
Successfully wrote 1-20 to numbers.txt

File contents:
1
2
3
4
5
...
20
```

### Common Mistakes
- Forgetting to add "\n" for newlines
- Not converting integers to strings
- Using "a" (append) instead of "w" (write)
- Not closing the file (forgetting with statement)

---

## Problem 3: Read and Sum Numbers from File

### Solution
```python
# Read numbers.txt and sum all numbers
with open("numbers.txt", "r") as f:
    lines = f.readlines()

total = 0
for line in lines:
    number = int(line.strip())
    total += number

print(f"Sum of all numbers in numbers.txt: {total}")

# Alternative one-liner approach
with open("numbers.txt", "r") as f:
    total_alt = sum(int(line.strip()) for line in f)

print(f"Alternative method: {total_alt}")
```

### Expected Output
```
Sum of all numbers in numbers.txt: 210
Alternative method: 210
```

### Common Mistakes
- Not converting strings to integers before summing
- Not stripping whitespace/newlines from input
- Not opening the file before reading
- Not closing the file properly

---

## Problem 4: Try/Except for ValueError

### Solution
```python
# Get integer input with error handling
while True:
    try:
        user_input = input("Enter an integer: ")
        num = int(user_input)
        print(f"You entered: {num}")
        break
    except ValueError:
        print(f"Error: '{user_input}' is not a valid integer. Try again.")

# Alternative - more specific error message
print("\nAnother example:")
while True:
    try:
        age = int(input("Enter your age: "))
        if age < 0:
            print("Age cannot be negative")
            continue
        print(f"Your age: {age}")
        break
    except ValueError:
        print("Please enter a valid number")
```

### Expected Output
```
Enter an integer: abc
Error: 'abc' is not a valid integer. Try again.
Enter an integer: 42
You entered: 42

Another example:
Enter your age: 25
Your age: 25
```

### Common Mistakes
- Not catching the right exception type (ValueError)
- Not looping to ask again after error
- Not stripping or cleaning input
- Catching too broad Exception class

---

## Problem 5: Docstrings for Functions

### Solution
```python
def area_circle(r):
    """Calculate and return the area of a circle with radius r."""
    import math
    return math.pi * r ** 2

def is_leap_year(year):
    """Return True if year is a leap year, False otherwise."""
    return (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0)

def reverse_string(s):
    """Return the string s reversed."""
    return s[::-1]

# Test the functions with docstrings
print(area_circle.__doc__)
print(is_leap_year.__doc__)
print(reverse_string.__doc__)

# Use the functions
print(f"\nArea of circle (r=5): {area_circle(5):.2f}")
print(f"Is 2024 leap year: {is_leap_year(2024)}")
print(f"Reverse of 'hello': {reverse_string('hello')}")
```

### Expected Output
```
Calculate and return the area of a circle with radius r.
Return True if year is a leap year, False otherwise.
Return the string s reversed.

Area of circle (r=5): 78.54
Is 2024 leap year: True
Reverse of 'hello': olleh
```

### Common Mistakes
- Using comments instead of docstrings (# vs """)
- Not including a clear description of what function does
- Not documenting parameters or return values
- Using multi-line comments instead of docstrings

---

## Problem 6: Safe File Open with Error Handling

### Solution
```python
def safe_open(filename):
    """Return file contents as string, or None if file not found."""
    try:
        with open(filename, "r") as f:
            return f.read()
    except FileNotFoundError:
        return None

# Test the function
result = safe_open("numbers.txt")
if result is not None:
    print("File found! Contents:")
    print(result)
else:
    print("File not found")

# Test with non-existent file
result2 = safe_open("nonexistent.txt")
if result2 is None:
    print("\nFile 'nonexistent.txt' not found (as expected)")
```

### Expected Output
```
File found! Contents:
1
2
3
...
20

File 'nonexistent.txt' not found (as expected)
```

### Common Mistakes
- Not catching FileNotFoundError
- Not returning None or appropriate value on error
- Not using with statement for file handling
- Letting exception propagate instead of handling

---

## Problem 7: Append Timestamped Log Entry

### Solution
```python
from datetime import datetime

def append_to_log(filename, message):
    """Append a timestamped entry to a log file."""
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    log_entry = f"[{timestamp}] {message}\n"

    try:
        with open(filename, "a") as f:
            f.write(log_entry)
        print(f"Logged: {log_entry.strip()}")
    except IOError as e:
        print(f"Error writing to log: {e}")

# Test the function
append_to_log("app.log", "User logged in")
append_to_log("app.log", "User performed action X")
append_to_log("app.log", "User logged out")

# Display the log
print("\nLog file contents:")
try:
    with open("app.log", "r") as f:
        print(f.read())
except FileNotFoundError:
    print("Log file not found")
```

### Expected Output
```
Logged: [2024-03-15 14:30:22] User logged in
Logged: [2024-03-15 14:30:23] User performed action X
Logged: [2024-03-15 14:30:24] User logged out

Log file contents:
[2024-03-15 14:30:22] User logged in
[2024-03-15 14:30:23] User performed action X
[2024-03-15 14:30:24] User logged out
```

### Common Mistakes
- Not importing datetime
- Using wrong date format
- Not appending (using "w" instead of "a")
- Not handling file write errors

---

## Problem 8: Load CSV File

### Solution
```python
def load_csv(filename):
    """Read a 2-column CSV file and return list of (key, value) tuples."""
    result = []

    try:
        with open(filename, "r") as f:
            for line in f:
                line = line.strip()
                if line:  # Skip empty lines
                    parts = line.split(",")
                    if len(parts) >= 2:
                        key = parts[0].strip()
                        value = parts[1].strip()
                        result.append((key, value))
    except FileNotFoundError:
        print(f"Error: File '{filename}' not found")
        return []

    return result

# Create a sample CSV file
with open("config.csv", "w") as f:
    f.write("name,John Doe\n")
    f.write("age,30\n")
    f.write("city,New York\n")

# Test the function
data = load_csv("config.csv")
print("Loaded configuration:")
for key, value in data:
    print(f"  {key}: {value}")

# Test with non-existent file
data2 = load_csv("missing.csv")
```

### Expected Output
```
Loaded configuration:
  name: John Doe
  age: 30
  city: New York
Error: File 'missing.csv' not found
```

### Common Mistakes
- Not handling missing files
- Not stripping whitespace from values
- Not splitting on comma correctly
- Not skipping empty lines
- Not checking if line has enough columns

---

## Problem 9: Get Valid Input in Range

### Solution
```python
def get_valid_input(prompt, min_val, max_val):
    """Keep asking until user enters integer in given range."""
    while True:
        try:
            user_input = input(prompt)
            num = int(user_input)

            if min_val <= num <= max_val:
                return num
            else:
                print(f"Please enter a number between {min_val} and {max_val}")
        except ValueError:
            print("Invalid input. Please enter an integer.")

# Test the function
age = get_valid_input("Enter your age (0-150): ", 0, 150)
print(f"You entered: {age}")

score = get_valid_input("Enter test score (0-100): ", 0, 100)
print(f"Your score: {score}")
```

### Expected Output
```
Enter your age (0-150): abc
Invalid input. Please enter an integer.
Enter your age (0-150): 200
Please enter a number between 0 and 150
Enter your age (0-150): 25
You entered: 25
Enter test score (0-100): 85
Your score: 85
```

### Common Mistakes
- Not checking both boundaries (min and max)
- Using separate if statements instead of range check
- Not looping to ask again
- Not catching ValueError for invalid input

---

## Problem 10: Complete Docstring for Divide Function

### Solution
```python
def divide(a, b):
    """Divide a by b and return the result.

    Args:
        a (float): The dividend (numerator)
        b (float): The divisor (denominator)

    Returns:
        float: The result of a / b

    Raises:
        ZeroDivisionError: If b is zero

    Examples:
        >>> divide(10, 2)
        5.0
        >>> divide(7, 2)
        3.5
        >>> divide(5, 0)
        Traceback (most recent call last):
            ...
        ZeroDivisionError: b cannot be zero
    """
    if b == 0:
        raise ZeroDivisionError("b cannot be zero")
    return a / b

# Test the function
print(divide(10, 2))
print(divide(7, 2))

# Test error case
try:
    print(divide(5, 0))
except ZeroDivisionError as e:
    print(f"Error: {e}")
```

### Expected Output
```
5.0
3.5
Error: b cannot be zero
```

### Common Mistakes
- Not including all sections (Args, Returns, Raises, Examples)
- Missing parameter types and descriptions
- Not documenting raised exceptions
- Not showing example usage
- Incomplete docstring format

---

## Problem 11: Modular Contact Book

### Solution
```python
def load_contacts(filename):
    """Load contacts from file. Return dict of name -> phone."""
    contacts = {}
    try:
        with open(filename, "r") as f:
            for line in f:
                line = line.strip()
                if line and "," in line:
                    name, phone = line.split(",", 1)
                    contacts[name.strip()] = phone.strip()
    except FileNotFoundError:
        pass
    return contacts

def save_contacts(filename, contacts):
    """Save contacts dict to file."""
    try:
        with open(filename, "w") as f:
            for name, phone in contacts.items():
                f.write(f"{name},{phone}\n")
    except IOError as e:
        print(f"Error saving contacts: {e}")

def add_contact(contacts, name, phone):
    """Add a contact to the dictionary."""
    contacts[name] = phone
    return f"Added {name}"

def find_contact(contacts, name):
    """Find and return phone for a contact."""
    if name in contacts:
        return contacts[name]
    else:
        return f"Contact '{name}' not found"

def delete_contact(contacts, name):
    """Remove a contact from the dictionary."""
    if name in contacts:
        del contacts[name]
        return f"Deleted {name}"
    else:
        return f"Contact '{name}' not found"

def contact_menu(contacts, filename):
    """Menu for contact operations."""
    while True:
        print("\n1. Add  2. Find  3. Delete  4. List  5. Save & Exit")
        choice = input("Choose: ").strip()

        if choice == "1":
            name = input("Name: ")
            phone = input("Phone: ")
            print(add_contact(contacts, name, phone))
        elif choice == "2":
            name = input("Name: ")
            print(find_contact(contacts, name))
        elif choice == "3":
            name = input("Name: ")
            print(delete_contact(contacts, name))
        elif choice == "4":
            if contacts:
                for name, phone in contacts.items():
                    print(f"  {name}: {phone}")
            else:
                print("  No contacts")
        elif choice == "5":
            save_contacts(filename, contacts)
            print("Contacts saved. Goodbye!")
            break
        else:
            print("Invalid choice")

# Main program
filename = "contacts.txt"
contacts = load_contacts(filename)
contact_menu(contacts, filename)
```

### Expected Output
```
(Menu interface with options to add/find/delete/list contacts)
```

### Common Mistakes
- Not separating file I/O from business logic
- Not checking if file exists before loading
- Not persisting data to file
- Not validating input data

---

## Problem 12: Parse Config File

### Solution
```python
def parse_config(filename):
    """Parse INI-style config file (key=value) and return dict."""
    config = {}

    try:
        with open(filename, "r") as f:
            for line_num, line in enumerate(f, 1):
                line = line.strip()

                # Skip empty lines and comments
                if not line or line.startswith("#"):
                    continue

                # Parse key=value
                if "=" in line:
                    key, value = line.split("=", 1)
                    key = key.strip()
                    value = value.strip()

                    if key:  # Key must not be empty
                        config[key] = value
                else:
                    print(f"Warning: Line {line_num} malformed: {line}")

    except FileNotFoundError:
        print(f"Error: File '{filename}' not found")
    except IOError as e:
        print(f"Error reading file: {e}")

    return config

# Create sample config file
with open("app.ini", "w") as f:
    f.write("# Application Configuration\n")
    f.write("app_name=MyApp\n")
    f.write("version=1.0.0\n")
    f.write("debug=true\n")
    f.write("port=8080\n")

# Test the function
config = parse_config("app.ini")
print("Configuration loaded:")
for key, value in config.items():
    print(f"  {key} = {value}")

# Test with missing file
config2 = parse_config("missing.ini")
```

### Expected Output
```
Configuration loaded:
  app_name = MyApp
  version = 1.0.0
  debug = true
  port = 8080
Error: File 'missing.ini' not found
```

### Common Mistakes
- Not handling comments (lines starting with #)
- Not handling malformed lines gracefully
- Not stripping whitespace from keys and values
- Not checking if key is empty after stripping
- Crashing on file not found instead of handling it

---

## Problem 13: Retry Wrapper Function

### Solution
```python
import time

def retry(func, args, max_attempts=3, delay=1):
    """Call func(*args), retrying up to max_attempts on exception.

    Args:
        func: The function to call
        args: Tuple of arguments to pass to func
        max_attempts: Maximum number of attempts (default 3)
        delay: Delay in seconds between retries (default 1)

    Returns:
        Result of func(*args) if successful, None if all attempts fail
    """
    for attempt in range(1, max_attempts + 1):
        try:
            print(f"Attempt {attempt}/{max_attempts}...")
            result = func(*args)
            print(f"Success!")
            return result
        except Exception as e:
            print(f"  Error: {e}")
            if attempt < max_attempts:
                print(f"  Retrying in {delay} second(s)...")
                time.sleep(delay)
            else:
                print(f"  All {max_attempts} attempts failed")
    return None

# Example function that fails sometimes
call_count = 0

def unstable_api(x):
    """Simulates an API that fails intermittently."""
    global call_count
    call_count += 1
    if call_count <= 2:
        raise ConnectionError("Network error")
    return x * 2

# Test the retry function
result = retry(unstable_api, (5,), max_attempts=3, delay=0.5)
if result is not None:
    print(f"Result: {result}")
```

### Expected Output
```
Attempt 1/3...
  Error: Network error
  Retrying in 0.5 second(s)...
Attempt 2/3...
  Error: Network error
  Retrying in 0.5 second(s)...
Attempt 3/3...
Success!
Result: 10
```

### Common Mistakes
- Not implementing delay between retries
- Not tracking attempt count
- Not catching generic Exception
- Not returning None on failure
- Not providing feedback on each attempt

---

## Problem 14: Score Tracker with Persistence

### Solution
```python
def load_scores(filename):
    """Load scores from CSV file."""
    scores = []
    try:
        with open(filename, "r") as f:
            for line in f:
                try:
                    score = float(line.strip())
                    scores.append(score)
                except ValueError:
                    pass
    except FileNotFoundError:
        pass
    return scores

def save_scores(filename, scores):
    """Save scores to CSV file."""
    try:
        with open(filename, "w") as f:
            for score in scores:
                f.write(f"{score}\n")
    except IOError as e:
        print(f"Error saving scores: {e}")

def add_score(scores, score):
    """Add a score and return statistics."""
    scores.append(score)
    return f"Added {score}. Average: {sum(scores)/len(scores):.2f}"

def view_stats(scores):
    """Display score statistics."""
    if not scores:
        return "No scores recorded"
    return f"Count: {len(scores)}, Average: {sum(scores)/len(scores):.2f}, Min: {min(scores)}, Max: {max(scores)}"

def score_menu(scores, filename):
    """Interactive menu for score management."""
    while True:
        print("\n1. Add Score  2. View Stats  3. Save & Exit")
        choice = input("Choose: ").strip()

        if choice == "1":
            try:
                score = float(input("Enter score: "))
                print(add_score(scores, score))
            except ValueError:
                print("Invalid input")
        elif choice == "2":
            print(view_stats(scores))
        elif choice == "3":
            save_scores(filename, scores)
            print("Scores saved. Goodbye!")
            break
        else:
            print("Invalid choice")

# Main program
filename = "scores.csv"
scores = load_scores(filename)
score_menu(scores, filename)
```

### Expected Output
```
(Interactive menu allowing users to add scores and view statistics)
```

### Common Mistakes
- Not persisting data between runs
- Not handling file errors gracefully
- Not validating score input
- Not calculating statistics correctly

---

## Problem 15: Find Functions Without Docstrings

### Solution
```python
def scan_python_file(filename):
    """Scan a Python file and report functions missing docstrings."""
    missing_docstrings = []

    try:
        with open(filename, "r") as f:
            lines = f.readlines()

        i = 0
        while i < len(lines):
            line = lines[i].strip()

            # Look for 'def' statements
            if line.startswith("def "):
                # Extract function name
                func_name = line.split("(")[0].replace("def ", "")
                line_num = i + 1

                # Check next non-empty line for docstring
                i += 1
                found_docstring = False

                while i < len(lines):
                    next_line = lines[i].strip()
                    if next_line:  # Found non-empty line
                        if next_line.startswith('"""') or next_line.startswith("'''"):
                            found_docstring = True
                        break
                    i += 1

                if not found_docstring:
                    missing_docstrings.append((func_name, line_num))

            i += 1

    except FileNotFoundError:
        print(f"Error: File '{filename}' not found")
        return []

    return missing_docstrings

# Create a test file
test_code = '''
def function_with_docstring():
    """This function has a docstring."""
    pass

def function_without_docstring():
    x = 5
    return x

def another_documented():
    """Also documented."""
    return 42
'''

with open("test_code.py", "w") as f:
    f.write(test_code)

# Scan the file
missing = scan_python_file("test_code.py")

if missing:
    print("Functions missing docstrings:")
    for func_name, line_num in missing:
        print(f"  - {func_name} (line {line_num})")
else:
    print("All functions have docstrings!")
```

### Expected Output
```
Functions missing docstrings:
  - function_without_docstring (line 4)
```

### Common Mistakes
- Not finding "def" statements correctly
- Not looking at the line immediately after function definition
- Not handling both """ and ''' docstring markers
- Not skipping empty lines before checking for docstring
- Crashing on file not found

---
