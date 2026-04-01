# Unit 4 - File IO & Data Processing: Teacher Misconception & Callout Guide

## Overview

Unit 4 moves students from in-memory programming to real-world data work: reading files, parsing structured formats, and handling errors gracefully. The biggest challenge is that students treat file handling as a technical detail rather than a critical responsibility. They'll open files without closing them, assume CSV data is always well-formed, skip exception handling because "it probably won't fail," and treat regex as black-box magic. Students also conflate data format parsing (CSV vs. JSON) with data validation—they assume parsing succeeded means the data is correct. This unit teaches defensive programming and builds the muscle memory for production-quality code.

---

## Misconceptions by Topic

### File I/O Basics (Days 1–3)

**⚠️ Misconception:** "I can open a file with `open()` and close it later with `.close()`. I don't need to use the `with` statement."

**What it looks like in code:**
```python
# Student writes:
f = open('data.txt', 'r')
content = f.read()
# ... lots of code ...
f.close()  # Maybe closes, maybe doesn't if an exception occurs

# Instead of:
with open('data.txt', 'r') as f:
    content = f.read()
# File is guaranteed closed
```

**Why students think this:** Manual `open()` and `close()` feels explicit and controllable.

**How to address it:** Emphasize **reliability**, not preference. Show what happens with exceptions:

```python
# BAD: File never closes if exception occurs
f = open('data.txt')
lines = f.readlines()
process_line(lines[0])  # What if this crashes? f.close() never runs!
f.close()

# GOOD: File closes no matter what
with open('data.txt') as f:
    lines = f.readlines()
    process_line(lines[0])  # If this crashes, __exit__ still runs and closes f
```

Make it a **law**: "Always use `with`. Non-negotiable."

---

**⚠️ Misconception:** "`f.read()` and `f.readlines()` do the same thing; I'll just use `read()` because it's simpler."

**What it looks like in code:**
```python
with open('data.txt') as f:
    content = f.read()  # Entire file as one string
    # content = "line1\nline2\nline3\n"
    # Student then tries to process:
    for line in content.split('\n'):
        process(line)

# Instead of:
with open('data.txt') as f:
    for line in f:  # Iterate directly; no need to load all
        process(line)
    # or
    lines = f.readlines()  # List of strings with newlines
```

**Why students think this:** Both get the data; both work eventually.

**How to address it:** Teach the **use case** for each:
- `f.read()` — Get entire file as one string. Use when: small files, you need raw text.
- `f.readline()` — Get one line at a time. Use when: huge files, memory is limited.
- `f.readlines()` — Get list of lines. Use when: you need all lines but want to process them as a list.
- Iterate `for line in f:` — Lazy line iteration. Use when: processing line-by-line.

Show memory comparison:
```python
# File: 1GB CSV
with open('huge.csv') as f:
    data = f.read()  # Loads 1GB into memory — might crash!

# Better:
with open('huge.csv') as f:
    for line in f:  # Loads one line at a time
        process(line)
```

---

**⚠️ Misconception:** "If I open a file in `'r'` mode and accidentally call `.write()`, it will fail silently or just add to the end."

**What it looks like in code:**
```python
with open('data.txt', 'r') as f:
    content = f.read()
    f.write('new data')  # IOError: not writable
```

**Why students think this:** They don't understand file modes deeply.

**How to address it:** Teach the **mode meanings**:
- `'r'` — Read only. File must exist.
- `'w'` — Write only. Overwrites existing file; creates if doesn't exist.
- `'a'` — Append. Adds to end of file; creates if doesn't exist.
- `'r+'` — Read and write. File must exist.
- `'x'` — Create. Fails if file exists.

Use a decision tree:
1. Do I need to read the file? Use `'r'` (or `'r+'` if also writing).
2. Do I want to overwrite or create fresh? Use `'w'`.
3. Do I want to add to the end? Use `'a'`.

Show the mistake:
```python
# WRONG: Mode read, then try to write
with open('data.txt', 'r') as f:
    f.write('oops')  # IOError

# RIGHT: Mode that allows both reading and writing
with open('data.txt', 'r+') as f:
    content = f.read()
    f.write('more')  # Works
```

---

### CSV Processing (Days 4–8)

**⚠️ Misconception:** "CSV is simple—just split by commas. I don't need the `csv` module."

**What it looks like in code:**
```python
# Student writes:
with open('data.csv') as f:
    for line in f:
        fields = line.split(',')
        name, age, score = fields

# Instead of:
import csv
with open('data.csv') as f:
    reader = csv.reader(f)
    for name, age, score in reader:
        ...
```

