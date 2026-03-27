# Day 11: Exception Handling Lab
**Learning Target:** I can apply exception handling skills to process real-world data with comprehensive error management.

### Key Concepts

**Error-resilient code:** Code that continues processing despite encountering errors.

**Multiple exception types:** Handling different errors appropriately based on their type.

**Data validation:** Checking data quality before processing.

**Logging errors:** Recording which lines/records failed and why.

**Partial success:** Processing as much data as possible even if some records fail.

### Code Examples

```python
# Example 1: Processing file with multiple error types
import os

def process_data_file(filename):
    if not os.path.exists(filename):
        raise FileNotFoundError(f"File {filename} not found")

    successful = 0
    failed = 0
    errors_log = []

    with open(filename, 'r') as f:
        for line_num, line in enumerate(f, 1):
            try:
                parts = line.strip().split(',')
                name = parts[0]
                age = int(parts[1])
                score = int(parts[2])

                if age < 0 or score < 0:
                    raise ValueError("Age and score must be non-negative")

                successful += 1
                print(f"✓ Line {line_num}: {name}, {age}, {score}")

            except IndexError:
                failed += 1
                errors_log.append(f"Line {line_num}: Missing fields")
            except ValueError as e:
                failed += 1
                errors_log.append(f"Line {line_num}: {e}")

    return successful, failed, errors_log

# Example 2: Validating and converting CSV data
def validate_and_convert(csv_data):
    records = []
    errors = []

    for line_num, line in enumerate(csv_data.split('\n'), 1):
        if not line.strip():
            continue

        try:
            fields = line.split(',')
            if len(fields) != 3:
                raise ValueError(f"Expected 3 fields, got {len(fields)}")

            name, age_str, email = fields

            if not name.strip():
                raise ValueError("Name cannot be empty")

            age = int(age_str)

            if age < 0 or age > 120:
                raise ValueError(f"Invalid age: {age}")

            if '@' not in email:
                raise ValueError(f"Invalid email: {email}")

            records.append({'name': name, 'age': age, 'email': email})

        except ValueError as e:
            errors.append(f"Line {line_num}: {e}")

    return records, errors

# Example 3: Safe list processing
def process_list_safely(items, converter):
    results = []
    skipped = 0

    for i, item in enumerate(items):
        try:
            converted = converter(item)
            results.append(converted)
        except (ValueError, TypeError) as e:
            skipped += 1
            print(f"Skipped item {i}: {item} ({e})")

    return results, skipped

# Example 4: Nested try/except for complex operations
def extract_and_validate_data(data_string):
    try:
        # Try to parse the data
        lines = data_string.split('\n')
        processed = []

        for line_num, line in enumerate(lines, 1):
            try:
                # Process each line
                cleaned = line.strip()
                if not cleaned:
                    continue

                parts = cleaned.split(':')
                key = parts[0]
                value = int(parts[1])

                if value < 0:
                    raise ValueError("Value cannot be negative")

                processed.append((key, value))

            except (IndexError, ValueError) as e:
                print(f"Warning at line {line_num}: {e}")
                continue

        return processed

    except Exception as e:
        print(f"Fatal error: {e}")
        return []

# Example 5: Exception handling with recovery
def read_and_process_with_retry(filename, max_retries=3):
    for attempt in range(max_retries):
        try:
            with open(filename, 'r') as f:
                return f.read()
        except FileNotFoundError:
            print(f"Attempt {attempt + 1}: File not found")
            if attempt < max_retries - 1:
                print(f"Retrying... ({max_retries - attempt - 1} attempts left)")
            else:
                raise
```

### Guided Practice

**Activity: CSV Data Processor**

1. Create a program that processes messy CSV data:
   ```
   Alice,25,95
   Bob,abc,87
   Charlie,30,
   Diana,28,92
   ```

2. For each line:
   - Try to parse it
   - Catch specific errors (ValueError, IndexError)
   - Log errors with line numbers
   - Keep track of successes and failures

