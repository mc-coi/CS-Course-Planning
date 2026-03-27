# Day 16: JSON — What Is JSON? json.loads() & json.dumps()
**Learning Target:** I can parse JSON strings and convert Python objects to JSON format using the json module.

### Key Concepts

**JSON (JavaScript Object Notation):** A lightweight text format for representing structured data using curly braces, square brackets, and key-value pairs.

**Why JSON matters:** Used everywhere—APIs, configuration files, web applications, mobile apps, and data storage.

**json.loads():** Parses a JSON string and converts it to a Python object (usually a dict or list). The 's' stands for "string."

**json.dumps():** Converts a Python object to a JSON string. The 's' stands for "string."

**JSON syntax:** Strict rules—double quotes for strings, colons for key-value pairs, commas between items.

**JSON data types:** Objects (dicts), arrays (lists), strings, numbers, booleans, null (None).

### Code Examples

```python
import json

# Example 1: Parse a simple JSON object
json_string = '{"name": "Alice", "age": 25, "city": "NYC"}'
data = json.loads(json_string)
print(data)  # {'name': 'Alice', 'age': 25, 'city': 'NYC'}
print(data['name'])  # Alice

# Example 2: Convert Python dict to JSON string
person = {'name': 'Bob', 'age': 30, 'city': 'LA'}
json_output = json.dumps(person)
print(json_output)  # {"name": "Bob", "age": 30, "city": "LA"}

# Example 3: Pretty-printing JSON (indented for readability)
person = {
    'name': 'Carol',
    'age': 28,
    'hobbies': ['reading', 'coding', 'gaming']
}
pretty_json = json.dumps(person, indent=2)
print(pretty_json)
# Output (formatted):
# {
#   "name": "Carol",
#   "age": 28,
#   "hobbies": [
#     "reading",
#     "coding",
#     "gaming"
#   ]
# }

# Example 4: JSON arrays
json_array = '[10, 20, 30, 40]'
numbers = json.loads(json_array)
print(numbers)  # [10, 20, 30, 40]

# Example 5: JSON with nested objects
json_nested = '''
{
  "student": {
    "name": "Dave",
    "grades": [95, 87, 92]
  }
}
'''
data = json.loads(json_nested)
print(data['student']['name'])  # Dave
print(data['student']['grades'][0])  # 95

# Example 6: Converting Python list to JSON
students = [
    {'name': 'Alice', 'gpa': 3.9},
    {'name': 'Bob', 'gpa': 3.7}
]
json_list = json.dumps(students)
print(json_list)

# Example 7: Handling special characters in strings
text = 'He said "hello"'
data = {'message': text}
json_str = json.dumps(data)
print(json_str)  # {"message": "He said \"hello\""}

# Example 8: Parsing JSON with different data types
json_mixed = '{"name": "Eve", "age": 20, "active": true, "notes": null}'
data = json.loads(json_mixed)
print(data)  # {'name': 'Eve', 'age': 20, 'active': True, 'notes': None}

# Example 9: Error handling with invalid JSON
try:
    bad_json = "{'name': 'Frank'}"  # Single quotes invalid
    data = json.loads(bad_json)
except json.JSONDecodeError as e:
    print(f"JSON error: {e}")

# Example 10: Round-trip conversion
original = {'id': 1, 'name': 'Grace', 'active': True}
json_str = json.dumps(original)
recovered = json.loads(json_str)
print(recovered == original)  # True
```

### Guided Practice

**Activity: JSON Data Exchange**

1. Create a Python dict representing a book (title, author, year, pages)
2. Convert it to JSON using json.dumps()
3. Pretty-print the result
4. Parse the JSON back to Python using json.loads()
5. Verify the data matches

**Step-by-step code:**
```python
import json

# Create a book record
book = {
    'title': 'Python Basics',
    'author': 'John Smith',
    'year': 2020,
    'pages': 350,
    'tags': ['programming', 'python', 'tutorial']
}

# Convert to JSON
json_str = json.dumps(book, indent=2)
print("JSON representation:")
print(json_str)

# Parse back to Python
recovered = json.loads(json_str)
print("\nRecovered data:")
print(recovered)
print(f"Author: {recovered['author']}")
```

### Practice Problems

**Problem 1 — Beginner:** Write code that parses this JSON string and prints the age: `'{"name": "Helen", "age": 22, "city": "Boston"}'`

**Problem 2 — Intermediate:** Create a dictionary representing a movie (title, director, year, rating), convert to JSON, and print it with indentation.

**Problem 3 — Challenge:** Create a list of students (each with name and grades), convert to JSON, then parse it back and calculate the average grade across all students.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use json.loads() to parse the string.
- Access the 'age' key from the resulting dict.

**Problem 2:**
- Create a dict with movie info.
- Use json.dumps() with indent=2.
- Print the result.

**Problem 3:**
- Create a list of dicts.
- Convert to JSON.
- Parse back and extract grades.
- Calculate average.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
import json

# Problem 1
json_string = '{"name": "Helen", "age": 22, "city": "Boston"}'
data = json.loads(json_string)
print(data['age'])  # 22

# Problem 2
movie = {
    'title': 'Inception',
    'director': 'Christopher Nolan',
    'year': 2010,
    'rating': 8.8
}
json_movie = json.dumps(movie, indent=2)
print(json_movie)

# Problem 3
students = [
    {'name': 'Alice', 'grades': [95, 92, 98]},
    {'name': 'Bob', 'grades': [87, 90, 85]},
    {'name': 'Carol', 'grades': [92, 94, 91]}
]

json_str = json.dumps(students)
parsed = json.loads(json_str)

all_grades = []
for student in parsed:
    all_grades.extend(student['grades'])

average = sum(all_grades) / len(all_grades)
print(f"Average grade: {average:.2f}")
```

</details>
