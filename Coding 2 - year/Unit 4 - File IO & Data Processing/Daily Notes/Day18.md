# Day 18: Working with Nested JSON Data
**Learning Target:** I can access, manipulate, and process complex nested JSON structures.

### Key Concepts

**Nested JSON:** JSON objects and arrays contained within other objects/arrays, creating hierarchical data.

**Multi-level access:** Using bracket/dot notation multiple times: `data['key']['subkey'][0]['field']`.

**Iterating through nested data:** Using loops to traverse nested structures.

**Modifying nested data:** Changing values deep in a structure.

**Flattening data:** Converting nested structures into simpler formats.

### Code Examples

```python
import json
import io

# Example 1: Accessing nested objects
json_text = '''
{
  "school": "Tech High",
  "principal": {
    "name": "Dr. Smith",
    "office": "Building A"
  }
}
'''

f = io.StringIO(json_text)
data = json.load(f)
print(data['principal']['name'])  # Dr. Smith

# Example 2: Accessing nested arrays
json_text = '''
{
  "class": {
    "name": "Math 101",
    "students": [
      {"name": "Alice", "grade": "A"},
      {"name": "Bob", "grade": "B"}
    ]
  }
}
'''

f = io.StringIO(json_text)
data = json.load(f)
first_student = data['class']['students'][0]
print(first_student['name'])  # Alice

# Example 3: Iterating through nested arrays
json_text = '''
{
  "school": "Tech High",
  "classes": [
    {
      "name": "Math",
      "students": [
        {"name": "Alice", "score": 95},
        {"name": "Bob", "score": 87}
      ]
    },
    {
      "name": "English",
      "students": [
        {"name": "Alice", "score": 92},
        {"name": "Carol", "score": 88}
      ]
    }
  ]
}
'''

f = io.StringIO(json_text)
data = json.load(f)

for cls in data['classes']:
    print(f"Class: {cls['name']}")
    for student in cls['students']:
        print(f"  {student['name']}: {student['score']}")

# Example 4: Finding values in nested structures
def find_student_by_name(data, name):
    """Search for a student in nested classes"""
    for cls in data['classes']:
        for student in cls['students']:
            if student['name'] == name:
                return student, cls['name']
    return None, None

student, class_name = find_student_by_name(data, 'Alice')
if student:
    print(f"{student['name']} is in {class_name} with score {student['score']}")

# Example 5: Modifying nested data
json_text = '{"user": {"name": "Eve", "scores": [85, 90, 92]}}'
f = io.StringIO(json_text)
user = json.load(f)

# Add a new score
user['scores'].append(95)

# Update name
user['name'] = 'Eve Smith'

output = io.StringIO()
json.dump(user, output, indent=2)
print(output.getvalue())

# Example 6: Computing statistics from nested data
json_text = '''
{
  "departments": [
    {
      "name": "Sales",
      "employees": [
        {"name": "Alice", "salary": 60000},
        {"name": "Bob", "salary": 55000}
      ]
    },
    {
      "name": "Engineering",
      "employees": [
        {"name": "Carol", "salary": 80000},
        {"name": "Dave", "salary": 85000}
      ]
    }
  ]
}
'''

f = io.StringIO(json_text)
company = json.load(f)

total_salary = 0
employee_count = 0

for dept in company['departments']:
    print(f"Department: {dept['name']}")
    for emp in dept['employees']:
        print(f"  {emp['name']}: ${emp['salary']}")
        total_salary += emp['salary']
        employee_count += 1

print(f"\nTotal employees: {employee_count}")
print(f"Average salary: ${total_salary / employee_count:.2f}")

# Example 7: Filtering nested data
json_text = '''
{
  "students": [
    {
      "name": "Alice",
      "courses": [
        {"subject": "Math", "grade": 95},
        {"subject": "English", "grade": 88}
      ]
    },
    {
      "name": "Bob",
      "courses": [
        {"subject": "Math", "grade": 82},
        {"subject": "Science", "grade": 90}
      ]
    }
  ]
}
'''

f = io.StringIO(json_text)
data = json.load(f)

# Find all A grades (90+)
a_grades = []
for student in data['students']:
    for course in student['courses']:
        if course['grade'] >= 90:
            a_grades.append({
                'student': student['name'],
                'subject': course['subject'],
                'grade': course['grade']
            })

print("A grades:")
for item in a_grades:
    print(f"  {item['student']}: {item['subject']} - {item['grade']}")

# Example 8: Transforming nested data
json_text = '''
[
  {"name": "Product A", "price": 19.99, "category": "Electronics"},
  {"name": "Product B", "price": 29.99, "category": "Electronics"},
  {"name": "Product C", "price": 9.99, "category": "Books"}
]
'''

f = io.StringIO(json_text)
products = json.load(f)

# Group by category
by_category = {}
for product in products:
    cat = product['category']
    if cat not in by_category:
        by_category[cat] = []
    by_category[cat].append(product)

output = io.StringIO()
json.dump(by_category, output, indent=2)
print(output.getvalue())

# Example 9: Deep access with safety
def safe_get(data, *keys):
    """Safely access nested values"""
    current = data
    for key in keys:
        if isinstance(current, dict):
            current = current.get(key)
        elif isinstance(current, list) and isinstance(key, int):
            try:
                current = current[key]
            except IndexError:
                return None
        else:
            return None
    return current

test_data = {'a': {'b': {'c': [1, 2, 3]}}}
print(safe_get(test_data, 'a', 'b', 'c', 0))  # 1
print(safe_get(test_data, 'a', 'x', 'y'))  # None

# Example 10: Flattening nested JSON
def flatten_json(nested_json, sep='_'):
    """Convert nested JSON to flat structure"""
    out = {}

    def flatten(x, name=''):
        if isinstance(x, dict):
            for key in x:
                flatten(x[key], name + key + sep)
        elif isinstance(x, list):
            i = 0
            for item in x:
                flatten(item, name + str(i) + sep)
                i += 1
        else:
            out[name[:-1]] = x

    flatten(nested_json)
    return out

nested = {'person': {'name': 'Frank', 'age': 30}}
flat = flatten_json(nested)
print(flat)  # {'person_name': 'Frank', 'person_age': 30}
```

