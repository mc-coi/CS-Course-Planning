# Unit 4: File IO & Data Processing — Complete Answer Key

---

## Problem Set 1: File I/O Basics

---

## Problem 1: Read and Count Lines

### Solution
```python
# Method 1: Using readlines()
with open('file.txt', 'r') as f:
    lines = f.readlines()
    print(f"Number of lines: {len(lines)}")

# Method 2: Using sum with generator (more memory efficient)
with open('file.txt', 'r') as f:
    count = sum(1 for _ in f)
    print(f"Number of lines: {count}")
```

### Expected Output
```
Number of lines: 5
(or whatever number of lines in file)
```

### Common Mistakes
- Not using `with` statement (file may not close properly)
- Using `len(f.read())` (counts characters, not lines)
- Using `readlines()` but not accessing `.count()` method
- Not closing file explicitly if not using `with`

---

## Problem 2: Find Word Frequency

### Solution
```python
word_to_find = 'python'
count = 0

with open('file.txt', 'r') as f:
    for line in f:
        words = line.lower().split()
        count += words.count(word_to_find)

print(f"'{word_to_find}' appears {count} times")
```

### Expected Output
```
'python' appears 3 times
(or whatever count in the file)
```

### Common Mistakes
- Not converting to lowercase (case-sensitive match fails)
- Using `line.split(word_to_find)` instead of `split()` then `count(word_to_find)`
- Not counting across lines (resetting count)
- Not splitting words properly

---

## Problem 3: Copy File

### Solution
```python
# Method 1: Read and write all at once
with open('source.txt', 'r') as source:
    with open('destination.txt', 'w') as dest:
        dest.write(source.read())

# Method 2: Copy line by line (better for large files)
with open('source.txt', 'r') as source:
    with open('destination.txt', 'w') as dest:
        for line in source:
            dest.write(line)
```

### Expected Output
```
(destination.txt contains exact copy of source.txt)
```

### Common Mistakes
- Not opening destination in write mode ('w')
- Not opening source in read mode (though 'r' is default)
- Using both `with` statements without nesting properly
- Reading into variable but not writing it

---

## Problem Set 2: CSV Processing

---

## Problem 4: Count CSV Rows

### Solution
```python
import csv

with open('data.csv', 'r') as f:
    reader = csv.reader(f)
    next(reader)  # Skip header row
    count = sum(1 for _ in reader)
    print(f"Data rows: {count}")
```

### Expected Output
```
Data rows: 5
(or whatever count)
```

