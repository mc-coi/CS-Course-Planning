# Day 17: JSON — Reading Files with json.load() & json.dump()
**Learning Target:** I can read JSON data from files and write Python objects to JSON files.

### Key Concepts

**json.load():** Reads and parses a JSON file directly (no 's' at the end). Takes an open file object.

**json.dump():** Writes a Python object to a file as JSON (no 's' at the end). Takes an object and file object.

**loads/dumps vs load/dump:** 's' = "string", no 's' = "file".

**with statement:** Always use for safe file handling.

**JSON file extension:** Typically `.json`.

**Pretty-printing files:** Use `indent=2` to make JSON files human-readable.

### Code Examples

```python
import json
import io

# Example 1: Reading JSON from a simulated file
json_content = '{"name": "Alice", "age": 25, "grades": [95, 92, 88]}'
f = io.StringIO(json_content)
data = json.load(f)
print(data)  # {'name': 'Alice', 'age': 25, 'grades': [95, 92, 88]}

# Example 2: Writing JSON to a simulated file
student = {'name': 'Bob', 'age': 23, 'gpa': 3.8}
f = io.StringIO()
json.dump(student, f)
json_text = f.getvalue()
print(json_text)

# Example 3: Writing with indentation
f = io.StringIO()
json.dump(student, f, indent=2)
json_text = f.getvalue()
print(json_text)

# Example 4: Reading a JSON array from file
json_array = '[{"id": 1, "name": "Alice"}, {"id": 2, "name": "Bob"}]'
f = io.StringIO(json_array)
students = json.load(f)
print(f"Loaded {len(students)} students")
for student in students:
    print(f"  {student['name']}")

# Example 5: Writing an array of objects
students = [
    {'name': 'Alice', 'score': 95},
    {'name': 'Bob', 'score': 87},
    {'name': 'Charlie', 'score': 92}
]

f = io.StringIO()
json.dump(students, f, indent=2)
print(f.getvalue())

# Example 6: Reading and processing JSON data
json_content = '''
{
  "school": "Tech High",
  "students": [
    {"name": "Alice", "gpa": 3.9},
    {"name": "Bob", "gpa": 3.7},
    {"name": "Charlie", "gpa": 3.8}
  ]
}
'''

f = io.StringIO(json_content)
school_data = json.load(f)

print(f"School: {school_data['school']}")
for student in school_data['students']:
    print(f"  {student['name']}: {student['gpa']}")

# Example 7: Updating and saving JSON data
f = io.StringIO(json_content)
data = json.load(f)

# Add a new student
data['students'].append({'name': 'Diana', 'gpa': 3.95})

# Write back
output = io.StringIO()
json.dump(data, output, indent=2)
print(output.getvalue())

# Example 8: Error handling when reading JSON
bad_json = '{"name": "Eve" "age": 20}'  # Missing comma
try:
    f = io.StringIO(bad_json)
    data = json.load(f)
except json.JSONDecodeError as e:
    print(f"Error parsing JSON: {e}")

# Example 9: Filtering and exporting
json_content = '''
[
  {"name": "Alice", "age": 25, "major": "CS"},
  {"name": "Bob", "age": 23, "major": "Math"},
  {"name": "Charlie", "age": 24, "major": "CS"}
]
'''

f = io.StringIO(json_content)
students = json.load(f)

# Filter CS majors
cs_students = [s for s in students if s['major'] == 'CS']

# Export filtered results
output = io.StringIO()
json.dump(cs_students, output, indent=2)
print("CS Majors:")
print(output.getvalue())

# Example 10: Complete read-process-write cycle
def process_student_file(json_content):
    # Read
    f_in = io.StringIO(json_content)
    students = json.load(f_in)

    # Process (add computed field)
    for student in students:
        student['honors'] = student['gpa'] >= 3.8

    # Write
    f_out = io.StringIO()
    json.dump(students, f_out, indent=2)
    return f_out.getvalue()

input_json = '''
[
  {"name": "Alice", "gpa": 3.9},
  {"name": "Bob", "gpa": 3.5}
]
'''

result = process_student_file(input_json)
print(result)
```

### Guided Practice

**Activity: JSON Data Processing**

1. Create a JSON file content with student data
2. Use json.load() to read it
3. Process the data (add computed field, filter, etc.)
4. Use json.dump() to save results

**Step-by-step code:**
```python
import json
import io

# Step 1: Create JSON content
student_json = '''
{
  "class": "Period 3",
  "students": [
    {"name": "Alice", "score": 95},
    {"name": "Bob", "score": 87},
    {"name": "Charlie", "score": 92},
    {"name": "Diana", "score": 78}
  ]
}
'''

# Step 2: Read JSON
f = io.StringIO(student_json)
data = json.load(f)

# Step 3: Process - add letter grades
for student in data['students']:
    score = student['score']
    if score >= 90:
        student['grade'] = 'A'
    elif score >= 80:
        student['grade'] = 'B'
    else:
        student['grade'] = 'C'

# Step 4: Write results
output = io.StringIO()
json.dump(data, output, indent=2)
print("Updated data:")
print(output.getvalue())
```

### Practice Problems

**Problem 1 — Beginner:** Write code that uses json.load() to read a JSON string and access nested data.

**Problem 2 — Intermediate:** Write code that reads a JSON file, modifies it, and writes it back using json.dump().

**Problem 3 — Challenge:** Write a program that reads a JSON array of records, filters based on a condition, and writes the filtered results to a new JSON file.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use json.load() with StringIO.
- Access nested dict keys.

**Problem 2:**
- Read with json.load().
- Modify the data structure.
- Write with json.dump() and indent=2.

**Problem 3:**
- Read array with json.load().
- Filter using list comprehension.
- Write filtered results.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
import json
import io

# Problem 1
json_str = '{"person": {"name": "Frank", "age": 30}}'
f = io.StringIO(json_str)
data = json.load(f)
print(data['person']['name'])  # Frank

# Problem 2
json_input = '{"items": [{"id": 1, "name": "A"}]}'
f_in = io.StringIO(json_input)
data = json.load(f_in)

data['items'].append({'id': 2, 'name': 'B'})

f_out = io.StringIO()
json.dump(data, f_out, indent=2)
print(f_out.getvalue())

# Problem 3
json_array = '''
[
  {"name": "Alice", "score": 95},
  {"name": "Bob", "score": 70},
  {"name": "Charlie", "score": 92}
]
'''

f_in = io.StringIO(json_array)
records = json.load(f_in)

filtered = [r for r in records if r['score'] >= 90]

f_out = io.StringIO()
json.dump(filtered, f_out, indent=2)
print(f_out.getvalue())
```

</details>