**Why students think this:** It looks simple, and string splitting is familiar.

**How to address it:** Show the **edge cases** that break manual splitting:

```python
# This CSV line will break manual splitting:
# "Smith, John", 25, 92.5

# Split by comma:
line = '"Smith, John", 25, 92.5'
fields = line.split(',')
print(fields)
# ['"Smith', ' John"', ' 25', ' 92.5']  — WRONG! Name is split!

# csv.reader handles quoted fields:
import csv
reader = csv.reader(StringIO('"Smith, John", 25, 92.5'))
for row in reader:
    print(row)
# ['"Smith, John"', '25', '92.5']  — CORRECT!
```

Show real-world complexities: quoted fields, escaped quotes, different delimiters, trailing/leading spaces. Say: "The `csv` module handles all these. Your custom solution won't."

---

**⚠️ Misconception:** "I should use `csv.reader()` to read a CSV into a list of lists, then access columns by index."

**What it looks like in code:**
```python
import csv

with open('students.csv') as f:
    reader = csv.reader(f)
    rows = list(reader)

# Accessing data:
name = rows[0][0]  # First student's name
grade = rows[0][2]  # First student's grade

# Later, if CSV column order changes, code breaks!
```

**Why students think this:** It works, and they're used to indexing.

**How to address it:** Teach the **column-by-name advantage** of `csv.DictReader`:

```python
import csv

with open('students.csv') as f:
    reader = csv.DictReader(f)  # Auto-reads header row
    for row in reader:  # Each row is a dict
        name = row['name']  # Access by column name
        grade = row['grade']
        # If CSV column order changes, this still works!
```

Show the benefit:
```python
# csv.reader approach: fragile
rows = [['Alice', 95], ['Bob', 87]]
name = rows[0][0]
# If CSV adds a new column: [['id', 'name', 'score'], [1, 'Alice', 95], ...]
# OLD CODE BREAKS: rows[0][0] is now 'id', not name

# DictReader approach: robust
rows = [{'name': 'Alice', 'score': 95}, ...]
name = rows[0]['name']
# If CSV adds new column, this still works!
```

Recommend: **Always use `DictReader` for CSVs with headers.**

---

**⚠️ Misconception:** "When writing CSV, I can just use `f.write()` and join fields with commas."

**What it looks like in code:**
```python
# Student writes:
with open('output.csv', 'w') as f:
    f.write('name,age,score\n')
    f.write('Alice,' + str(25) + ',' + str(95) + '\n')

# Instead of:
import csv
with open('output.csv', 'w', newline='') as f:
    writer = csv.writer(f)
    writer.writerow(['name', 'age', 'score'])
    writer.writerow(['Alice', 25, 95])
```

**Why students think this:** String concatenation feels direct.

**How to address it:** Show the **problems with manual writing**:

```python
# Manual approach: breaks with special data
data = ['Alice', 'Smith, John', 25]  # Name contains comma!
# Naive write:
f.write(','.join(str(x) for x in data))
# Result: Alice,Smith, John,25  — BROKEN! Looks like 4 fields!

# csv.writer handles quoting:
import csv
writer = csv.writer(f)
writer.writerow(data)
# Result: Alice,"Smith, John",25  — CORRECT! Name is quoted!
```

Also emphasize the `newline=''` parameter:
```python
# WRONG: Python adds extra newlines on Windows
with open('file.csv', 'w') as f:
    writer = csv.writer(f)
    writer.writerow(['a', 'b'])
    # Result: 'a,b\r\r\n' on Windows (extra \r)

# RIGHT: newline='' prevents Python from translating line endings
with open('file.csv', 'w', newline='') as f:
    writer = csv.writer(f)
    writer.writerow(['a', 'b'])
    # Result: 'a,b\n' (correct)
```

---

### JSON Processing (Days 9–11)

**⚠️ Misconception:** "JSON and Python dicts are identical. I can use a Python dict as JSON and vice versa."

**What it looks like in code:**
```python
# Student confuses them:
data_dict = {'name': 'Alice', 'age': 25}
json_string = str(data_dict)  # '{\'name\': \'Alice\', \'age\': 25}'
# This is NOT valid JSON!

# Instead:
import json
json_string = json.dumps(data_dict)  # '{"name": "Alice", "age": 25}'
```

**Why students think this:** Python dicts look similar to JSON.

**How to address it:** Show the **differences**:

```python
# Python dict:
data = {'name': 'Alice', 'age': None, 'is_valid': True}

# As Python str():
str(data)  # "{'name': 'Alice', 'age': None, 'is_valid': True}"
# — Single quotes, Python-specific syntax (None, True)

# As JSON:
json.dumps(data)  # '{"name": "Alice", "age": null, "is_valid": true}'
# — Double quotes, JSON-specific keywords (null, true)

# JSON is a string format for data exchange. Python dict is an object.
```

Also show type mismatches:
```python
import json

# Python dict with unsupported types
data = {'func': lambda x: x, 'set': {1, 2, 3}}

json.dumps(data)  # TypeError: Object of type function is not JSON serializable

# Only these types are JSON-safe:
# str, int, float, bool, None, list, dict (with string keys)
```

---

**⚠️ Misconception:** "When reading JSON, I use `json.loads()` to parse the file content."

**What it looks like in code:**
```python
# Student does this:
with open('data.json') as f:
    content = f.read()  # Read as string
    data = json.loads(content)  # Parse string

# Instead of:
with open('data.json') as f:
    data = json.load(f)  # load() handles reading and parsing
```

**Why students think this:** Both work, and they learned about `loads()` first.

**How to address it:** Teach the **convenience**: `json.load()` reads and parses in one step. It's cleaner and handles encoding automatically.

```python
# Same result, but load() is simpler:

# Method 1: read() then loads()
with open('data.json') as f:
    data = json.loads(f.read())

# Method 2: load()
with open('data.json') as f:
    data = json.load(f)

# Recommendation: Use load() for files, loads() for strings
```

---

**⚠️ Misconception:** "When I `json.loads()` a string and it succeeds, the data is valid and ready to use."

**What it looks like in code:**
```python
import json

json_str = '{"name": "Alice", "age": 25}'
data = json.loads(json_str)  # Succeeds

# Student assumes data is complete and correct:
print(data['email'])  # KeyError: 'email' — assumed it existed

# Or assumes types are correct:
years_until_retirement = 65 - data['age']  # Works if age is int
# But if API returns {"age": "25"} as string, this breaks
```

**Why students think this:** Parsing succeeds, so they assume the structure is as expected.

**How to address it:** Teach **defensive parsing**: Validate structure and types.

```python
import json

def safe_parse_user(json_str):
    try:
        data = json.loads(json_str)
    except json.JSONDecodeError:
        return None  # Not valid JSON

    # Validate structure
    if not isinstance(data, dict):
        return None

    # Validate required fields
    if 'name' not in data or 'age' not in data:
        return None

    # Validate types
    if not isinstance(data['name'], str) or not isinstance(data['age'], int):
        return None

    return data

# Now safe to use:
data = safe_parse_user(json_str)
if data:
    print(data['name'])
```

Or use a schema library like `jsonschema`.

---

### Exception Handling (Days 12–16)

**⚠️ Misconception:** "I should catch all exceptions with a bare `except:` to avoid crashes."

**What it looks like in code:**
```python
# Student writes:
try:
    data = json.loads(user_input)
    process(data)
except:
    print("Error")  # Catches EVERYTHING, including bugs!

# If process(data) has a bug, the bare except hides it
```

**Why students think this:** A bare `except:` prevents crashes.

**How to address it:** Teach the **principle**: Catch *specific* exceptions you can handle. Let others propagate so you see bugs.

```python
# GOOD: Specific exception handling
try:
    data = json.loads(user_input)
except json.JSONDecodeError:
    print("Invalid JSON format")

# BETTER: Handle expected error, let bugs propagate
try:
    data = json.loads(user_input)
    process(data)
except json.JSONDecodeError:
    print("Invalid JSON format")
except KeyError as e:
    print(f"Missing key: {e}")
# If process() has a different bug (e.g., TypeError), it crashes — good! We see the bug.

# AVOID: Bare except
try:
    ...
except:  # Hides bugs!
    ...
```

Rule: "Never use bare `except:`. Always specify the exception type."

---

**⚠️ Misconception:** "When I catch an exception, I should always re-raise it or log it, or the error is lost."

**What it looks like in code:**
```python
try:
    data = json.loads(user_input)
except json.JSONDecodeError as e:
    print(f"Error: {e}")
    raise  # Re-raise unnecessarily

# Student thinks they must always re-raise
```

**Why students think this:** They learned "don't swallow exceptions" too broadly.

**How to address it:** Clarify: "Catch an exception when you can **handle** it (recover or provide user feedback). If you can't handle it, let it propagate. If you do handle it, don't re-raise unless you're adding context."