### Common Mistakes
- Not calling `next(reader)` to skip header
- Counting header as data row
- Counting all lines including header
- Not using csv module (manual splitting doesn't handle commas in quotes)

---

## Problem 5: Filter CSV by Value

### Solution
```python
import csv

# Read and filter
with open('students.csv', 'r') as infile:
    reader = csv.DictReader(infile)
    rows = [r for r in reader if int(r['Score']) >= 90]

# Write filtered results
with open('honors.csv', 'w', newline='') as outfile:
    writer = csv.DictWriter(outfile, fieldnames=['Name', 'Score'])
    writer.writeheader()
    writer.writerows(rows)
```

### Expected Output
```
(honors.csv contains only students with Score >= 90)
```

### Common Mistakes
- Not using `DictReader` (harder to access by column name)
- Not filtering correctly: `>= 90` vs `> 90`
- Not using `newline=''` in write mode (creates extra blank lines)
- Not writing header row
- Not converting Score to int before comparing

---

## Problem 6: CSV Statistics

### Solution
```python
import csv

scores = []
with open('scores.csv', 'r') as f:
    reader = csv.DictReader(f)
    for row in reader:
        scores.append(float(row['Score']))

mean = sum(scores) / len(scores)
max_score = max(scores)

print(f"Mean: {mean:.2f}, Max: {max_score}")
```

### Expected Output
```
Mean: 85.50, Max: 98.00
(or actual values)
```

### Common Mistakes
- Not converting scores to float (string comparison)
- Not using DictReader (would need to know column index)
- Dividing by wrong number (len(rows) includes all fields)
- Not formatting output to 2 decimal places

---

## Problem 7: Merge CSV Files

### Solution
```python
import csv

rows = []

# Read first file
with open('file1.csv', 'r') as f:
    reader = csv.DictReader(f)
    rows.extend(list(reader))

# Read second file
with open('file2.csv', 'r') as f:
    reader = csv.DictReader(f)
    rows.extend(list(reader))

# Write combined
with open('merged.csv', 'w', newline='') as f:
    writer = csv.DictWriter(f, fieldnames=rows[0].keys())
    writer.writeheader()
    writer.writerows(rows)
```

### Expected Output
```
(merged.csv contains all rows from both files)
```

### Common Mistakes
- Not using `extend()` to add lists to list
- Using `append()` which nests lists
- Fieldnames from wrong source (should use first row)
- Not writing header
- Files must have same column names

---

## Problem 8: CSV Transformation

### Solution
```python
import csv

# Read input
with open('items.csv', 'r') as infile:
    reader = csv.DictReader(infile)
    rows = list(reader)

# Add total column
for row in rows:
    price = float(row['Price'])
    qty = float(row['Quantity'])
    row['Total'] = f"{price * qty:.2f}"

# Write output
with open('totals.csv', 'w', newline='') as outfile:
    fieldnames = list(rows[0].keys())
    writer = csv.DictWriter(outfile, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(rows)
```

### Expected Output
```
(totals.csv has same columns plus new 'Total' column)
```

### Common Mistakes
- Not converting Price and Quantity to float
- Calculating but not storing in row
- Not including new column in fieldnames
- Not formatting Total to 2 decimal places
- Reading then overwriting file (read first, write to different file)

---

## Problem Set 3: JSON Processing

---

## Problem 9: Parse JSON String

### Solution
```python
import json

json_str = '{"user": {"name": "Alice", "email": "alice@example.com"}}'
data = json.loads(json_str)

print(data['user']['email'])  # alice@example.com
```

### Expected Output
```
alice@example.com
```

### Common Mistakes
- Using `json.load()` instead of `json.loads()` (load is for files, loads is for strings)
- Not handling nested dictionaries properly
- Using `data.user` instead of `data['user']` (dot notation doesn't work)
- Keys are strings, must use quotes in access

---

## Problem 10: Write JSON File

### Solution
```python
import json

products = [
    {"name": "Widget", "price": 19.99},
    {"name": "Gadget", "price": 29.99}
]

with open('products.json', 'w') as f:
    json.dump(products, f, indent=2)
```

### Expected Output
```json
[
  {
    "name": "Widget",
    "price": 19.99
  },
  {
    "name": "Gadget",
    "price": 29.99
  }
]
```

### Common Mistakes
- Using `json.dumps()` instead of `json.dump()` (dumps returns string)
- Not using `indent=2` (unformatted JSON is hard to read)
- Not opening file in write mode
- Forgetting to close file

---

## Problem 11: Transform JSON

### Solution
```python
import json

# Read JSON file
with open('students.json', 'r') as f:
    students = json.load(f)

# Add grade based on score
for student in students:
    score = student['score']
    if score >= 90:
        student['grade'] = 'A'
    elif score >= 80:
        student['grade'] = 'B'
    else:
        student['grade'] = 'C'

# Write to new file
with open('students_graded.json', 'w') as f:
    json.dump(students, f, indent=2)
```

### Expected Output
```json
[
  {
    "name": "Alice",
    "score": 95,
    "grade": "A"
  },
  ...
]
```

### Common Mistakes
- Thresholds wrong: `>= 89` instead of `>= 90` for A
- Not modifying student dictionary in place
- Using `json.dumps()` and then writing string
- Not preserving existing fields
- Grade boundaries overlapping

---

## Problem Set 4: Exception Handling

---

## Problem 12: Safe File Reading

### Solution
```python
try:
    with open('file.txt', 'r') as f:
        content = f.read()
    print(content)
except FileNotFoundError:
    print("Error: File not found")
```

### Expected Output
```
(file contents if exists)
or
Error: File not found
```

### Common Mistakes
- Not catching specific exception (catching generic Exception)
- Printing exception object instead of custom message
- Not using `with` statement
- Catching exception but not handling it (silently failing)

---

## Problem 13: CSV with Error Handling

### Solution
```python
import csv

valid_rows = []
with open('data.csv', 'r') as f:
    reader = csv.DictReader(f)
    for i, row in enumerate(reader, 1):
        try:
            value = float(row['Score'])
            valid_rows.append(row)
        except ValueError:
            print(f"Skipped row {i}: invalid score")

print(f"Processed {len(valid_rows)} valid rows")
```

### Expected Output
```
Skipped row 3: invalid score
Processed 5 valid rows
(or similar)
```

### Common Mistakes
- Not converting to float (string comparison doesn't fail)
- Using enumerate starting at 0 instead of 1 (off by one error)
- Catching generic Exception instead of ValueError
- Not continuing to next row after error
- Not tracking line numbers correctly

---

## Problem 14: Custom Exception Validation

### Solution
```python
def validate_age(age):
    """Validate age is number between 0-150."""
    try:
        age_int = int(age)
        if age_int < 0 or age_int > 150:
            raise ValueError("Age must be 0-150")
        return age_int
    except ValueError:
        raise ValueError("Age must be a number")

# Test
try:
    print(validate_age("25"))   # 25
    print(validate_age("-5"))   # ValueError
except ValueError as e:
    print(f"Error: {e}")
```

### Expected Output
```
25
Error: Age must be 0-150
```

### Common Mistakes
- Not converting to int first
- Catching ValueError then raising ValueError with different message
- Not checking bounds after conversion
- Returning invalid values instead of raising error

---

## Problem Set 5: Data Validation and Regex

---

## Problem 15: Email Validation

### Solution
```python
import re

def validate_email(email):
    """Validate email format using regex."""
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return bool(re.match(pattern, email))

# Test
print(validate_email("alice@example.com"))    # True
print(validate_email("invalid-email"))        # False
print(validate_email("bob+test@gmail.co.uk")) # True
```

### Expected Output
```
True
False
True
```

### Common Mistakes
- Pattern too simple: `.*@.*` (matches invalid emails)
- Missing escape for special characters: `.` should be `\.` in regex
- Using `re.search()` instead of `re.match()` (match is from beginning)
- Not returning boolean: returning Match object instead
- Pattern too strict: excluding valid characters like +

---

## Problem 16: Phone Number Extraction

### Solution
```python
import re

text = "Call 555-123-4567 or 555-987-6543 for info"

# Extract all phone numbers in XXX-XXX-XXXX format
phones = re.findall(r'\d{3}-\d{3}-\d{4}', text)

print(phones)  # ['555-123-4567', '555-987-6543']
```

### Expected Output
```
['555-123-4567', '555-987-6543']
```

### Common Mistakes
- Pattern wrong: `\d{3}\d{3}\d{4}` (no hyphens)
- Using `re.search()` instead of `re.findall()` (only finds first)
- Pattern too greedy: `\d+` (matches multiple digits together)
- Forgetting raw string `r'...'` (backslashes interpreted)

---

## Problem 17: Data Cleaning

### Solution
```python
import csv

def is_valid_record(row):
    """Check if record has valid numeric fields."""
    try:
        int(row['Age'])
        float(row['Score'])
        return True
    except (ValueError, KeyError):
        return False

valid_records = []
with open('students.csv', 'r') as f:
    reader = csv.DictReader(f)
    for row in reader:
        if is_valid_record(row):
            valid_records.append(row)

print(f"Valid records: {len(valid_records)}")
```

### Expected Output
```
Valid records: 8
(or actual count)
```

### Common Mistakes
- Not handling both ValueError and KeyError
- Not skipping invalid rows
- Raising exception instead of returning False
- Not converting to proper types before checking
- Not checking for both fields

---

## Problem 18: Text Normalization

### Solution
```python
# Read input, normalize, write output
with open('input.txt', 'r') as infile:
    with open('output.txt', 'w') as outfile:
        for line in infile:
            # Lowercase and remove extra whitespace
            cleaned = ' '.join(line.lower().split())
            outfile.write(cleaned + '\n')
```

### Expected Output
```
(output.txt contains normalized text)
```

### Common Mistakes
- Not using `split()` without arguments (splits on any whitespace)
- Using `line.strip()` alone (doesn't remove internal extra spaces)
- Not adding newlines when writing
- Not converting to lowercase
- Not joining cleaned words

---

## Problem 19: Data Analysis

### Solution
```python
import csv

# Read and extract values
with open('data.csv', 'r') as f:
    reader = csv.DictReader(f)
    values = [float(r['Value']) for r in reader]

# Calculate statistics
report = f"""DATA REPORT
Count: {len(values)}
Mean: {sum(values)/len(values):.2f}
Max: {max(values):.2f}
"""

# Write report
with open('report.txt', 'w') as f:
    f.write(report)

print("Report saved to report.txt")
```

### Expected Output
```
(report.txt contains formatted report)
```

### Common Mistakes
- Not converting values to float
- Division by zero if no values
- Not formatting floats to 2 decimal places
- Not writing to file
- Calculating on strings instead of numbers

---

## Problem 20: Complete Pipeline

### Solution
```python
import csv
import json

# Read and validate CSV
valid_data = []
with open('input.csv', 'r') as f:
    reader = csv.DictReader(f)
    for row in reader:
        try:
            valid_data.append({
                'name': row['Name'].strip(),
                'age': int(row['Age']),
                'score': float(row['Score'])
            })
        except (ValueError, KeyError):
            pass

# Write JSON
with open('output.json', 'w') as f:
    json.dump(valid_data, f, indent=2)

print(f"Processed {len(valid_data)} records")
```

### Expected Output
```json
[
  {
    "name": "Alice Smith",
    "age": 20,
    "score": 95.5
  },
  ...
]
```

### Common Mistakes
- Not handling missing fields
- Not validating data types
- Not stripping whitespace from strings
- Not handling exceptions in pipeline
- Not converting types before storing
- Not writing to file with proper formatting

---
