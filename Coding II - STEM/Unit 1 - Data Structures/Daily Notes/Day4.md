# Day 4: Dictionaries (Key-Value Pairs, Creating, Accessing, Updating)
**Learning Target:** I can create dictionaries and perform key-value operations efficiently.

### Key Concepts
A **dictionary** stores data as key-value pairs. Use curly braces `{}` and colons to separate keys from values.

**Keys** must be immutable (strings, numbers, tuples). **Values** can be anything.

**Common operations:**
- Access: `dict[key]`
- Add/update: `dict[key] = value`
- Delete: `del dict[key]` or `dict.pop(key)`
- Check existence: `"key" in dict`
- Iterate: `for key in dict:` or `for key, value in dict.items():`

**Useful methods:**
- `.keys()` — get all keys
- `.values()` — get all values
- `.items()` — get key-value pairs as tuples
- `.get(key, default)` — safely access with default
- `.update(other_dict)` — merge dictionaries

### Code Examples
```python
# Creating dictionaries
student = {
    "name": "Zach McCoy",
    "grade": 11,
    "gpa": 3.8,
    "subjects": ["Math", "Python", "Physics"]
}

# Accessing values
print(student["name"])          # "Zach McCoy"
print(student["grade"])         # 11

# Safe access with default
print(student.get("age", "N/A"))  # "N/A" (age doesn't exist)

# Adding/updating
student["age"] = 17
student["gpa"] = 3.9            # Update existing

# Deleting
del student["subjects"]
# or
removed_value = student.pop("age")

# Checking if key exists
if "name" in student:
    print(student["name"])

# Iterating through keys
for key in student:
    print(key, student[key])

# Iterating through key-value pairs
for key, value in student.items():
    print(f"{key}: {value}")

# Iterating through values only
for value in student.values():
    print(value)

# Creating dictionary from lists
keys = ["a", "b", "c"]
values = [1, 2, 3]
dictionary = dict(zip(keys, values))  # {"a": 1, "b": 2, "c": 3}

# Nested dictionaries
school = {
    "students": {
        "alice": {"grade": 10, "gpa": 3.9},
        "bob": {"grade": 11, "gpa": 3.7}
    },
    "teachers": ["Mr. Smith", "Ms. Johnson"]
}
print(school["students"]["alice"]["gpa"])  # 3.9
```

### Guided Practice
Create a student gradebook program:
1. Create a dictionary with student names as keys and GPA as values
2. Add a new student
3. Update an existing student's GPA
4. Print all students and their GPAs
5. Count how many students have GPA >= 3.5

### Practice Problems
**Problem 1 — Beginner:** Create a dictionary with 3 fruits as keys and their prices as values. Print one value.

**Problem 2 — Intermediate:** Create a dictionary of student names and grades. Add a new student, update an existing grade, and print all entries.

**Problem 3 — Challenge:** Create a nested dictionary representing a school with departments containing teacher names. Access and print a specific teacher.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use square brackets for access
- Problem 2: Use .items() for iterating
- Problem 3: Use multiple levels of square brackets for nested access
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
prices = {"apple": 0.99, "banana": 0.59, "orange": 1.29}
print(prices["apple"])  # 0.99

# Problem 2 Example
grades = {"Alice": 92, "Bob": 85}
grades["Charlie"] = 88  # Add
grades["Alice"] = 95    # Update
for name, grade in grades.items():
    print(f"{name}: {grade}")

# Problem 3 Example
school = {
    "math": ["Ms. Johnson", "Mr. Chen"],
    "english": ["Ms. Williams"]
}
print(school["math"][1])  # Mr. Chen
```
</details>

---
