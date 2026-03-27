# Unit 4: File I/O & Data Processing
> Learn to read, write, and process data from files. Master CSV, JSON, and exception handling for robust applications.

##  Unit Overview
- **Duration:** 9 days / 3 weeks
- **Key Concepts:** File I/O, text processing, CSV/JSON handling, exception handling, data validation, and data analysis
- **Big Idea:** Real-world programs work with external data; exception handling ensures reliability
- **TN Standard:** 9-12.CCI.4 — Use external data sources

##  Learning Targets
- I can read, write, and append files using Python's file operations
- I can process text files line-by-line
- I can read and write CSV files
- I can parse and create JSON data
- I can implement robust exception handling
- I can create custom exceptions
- I can validate and clean data
- I can perform basic data analysis on file data

---

# Day 1: File Reading & Writing
**Learning Target:** I can open, read, write, and close files safely using the with statement.

### Key Concepts
File operations: `open()`, `read()`, `write()`, `close()`

**File modes:**
- `'r'` — read (default)
- `'w'` — write (overwrites)
- `'a'` — append (add to end)
- `'r+'` — read and write

**Best practice:** Use `with` statement for automatic closing

### Code Examples
```python
# Reading a file
with open("data.txt", "r") as file:
    content = file.read()
    print(content)

# Reading line by line
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())

# Writing to a file
with open("output.txt", "w") as file:
    file.write("Line 1\n")
    file.write("Line 2\n")

# Appending to a file
with open("output.txt", "a") as file:
    file.write("Line 3\n")

# Reading all lines as list
with open("data.txt", "r") as file:
    lines = file.readlines()
```

### Guided Practice
Create a program that reads a file and counts lines/words.

### Practice Problems
**Problem 1 — Beginner:** Write a program that reads a file and prints its contents.

**Problem 2 — Intermediate:** Create a program that reads a file, counts words, and writes stats.

**Problem 3 — Challenge:** Create a file copy program that reads one file and writes to another.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
with open("input.txt", "r") as f:
    content = f.read()
    word_count = len(content.split())

with open("stats.txt", "w") as f:
    f.write(f"Words: {word_count}\n")
```
</details>

---

# Day 2: Text File Processing
**Learning Target:** I can process text files, parsing and transforming line-by-line data.

### Key Concepts
Text file processing: splitting, parsing, transforming data.

### Code Examples
```python
# Process each line
with open("names.txt", "r") as file:
    for line in file:
        name, age = line.strip().split(",")
        print(f"{name} is {age} years old")

# Filter and write
with open("input.txt", "r") as infile, open("output.txt", "w") as outfile:
    for line in infile:
        if len(line.strip()) > 0:  # Skip empty lines
            outfile.write(line.upper())

# Parse structured text
data = []
with open("data.txt", "r") as file:
    for line in file:
        parts = line.strip().split(":")
        data.append({"key": parts[0], "value": parts[1]})
```

### Guided Practice
Read a file with student names/grades, filter by passing grade, write to new file.

### Practice Problems
**Problem 1 — Beginner:** Read a file and count occurrences of a word.

**Problem 2 — Intermediate:** Read a CSV-like file and parse it.

**Problem 3 — Challenge:** Transform and clean messy data from a file.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
with open("file.txt", "r") as f:
    content = f.read()
    count = content.count("word")
```
</details>

---

# Day 3: CSV Files
**Learning Target:** I can read and write CSV files using the csv module.

### Key Concepts
CSV (Comma-Separated Values) format for tabular data.

`csv.reader()` and `csv.writer()` for simple access.
`csv.DictReader()` and `csv.DictWriter()` for dict-based access.

### Code Examples
```python
import csv

# Reading CSV
with open("students.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)

# Writing CSV
with open("output.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Age", "Grade"])
    writer.writerow(["Alice", 25, "A"])
    writer.writerow(["Bob", 23, "B"])

# Using DictReader (returns dicts)
with open("students.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row["Name"], row["Grade"])

# Using DictWriter
with open("output.csv", "w", newline="") as file:
    fieldnames = ["Name", "Age"]
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerow({"Name": "Zach", "Age": 17})
```

