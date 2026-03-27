# Unit 7: Capstone Technical Warm-Ups
> 15 small coding challenges to practice key concepts. Use these when you're stuck, between sprints, or when you need a mental break from your capstone.

---

## How to Use This File

**When to use:** Start of work session, when stuck on a concept, or when waiting for feedback

**How to use:** Pick a challenge matching your project, code the solution, test it, then return to your capstone

**Difficulty:** Easy (E), Medium (M), Hard (H)

---

## Challenge 1: Class Basics (Unit 2, E)

**Concept:** Create and use a simple class

**Problem:** Write a `Book` class with attributes `title`, `author`, and `year_published`. Add a method `get_summary()` that returns a string like "Harry Potter by J.K. Rowling (1997)".

**Template:**
```python
class Book:
    def __init__(self, title, author, year_published):
        # Your code here
        pass

    def get_summary(self):
        # Your code here
        pass

# Test
book = Book("Harry Potter", "J.K. Rowling", 1997)
print(book.get_summary())
# Expected: "Harry Potter by J.K. Rowling (1997)"
```

**Solution:**
```python
class Book:
    def __init__(self, title, author, year_published):
        self.title = title
        self.author = author
        self.year_published = year_published

    def get_summary(self):
        return f"{self.title} by {self.author} ({self.year_published})"
```

---

## Challenge 2: File Writing (Unit 4, E)

**Concept:** Write data to a file

**Problem:** Write a function `save_notes(filename, notes_list)` that takes a list of strings and writes each to a new line in the file.

**Template:**
```python
def save_notes(filename, notes_list):
    # Your code here
    pass

# Test
save_notes("notes.txt", ["Learn Python", "Build projects", "Practice daily"])
# Check: notes.txt should have 3 lines
```

**Solution:**
```python
def save_notes(filename, notes_list):
    with open(filename, "w") as f:
        for note in notes_list:
            f.write(note + "\n")
```

---

## Challenge 3: File Reading (Unit 4, E)

**Concept:** Read data from a file

**Problem:** Write a function `load_notes(filename)` that reads a file and returns a list of lines (without newlines).

**Template:**
```python
def load_notes(filename):
    # Your code here
    pass

# Test
notes = load_notes("notes.txt")
print(notes)
# Expected: ["Learn Python", "Build projects", "Practice daily"]
```

**Solution:**
```python
def load_notes(filename):
    with open(filename) as f:
        return [line.strip() for line in f]
```

---

## Challenge 4: JSON Writing (Unit 4, M)

**Concept:** Save data to JSON format

**Problem:** Write a function `save_to_json(filename, data_dict)` that saves a dictionary to a JSON file with nice formatting (indentation).

**Template:**
```python
import json

def save_to_json(filename, data_dict):
    # Your code here
    pass

# Test
data = {"name": "Alice", "age": 20, "gpa": 3.8}
save_to_json("student.json", data)
# Check: student.json should be readable and nicely formatted
```

**Solution:**
```python
import json

def save_to_json(filename, data_dict):
    with open(filename, "w") as f:
        json.dump(data_dict, f, indent=2)
```

---

## Challenge 5: JSON Reading (Unit 4, M)

**Concept:** Load data from JSON file

**Problem:** Write a function `load_from_json(filename)` that reads a JSON file and returns the data as a dictionary. Handle the case where the file doesn't exist.

**Template:**
```python
import json

def load_from_json(filename):
    # Your code here
    pass

# Test
data = load_from_json("student.json")
print(data)
```

**Solution:**
```python
import json

def load_from_json(filename):
    try:
        with open(filename) as f:
            return json.load(f)
    except FileNotFoundError:
        return {}
```

---

## Challenge 6: List Comprehension (Unit 6, M)

**Concept:** Use list comprehension to filter and transform data

**Problem:** Write a function `get_high_achievers(students)` that takes a list of student dicts and returns names of students with GPA >= 3.5.

**Template:**
```python
def get_high_achievers(students):
    # students is a list of dicts: [{"name": "Alice", "gpa": 3.8}, ...]
    # Your code here
    pass

# Test
students = [
    {"name": "Alice", "gpa": 3.8},
    {"name": "Bob", "gpa": 3.2},
    {"name": "Carol", "gpa": 3.9},
]
print(get_high_achievers(students))
# Expected: ["Alice", "Carol"]
```

**Solution:**
```python
def get_high_achievers(students):
    return [s["name"] for s in students if s["gpa"] >= 3.5]
```

---

## Challenge 7: Sorting (Unit 6, M)

