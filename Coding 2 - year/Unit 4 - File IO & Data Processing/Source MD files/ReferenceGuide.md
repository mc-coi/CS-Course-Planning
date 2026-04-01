# Unit 4: File I/O & Data Processing — Quick Reference Guide

## File Operations

### Opening Files (with statement — ALWAYS use this!)
```python
# Reading
with open('file.txt', 'r') as f:
    content = f.read()          # entire file as string
    line = f.readline()         # one line
    lines = f.readlines()       # list of all lines

# Writing
with open('file.txt', 'w') as f:
    f.write('text')             # write string
    f.writelines(lines)         # write list of strings

# Appending
with open('file.txt', 'a') as f:
    f.write('more text')        # add to end
```

### File Modes
- `'r'` — Read (default, file must exist)
- `'w'` — Write (overwrites existing file)
- `'a'` — Append (adds to end of file)
- `'x'` — Create (fails if file exists)
- `'rb'`, `'wb'`, `'ab'` — Binary modes

---

## CSV Files

### csv.reader (simple lists)
```python
import csv
with open('data.csv', 'r') as f:
    reader = csv.reader(f)
    for row in reader:          # each row is a list
        name, age, score = row
```

### csv.DictReader (easier — use names!)
```python
import csv
with open('data.csv', 'r') as f:
    reader = csv.DictReader(f)  # auto reads header
    for row in reader:          # each row is a dict
        print(row['name'])      # access by column name
```

### csv.writer / csv.DictWriter
```python
import csv

# Write lists
with open('output.csv', 'w', newline='') as f:
    writer = csv.writer(f)
    writer.writerow(['Name', 'Age'])
    writer.writerow(['Alice', 25])

# Write dicts
with open('output.csv', 'w', newline='') as f:
    writer = csv.DictWriter(f, fieldnames=['Name', 'Age'])
    writer.writeheader()
    writer.writerow({'Name': 'Alice', 'Age': 25})
```

---

## JSON Files

### json.loads() / json.dumps() (strings)
```python
import json

# Parse JSON string → Python object
json_str = '{"name": "Alice", "age": 25}'
data = json.loads(json_str)      # dict
print(data['name'])              # Alice

# Convert Python object → JSON string
person = {'name': 'Bob', 'age': 30}
json_str = json.dumps(person)    # string
json_pretty = json.dumps(person, indent=2)  # formatted
```

### json.load() / json.dump() (files)
```python
import json

# Read JSON file
with open('data.json', 'r') as f:
    data = json.load(f)          # automatically parsed

# Write JSON file
with open('data.json', 'w') as f:
    json.dump(data, f, indent=2) # automatically formatted
```

---

## Exception Handling

### Basic Pattern
```python
try:
    # code that might fail
    result = risky_operation()
except SpecificError:
    # handle specific error
    print("Specific error occurred")
except Exception:
    # catch-all for unexpected errors
    print("Some error occurred")
```

### Complete Pattern
```python
try:
    # code that might fail
    with open(filename, 'r') as f:
        data = json.load(f)
except FileNotFoundError:
    print(f"File not found: {filename}")
except json.JSONDecodeError:
    print(f"Invalid JSON in {filename}")
else:
    # runs only if no exception
    print("Success!")
finally:
    # always runs (cleanup)
    print("Done")
```

### Raising Exceptions
```python
def validate_age(age):
    if age < 0 or age > 150:
        raise ValueError("Age must be 0-150")
    return age
```

---

## Data Validation

### Common Checks
```python
# Type check
if not isinstance(value, int):
    raise TypeError("Must be integer")

# Range check
if not (0 <= value <= 100):
    raise ValueError("Must be 0-100")

# Required field
if not data.get('name'):
    raise KeyError("name is required")

# Email format (simple)
if '@' not in email or '.' not in email:
    raise ValueError("Invalid email")

# Pattern matching
import re
if not re.match(r'^\d{3}-\d{4}$', phone):
    raise ValueError("Invalid phone format")
```

---

## Regular Expressions (regex)