### Guided Practice
Read a CSV, filter rows, write filtered data.

### Practice Problems
**Problem 1 — Beginner:** Read a CSV and print all rows.

**Problem 2 — Intermediate:** Read CSV and calculate statistics.

**Problem 3 — Challenge:** Merge multiple CSV files.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
import csv
with open("data.csv", "r") as f:
    reader = csv.DictReader(f)
    grades = [float(row["Grade"]) for row in reader]
    avg = sum(grades) / len(grades)
```
</details>

---

# Day 4: JSON Files
**Learning Target:** I can parse and create JSON data using the json module.

### Key Concepts
JSON (JavaScript Object Notation) — lightweight data format.

`json.load()` / `json.loads()` — parse JSON
`json.dump()` / `json.dumps()` — create JSON

### Code Examples
```python
import json

# Reading JSON
with open("data.json", "r") as file:
    data = json.load(file)
    print(data["name"])

# Writing JSON
data = {
    "name": "Zach McCoy",
    "age": 17,
    "grades": [95, 88, 92]
}

with open("student.json", "w") as file:
    json.dump(data, file, indent=2)

# Parse JSON string
json_string = '{"name": "Alice", "age": 25}'
data = json.loads(json_string)

# Convert object to JSON string
data = {"name": "Bob"}
json_str = json.dumps(data)

# Handling nested JSON
with open("complex.json", "r") as file:
    data = json.load(file)
    for student in data["students"]:
        print(student["name"], student["grades"])
```

### Guided Practice
Read JSON, modify, and write back.

### Practice Problems
**Problem 1 — Beginner:** Read a JSON file and print a value.

**Problem 2 — Intermediate:** Convert a list of dicts to JSON file.

**Problem 3 — Challenge:** Merge multiple JSON files into one.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
import json
students = [
    {"name": "Alice", "grade": 90},
    {"name": "Bob", "grade": 85}
]
with open("students.json", "w") as f:
    json.dump(students, f, indent=2)
```
</details>

---

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

# Day 6: Custom Exceptions
**Learning Target:** I can create and use custom exception classes.

### Key Concepts
Create custom exceptions by inheriting from `Exception`.

Useful for application-specific errors.

### Code Examples
```python
# Define custom exception
class InsufficientFundsError(Exception):
    pass

class InvalidAgeError(Exception):
    def __init__(self, age):
        self.age = age
        super().__init__(f"Age {age} is invalid")

# Use custom exception
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def withdraw(self, amount):
        if amount > self.balance:
            raise InsufficientFundsError("Not enough money!")
        self.balance -= amount

account = BankAccount(100)
try:
    account.withdraw(200)
except InsufficientFundsError as e:
    print(f"Error: {e}")

# Catching custom exceptions
def validate_age(age):
    if age < 0 or age > 150:
        raise InvalidAgeError(age)

try:
    validate_age(-5)
except InvalidAgeError as e:
    print(f"Error: {e}")
```

### Guided Practice
Create custom exceptions for validation errors.

### Practice Problems
**Problem 1 — Beginner:** Create a simple custom exception class.

**Problem 2 — Intermediate:** Create exceptions for a Student class.

**Problem 3 — Challenge:** Create exception hierarchy with parent/child exceptions.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class CustomError(Exception):
    pass

# Problem 2
class InvalidGPAError(Exception):
    pass

class Student:
    def __init__(self, name, gpa):
        if gpa < 0 or gpa > 4.0:
            raise InvalidGPAError(f"GPA must be 0-4.0, got {gpa}")
        self.gpa = gpa
```
</details>

---

# Day 7: Data Cleaning
**Learning Target:** I can validate, clean, and normalize data from files.

### Key Concepts
Data cleaning: handling missing data, type conversion, normalization, removing duplicates.

### Code Examples
```python
# Remove duplicates
data = [1, 2, 2, 3, 3, 3]
cleaned = list(set(data))