**Concept:** Sort a list of objects by an attribute

**Problem:** Write a function `sort_by_gpa(students)` that returns students sorted by GPA (highest first).

**Template:**
```python
def sort_by_gpa(students):
    # students is a list of dicts or objects with "gpa" attribute
    # Your code here
    pass

# Test
students = [
    {"name": "Alice", "gpa": 3.8},
    {"name": "Bob", "gpa": 3.2},
    {"name": "Carol", "gpa": 3.9},
]
print(sort_by_gpa(students))
# Expected: Carol (3.9), Alice (3.8), Bob (3.2)
```

**Solution:**
```python
def sort_by_gpa(students):
    return sorted(students, key=lambda s: s["gpa"], reverse=True)
```

---

## Challenge 8: Exception Handling (Unit 5, M)

**Concept:** Catch and handle errors gracefully

**Problem:** Write a function `get_valid_gpa(prompt)` that asks user for GPA and keeps asking until they enter a valid number between 0 and 4.0.

**Template:**
```python
def get_valid_gpa(prompt):
    while True:
        # Your code here: get input, validate, return if valid
        pass

# Test
gpa = get_valid_gpa("Enter GPA (0-4.0): ")
print(f"You entered: {gpa}")
```

**Solution:**
```python
def get_valid_gpa(prompt):
    while True:
        try:
            gpa = float(input(prompt))
            if not 0 <= gpa <= 4.0:
                print("GPA must be between 0 and 4.0")
                continue
            return gpa
        except ValueError:
            print("Invalid input. Enter a number.")
```

---

## Challenge 9: Searching (Unit 6, M)

**Concept:** Search a list for matching items

**Problem:** Write a function `search_by_name(students, name)` that returns all students whose names contain the search term (case-insensitive).

**Template:**
```python
def search_by_name(students, name):
    # students is a list of dicts: [{"name": "Alice", ...}, ...]
    # Your code here
    pass

# Test
students = [
    {"name": "Alice Smith", "gpa": 3.8},
    {"name": "Alice Johnson", "gpa": 3.2},
    {"name": "Bob Brown", "gpa": 3.9},
]
print(search_by_name(students, "alice"))
# Expected: 2 results (both Alices)
```

**Solution:**
```python
def search_by_name(students, name):
    return [s for s in students if name.lower() in s["name"].lower()]
```

---

## Challenge 10: API Request (Unit 4, M)

**Concept:** Fetch data from an API

**Problem:** Write a function `get_weather(city)` that fetches current temperature for a city using a free weather API (e.g., Open-Meteo).

**Template:**
```python
import requests

def get_weather(city):
    # Fetch latitude/longitude for city
    # Then fetch current weather
    # Return temperature
    pass

# Test (no API key needed for Open-Meteo)
# temp = get_weather("London")
# print(f"Temperature: {temp}°C")
```

**Solution:**
```python
import requests

def get_weather(city):
    try:
        # Get coordinates for city
        geo_url = f"https://geocoding-api.open-meteo.com/v1/search?name={city}&count=1&language=en&format=json"
        geo_response = requests.get(geo_url)
        geo_data = geo_response.json()

        if not geo_data["results"]:
            return None

        lat = geo_data["results"][0]["latitude"]
        lon = geo_data["results"][0]["longitude"]

        # Get weather
        weather_url = f"https://api.open-meteo.com/v1/forecast?latitude={lat}&longitude={lon}&current=temperature_2m"
        weather_response = requests.get(weather_url)
        weather_data = weather_response.json()

        return weather_data["current"]["temperature_2m"]
    except Exception as e:
        print(f"Error: {e}")
        return None
```

---

## Challenge 11: CSV Reading (Unit 4, M)

**Concept:** Parse CSV files

**Problem:** Write a function `read_csv(filename)` that reads a CSV file and returns a list of dicts (one dict per row).

**Template:**
```python
import csv

def read_csv(filename):
    # Your code here
    pass

# Test (create sample.csv first with headers)
# data = read_csv("sample.csv")
# print(data)
```

**Solution:**
```python
import csv

def read_csv(filename):
    try:
        with open(filename) as f:
            reader = csv.DictReader(f)
            return list(reader)
    except FileNotFoundError:
        return []
```

---

## Challenge 12: CSV Writing (Unit 4, M)

**Concept:** Write data to CSV format

**Problem:** Write a function `write_csv(filename, data)` that saves a list of dicts to a CSV file (with headers).

