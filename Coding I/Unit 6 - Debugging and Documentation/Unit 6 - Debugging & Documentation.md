# Unit 6: Debugging & Documentation
> Write clean, well-documented code and master bug-fixing techniques.

##  Unit Overview
- **Duration:** 6 days / 2 weeks (Days 43–48)
- **Key Concepts:** Error types, debugging strategies, file I/O, exception handling, docstrings, code documentation
- **Big Idea:** Professional code is correct, readable, well-documented, and handles problems gracefully
- **TN Standards Addressed:** Error handling, file I/O, testing, documentation, debugging strategies

## Learning Targets
- I can identify and classify errors as syntax, runtime, or logic errors
- I can use systematic debugging strategies to find and fix bugs
- I can read from and write to files using Python
- I can handle errors gracefully with `try`/`except`/`finally`
- I can catch specific exception types
- I can write clear docstrings and inline comments
- I can build complete programs combining all debugging and documentation skills

---

# Day 1: Types of Errors & Debugging Strategies

### Key Concepts

Every bug fits into one of three categories:

| Error Type | When It Appears | Description | Example |
|-----------|----------------|-------------|---------|
| **Syntax Error** | Before running | Code breaks the rules of Python | Missing colon, wrong indent |
| **Runtime Error** | While running | Legal code causes a crash | Dividing by 0, using undefined variable |
| **Logic Error** | While running (no crash) | Program runs but gives wrong answer | Off-by-one, wrong operator |

### Common Runtime Errors (Exceptions)

| Exception | Cause | Example |
|-----------|-------|---------|
| `NameError` | Using undefined variable | `print(x)` when x never set |
| `TypeError` | Wrong data type | `"hello" + 5` |
| `ValueError` | Right type, wrong value | `int("hello")` |
| `ZeroDivisionError` | Dividing by zero | `10 / 0` |
| `IndexError` | List index out of range | `mylist[99]` on a 3-element list |
| `FileNotFoundError` | File doesn't exist | `open("missing.txt")` |
| `AttributeError` | Method doesn't exist | `"hello".push("!")` |
| `KeyError` | Dict key doesn't exist | `mydict["bad_key"]` |

### Debugging Strategies

1. **Read the error message** — it tells you the line number and type
2. **Add print statements** — trace what values actually are
3. **Check assumptions** — is that variable really what you think it is?
4. **Rubber duck debugging** — explain your code out loud line by line
5. **Isolate the problem** — comment out sections to narrow it down
6. **Check edge cases** — what happens with 0, empty list, very large numbers?

### Code Examples

```python
# ── Syntax Error (Python won't even start) ─────────────────
# for i in range(10)     # ❌ SyntaxError: expected ':'
#     print(i)           # ❌ IndentationError

# ── Runtime Error (crashes during execution) ───────────────
x = int("hello")         # ❌ ValueError: invalid literal for int()
nums = [1, 2, 3]
print(nums[10])          # ❌ IndexError: list index out of range
print(10 / 0)            # ❌ ZeroDivisionError

# ── Logic Error (runs, but answer is wrong) ────────────────
# Goal: sum of 1 to 10
total = 0
for i in range(10):      # BUG: should be range(1, 11)
    total = i            # BUG: should be total += i
print(total)             # prints 9, not 55

# ── Fixed version ──────────────────────────────────────────
total = 0
for i in range(1, 11):   # 1 through 10 inclusive
    total += i            # accumulate
print(total)             # 55 ✅

# ── Debugging with print statements ───────────────────────
def calculate_bonus(sales, rate):
    print(f"DEBUG: sales={sales}, rate={rate}")   # trace inputs
    bonus = sales * rate
    print(f"DEBUG: bonus={bonus}")                 # trace output
    return bonus

result = calculate_bonus(5000, 0.1)
print(f"Bonus: ${result}")

# Remove DEBUG lines once problem is found
```

### Find & Fix the Bugs