# Handle missing data
data = {"name": "Alice", "age": None}
age = data.get("age", 0)  # Default to 0 if missing

# Validate types
def validate_number(value):
    try:
        return float(value)
    except ValueError:
        return None

# Normalize data
names = ["alice", "Bob", "  charlie  "]
normalized = [name.strip().lower() for name in names]

# Remove empty values
data = ["item1", "", "item2", None, "item3"]
cleaned = [x for x in data if x]

# Data validation class
class DataValidator:
    @staticmethod
    def validate_email(email):
        return "@" in email and "." in email

    @staticmethod
    def validate_age(age):
        try:
            return 0 <= int(age) <= 150
        except ValueError:
            return False
```

### Guided Practice
Clean messy CSV data.

### Practice Problems
**Problem 1 — Beginner:** Remove duplicates from a list.

**Problem 2 — Intermediate:** Clean and validate CSV data.

**Problem 3 — Challenge:** Create a data cleaning pipeline.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
data = [1, 1, 2, 3, 3]
cleaned = list(dict.fromkeys(data))  # Preserves order

# Problem 2
import csv
with open("messy.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        if row["age"]:  # Check not empty
            age = int(row["age"])
            if 0 <= age <= 150:
                print(row)
```
</details>

---

# Day 8: Data Analysis Basics
**Learning Target:** I can calculate statistics from file data.

### Key Concepts
Basic statistics: mean, median, mode, standard deviation, min, max, sorting.

### Code Examples
```python
def analyze_numbers(numbers):
    # Mean
    mean = sum(numbers) / len(numbers)

    # Median (middle value)
    sorted_nums = sorted(numbers)
    n = len(sorted_nums)
    median = sorted_nums[n // 2] if n % 2 else (sorted_nums[n//2 - 1] + sorted_nums[n//2]) / 2

    # Mode (most frequent)
    from collections import Counter
    mode = Counter(numbers).most_common(1)[0][0]

    # Min/Max
    min_val = min(numbers)
    max_val = max(numbers)

    # Range
    range_val = max_val - min_val

    return {"mean": mean, "median": median, "mode": mode, "min": min_val, "max": max_val, "range": range_val}

# Using with files
import csv
grades = []
with open("grades.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        grades.append(float(row["Grade"]))

stats = analyze_numbers(grades)
print(f"Average: {stats['mean']:.2f}")
print(f"Median: {stats['median']:.2f}")
```

### Guided Practice
Read CSV of student grades, calculate statistics.

### Practice Problems
**Problem 1 — Beginner:** Calculate mean of a list.

**Problem 2 — Intermediate:** Calculate mean, median, mode.

**Problem 3 — Challenge:** Create comprehensive statistics report from file data.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
numbers = [1, 2, 3, 4, 5]
mean = sum(numbers) / len(numbers)

# Problem 2 (shown above)
```
</details>

---

# Day 9: Project Day — Student Data Analyzer
**Learning Target:** I can build a complete data analysis program.

### Project Overview
Analyze student data from CSV files:
- Read student records (name, grade, GPA)
- Calculate class statistics
- Identify top/bottom performers
- Generate reports
- Handle errors gracefully

### Requirements
- Read CSV file with error handling
- Calculate mean, median, min, max
- Filter data by criteria
- Write results to output file
- Handle invalid/missing data

### Scaffold & Starter Code
```python
import csv
from statistics import mean, median