**Template:**
```python
import csv

def write_csv(filename, data):
    # data is a list of dicts: [{"name": "Alice", "gpa": 3.8}, ...]
    # Your code here
    pass

# Test
students = [
    {"name": "Alice", "gpa": 3.8, "id": 100},
    {"name": "Bob", "gpa": 3.2, "id": 101},
]
write_csv("output.csv", students)
```

**Solution:**
```python
import csv

def write_csv(filename, data):
    if not data:
        return

    keys = data[0].keys()
    with open(filename, "w", newline="") as f:
        writer = csv.DictWriter(f, fieldnames=keys)
        writer.writeheader()
        writer.writerows(data)
```

---

## Challenge 13: Data Validation (Unit 5, H)

**Concept:** Validate and sanitize user input

**Problem:** Write a function `validate_student(name, student_id, gpa)` that checks if all inputs are valid. Return True if valid, False if not.

**Rules:**
- Name: non-empty string, no numbers
- Student ID: positive integer
- GPA: float between 0 and 4.0

**Template:**
```python
def validate_student(name, student_id, gpa):
    # Check all conditions
    # Return True if all valid, False otherwise
    pass

# Test
print(validate_student("Alice", 100, 3.8))  # True
print(validate_student("Alice123", 100, 3.8))  # False (name has numbers)
print(validate_student("Bob", -1, 3.8))  # False (negative ID)
print(validate_student("Carol", 102, 5.0))  # False (GPA too high)
```

**Solution:**
```python
def validate_student(name, student_id, gpa):
    # Validate name
    if not name or not name.replace(" ", "").isalpha():
        return False

    # Validate student ID
    try:
        if int(student_id) <= 0:
            return False
    except (ValueError, TypeError):
        return False

    # Validate GPA
    try:
        gpa = float(gpa)
        if not 0 <= gpa <= 4.0:
            return False
    except (ValueError, TypeError):
        return False

    return True
```

---

## Challenge 14: Plotting Data (Unit 4, H)

**Concept:** Create a chart with matplotlib

**Problem:** Write a function `plot_gpa_distribution(students)` that creates a histogram showing GPA distribution.

**Template:**
```python
import matplotlib.pyplot as plt

def plot_gpa_distribution(students):
    # Extract GPAs
    # Create histogram
    # Label and show
    pass

# Test
students = [
    {"name": "Alice", "gpa": 3.8},
    {"name": "Bob", "gpa": 3.2},
    {"name": "Carol", "gpa": 3.9},
    {"name": "David", "gpa": 3.5},
]
plot_gpa_distribution(students)
```

**Solution:**
```python
import matplotlib.pyplot as plt

def plot_gpa_distribution(students):
    gpas = [s["gpa"] for s in students]
    plt.hist(gpas, bins=5, edgecolor="black")
    plt.xlabel("GPA")
    plt.ylabel("Number of Students")
    plt.title("GPA Distribution")
    plt.show()
```

---

## Challenge 15: Complex Integration (Unit 1–6, H)

**Concept:** Combine multiple concepts

**Problem:** Write a program that:
1. Reads a JSON file of student records
2. Allows user to search by name or sort by GPA
3. Saves filtered results to a CSV file

**Template:**
```python
import json
import csv

def load_students(filename):
    # Load from JSON
    pass

def search_and_save():
    # Main program
    # 1. Load students
    # 2. Ask user: search by name (S), sort by GPA (G), or exit (E)
    # 3. Process choice
    # 4. Save results to CSV
    pass

# Test with sample data
```

**Solution:**
```python
import json
import csv

def load_students(filename):
    try:
        with open(filename) as f:
            return json.load(f)
    except FileNotFoundError:
        return []

def search_and_save():
    students = load_students("students.json")

    while True:
        print("\n1. Search by name")
        print("2. Sort by GPA")
        print("3. Exit")
        choice = input("Pick: ").strip()

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

---

## Summary

**By Difficulty:**
- **Easy (E):** 1, 2, 3 — Warmup challenges
- **Medium (M):** 4–12 — Core concepts
- **Hard (H):** 13–15 — Integration and complexity

**By Unit:**
- **Unit 2 (OOP):** 1
- **Unit 4 (File I/O):** 2, 3, 4, 5, 10, 11, 12, 14
- **Unit 5 (Exceptions):** 8, 13
- **Unit 6 (Sorting/Searching):** 6, 7, 9

**Quick Tips:**
- Copy the template, fill in the code, test it
- Use these to warm up or when stuck
- Refer to **ReferenceGuide.md** for syntax help
- Don't just read solutions; type them out and understand them

---

**Keep practicing. The more you code, the better you become!**