```python
# Problem 1: Find all bugs
def average(numbers)
    total = 0
    for n in numbers
        total = total + n
    return total / len(numbers)

# Problem 2: Logic error — what's wrong?
def is_teenager(age):
    if age > 12 and age < 18:
        return True
    return False
# Test: is_teenager(18) should return False... does it?

# Problem 3: What error will this produce?
name = "Alice"
score = 95
print("Name: " + name + ", Score: " + score)
```

<details>
<summary>✅ Answers</summary>

```python
# Problem 1 fixes:
def average(numbers):            # added colon
    total = 0
    for n in numbers:            # added colon
        total = total + n
    return total / len(numbers)

# Problem 2: is actually correct — 18 is NOT a teenager
# is_teenager(18) → (18 > 12 and 18 < 18) → (True and False) → False ✅

# Problem 3: TypeError — can't concatenate str and int
# Fix:
print(f"Name: {name}, Score: {score}")
# OR
print("Name: " + name + ", Score: " + str(score))
```
</details>

---

# Day 2: Writing to Files

### Key Concepts
- **File I/O:** Input/Output — reading from and writing to files
- `open(filename, mode)` opens a file; always close it when done
- **`with` statement** automatically closes the file — always use this!
- File modes: `"w"` (write/overwrite), `"a"` (append), `"r"` (read), `"x"` (create new, fail if exists)
- `f.write(text)` writes a string — you must add `"\n"` yourself for newlines
- `f.writelines(list)` writes a list of strings

### File Modes Summary

| Mode | Behavior | File Exists? | File Missing? |
|------|---------|-------------|--------------|
| `"w"` | Write (overwrite) | Clears old content | Creates new |
| `"a"` | Append | Adds to end | Creates new |
| `"r"` | Read only | Opens file | Raises error |
| `"x"` | Exclusive create | Raises error | Creates new |

### Code Examples

```python
# ── Write to a file (creates or overwrites) ────────────────
with open("notes.txt", "w") as f:
    f.write("First line\n")
    f.write("Second line\n")
    f.write("Third line\n")

# ── Append to existing file ────────────────────────────────
with open("notes.txt", "a") as f:
    f.write("Fourth line\n")
    f.write("Fifth line\n")

# ── Write multiple lines at once ──────────────────────────
lines = ["Monday\n", "Tuesday\n", "Wednesday\n"]
with open("days.txt", "w") as f:
    f.writelines(lines)

# ── Write formatted data ───────────────────────────────────
students = [
    ("Alice", 92),
    ("Bob", 85),
    ("Carlos", 78),
]
with open("grades.csv", "w") as f:
    f.write("Name,Score\n")   # header row
    for name, score in students:
        f.write(f"{name},{score}\n")

# ── Write using a loop ─────────────────────────────────────
with open("countdown.txt", "w") as f:
    for i in range(10, 0, -1):
        f.write(f"{i}\n")
    f.write("Blastoff!\n")

# ── Check if file was created ──────────────────────────────
import os
if os.path.exists("notes.txt"):
    print(f"File created! Size: {os.path.getsize('notes.txt')} bytes")
```

### Practice Problems — Day 2

**Beginner:**
1. Write a program that creates `my_info.txt` with your name, grade, and favorite class on separate lines.
2. Write a function `save_numbers(filename, numbers)` that writes each number in the list to a separate line of the file.

**Intermediate:**