### Common Patterns
```python
import re

# Email (simple)
email_pattern = r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}'

# Phone (XXX-XXX-XXXX)
phone_pattern = r'\d{3}-\d{3}-\d{4}'

# Date (MM/DD/YYYY)
date_pattern = r'(0[1-9]|1[0-2])/(0[1-9]|[12]\d|3[01])/\d{4}'

# URL (http or https)
url_pattern = r'https?://[a-zA-Z0-9.-]+'

# Word characters only
word_pattern = r'^\w+$'
```

### Main Functions
```python
import re

text = "Contact alice@example.com or bob@test.org"

# Search: find first match
match = re.search(r'\w+@\w+\.\w+', text)
if match:
    print(match.group())        # alice@example.com

# Find all matches
emails = re.findall(r'\w+@\w+\.\w+', text)
# ['alice@example.com', 'bob@test.org']

# Match: check if entire string matches pattern
if re.match(r'^\d{3}-\d{4}$', '123-4567'):
    print("Valid phone")

# Replace
new_text = re.sub(r'@\w+\.', '@newdomain.', text)

# Split
words = re.split(r'[,;]', text)
```

---

## Working with Directories

### Using pathlib (modern, recommended)
```python
from pathlib import Path

# Create path
p = Path('data') / 'students' / 'roster.txt'

# Check existence
if p.exists():
    if p.is_file():
        print("It's a file")
    if p.is_dir():
        print("It's a directory")

# List files
data_dir = Path('data')
for file in data_dir.iterdir():
    print(file.name)

# Find files by pattern
txt_files = list(data_dir.glob('*.txt'))
all_txt = list(data_dir.rglob('*.txt'))  # recursive

# Get file info
size = p.stat().st_size
is_readable = os.access(p, os.R_OK)

# Create directory
Path('output').mkdir(parents=True, exist_ok=True)
```

### Using os (older, still useful)
```python
import os

# Current directory
cwd = os.getcwd()

# Join paths (cross-platform)
path = os.path.join('data', 'file.txt')

# Check existence
if os.path.exists(path):
    if os.path.isfile(path):
        print("It's a file")
    if os.path.isdir(path):
        print("It's a directory")

# List directory
files = os.listdir('data')

# Create directory
os.makedirs('output', exist_ok=True)

# File size
size = os.path.getsize('data.txt')
```

---

## Data Analysis Quick Stats

```python
def compute_stats(numbers):
    """Compute mean, median, min, max"""
    if not numbers:
        return None

    sorted_nums = sorted(numbers)
    n = len(sorted_nums)

    mean = sum(numbers) / n

    if n % 2 == 1:
        median = sorted_nums[n // 2]
    else:
        median = (sorted_nums[n // 2 - 1] + sorted_nums[n // 2]) / 2

    return {
        'count': n,
        'sum': sum(numbers),
        'mean': mean,
        'median': median,
        'min': min(numbers),
        'max': max(numbers),
    }
```

---

## Common Error Messages and Solutions

| Error | Likely Cause | Solution |
|-------|------|----------|
| FileNotFoundError | File doesn't exist | Check file path and name |
| PermissionError | Can't access file | Check file permissions |
| json.JSONDecodeError | Invalid JSON | Check JSON format (quotes, commas) |
| ValueError | Bad value for operation | Validate data type/format |
| IndexError | List index out of range | Check list length first |
| KeyError | Dict key doesn't exist | Use `.get()` or check keys first |
| UnicodeDecodeError | Wrong file encoding | Try `encoding='utf-8'` in open() |

---

## Best Practices Checklist

- [ ] Always use `with` statement for files
- [ ] Always handle `FileNotFoundError` when reading
- [ ] Validate data before processing
- [ ] Use meaningful variable names
- [ ] Add comments explaining complex logic
- [ ] Test with edge cases (empty files, missing fields)
- [ ] Handle multiple exception types if needed
- [ ] Don't leave files open without `with` or `.close()`
- [ ] Use regex for pattern validation
- [ ] Document assumptions about data format
