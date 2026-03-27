# Unit 7: Capstone Reference Guide
> Quick reminders and code templates for concepts from Units 1–6. Use this when you're building your capstone project.

---

## Table of Contents
1. [OOP: Class Template](#oop-class-template)
2. [File I/O: Reading and Writing](#file-io-reading-and-writing)
3. [APIs: HTTP Requests](#apis-http-requests)
4. [Sorting & Searching](#sorting--searching)
5. [Exception Handling](#exception-handling)
6. [Visualization: Matplotlib](#visualization-matplotlib)
7. [Common Patterns](#common-patterns)

---

## OOP: Class Template

**From Unit 2**

Use this template for any class in your capstone:

```python
class ClassName:
    """Brief description of what this class represents."""

    def __init__(self, param1, param2):
        """Initialize the object.

        Args:
            param1 (type): Description
            param2 (type): Description
        """
        self.param1 = param1
        self.param2 = param2

    def method_name(self, arg):
        """Describe what this method does.

        Args:
            arg (type): Description

        Returns:
            type: Description of return value
        """
        # Implementation
        return result

    def __str__(self):
        """Return a human-readable string representation."""
        return f"{self.param1}, {self.param2}"

    def __repr__(self):
        """Return a developer-friendly string representation."""
        return f"ClassName(param1={self.param1}, param2={self.param2})"
```

**Quick Reminders:**
- `__init__` runs when you create an object: `obj = ClassName(val1, val2)`
- Use `self.attribute` to store data on the object
- Use `def method(self):` for instance methods
- Docstrings go right after `def`
- `__str__` is for users; `__repr__` is for developers

**Example:**
```python
class Student:
    """Represents a student record."""

    def __init__(self, name, student_id, gpa):
        self.name = name
        self.student_id = student_id
        self.gpa = gpa

    def add_course(self, course):
        """Add a course to this student's enrollment."""
        # Implementation
        pass

    def __str__(self):
        return f"{self.name} (ID: {self.student_id}, GPA: {self.gpa})"
```

---

## File I/O: Reading and Writing

**From Unit 4**

### Reading Files

**Read entire file:**
```python
with open("filename.txt") as f:
    content = f.read()  # Entire file as one string
    print(content)
```

**Read line by line:**
```python
with open("filename.txt") as f:
    for line in f:
        line = line.strip()  # Remove trailing newline
        print(line)
```

**Read into a list:**
```python
with open("filename.txt") as f:
    lines = f.readlines()  # List of lines
    for line in lines:
        print(line.strip())
```

### Writing Files

**Write text:**
```python
with open("filename.txt", "w") as f:
    f.write("Hello\n")
    f.write("World\n")
```

**Append to file:**
```python
with open("filename.txt", "a") as f:
    f.write("New line\n")
```

### CSV Files

**Read CSV:**
```python
import csv

with open("data.csv") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)  # row is a list

# Or read into list of dicts (header row required):
with open("data.csv") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row)  # row is a dict
```

**Write CSV:**
```python
import csv

data = [
    ["Name", "Age", "City"],
    ["Alice", 20, "NYC"],
    ["Bob", 21, "LA"],
]

with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f)
    for row in data:
        writer.writerow(row)
```

### JSON Files

**Read JSON:**
```python
import json

with open("data.json") as f:
    data = json.load(f)  # Parse JSON into dict/list
    print(data)
```

**Write JSON:**
```python
import json

data = {"name": "Alice", "age": 20, "courses": ["Math", "Physics"]}

with open("output.json", "w") as f:
    json.dump(data, f, indent=2)  # indent=2 makes it readable
```

**Convert objects to JSON-compatible format:**
```python
# Problem: Can't directly serialize custom objects
data = [Student("Alice", 100, 3.8), ...]
json.dump(data, f)  # ERROR!

# Solution 1: Convert to dict manually
students_data = [
    {"name": s.name, "id": s.student_id, "gpa": s.gpa}
    for s in students
]
json.dump(students_data, f)

# Solution 2: Use object's __dict__
students_data = [s.__dict__ for s in students]
json.dump(students_data, f)

# Solution 3: Implement to_dict() method
class Student:
    def to_dict(self):
        return {"name": self.name, "id": self.student_id, "gpa": self.gpa}

students_data = [s.to_dict() for s in students]
json.dump(students_data, f)
```

---

## APIs: HTTP Requests

**From Unit 4 / Optional in Capstone**

### Making API Requests

```python
import requests
import json

# Basic GET request
url = "https://api.example.com/data"
response = requests.get(url)
print(response.status_code)  # 200 = success, 404 = not found, 500 = error

# Parse JSON response
data = response.json()
print(data)

# With parameters
params = {"city": "NYC", "limit": 10}
response = requests.get(url, params=params)
data = response.json()
```

### Error Handling for APIs

```python
import requests

try:
    response = requests.get("https://api.example.com/data", timeout=5)
    response.raise_for_status()  # Raise error if status >= 400
    data = response.json()
except requests.exceptions.ConnectionError:
    print("No internet connection")
    data = None
except requests.exceptions.Timeout:
    print("Request timed out")
    data = None
except requests.exceptions.HTTPError as e:
    print(f"HTTP error: {e}")
    data = None
except json.JSONDecodeError:
    print("Invalid JSON response")
    data = None
```

### Common API Examples

**Weather API (OpenWeatherMap):**
```python
import requests

api_key = "YOUR_API_KEY"
city = "London"
url = f"https://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"

response = requests.get(url)
data = response.json()
print(f"Temperature: {data['main']['temp']}°C")
print(f"Condition: {data['weather'][0]['main']}")
```

**News API (NewsAPI.org):**
```python
import requests

api_key = "YOUR_API_KEY"
url = "https://newsapi.org/v2/top-headlines"
params = {"country": "us", "apiKey": api_key}

response = requests.get(url, params=params)
articles = response.json()["articles"]

for article in articles[:5]:
    print(article["title"])
    print(article["description"])
    print()
```

---

## Sorting & Searching

**From Unit 6**

### Sorting

**Sort list of numbers:**
```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
sorted_nums = sorted(numbers)
print(sorted_nums)  # [1, 1, 2, 3, 4, 5, 6, 9]

# Reverse order
sorted_nums = sorted(numbers, reverse=True)
print(sorted_nums)  # [9, 6, 5, 4, 3, 2, 1, 1]
```

**Sort list of objects by attribute:**
```python
students = [
    Student("Alice", 100, 3.8),
    Student("Bob", 101, 3.5),
    Student("Carol", 102, 3.9),
]

# Sort by GPA (highest first)
sorted_students = sorted(students, key=lambda s: s.gpa, reverse=True)
for s in sorted_students:
    print(f"{s.name}: {s.gpa}")

# Sort by name
sorted_students = sorted(students, key=lambda s: s.name)

# Sort by multiple attributes (name first, then GPA)
sorted_students = sorted(students, key=lambda s: (s.name, -s.gpa))
```

**Sort dictionaries:**
```python
data = [
    {"name": "Alice", "age": 20},
    {"name": "Bob", "age": 19},
]

# Sort by age
sorted_data = sorted(data, key=lambda d: d["age"])

# Sort by name
sorted_data = sorted(data, key=lambda d: d["name"])
```

### Searching

**Linear search (works for any list):**
```python
def linear_search(items, target):
    """Return index of target, or -1 if not found."""
    for i, item in enumerate(items):
        if item == target:
            return i
    return -1

index = linear_search([1, 3, 5, 7], 5)
print(index)  # 2
```

**Search in list of objects:**
```python
students = [...]

# Find by name (partial match)
def search_by_name(students, name):
    """Return list of students matching the name."""
    return [s for s in students if name.lower() in s.name.lower()]

results = search_by_name(students, "alice")
for s in results:
    print(s)

# Find by ID
def search_by_id(students, student_id):
    """Return student with matching ID, or None."""
    for s in students:
        if s.student_id == student_id:
            return s
    return None

alice = search_by_id(students, 100)
```

**Using `in` operator:**
```python
students = [...]
names = [s.name for s in students]

if "Alice" in names:
    print("Alice is a student")

# More efficient for large lists: convert to set
name_set = {s.name for s in students}
if "Alice" in name_set:
    print("Alice is a student")
```

---

## Exception Handling

**From Unit 5**

### Basic Try-Except

```python
try:
    # Code that might fail
    value = int(input("Enter a number: "))
except ValueError:
    # Code to run if error occurs
    print("Invalid number")
```

### Multiple Exceptions

```python
try:
    with open("data.json") as f:
        data = json.load(f)
except FileNotFoundError:
    print("File not found")
    data = {}
except json.JSONDecodeError:
    print("Invalid JSON format")
    data = {}
```

### Exception with Details

```python
try:
    value = float(input("GPA: "))
except ValueError as e:
    print(f"Invalid input: {e}")
```

### Catch Everything (Not Recommended)

```python
try:
    # Code
    pass
except Exception as e:
    print(f"An error occurred: {e}")
```

### Finally (Cleanup)

```python
try:
    f = open("data.json")
    data = json.load(f)
except FileNotFoundError:
    print("File not found")
finally:
    f.close()  # Always runs, even if error occurred

# Better: use with statement
with open("data.json") as f:
    data = json.load(f)  # File closes automatically
```

### Raise Exceptions

```python
def set_gpa(self, gpa):
    """Set GPA with validation."""
    if not 0 <= gpa <= 4.0:
        raise ValueError("GPA must be 0-4.0")
    self.gpa = gpa

# Usage:
try:
    student.set_gpa(5.0)
except ValueError as e:
    print(f"Invalid GPA: {e}")
```

---

## Visualization: Matplotlib

**From Unit 4 / Optional in Capstone**

### Basic Setup

```python
import matplotlib.pyplot as plt

# Create a simple line plot
x = [1, 2, 3, 4, 5]
y = [1, 4, 9, 16, 25]

plt.plot(x, y)
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.title("My Plot")
plt.show()
```

### Common Chart Types

**Bar chart:**
```python
import matplotlib.pyplot as plt

names = ["Alice", "Bob", "Carol"]
gpas = [3.8, 3.5, 3.9]

plt.bar(names, gpas)
plt.ylabel("GPA")
plt.title("Student GPAs")
plt.show()
```

**Line chart:**
```python
import matplotlib.pyplot as plt

months = ["Jan", "Feb", "Mar", "Apr"]
temps = [45, 48, 52, 60]

plt.plot(months, temps, marker='o')
plt.ylabel("Temperature (°F)")
plt.title("Monthly Temperatures")
plt.show()
```

**Histogram:**
```python
import matplotlib.pyplot as plt

gpas = [3.2, 3.5, 3.8, 3.6, 3.9, 3.4, 3.7, 3.1]

plt.hist(gpas, bins=5)
plt.xlabel("GPA")
plt.ylabel("Number of Students")
plt.title("GPA Distribution")
plt.show()
```

**Scatter plot:**
```python
import matplotlib.pyplot as plt

hours_studied = [1, 2, 3, 4, 5]
test_scores = [60, 72, 85, 90, 95]

plt.scatter(hours_studied, test_scores)
plt.xlabel("Hours Studied")
plt.ylabel("Test Score")
plt.title("Study Time vs Score")
plt.show()
```

### Save Chart Instead of Show

```python
plt.bar(names, gpas)
plt.ylabel("GPA")
plt.title("Student GPAs")
plt.savefig("chart.png")  # Save as image
plt.close()
```

---

## Common Patterns

### Reading Configuration from JSON

```python
# config.json
{
    "api_key": "your_key_here",
    "data_file": "data/students.json",
    "max_results": 100
}

# Python code
import json

with open("config.json") as f:
    config = json.load(f)

api_key = config["api_key"]
data_file = config["data_file"]
```

### Logging Progress

```python
# Instead of: print("Doing X...")
# Use:

def process_data(items):
    """Process items with progress logging."""
    total = len(items)
    for i, item in enumerate(items, 1):
        print(f"Processing {i}/{total}: {item}")
        # Do work
```

### Validating Input

```python
def get_positive_number(prompt):
    """Get a positive number from user with validation."""
    while True:
        try:
            value = float(input(prompt))
            if value <= 0:
                print("Must be positive")
                continue
            return value
        except ValueError:
            print("Invalid number")

num = get_positive_number("Enter a positive number: ")
```

### Creating Sample Data

```python
import json
import random

# Generate sample students
students = []
for i in range(100, 110):
    name = f"Student {i}"
    gpa = round(random.uniform(3.0, 4.0), 2)
    students.append({
        "name": name,
        "student_id": i,
        "gpa": gpa,
        "courses": ["Math", "Physics"]
    })

with open("data/sample_students.json", "w") as f:
    json.dump(students, f, indent=2)
```

### Timing Code

```python
import time

start = time.time()

# Code to time
for i in range(1000000):
    x = i ** 2

elapsed = time.time() - start
print(f"Took {elapsed:.2f} seconds")
```

---

## Quick Reference Table

| Concept | Units | Quick Example |
|---------|-------|---------------|
| **Classes** | Unit 2 | `class Student: def __init__(self, name): self.name = name` |
| **File I/O** | Unit 4 | `with open("file.txt") as f: data = f.read()` |
| **JSON** | Unit 4 | `json.load(f)` / `json.dump(data, f)` |
| **CSV** | Unit 4 | `csv.reader(f)` / `csv.DictReader(f)` |
| **Exceptions** | Unit 5 | `try: ... except ValueError: ...` |
| **Sorting** | Unit 6 | `sorted(items, key=lambda x: x.attr)` |
| **Searching** | Unit 6 | `[x for x in items if condition]` |
| **APIs** | Unit 4 | `requests.get(url).json()` |
| **Matplotlib** | Unit 4 | `plt.bar(x, y); plt.show()` |

---

**Keep this guide open while you code. Copy and paste templates, modify for your needs, and build awesome projects!**
