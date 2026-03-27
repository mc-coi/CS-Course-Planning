# Day 11: Dictionary Lab — Real-World Applications
**Learning Target:** I can apply dictionaries to solve real-world data management and lookup problems.

### Key Concepts

**Data Organization**: Using dictionaries to structure data logically, matching real-world concepts of key-value relationships.

**Efficient Lookup**: Dictionary lookups are O(1) on average, making them far more efficient than searching through lists for large datasets.

**Default Handling**: Safely handling missing keys using get() or setdefault() instead of risking KeyErrors.

**Data Transformation**: Converting between different data representations (lists to dicts, nested structures, aggregations).

**Database-Like Operations**: Simulating basic CRUD (Create, Read, Update, Delete) operations on dictionary-based data structures.

### Code Examples

```python
# Example 1: Simple Contact Management
contacts = {}

def add_contact(name, phone):
    contacts[name] = phone
    return f"{name} added"

def lookup(name):
    return contacts.get(name, "Not found")

def update_contact(name, phone):
    if name in contacts:
        contacts[name] = phone
        return "Updated"
    return "Not found"

# Usage
add_contact("Alice", "555-1234")
print(lookup("Alice"))

# Example 2: Student Grade Analysis
grades = {
    "Alice": {"math": 85, "english": 92, "science": 88},
    "Bob": {"math": 92, "english": 78, "science": 85},
    "Charlie": {"math": 78, "english": 88, "science": 92}
}

# Calculate averages
for student, scores in grades.items():
    average = sum(scores.values()) / len(scores)
    print(f"{student}: {average:.1f}")

# Example 3: Inventory System
inventory = {
    "apple": {"qty": 50, "price": 0.50},
    "banana": {"qty": 30, "price": 0.30},
    "orange": {"qty": 25, "price": 0.75}
}

# Total value
total = sum(item["qty"] * item["price"] for item in inventory.values())
print(f"Total value: ${total:.2f}")

# Example 4: Word Frequency
text = "the quick brown fox jumps over the lazy dog the fox"
words = text.lower().split()

freq = {}
for word in words:
    freq[word] = freq.get(word, 0) + 1

print(freq)

# Example 5: Student Records
students_db = {
    "001": {"name": "Alice", "major": "CS", "gpa": 3.8},
    "002": {"name": "Bob", "major": "Math", "gpa": 3.6},
    "003": {"name": "Charlie", "major": "Physics", "gpa": 3.9}
}

# Find high GPA students
high_gpa = {
    sid: info for sid, info in students_db.items()
    if info["gpa"] >= 3.7
}
print(high_gpa)

# Example 6: Product Lookup
products = [
    {"id": 1, "name": "Laptop", "price": 999.99},
    {"id": 2, "name": "Mouse", "price": 29.99},
    {"id": 3, "name": "Keyboard", "price": 79.99}
]

# Create lookup by name
name_lookup = {p["name"]: p["price"] for p in products}
print(f"Mouse: ${name_lookup['Mouse']}")

# Example 7: Configuration System
config = {
    "database": {
        "host": "localhost",
        "port": 5432
    },
    "server": {
        "host": "0.0.0.0",
        "port": 8000
    }
}

print(config["database"]["host"])

# Example 8: Data Aggregation
sales = [
    ("apple", 10, 0.50),
    ("apple", 5, 0.50),
    ("banana", 8, 0.30),
    ("orange", 12, 0.75)
]

sales_summary = {}
for product, qty, price in sales:
    if product not in sales_summary:
        sales_summary[product] = {"qty": 0, "revenue": 0}
    sales_summary[product]["qty"] += qty
    sales_summary[product]["revenue"] += qty * price

for product, data in sales_summary.items():
    print(f"{product}: {data['qty']} units, ${data['revenue']:.2f}")
```

### Guided Practice

**Activity: Building a Student Grade Manager (50 minutes)**

1. Create a nested dictionary for student records (name, grades, GPA)
2. Implement functions for:
   - Adding a new student
   - Recording grades
   - Calculating GPA
   - Finding top students
   - Sorting by performance
3. Test with sample data
4. Add error handling

### Practice Problems

**Problem 1 — Beginner:** Contact Management
```python
phonebook = {}

# TODO: Add contacts: Alice (555-1234), Bob (555-5678)
# TODO: Look up Alice's number
# TODO: Update Alice's number to 555-9999
# TODO: List all contacts
```

**Problem 2 — Intermediate:** Sales Analysis
```python
sales = [
    ("apple", 10, 0.50),
    ("apple", 5, 0.50),
    ("banana", 8, 0.30),
    ("orange", 12, 0.75),
    ("apple", 3, 0.50)
]

# TODO: Create summary dict with qty and revenue per product
# TODO: Find best-selling product
# TODO: Calculate total revenue
```

**Problem 3 — Challenge:** Course Management
```python
students_courses = {
    "Alice": ["CS101", "MATH101"],
    "Bob": ["CS101", "CS201"],
    "Charlie": ["MATH101"]
}

courses_info = {
    "CS101": {"title": "Intro to Python", "instructor": "Dr. Smith"},
    "CS201": {"title": "Data Structures", "instructor": "Dr. Jones"},
    "MATH101": {"title": "Calculus I", "instructor": "Dr. Brown"}
}

# TODO: Find courses for a student
# TODO: Find students in a course
# TODO: Find most popular course
# TODO: Build course roster dict
```

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use `phonebook[name] = phone` to add/update
- Use `get()` to safely lookup
- Iterate with `.items()` to list all

**Problem 2:**
- Use a loop with `setdefault()` or check `if not in`
- Aggregate qty and revenue
- Use `max()` with key parameter

**Problem 3:**
- For courses: iterate through student's course list
- For students: filter students whose list contains the course
- Count students per course, find max

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
phonebook = {}
phonebook["Alice"] = "555-1234"
phonebook["Bob"] = "555-5678"
print(phonebook.get("Alice"))
phonebook["Alice"] = "555-9999"
for name, phone in phonebook.items():
    print(f"{name}: {phone}")

# Problem 2
sales = [...]
summary = {}
for product, qty, price in sales:
    if product not in summary:
        summary[product] = {"qty": 0, "revenue": 0}
    summary[product]["qty"] += qty
    summary[product]["revenue"] += qty * price

best = max(summary.items(), key=lambda x: x[1]["qty"])
total = sum(data["revenue"] for data in summary.values())
print(best, total)

# Problem 3
def get_students_in_course(course_id):
    return [s for s, courses in students_courses.items() 
            if course_id in courses]

roster = {c: get_students_in_course(c) 
          for c in courses_info.keys()}

most_popular = max(roster.items(), key=lambda x: len(x[1]))
```

</details>
