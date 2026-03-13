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

---