class StudentAnalyzer:
    def __init__(self, filename):
        self.filename = filename
        self.students = []
        self.load_data()

    def load_data(self):
        try:
            with open(self.filename, 'r') as f:
                reader = csv.DictReader(f)
                for row in reader:
                    try:
                        self.students.append({
                            'name': row['Name'],
                            'grade': float(row['Grade'])
                        })
                    except ValueError:
                        print(f"Skipping invalid grade for {row['Name']}")
        except FileNotFoundError:
            print(f"File {self.filename} not found!")

    def get_statistics(self):
        if not self.students:
            return None
        grades = [s['grade'] for s in self.students]
        return {
            'mean': mean(grades),
            'median': median(grades),
            'min': min(grades),
            'max': max(grades),
            'count': len(self.students)
        }

    def generate_report(self, output_file):
        stats = self.get_statistics()
        with open(output_file, 'w') as f:
            f.write("STUDENT ANALYSIS REPORT\n")
            f.write(f"Students: {stats['count']}\n")
            f.write(f"Average Grade: {stats['mean']:.2f}\n")
            f.write(f"Median Grade: {stats['median']:.2f}\n")

# Usage
analyzer = StudentAnalyzer("students.csv")
analyzer.generate_report("report.txt")
```

### Enhancement Ideas
- Letter grade distribution
- Student rankings
- Trend analysis over time
- Export to JSON/Excel
- Data visualization

---

# Unit Practice Bank

1. **Beginner:** Open and read a file.
2. **Beginner:** Write text to a file.
3. **Beginner:** Read and print each line of a file.
4. **Intermediate:** Read CSV and process rows.
5. **Intermediate:** Write CSV from data.
6. **Intermediate:** Handle FileNotFoundError.
7. **Intermediate:** Parse JSON file.
8. **Challenge:** Read CSV, filter, and write results.
9. **Challenge:** Create custom exceptions for validation.
10. **Challenge:** Build data cleaning pipeline.
11. **Challenge:** Generate statistics report from file.
12. **Challenge:** Merge multiple data files.
13. **Challenge:** Create interactive data analyzer.
14. **Challenge:** Build robust file processor with error handling.
15. **Challenge:** Process and visualize data from files.

---

# Common Mistakes & How to Fix Them
| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Forgetting to close file | Resource leak | Use `with` statement |
| Using 'w' mode when 'a' needed | Overwrites file | Choose correct mode |
| csv.writer with no newline='' | Extra blank lines | Use `newline=""` parameter |
| Catching all exceptions generically | Hides real errors | Catch specific exceptions |
| No try/except for file operations | Crashes on missing file | Always use exception handling |
| Assuming file format | Crashes on different format | Validate/handle variations |

---

# Unit Assessment Prep

**Review Questions:**

1. What are the three main file modes in Python?
2. Why use the `with` statement for files?
3. What's the difference between `read()` and `readlines()`?
4. How do you read a CSV file?
5. What's JSON used for?
6. Explain try/except/else/finally.
7. What are custom exceptions?
8. How do you calculate mean and median?
9. When should you use `DictReader` vs `reader`?
10. How do you handle missing data?

**Answers:**

1. `'r'` (read), `'w'` (write/overwrite), `'a'` (append)
2. It automatically closes the file, even if errors occur
3. `read()` returns entire string; `readlines()` returns list of lines
4. `csv.reader()` or `csv.DictReader()` from csv module
5. Lightweight format for storing/exchanging structured data
6. try runs code, except catches errors, else runs if no error, finally always runs
7. Custom classes inheriting from Exception for application-specific errors
8. Mean: sum/count; Median: middle value of sorted data
9. DictReader when you want dict access (column names); reader for list access
10. Use defaults, skip rows, validate before use

---

# Vocabulary & Quick Reference

**Key Terms:**
- **File mode:** How file is opened (r, w, a)
- **CSV:** Comma-separated values (tabular format)
- **JSON:** JavaScript Object Notation (structured text)
- **Exception:** Error that can be caught and handled
- **Validation:** Checking data is correct/safe
- **Normalization:** Converting data to standard format
- **Statistic:** Mathematical summary of data

**Key Syntax:**
```python
# File operations
with open("file.txt", "r") as f:
    data = f.read()

# CSV
import csv
reader = csv.DictReader(file)

# JSON
import json
data = json.load(file)

# Exception handling
try:
    # code
except SpecificError as e:
    # handle
finally:
    # cleanup
```