```python
# Example 1: Handle (don't re-raise)
try:
    age = int(user_input)
except ValueError:
    age = 18  # Default value — handled!

# Example 2: Handle + provide feedback (don't re-raise)
try:
    data = json.loads(json_str)
except json.JSONDecodeError:
    print("Invalid JSON. Please check your input.")
    # User sees feedback; error is handled.

# Example 3: Can't handle — re-raise (with context)
try:
    result = database.query(sql)
except DatabaseError as e:
    print("Database connection failed. Please try again later.")
    raise RuntimeError("Critical database error") from e  # Add context, then raise

# Example 4: Just log, don't re-raise
try:
    send_analytics(event)
except NetworkError:
    logger.warning("Analytics sent failed, but continuing")
    # Non-critical; just log and move on
```

---

**⚠️ Misconception:** "I don't need exception handling; I'll just test the code thoroughly."

**What it looks like in code:**
```python
# Student skips try-except for file operations:
with open('user_data.csv') as f:
    data = list(csv.DictReader(f))

# What if the file doesn't exist? The program crashes in production.
```

**Why students think this:** Testing passes, so they assume it's safe.

**How to address it:** Show the **reality of production**:
- Your code works in development (file exists, network is up).
- In production, files might be deleted, networks might fail, permissions might change.
- Exception handling is **part of design**, not just debugging.

```python
# Defensive approach:
import os

csv_file = 'user_data.csv'

if not os.path.exists(csv_file):
    print(f"Error: {csv_file} not found")
    exit(1)

try:
    with open(csv_file) as f:
        data = list(csv.DictReader(f))
except IOError as e:
    print(f"Error reading file: {e}")
    exit(1)
except csv.Error as e:
    print(f"Error parsing CSV: {e}")
    exit(1)

# Now it handles missing files, permission errors, malformed CSVs
```

---

### Data Validation & Regular Expressions (Days 17–20)

**⚠️ Misconception:** "Regular expressions are magic. I'll copy-paste a pattern from the internet and hope it works."

**What it looks like in code:**
```python
import re

# Student copies email regex without understanding it:
pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
if re.match(pattern, email):
    print("Valid email")

# If the email format changes slightly, they have no idea how to modify the pattern
```

**Why students think this:** Regex looks incomprehensible.

**How to address it:** **Teach common patterns** incrementally. Don't ask students to write complex regex. Teach them to read and modify simple ones.

Start with basics:
```python
import re

# . (dot) matches any character
re.search(r'a.c', 'abc')  # Matches
re.search(r'a.c', 'aXc')  # Matches
re.search(r'a.c', 'ac')   # No match (need exactly one character)

# * (star) means "zero or more of the previous"
re.search(r'ab*c', 'ac')   # Matches (zero 'b's)
re.search(r'ab*c', 'abc')  # Matches (one 'b')
re.search(r'ab*c', 'abbbc')  # Matches (three 'b's)

# + (plus) means "one or more"
re.search(r'ab+c', 'ac')  # No match (need at least one 'b')
re.search(r'ab+c', 'abc')  # Matches

# ? (question) means "zero or one"
re.search(r'ab?c', 'ac')  # Matches
re.search(r'ab?c', 'abc')  # Matches
re.search(r'ab?c', 'abbc')  # No match (too many 'b's)

# [] (brackets) means "any one of these characters"
re.search(r'[aeiou]', 'hello')  # Matches 'e'
re.search(r'[0-9]', 'abc')  # No match

# | (pipe) means "or"
re.search(r'cat|dog', 'I have a cat')  # Matches 'cat'
```

For email validation, show that perfect regex doesn't exist, but a good-enough one works:
```python
# Simple email pattern (catches 90% of cases)
email_pattern = r'^[^@]+@[^@]+$'  # Just: something@something

# Better email pattern (catches 99%)
email_pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'

# Perfect email pattern: doesn't exist (RFC 5322 is complex)

# Recommendation: Use a simple pattern + validation library
import re
if re.match(r'^.+@.+$', email):  # Basic check
    # Then validate by sending a confirmation email
```

---

**⚠️ Misconception:** "Data validation is optional. If the user enters bad data, it's their fault."

**What it looks like in code:**
```python
# Student skips validation:
age = int(input("Enter age: "))

# If user enters -5 or 150, the code doesn't catch it
```

**Why students think this:** Validation feels like extra work.

