# Unit 7: Capstone Project — Technical Warm-Ups Answer Key

Complete solutions for all 15 technical warm-up challenges to support capstone development.

---

## Challenge 1: Class Basics (Unit 2, Difficulty: E)

### Solution
```python
class Book:
    """Simple Book class."""

    def __init__(self, title, author, year_published):
        self.title = title
        self.author = author
        self.year_published = year_published

    def get_summary(self):
        """Return formatted book summary."""
        return f"{self.title} by {self.author} ({self.year_published})"

# Test
book = Book("Harry Potter", "J.K. Rowling", 1997)
print(book.get_summary())
```

### Expected Output
```
Harry Potter by J.K. Rowling (1997)
```

### Common Mistakes
- Not storing all parameters as instance variables
- Using wrong format string: `{title}` instead of `{self.title}`
- Missing return statement in get_summary()
- Forgetting `__init__` parameters

---

## Challenge 2: File Writing (Unit 4, Difficulty: E)

### Solution
```python
def save_notes(filename, notes_list):
    """Save list of notes to file, one per line."""
    with open(filename, "w") as f:
        for note in notes_list:
            f.write(note + "\n")

# Test
save_notes("notes.txt", ["Learn Python", "Build projects", "Practice daily"])
# File should now contain 3 lines
```

### Expected Output
```
(notes.txt created with 3 lines)
```

### Common Mistakes
- Not adding newline character after each note
- Not opening file in write mode ("w")
- Not using with statement
- Trying to write the whole list instead of iterating

---

## Challenge 3: File Reading (Unit 4, Difficulty: E)

### Solution
```python
def load_notes(filename):
    """Read notes from file and return as list."""
    with open(filename) as f:
        return [line.strip() for line in f]

# Test
notes = load_notes("notes.txt")
print(notes)
# Expected: ["Learn Python", "Build projects", "Practice daily"]
```

### Expected Output
```
['Learn Python', 'Build projects', 'Practice daily']
```

### Common Mistakes
- Not using `strip()` (includes newline characters)
- Using `readlines()` which includes `\n`
- Not using list comprehension
- Not returning the list

---

## Challenge 4: JSON Writing (Unit 4, Difficulty: M)

### Solution
```python
import json

def save_to_json(filename, data_dict):
    """Save dictionary to JSON file with formatting."""
    with open(filename, "w") as f:
        json.dump(data_dict, f, indent=2)

# Test
data = {"name": "Alice", "age": 20, "gpa": 3.8}
save_to_json("student.json", data)
# Check: student.json should be readable and nicely formatted
```

### Expected Output
```json
{
  "name": "Alice",
  "age": 20,
  "gpa": 3.8
}
```

### Common Mistakes
- Using `json.dumps()` instead of `json.dump()` (dumps returns string)
- Not using `indent=2` (unformatted JSON)
- Not opening file in write mode
- Using `json.load()` instead of `dump()`

---

## Challenge 5: JSON Reading (Unit 4, Difficulty: M)

### Solution
```python
import json

def load_from_json(filename):
    """Load JSON file and return data, handle missing file."""
    try:
        with open(filename) as f:
            return json.load(f)
    except FileNotFoundError:
        return {}

# Test
data = load_from_json("student.json")
print(data)
```

### Expected Output
```
{'name': 'Alice', 'age': 20, 'gpa': 3.8}
```

### Common Mistakes
- Not handling FileNotFoundError
- Using `json.loads()` instead of `json.load()` (loads is for strings)
- Not returning default empty dict
- Not closing file (missing with statement)

---

## Challenge 6: List Comprehension (Unit 3, Difficulty: M)

### Solution
```python
def get_high_achievers(students):
    """Return names of students with GPA >= 3.5."""
    return [s["name"] for s in students if s["gpa"] >= 3.5]

# Test
students = [
    {"name": "Alice", "gpa": 3.8},
    {"name": "Bob", "gpa": 3.2},
    {"name": "Carol", "gpa": 3.9},
]
print(get_high_achievers(students))
# Expected: ["Alice", "Carol"]
```

### Expected Output
```
['Alice', 'Carol']
```

### Common Mistakes
- Using wrong threshold: `> 3.5` instead of `>= 3.5`
- Returning whole student dict instead of just name
- Using for loop instead of list comprehension
- Wrong condition: `if s["gpa"] < 3.5`

---

## Challenge 7: Sorting (Unit 5, Difficulty: M)

### Solution
```python
def sort_by_gpa(students):
    """Sort students by GPA in descending order."""
    return sorted(students, key=lambda s: s["gpa"], reverse=True)

# Test
students = [
    {"name": "Alice", "gpa": 3.8},
    {"name": "Bob", "gpa": 3.2},
    {"name": "Carol", "gpa": 3.9},
]
result = sort_by_gpa(students)
# Expected: Carol (3.9), Alice (3.8), Bob (3.2)
```

### Expected Output
```
[{'name': 'Carol', 'gpa': 3.9}, {'name': 'Alice', 'gpa': 3.8}, {'name': 'Bob', 'gpa': 3.2}]
```