**Step-by-step code:**
```python
csv_data = """Alice,25,95
Bob,abc,87
Charlie,30,
Diana,28,92"""

successful = []
failed = []

for line_num, line in enumerate(csv_data.split('\n'), 1):
    try:
        name, age, score = line.split(',')
        age = int(age)
        score = int(score)
        successful.append((name, age, score))
        print(f"✓ {name}")
    except ValueError:
        failed.append((line_num, "Non-numeric value"))
        print(f"✗ Line {line_num}: Invalid number")
    except IndexError:
        failed.append((line_num, "Missing field"))
        print(f"✗ Line {line_num}: Missing field")

print(f"\nProcessed: {len(successful)} success, {len(failed)} failed")
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that reads a list of numbers (as strings), tries to convert each to int, and reports which ones failed.

**Problem 2 — Intermediate:** Write a program that processes a CSV-like format, handles multiple error types, and prints a summary of successes and failures.

**Problem 3 — Challenge:** Write a program that reads a file with student records, validates each field (name not empty, age 5-100, GPA 0-4.0), logs all errors by line, and writes valid records to an output file.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Loop through the list.
- Use try/except with ValueError.
- Keep counters for successes and failures.

**Problem 2:**
- Parse CSV with split(',').
- Handle both ValueError (conversion) and IndexError (missing fields).
- Use a summary section to report counts.

**Problem 3:**
- Read file line-by-line with enumerate.
- Validate each field separately.
- Write valid records to a new file.
- Create an error log file.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
numbers_str = ["10", "20", "abc", "30", "xyz", "40"]
success = 0
failed = 0

for item in numbers_str:
    try:
        num = int(item)
        success += 1
    except ValueError:
        failed += 1
        print(f"Failed to convert: {item}")

print(f"Results: {success} successful, {failed} failed")

# Problem 2
csv_data = """Alice,25,95
Bob,thirty,87
Charlie,30,"""

valid = []
invalid = []

for line_num, line in enumerate(csv_data.split('\n'), 1):
    try:
        name, age, score = line.split(',')
        age = int(age)
        score = int(score)
        valid.append((name, age, score))
    except ValueError as e:
        invalid.append((line_num, "Invalid number"))
    except IndexError:
        invalid.append((line_num, "Missing field"))

print(f"Valid: {len(valid)}, Invalid: {len(invalid)}")

# Problem 3
file_content = """Alice,25,3.8
Bob,thirty,3.5
Charlie,150,3.2
Diana,28,4.1"""

valid_records = []
error_log = []

for line_num, line in enumerate(file_content.split('\n'), 1):
    try:
        name, age_str, gpa_str = line.split(',')

        if not name.strip():
            raise ValueError("Name empty")

        age = int(age_str)
        if age < 5 or age > 100:
            raise ValueError(f"Age {age} out of range")

        gpa = float(gpa_str)
        if gpa < 0 or gpa > 4.0:
            raise ValueError(f"GPA {gpa} out of range")

        valid_records.append((name, age, gpa))

    except (ValueError, IndexError) as e:
        error_log.append(f"Line {line_num}: {e}")

print(f"Valid: {len(valid_records)}")
print("Error log:")
for error in error_log:
    print(f"  {error}")
```

</details>

## Code Examples

```python
import json

# Example 1: Nested dictionary access
json_string = '''
{
  "school": "Tech High",
  "principal": "Dr. Smith",
  "students": [
    {
      "name": "Alice",
      "age": 16,
      "grades": [90, 85, 92]
    },
    {
      "name": "Bob",
      "age": 17,
      "grades": [88, 91, 87]
    }
  ]
}
'''
school_data = json.loads(json_string)
print(school_data['principal'])  # Dr. Smith
print(school_data['students'][0]['name'])  # Alice
print(school_data['students'][1]['grades'][0])  # 88

# Example 2: Iterating through nested structures
for student in school_data['students']:
    print(f"{student['name']}: {student['grades']}")

# Example 3: Extracting specific values from nested arrays
alice_grades = school_data['students'][0]['grades']
alice_average = sum(alice_grades) / len(alice_grades)
print(f"Alice's average: {alice_average}")

# Example 4: Building nested JSON structures
person = {
    "name": "Carol",
    "address": {
        "street": "123 Main St",
        "city": "Portland",
        "zip": "97201"
    },
    "contacts": [
        {"type": "email", "value": "carol@example.com"},
        {"type": "phone", "value": "555-1234"}
    ]
}
json_output = json.dumps(person, indent=2)
print(json_output)

# Example 5: Accessing deeply nested data safely
json_data = '''
{
  "response": {
    "data": {
      "users": [
        {
          "id": 1,
          "profile": {
            "name": "User1",
            "settings": {
              "notifications": true
            }
          }
        }
      ]
    }
  }
}
'''
data = json.loads(json_data)
user_notifications = data['response']['data']['users'][0]['profile']['settings']['notifications']
print(user_notifications)  # True
```

---

## Guided Practice

1. **Parse this nested JSON** (simulating a weather API response):
   ```json
   {
     "location": "Portland, OR",
     "forecast": [
       {"day": "Monday", "high": 65, "low": 50},
       {"day": "Tuesday", "high": 68, "low": 52}
     ]
   }
   ```
2. **Extract and print** the forecast for Tuesday.
3. **Calculate and print** the average high temperature across both days.
4. **Create your own nested JSON** representing a social media post (with author info, comment list, etc.).
5. **Convert it to JSON** and pretty-print it.

---

## Practice Problems

**Beginner:** Parse a JSON string containing a person object with a nested address object. Print the person's city.

**Intermediate:** Parse a JSON array of products, each with a nested inventory object. Calculate the total quantity in stock across all products.

**Challenge:** Parse a JSON structure representing a social network (users, each with a list of friends, each friend with a list of posts). Find the total number of posts by all friends of a specific user.

<details>
<summary>💡 Hints</summary>
- Beginner: Use multiple levels of bracket notation: `person['address']['city']`.
- Intermediate: Loop through the products array, access each item's inventory, sum the quantities.
- Challenge: Nested loops! Outer loop through friends, inner loop through each friend's posts.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
import json

# Beginner
person_json = '{"name": "Dave", "address": {"city": "Seattle", "zip": "98101"}}'
person = json.loads(person_json)
print(person['address']['city'])  # Seattle

# Intermediate
products_json = '''[
  {"name": "Item1", "inventory": {"quantity": 50}},
  {"name": "Item2", "inventory": {"quantity": 30}}
]'''
products = json.loads(products_json)
total_qty = sum(p['inventory']['quantity'] for p in products)
print(f"Total: {total_qty}")

# Challenge
network_json = '''[
  {
    "name": "Friend1",
    "posts": [
      {"text": "Post1"},
      {"text": "Post2"}
    ]
  },
  {
    "name": "Friend2",
    "posts": [
      {"text": "Post3"}
    ]
  }
]'''
friends = json.loads(network_json)
total_posts = sum(len(friend['posts']) for friend in friends)
print(f"Total posts by friends: {total_posts}")
```
</details>