**How to address it:** Teach **defensive programming**: "Assume all input is wrong until proven right."

```python
def get_age():
    while True:
        try:
            age_str = input("Enter your age: ")
            age = int(age_str)

            # Validate range
            if age < 0 or age > 150:
                print("Age must be between 0 and 150")
                continue

            return age
        except ValueError:
            print("Please enter a valid number")

age = get_age()  # Won't proceed until valid
```

Show that validation is a **feature**, not bureaucracy. It catches errors early and provides good user feedback.

---

### Data Analysis & Reporting (Days 21–22)

**⚠️ Misconception:** "When computing statistics, I should just use raw data without handling missing values."

**What it looks like in code:**
```python
import statistics

data = [10, 20, None, 30, 40]
average = statistics.mean(data)  # TypeError: unsupported operand type(s) for +: 'int' and 'NoneType'

# Student doesn't know how to handle it
```

**Why students think this:** Real-world data has missing values; they've never dealt with it.

**How to address it:** Teach **data cleaning**:

```python
import statistics

data = [10, 20, None, 30, 40, '?']

# Strategy 1: Filter out missing values
clean_data = [x for x in data if x is not None and isinstance(x, (int, float))]
average = statistics.mean(clean_data)  # 25.0

# Strategy 2: Replace missing values
clean_data = [x if x is not None and isinstance(x, (int, float)) else 0 for x in data]
average = statistics.mean(clean_data)  # 20.0

# Strategy 3: Use a default or skip
# Depends on the domain and what's appropriate
```

Also teach **documentation**: "Always note how you handled missing data."

---

## Whole-Class Warning Signs

- **Students open files without `with` statements** — stop immediately and enforce it. "Always `with`. Non-negotiable."
- **Students parse CSV with `.split(',')`** — they'll hit quoted fields and fail. Show `csv.DictReader` immediately.
- **Students confuse `json.load()` and `json.loads()`** — teach: "load for files, loads for strings."
- **Students use bare `except:` clauses** — catch specific exceptions. Teach by example in the first lesson.
- **Students assume parsed data is valid** — show validation examples: check keys exist, check types.
- **Students write regex by trial-and-error** — teach common patterns (email, phone, date). Provide templates.
- **Students skip data validation** — show that real-world data is messy. Validation is defensive programming.
- **Students don't handle `FileNotFoundError`** — teach: check file existence or handle the exception.

---

## Questions That Reveal Understanding