### Common Mistakes
- Forgetting `reverse=True` (ascending instead of descending)
- Wrong lambda: `lambda s: s` doesn't sort by GPA
- Using `s.gpa` instead of `s["gpa"]` (dictionaries use brackets)
- Using `max()` instead of `sorted()`

---

## Challenge 8: Exception Handling (Unit 5, Difficulty: M)

### Solution
```python
def get_valid_gpa(prompt):
    """Get GPA from user, keep asking until valid."""
    while True:
        try:
            gpa = float(input(prompt))
            if not 0 <= gpa <= 4.0:
                print("GPA must be between 0 and 4.0")
                continue
            return gpa
        except ValueError:
            print("Invalid input. Enter a number.")

# Test
gpa = get_valid_gpa("Enter GPA (0-4.0): ")
print(f"You entered: {gpa}")
```

### Expected Output
```
Enter GPA (0-4.0): abc
Invalid input. Enter a number.
Enter GPA (0-4.0): -1
GPA must be between 0 and 4.0
Enter GPA (0-4.0): 3.8
You entered: 3.8
```

### Common Mistakes
- Not converting to float (string comparison)
- Not checking bounds after conversion
- Not catching ValueError
- Not using `continue` to re-ask
- Breaking on first error instead of looping

---

## Challenge 9: Searching (Unit 5, Difficulty: M)

### Solution
```python
def search_by_name(students, name):
    """Return all students whose name contains search term."""
    return [s for s in students if name.lower() in s["name"].lower()]

# Test
students = [
    {"name": "Alice Smith", "gpa": 3.8},
    {"name": "Alice Johnson", "gpa": 3.2},
    {"name": "Bob Brown", "gpa": 3.9},
]
print(search_by_name(students, "alice"))
# Expected: 2 results (both Alices)
```

### Expected Output
```
[{'name': 'Alice Smith', 'gpa': 3.8}, {'name': 'Alice Johnson', 'gpa': 3.2}]
```