3. Write a function `append_log(filename, message)` that appends a message to a log file along with a timestamp. (Use Python's `datetime.datetime.now()` for the timestamp.)
4. Write a function `save_scores(filename, scores_dict)` where `scores_dict` maps student names to scores. Save in CSV format: `Name,Score`.

**Challenge:**

5. Write a `FileJournal` class — no wait, write a functional journal program: `start_journal(filename)` writes a header, `add_entry(filename, entry)` appends a dated entry, `view_journal(filename)` reads and prints all entries.

---

# Day 3: Reading from Files

### Key Concepts
- `f.read()` reads the entire file as one string
- `f.readline()` reads one line (including the `\n`)
- `f.readlines()` reads all lines as a list of strings
- Iterate with `for line in f:` — most memory-efficient way
- `.strip()` removes trailing whitespace/newline from a line
- Always handle `FileNotFoundError` when reading files you don't control

### Code Examples

```python
# ── Read entire file as one string ────────────────────────
with open("notes.txt", "r") as f:
    content = f.read()
print(content)          # prints everything including newlines

# ── Read all lines as a list ──────────────────────────────
with open("notes.txt", "r") as f:
    lines = f.readlines()   # e.g., ["First line\n", "Second line\n"]

for i, line in enumerate(lines):
    print(f"Line {i+1}: {line.strip()}")

# ── Read line by line (best for large files) ───────────────
with open("notes.txt", "r") as f:
    for line in f:
        print(line.strip())   # strip() removes the trailing \n

# ── Read and process CSV data ─────────────────────────────
scores = []
with open("grades.csv", "r") as f:
    next(f)   # skip the header line
    for line in f:
        parts = line.strip().split(",")
        name = parts[0]
        score = int(parts[1])
        scores.append((name, score))

for name, score in scores:
    print(f"{name}: {score}")

# ── Read into a dictionary ────────────────────────────────
student_grades = {}
with open("grades.csv", "r") as f:
    next(f)   # skip header
    for line in f:
        name, score = line.strip().split(",")
        student_grades[name] = int(score)

print(student_grades)

# ── Read a config-style file ──────────────────────────────
# config.txt:
# school=Westside High
# year=2024
# subject=Python

config = {}
with open("config.txt", "r") as f:
    for line in f:
        key, value = line.strip().split("=")
        config[key] = value

print(config["school"])
```

### Practice Problems — Day 3

**Beginner:**
1. Read the file you created in Day 44 (`my_info.txt`) and print each line with its line number.
2. Write `count_lines(filename)` that returns the number of lines in a file.

**Intermediate:**

3. Write `read_scores(filename)` that reads a CSV file of name,score pairs and returns a dictionary.
4. Write `find_in_file(filename, keyword)` that reads a file and returns a list of all lines containing the keyword.

**Challenge:**

5. Write a complete word frequency counter: read a text file, split into words (lowercase, strip punctuation), count how often each word appears, and write a new file with the results sorted from most to least frequent.

<details>
<summary>💡 Hint for #5</summary>

```python
import string

def count_word_frequency(input_file, output_file):
    freq = {}
    with open(input_file, "r") as f:
        for line in f:
            words = line.lower().split()
            for word in words:
                word = word.strip(string.punctuation)
                if word:
                    freq[word] = freq.get(word, 0) + 1

    sorted_words = sorted(freq.items(), key=lambda x: x[1], reverse=True)

    with open(output_file, "w") as f:
        for word, count in sorted_words:
            f.write(f"{word}: {count}\n")
```
</details>

---

# Day 4: try/except/finally — Exception Handling

### Key Concepts
- `try` block: code that might fail
- `except` block: what to do if that specific error occurs
- `else` block: runs only if no exception occurred
- `finally` block: always runs, whether or not there was an error
- Catch specific exceptions, not just bare `except`
- You can have multiple `except` blocks for different error types

### Structure

```
try:
    risky code
except SpecificError:
    handle that error
except AnotherError:
    handle this different error
else:
    runs only if no error happened
finally:
    always runs (cleanup)
```

### Code Examples

```python
# ── Basic try/except ──────────────────────────────────────
try:
    number = int(input("Enter a number: "))
    result = 100 / number
    print(f"100 / {number} = {result}")
except ValueError:
    print("That's not a valid number!")
except ZeroDivisionError:
    print("Can't divide by zero!")

# ── else and finally ──────────────────────────────────────
try:
    x = int(input("Enter a number: "))
    y = int(input("Enter another: "))
    result = x / y
except ValueError:
    print("Not a number!")
except ZeroDivisionError:
    print("Can't divide by zero!")
else:
    print(f"Result: {result}")     # only if no exceptions
finally:
    print("Calculation attempt complete.")  # always runs

# ── Handling FileNotFoundError ────────────────────────────
def read_file_safely(filename):
    try:
        with open(filename, "r") as f:
            return f.read()
    except FileNotFoundError:
        print(f"Error: '{filename}' not found.")
        return None

content = read_file_safely("data.txt")
if content:
    print(content)

# ── Input validation with try/except ─────────────────────
def get_valid_integer(prompt):
    while True:
        try:
            return int(input(prompt))
        except ValueError:
            print("Please enter a whole number.")

age = get_valid_integer("Enter your age: ")
print(f"Your age: {age}")

# ── Multiple exceptions in one block ─────────────────────
def safe_divide(a, b):
    try:
        return a / b
    except (ZeroDivisionError, TypeError) as e:
        print(f"Error: {e}")
        return None

print(safe_divide(10, 2))     # 5.0
print(safe_divide(10, 0))     # Error: division by zero
print(safe_divide("10", 2))   # Error: unsupported operand type(s)

# ── Getting error details ─────────────────────────────────
try:
    items = [1, 2, 3]
    print(items[10])
except IndexError as e:
    print(f"Index error: {e}")         # list index out of range
    print(f"Error type: {type(e).__name__}")  # IndexError

# ── Raising your own exceptions ───────────────────────────
def set_age(age):
    if age < 0 or age > 150:
        raise ValueError(f"Age {age} is not realistic (must be 0–150)")
    return age

try:
    set_age(-5)
except ValueError as e:
    print(f"Invalid age: {e}")
```

### Practice Problems — Day 4

**Beginner:**
1. Write a program that asks for two numbers and divides them. Use `try/except` to handle both `ValueError` (not a number) and `ZeroDivisionError`.
2. Wrap `open("missing.txt")` in a `try/except` block that prints a friendly message if the file doesn't exist.

**Intermediate:**

3. Write `get_float(prompt)` that keeps asking until the user enters a valid decimal number.
4. Write `safe_list_get(lst, index, default=None)` that returns `lst[index]` or `default` if the index is out of range.

**Challenge:**

5. Write a `safe_calculator()` program that:
   - Accepts two numbers and an operator (+, -, *, /)
   - Uses `try/except` to handle invalid number input, division by zero, and invalid operators
   - Loops until the user types "quit"
   - Logs each successful calculation to `calc_history.txt`

<details>
<summary>✅ Answer for #5 (partial)</summary>

```python
def safe_calculator():
    log_file = "calc_history.txt"
    print("Calculator — type 'quit' to exit")

    while True:
        try:
            entry = input("\nExpression (e.g. 10 + 5): ").strip()
            if entry.lower() == "quit":
                break

            parts = entry.split()
            if len(parts) != 3:
                raise ValueError("Format must be: number operator number")

            a = float(parts[0])
            op = parts[1]
            b = float(parts[2])

            if op == "+": result = a + b
            elif op == "-": result = a - b
            elif op == "*": result = a * b
            elif op == "/":
                if b == 0:
                    raise ZeroDivisionError("Cannot divide by zero")
                result = a / b
            else:
                raise ValueError(f"Unknown operator: {op}")

            output = f"{a} {op} {b} = {result}"
            print(output)
            with open(log_file, "a") as f:
                f.write(output + "\n")

        except ValueError as e:
            print(f"Input error: {e}")
        except ZeroDivisionError as e:
            print(f"Math error: {e}")
```
</details>

---

# Day 5: Documentation — Comments & Docstrings

### Key Concepts
- **Inline comments (`#`):** Short notes explaining *why* something is done
- **Docstrings (`"""..."""`):** Multi-line documentation for functions, classes, and modules
- Docstrings appear right after the `def` line and describe what the function does
- Docstrings are accessible at runtime: `help(my_function)` or `my_function.__doc__`
- Good comments explain *why*, not *what* — the code already shows what

### When to Comment vs. When Not To

| Comment This | Don't Comment This |
|-------------|-------------------|
| Complex algorithm choices | `x = x + 1  # add 1 to x` (obvious) |
| Business rules / magic numbers | `for i in range(10):  # loop 10 times` |
| Workarounds or known limitations | `name = "Alice"  # set name to Alice` |
| Why a particular approach was chosen | Self-explanatory variable names |

### Docstring Formats

```python
# ── Simple one-liner docstring ─────────────────────────────
def double(n):
    """Return n multiplied by 2."""
    return n * 2

# ── Multi-line (Google style) ─────────────────────────────
def calculate_grade(score):
    """Convert a numeric score to a letter grade.

    Args:
        score (int): Numeric score from 0 to 100.

    Returns:
        str: Letter grade ('A', 'B', 'C', 'D', or 'F').

    Raises:
        ValueError: If score is outside the 0–100 range.

    Examples:
        >>> calculate_grade(92)
        'A'
        >>> calculate_grade(75)
        'C'
    """
    if not 0 <= score <= 100:
        raise ValueError(f"Score {score} out of valid range (0-100)")
    if score >= 90: return "A"
    if score >= 80: return "B"
    if score >= 70: return "C"
    if score >= 60: return "D"
    return "F"

# ── Access docstrings at runtime ──────────────────────────
print(calculate_grade.__doc__)   # prints the docstring
help(calculate_grade)             # formatted help output
```

### Code Examples — Full Documentation

```python
"""
student_tracker.py
Module for tracking student grades and generating reports.
Author: [Your Name]
Date: [Date]
"""

# Constants — these numbers have special meaning
PASSING_SCORE = 70       # school policy: 70 is passing
MAX_SCORE = 100          # all scores out of 100
HONOR_ROLL_GPA = 3.5     # minimum GPA for honor roll

def get_letter_grade(score):
    """Convert a numeric score (0-100) to a letter grade.

    Args:
        score (float): The numeric score.

    Returns:
        str: Letter grade A through F.
    """
    if score >= 90: return "A"
    if score >= 80: return "B"
    if score >= 70: return "C"
    if score >= 60: return "D"
    return "F"

def is_passing(score):
    """Check if a score meets the passing threshold.

    Args:
        score (float): The score to check.

    Returns:
        bool: True if passing (>= 70), False otherwise.
    """
    return score >= PASSING_SCORE

def class_average(scores):
    """Calculate the average of a list of scores.

    Args:
        scores (list of float): Non-empty list of numeric scores.

    Returns:
        float: The arithmetic mean of the scores.
        Returns 0.0 if the list is empty.
    """
    if not scores:
        return 0.0
    return sum(scores) / len(scores)

def generate_report(student_name, scores):
    """Print a formatted grade report for a student.

    Args:
        student_name (str): The student's full name.
        scores (list of float): List of scores for the semester.
    """
    avg = class_average(scores)
    grade = get_letter_grade(avg)
    status = "PASSING" if is_passing(avg) else "FAILING"

    # Build header — same width regardless of name length
    print("=" * 40)
    print(f"  Grade Report: {student_name}")
    print("=" * 40)
    print(f"  Scores:  {scores}")
    print(f"  Average: {avg:.1f}")
    print(f"  Grade:   {grade}")
    print(f"  Status:  {status}")
    print("=" * 40)
```

### Practice Problems — Day 5

**Beginner:**
1. Add a docstring to each of these functions (write them yourself, then add docs):
   - `fahrenheit_to_celsius(f)` — converts temperature
   - `is_palindrome(text)` — checks if string reads same backwards
2. Add meaningful inline comments to a bubble sort algorithm.

**Intermediate:**

3. Write `validate_password(password)` with a full docstring including Args, Returns, Raises, and at least 3 inline comments explaining the logic.
4. Take a poorly commented program and improve it: add module-level docstring, function docstrings, and fix any confusing comments.

**Challenge:**

5. Write a fully documented `todo_list` module with functions: `create_list()`, `add_item(lst, task)`, `complete_item(lst, index)`, `remove_item(lst, index)`, `show_list(lst)`. Every function must have a complete docstring.

---

# Day 6: Unit 6 Project — Data Analyzer

### Project Description
Build a modular data analysis program that reads scores from a file, processes them, and produces a report. This project combines file I/O, error handling, functions, and documentation.

### Requirements
1. **Read data from a file** — handle the case where the file doesn't exist
2. **Analyze the data** — calculate stats (average, highest, lowest, passing count)
3. **Categorize results** — assign letter grades
4. **Write a report** — save results to a new file
5. **Handle errors** — use `try/except` for file operations and data conversion
6. **Documentation** — every function must have a docstring

### Starter Template

```python
"""
data_analyzer.py
Reads student score data from a CSV file, analyzes it,
and writes a summary report.
"""

def load_scores(filename):
    """Read student scores from a CSV file.

    Expected format: Name,Score (one per line, with header)

    Args:
        filename (str): Path to the CSV file.

    Returns:
        list of tuples: [(name, score), ...] or empty list on failure.
    """
    students = []
    try:
        with open(filename, "r") as f:
            next(f)  # skip header line
            for line in f:
                parts = line.strip().split(",")
                if len(parts) == 2:
                    name = parts[0]
                    score = float(parts[1])
                    students.append((name, score))
    except FileNotFoundError:
        print(f"Error: '{filename}' not found.")
    except ValueError as e:
        print(f"Error parsing file: {e}")
    return students

def calculate_stats(students):
    """Calculate summary statistics for a list of students.

    Args:
        students (list of tuples): [(name, score), ...]

    Returns:
        dict: Keys: average, highest, lowest, passing_count, total
    """
    if not students:
        return {}

    scores = [s for _, s in students]
    passing = sum(1 for s in scores if s >= 70)

    return {
        "average": sum(scores) / len(scores),
        "highest": max(scores),
        "lowest": min(scores),
        "passing_count": passing,
        "total": len(scores)
    }

def get_letter_grade(score):
    """Convert score to letter grade."""
    if score >= 90: return "A"
    if score >= 80: return "B"
    if score >= 70: return "C"
    if score >= 60: return "D"
    return "F"

def write_report(filename, students, stats):
    """Write a formatted grade report to a file.

    Args:
        filename (str): Output file path.
        students (list of tuples): [(name, score), ...]
        stats (dict): Summary statistics from calculate_stats().
    """
    try:
        with open(filename, "w") as f:
            f.write("=" * 45 + "\n")
            f.write("          STUDENT GRADE REPORT\n")
            f.write("=" * 45 + "\n\n")

            for name, score in sorted(students, key=lambda x: x[1], reverse=True):
                grade = get_letter_grade(score)
                f.write(f"  {name:<20} {score:>5.1f}  ({grade})\n")

            f.write("\n" + "-" * 45 + "\n")
            f.write(f"  Total students:  {stats['total']}\n")
            f.write(f"  Class average:   {stats['average']:.1f}\n")
            f.write(f"  Highest score:   {stats['highest']}\n")
            f.write(f"  Lowest score:    {stats['lowest']}\n")
            f.write(f"  Passing (>=70):  {stats['passing_count']}/{stats['total']}\n")
            f.write("=" * 45 + "\n")

        print(f"Report saved to '{filename}'")
    except IOError as e:
        print(f"Error writing report: {e}")

def main():
    """Run the data analyzer program."""
    input_file = "scores.csv"
    output_file = "grade_report.txt"

    print(f"Loading scores from '{input_file}'...")
    students = load_scores(input_file)

    if not students:
        print("No data to analyze.")
        return

    stats = calculate_stats(students)
    print(f"Analyzed {stats['total']} students.")

    write_report(output_file, students, stats)

main()
```

### Evaluation Checklist
- [ ] Reads data from file using `with open()`
- [ ] Handles `FileNotFoundError` with `try/except`
- [ ] Handles invalid data with `try/except`
- [ ] At least 4 functions, each with a docstring
- [ ] Writes results to an output file
- [ ] Calculates at least 3 statistics
- [ ] Main function orchestrates everything
- [ ] Program runs without crashing on valid and invalid input

---

## Unit 6 Practice Bank (15 Problems)

### Tier 1 — Beginner

**P1.** Label each error as Syntax, Runtime, or Logic:
```python
# a)
for i in range(5)
    print(i)

# b)
x = 0
print(10 / x)

# c)
total = 0
for i in range(1, 6):
    total = i   # supposed to sum 1+2+3+4+5
```

**P2.** Write a program that writes the numbers 1–20 to `numbers.txt`, one per line.

**P3.** Write a program that reads `numbers.txt` and prints the sum of all numbers.

**P4.** Add a `try/except` block to handle `ValueError` when converting user input to `int`.

**P5.** Write a one-line docstring for each: `area_circle(r)`, `is_leap_year(year)`, `reverse_string(s)`.

### Tier 2 — Intermediate

**P6.** Write `safe_open(filename)` that returns the file contents as a string, or `None` if the file doesn't exist. Use `try/except`.

<details>
<summary>✅ Answer for P6</summary>

```python
def safe_open(filename):
    """Return file contents or None if file not found."""
    try:
        with open(filename, "r") as f:
            return f.read()
    except FileNotFoundError:
        return None
```
</details>

**P7.** Write `append_to_log(filename, message)` that appends a timestamped entry:
`[2024-03-15 10:30:22] User logged in`

**P8.** Write `load_csv(filename)` that reads a 2-column CSV file and returns a list of `(key, value)` tuples.

**P9.** Write `get_valid_input(prompt, min_val, max_val)` that keeps asking until the user enters an integer in the given range.

**P10.** Add complete docstrings (Args, Returns, Raises, Examples) to:
```python
def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("b cannot be zero")
    return a / b
```

### Tier 3 — Challenge

**P11.** Write a modular contact book: `load_contacts(file)`, `save_contacts(file, contacts)`, `add_contact(contacts, name, phone)`, `find_contact(contacts, name)`, `delete_contact(contacts, name)`. All data persists to file between runs.

**P12.** Write `parse_config(filename)` that reads a `.ini`-style config file (lines like `key=value`) and returns a dictionary. Handle missing file, malformed lines, and empty values gracefully.

**P13.** Write a fully documented `retry` wrapper: `retry(func, args, max_attempts=3, delay=1)` that calls `func(*args)`, catching exceptions, and retries up to `max_attempts` times before giving up.

**P14.** Build a modular score tracker that: loads scores from CSV on startup, lets user add/remove/edit scores, shows stats, and saves back to CSV on exit — all with complete docstrings and error handling.

**P15.** Write a program that scans a Python `.py` file and reports any functions that are missing docstrings. Read the file line by line, detect `def` lines, and check if the next non-empty line starts with `"""`.

---

## Common Mistakes

| Mistake | What Goes Wrong | Fix |
|---------|----------------|-----|
| Not using `with` statement | File may not close properly | Always `with open() as f:` |
| Forgetting `\n` in `f.write()` | All text runs together | `f.write("line\n")` — add newline |
| Bare `except:` clause | Catches ALL errors, hides bugs | `except ValueError:` — be specific |
| Opening file without `try/except` | Crashes if file missing | Wrap in `try/except FileNotFoundError` |
| Forgetting `.strip()` on read | Extra `\n` in each string | `line.strip()` removes whitespace |
| Reading closed file | `ValueError` | Stay inside the `with` block |
| Writing without newlines | One long line in file | `f.write(text + "\n")` |
| Over-commenting obvious code | Clutters code | Comment the *why*, not the *what* |
| Missing docstring | Functions undocumented | Add `"""description"""` after `def` |
| Catching then ignoring errors | Silent failures | At minimum, `print(f"Error: {e}")` |

---

## Assessment Prep — Q&A

**Q1: What are the three types of errors in Python?**
Syntax errors (code breaks Python's rules — won't run), runtime errors (valid code crashes during execution — e.g., `ZeroDivisionError`), and logic errors (code runs but produces wrong answers).

**Q2: What is the purpose of the `finally` block?**
The `finally` block always runs regardless of whether an exception occurred. It's used for cleanup — closing files, releasing resources, printing a completion message.

**Q3: What's wrong with `except:`?**
A bare `except:` catches every possible exception, including keyboard interrupts and system exits. This can hide real bugs and make debugging impossible. Always specify the exception type: `except ValueError:`.

**Q4: What are the differences between file modes `"w"`, `"a"`, and `"r"`?**
`"w"` writes/overwrites the file (erases existing content). `"a"` appends to the end. `"r"` reads the file (error if it doesn't exist).

**Q5: Why do we use `with open() as f:` instead of just `open()`?**
The `with` statement automatically closes the file when the block ends — even if an exception occurs. Without it, you must manually call `f.close()` and remember to do so even after errors.

**Q6: What is a docstring and how is it different from a comment?**
A docstring is a string literal (using `"""..."""`) placed immediately after a `def` statement. It becomes part of the function and is accessible via `help()` and `func.__doc__`. A regular comment (`#`) is discarded by Python and can't be accessed programmatically.

**Q7: What does `.strip()` do when reading file lines?**
It removes leading and trailing whitespace, including the `\n` newline character at the end of each line. Without it, lines would include the invisible newline.

**Q8: What is the `else` clause in a `try/except` block?**
The `else` block runs only if the `try` block completed without raising any exceptions. It separates "success" code from "error" code.

**Q9: How do you raise your own exception?**
Use the `raise` keyword: `raise ValueError("message here")`. This allows you to enforce rules in your functions.

**Q10: What good comments look like vs. bad:**
Bad: `x += 1  # add 1 to x` (states the obvious)
Good: `attempts += 1  # track login attempts for lockout logic` (explains why)

---

## Vocabulary & Quick Reference

| Term | Definition |
|------|-----------|
| **Syntax Error** | Code violates Python's rules; won't even start |
| **Runtime Error** | Code crashes while running; also called an Exception |
| **Logic Error** | Code runs but produces incorrect results |
| **Exception** | An error that occurs during program execution |
| **`try`** | Block of code that might raise an exception |
| **`except`** | Block that handles a specific exception |
| **`else`** | Block that runs if `try` had no exceptions |
| **`finally`** | Block that always runs (cleanup) |
| **`raise`** | Manually trigger an exception |
| **File I/O** | Input/Output — reading from and writing to files |
| **`open()`** | Built-in function to open a file |
| **`with` statement** | Context manager that auto-closes files |
| **`.read()`** | Read entire file as a string |
| **`.readlines()`** | Read all lines as a list |
| **`.write()`** | Write a string to a file |
| **`.strip()`** | Remove leading/trailing whitespace and newlines |
| **Docstring** | String documentation placed at start of a function |
| **Inline comment** | `#` note explaining code; should say *why* |
| **`__doc__`** | Attribute holding a function's docstring |

### Exception Quick Reference

```python
try:
    result = risky_operation()
except ValueError as e:
    print(f"Bad value: {e}")
except (TypeError, AttributeError) as e:
    print(f"Type issue: {e}")
except FileNotFoundError:
    print("File not found!")
except Exception as e:
    print(f"Unexpected error: {e}")   # fallback
else:
    print("Success!")                  # only if no exception
finally:
    print("Done.")                     # always runs
```

### File I/O Quick Reference

```python
# Write
with open("file.txt", "w") as f:
    f.write("line 1\n")

# Append
with open("file.txt", "a") as f:
    f.write("new line\n")

# Read all
with open("file.txt", "r") as f:
    content = f.read()

# Read line by line
with open("file.txt", "r") as f:
    for line in f:
        clean = line.strip()
```