1. **"Why should you always use `with` when opening files?"** (Answer: Guarantees the file closes even if an exception occurs. If they say "I can use `.close()`" they don't understand exception safety.)

2. **"What's the difference between `csv.reader()` and `csv.DictReader()`?"** (Answer: `reader` gives lists; `DictReader` gives dicts with column names as keys. If they don't see the advantage of named access, they haven't grasped it.)

3. **"You have JSON data with a missing field. How do you safely access it?"** (Answer: Use `.get()` with a default, or check existence first. If they do `data['field']` directly, they'll crash on missing fields.)

4. **"Write a try-except to handle a file that might not exist."** (Answer: Catch `FileNotFoundError` and handle appropriately. If they use bare `except:`, correct them.)

5. **"What's the difference between `json.load()` and `json.loads()`?"** (Answer: `load()` reads from a file; `loads()` parses a string. If they're confused, they don't understand the naming convention.)

6. **"Validate that a user-entered age is between 1 and 150."** (Answer: Parse with `int()`, check range with `if`. If they skip validation, they're not thinking defensively.)

7. **"Explain this regex pattern: `r'^[a-zA-Z0-9]+$'`."** (Answer: Starts with `^`, ends with `$`, allows letters and digits, at least one character. If they can't explain it, they don't understand character classes.)

---

## Common Student Questions & How to Answer Them

**Q: "Can I open a file without `with`?"**
A: "Technically yes, but no. The `with` statement guarantees the file closes, even if your code crashes. If you use just `open()` and `.close()`, an exception might skip the close. Always use `with`. It's a best practice that keeps you safe."

---

**Q: "How do I know if a CSV is well-formed?"**
A: "You don't until you try to read it. That's why we use the `csv` module—it handles edge cases like quoted fields. If you split by commas manually, malformed data will break. Use `csv.DictReader()` and let it handle the parsing."

---

**Q: "Should I validate every input?"**
A: "Yes, within reason. For public-facing applications (forms, APIs), validate everything. For internal tools, you can be lighter. But always validate data from external sources (files, networks). Assume it's wrong until proven right."

---

**Q: "What do I do if a regex pattern doesn't match what I expect?"**
A: "Test it in small pieces. Don't write the whole pattern at once. Start with a simple piece (like `[a-z]+` for lowercase letters), test it, then add more. Use a regex tester online to experiment. And remember: regex is for *pattern matching*, not validation of complex rules. For complex validation, use functions or libraries."

---

**Q: "My JSON parsing fails on valid-looking data. Why?"**
A: "Probably a hidden character or encoding issue. Try: (1) Print the raw JSON to see what's actually there. (2) Use `json.JSONDecodeError` to catch and see the exact error. (3) Check for BOM (Byte Order Mark) at the start of the file. (4) Try different encodings: `open('file.json', encoding='utf-8-sig')`."

---

## Analogies That Work

**1. File I/O and the `with` Statement:**
"Opening a file is like borrowing a tool from a friend. Using `with` is like keeping track of it automatically—even if you get distracted, the tool goes back. Not using `with` is like saying 'I'll return it later'—and you forget. Always use `with`."

---

**2. CSV vs. JSON:**
"CSV is like a spreadsheet: rows and columns, flat structure. JSON is like a filing cabinet with folders inside folders—hierarchical, flexible. Use CSV for simple tabular data; use JSON when you have nested structures or varying fields per record."

---

**3. Parsing vs. Validation:**
"Parsing is like opening a box—you can take out what's inside. But the box could contain trash, broken parts, or nothing. Validation is the inspection—you check what's inside before using it. Always validate after parsing."

---

**4. Exception Handling:**
"Try-except is like a safety net. You try something risky (like dividing by zero), and if it fails, the except catches you. A bare except is like a net that catches anything, including birds (bugs). Be specific about what you catch."

---

**5. Regular Expressions:**
"Regex is a pattern language. Instead of checking 'is this exactly john@example.com?', you say 'does this match the pattern of an email?' The pattern is reusable for any email. But complex patterns get messy—keep them simple or use validation libraries."

---

## Coding 1 Gaps to Watch For

Students enter Unit 4 with file basics and error awareness from earlier units. Watch for:

**Gap 1: String Methods vs. File Methods**
- **What to watch for:** Students forget that `f.read()` returns a string, so they try to use it like a list.
- **Quick fix:** Show that `f.read()` returns a string. If they want lines, use `f.readlines()` or iterate with `for line in f:`.

**Gap 2: Understanding Iterators**
- **What to watch for:** Students don't realize `f` is an iterator—once you iterate through, it's exhausted.
- **Quick fix:** Show that `for line in f:` consumes the iterator. To re-iterate, call `f.seek(0)` or reopen the file.

**Gap 3: Type Conversion**
- **What to watch for:** CSV data is all strings. Students forget to convert: `age = row['age']` is a string, not an int.
- **Quick fix:** Show explicit conversion: `age = int(row['age'])`. Wrap in try-except to handle bad data.

**Gap 4: Dictionary Defaults**
- **What to watch for:** When checking JSON or CSV data, students use `data['key']` and crash if missing.
- **Quick fix:** Teach `.get(key, default)`: `data.get('email', 'unknown@example.com')`.

**Gap 5: Understanding Encodings**
- **What to watch for:** Files with non-ASCII characters fail silently or raise encoding errors.
- **Quick fix:** Specify encoding: `open('file.txt', encoding='utf-8')`. This solves 99% of encoding issues.

---

## Quick Troubleshooting Guide

| Problem | Most Likely Cause | Fix |
|---------|------------------|-----|
| `FileNotFoundError` | File path is wrong or file doesn't exist | Check path, use `os.path.exists()` |
| File not closing | Not using `with` statement | Always use `with open(...)` |
| `UnicodeDecodeError` | Wrong encoding | Specify: `open(file, encoding='utf-8')` |
| CSV parsing fails on quoted fields | Manual `.split(',')` instead of `csv` module | Use `csv.DictReader()` |
| JSON parsing fails | Invalid JSON or wrong parsing | Use `json.JSONDecodeError` to debug |
| Missing keys in CSV/JSON | Not checking for existence | Use `.get()` or validate structure |
| `ValueError` on `int(data)` | Data is not an integer | Validate before converting or handle exception |
| `bare except:` catches all errors | Hiding bugs intentionally | Catch specific exceptions only |
| Regex doesn't match | Pattern is wrong or too strict | Test pattern incrementally; use online regex tester |
| Data includes None/missing values | No cleaning done | Filter or replace missing values before analysis |