### Common Mistakes
- Not converting to lowercase (case-sensitive match)
- Using `==` instead of `in` (doesn't match partial names)
- Not using list comprehension
- Wrong condition logic

---

## Challenge 10: API Request (Unit 4, Difficulty: M)

### Solution
```python
import requests

def get_weather(city):
    """Fetch current temperature for a city (Open-Meteo API)."""
    try:
        # Get coordinates for city
        geo_url = "https://geocoding-api.open-meteo.com/v1/search"
        geo_params = {"name": city, "count": 1, "language": "en", "format": "json"}
        geo_response = requests.get(geo_url, params=geo_params)
        geo_data = geo_response.json()

        if not geo_data["results"]:
            return None

        lat = geo_data["results"][0]["latitude"]
        lon = geo_data["results"][0]["longitude"]

        # Get weather for coordinates
        weather_url = "https://api.open-meteo.com/v1/forecast"
        weather_params = {"latitude": lat, "longitude": lon, "current": "temperature_2m"}
        weather_response = requests.get(weather_url, params=weather_params)
        weather_data = weather_response.json()

        return weather_data["current"]["temperature_2m"]
    except Exception as e:
        print(f"Error: {e}")
        return None

# Test
temp = get_weather("London")
if temp:
    print(f"Temperature: {temp}°C")
```

### Expected Output
```
Temperature: 8.5°C
(or actual current temperature)
```

### Common Mistakes
- Not checking if results exist before accessing
- Wrong JSON key names
- Not handling exceptions
- Hard-coding city name in URL instead of using params
- Not extracting latitude/longitude correctly

---

## Challenge 11: CSV Reading (Unit 4, Difficulty: M)

### Solution
```python
import csv

def read_csv(filename):
    """Read CSV and return list of dicts."""
    try:
        with open(filename) as f:
            reader = csv.DictReader(f)
            return list(reader)
    except FileNotFoundError:
        return []

# Test
data = read_csv("sample.csv")
for row in data:
    print(row)
```

### Expected Output
```
{'Name': 'Alice', 'Score': '95'}
{'Name': 'Bob', 'Score': '87'}
...
```

### Common Mistakes
- Not using `DictReader` (harder to access by name)
- Not handling FileNotFoundError
- Returning generator instead of list
- Not closing file (missing with statement)
- Using `reader()` instead of `DictReader()`

---

## Challenge 12: CSV Writing (Unit 4, Difficulty: M)

### Solution
```python
import csv

def write_csv(filename, data):
    """Write list of dicts to CSV file."""
    if not data:
        return

    keys = data[0].keys()
    with open(filename, "w", newline="") as f:
        writer = csv.DictWriter(f, fieldnames=keys)
        writer.writeheader()
        writer.writerows(data)

# Test
students = [
    {"name": "Alice", "gpa": 3.8, "id": 100},
    {"name": "Bob", "gpa": 3.2, "id": 101},
]
write_csv("output.csv", students)
```

### Expected Output
```
(output.csv created with header and 2 data rows)
```

### Common Mistakes
- Not checking if data is empty
- Not using `newline=""` in write mode (creates extra blank lines)
- Not writing header row
- Using `writer()` instead of `DictWriter()`
- Not extracting fieldnames from first dict

---

## Challenge 13: Data Validation (Unit 5, Difficulty: H)

### Solution
```python
def validate_student(name, student_id, gpa):
    """Validate student data."""
    # Validate name: non-empty, only letters and spaces
    if not name or not name.replace(" ", "").isalpha():
        return False

    # Validate student ID: positive integer
    try:
        if int(student_id) <= 0:
            return False
    except (ValueError, TypeError):
        return False

    # Validate GPA: float between 0 and 4.0
    try:
        gpa_float = float(gpa)
        if not 0 <= gpa_float <= 4.0:
            return False
    except (ValueError, TypeError):
        return False

    return True

# Test
print(validate_student("Alice", 100, 3.8))       # True
print(validate_student("Alice123", 100, 3.8))    # False
print(validate_student("Bob", -1, 3.8))          # False
print(validate_student("Carol", 102, 5.0))       # False
```

### Expected Output
```
True
False
False
False
```

### Common Mistakes
- Not checking if name is empty
- Using `isalpha()` on name with spaces (space is not alpha)
- Not checking if ID is positive
- Not converting to proper types
- Not catching both ValueError and TypeError

---

## Challenge 14: Plotting Data (Unit 4, Difficulty: H)

### Solution
```python
import matplotlib.pyplot as plt

def plot_gpa_distribution(students):
    """Create histogram of GPA distribution."""
    gpas = [s["gpa"] for s in students]
    plt.hist(gpas, bins=5, edgecolor="black")
    plt.xlabel("GPA")
    plt.ylabel("Number of Students")
    plt.title("GPA Distribution")
    plt.show()

# Test
students = [
    {"name": "Alice", "gpa": 3.8},
    {"name": "Bob", "gpa": 3.2},
    {"name": "Carol", "gpa": 3.9},
    {"name": "David", "gpa": 3.5},
]
plot_gpa_distribution(students)
```

### Expected Output
```
(Histogram showing distribution of GPAs)
```

### Common Mistakes
- Not using `edgecolor` (bars merge together)
- Wrong bins number (too many or too few)
- Not calling `plt.show()`
- Not extracting GPAs from student dicts
- Missing labels and title

---

## Challenge 15: Complex Integration (Unit 1-6, Difficulty: H)

### Solution
```python
import json
import csv

def load_students(filename):
    """Load students from JSON file."""
    try:
        with open(filename) as f:
            return json.load(f)
    except FileNotFoundError:
        return []

def search_and_save():
    """Main program: load, search/sort, save."""
    students = load_students("students.json")

    if not students:
        print("No students loaded")
        return

    while True:
        print("\n1. Search by name")
        print("2. Sort by GPA")
        print("3. Exit")
        choice = input("Pick: ").strip()

        results = []

        if choice == "1":
            name = input("Search for: ").strip()
            results = [s for s in students if name.lower() in s["name"].lower()]
        elif choice == "2":
            results = sorted(students, key=lambda s: s["gpa"], reverse=True)
        elif choice == "3":
            break
        else:
            print("Invalid choice")
            continue

        if results:
            print(f"Found {len(results)} results")
            filename = input("Save to CSV file: ").strip()
            if filename:
                save_csv(filename, results)
        else:
            print("No results")

def save_csv(filename, data):
    """Save data to CSV file."""
    if not data:
        return
    keys = data[0].keys()
    with open(filename, "w", newline="") as f:
        writer = csv.DictWriter(f, fieldnames=keys)
        writer.writeheader()
        writer.writerows(data)

if __name__ == "__main__":
    search_and_save()
```

### Expected Output
```
1. Search by name
2. Sort by GPA
3. Exit
Pick: 1
Search for: alice
Found 2 results
Save to CSV file: alice_students.csv
(alice_students.csv created)
```

### Common Mistakes
- Not handling empty file/missing file
- Not looping for multiple operations
- Wrong search logic (case sensitivity)
- Not sorting correctly
- Not saving with proper CSV format
- Not validating input

---

## Summary by Topic

**Classes & Objects (Challenge 1):**
- Instance variables and methods
- String representation

**File I/O (Challenges 2-3, 11-12):**
- Reading and writing text files
- CSV and JSON operations
- Error handling with try/except

**Data Structures (Challenge 6):**
- List comprehensions
- Filtering data

**Sorting & Searching (Challenges 7, 9):**
- Using lambda with sorted()
- Filtering with list comprehensions

**Error Handling (Challenge 8, 13):**
- Input validation
- Exception handling
- Type conversions

**APIs (Challenge 10):**
- Making HTTP requests
- Parsing JSON responses
- Handling errors

**Visualization (Challenge 14):**
- Creating histograms
- Labeling charts

**Integration (Challenge 15):**
- Combining multiple concepts
- Building interactive programs
- File I/O with JSON and CSV

---