### Guided Practice

**Activity: Complex JSON Processing**

1. Read a nested JSON structure (school with multiple classes, each with students)
2. Calculate statistics (average grade per class, top student overall)
3. Filter and export specific data (honors students)

**Step-by-step code:**
```python
import json
import io

school_json = '''
{
  "name": "Tech High",
  "classes": [
    {
      "name": "Math 101",
      "students": [
        {"name": "Alice", "grade": 95},
        {"name": "Bob", "grade": 87},
        {"name": "Charlie", "grade": 92}
      ]
    },
    {
      "name": "English 101",
      "students": [
        {"name": "Alice", "grade": 90},
        {"name": "Diana", "grade": 88}
      ]
    }
  ]
}
'''

f = io.StringIO(school_json)
school = json.load(f)

# Calculate average per class
for cls in school['classes']:
    grades = [s['grade'] for s in cls['students']]
    avg = sum(grades) / len(grades)
    print(f"{cls['name']}: Average {avg:.2f}")

# Find honors students (90+)
all_students = []
for cls in school['classes']:
    for student in cls['students']:
        all_students.append((student['name'], student['grade']))

honors = [s for s in all_students if s[1] >= 90]
print(f"\nHonors students:")
for name, grade in honors:
    print(f"  {name}: {grade}")
```

### Practice Problems

**Problem 1 — Beginner:** Read nested JSON and access a value 2 levels deep.

**Problem 2 — Intermediate:** Read JSON with nested arrays and iterate through all items to calculate a sum/average.

**Problem 3 — Challenge:** Read complex nested JSON, filter based on multiple conditions, and export transformed results.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use bracket notation: data['key1']['key2'].
- Print or use the value.

**Problem 2:**
- Use nested loops to traverse arrays.
- Collect values into a list.
- Calculate sum/average.

**Problem 3:**
- Use nested loops with conditions.
- Transform data as needed.
- Output in desired format.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
import json
import io

# Problem 1
json_str = '{"school": {"principal": {"name": "Dr. Smith"}}}'
f = io.StringIO(json_str)
data = json.load(f)
print(data['school']['principal']['name'])

# Problem 2
json_str = '''
{
  "classes": [
    {"name": "Math", "scores": [95, 87, 92]},
    {"name": "English", "scores": [88, 90, 85]}
  ]
}
'''
f = io.StringIO(json_str)
data = json.load(f)

all_scores = []
for cls in data['classes']:
    all_scores.extend(cls['scores'])

print(f"Average: {sum(all_scores) / len(all_scores):.2f}")

# Problem 3
json_str = '''
{
  "students": [
    {"name": "Alice", "major": "CS", "gpa": 3.9},
    {"name": "Bob", "major": "Math", "gpa": 3.5},
    {"name": "Carol", "major": "CS", "gpa": 3.8}
  ]
}
'''
f = io.StringIO(json_str)
data = json.load(f)

# Filter CS majors with GPA >= 3.8
honors_cs = [s for s in data['students'] if s['major'] == 'CS' and float(s['gpa']) >= 3.8]

output = io.StringIO()
json.dump(honors_cs, output, indent=2)
print(output.getvalue())
```

</details>
