# Unit 4 Practice Bank — 20 Problems with Solutions

## Problem Set 1: File I/O Basics (Problems 1-3)

### Problem 1: Read and Count Lines
Write a program that reads a text file and prints the number of lines in it.

<details>
<summary>💡 Hint</summary>
Use `.readlines()` or iterate through the file with a loop.
</details>

<details>
<summary>✅ Solution</summary>
```python
with open('file.txt', 'r') as f:
    lines = f.readlines()
    print(f"Number of lines: {len(lines)}")

# Alternative
with open('file.txt', 'r') as f:
    count = sum(1 for _ in f)
    print(f"Number of lines: {count}")
```
</details>

---

### Problem 2: Find Word Frequency
Read a file and count how many times a specific word appears.

<details>
<summary>💡 Hint</summary>
Convert each line to lowercase, split by spaces, and count occurrences.
</details>

<details>
<summary>✅ Solution</summary>
```python
word_to_find = 'python'
count = 0

with open('file.txt', 'r') as f:
    for line in f:
        words = line.lower().split()
        count += words.count(word_to_find)

print(f"'{word_to_find}' appears {count} times")
```
</details>

---

### Problem 3: Copy File
Write a program that reads one file and writes its content to another file.

<details>
<summary>💡 Hint</summary>
Read from source, write to destination. Use `with` statements for both.
</details>

<details>
<summary>✅ Solution</summary>
```python
with open('source.txt', 'r') as source:
    with open('destination.txt', 'w') as dest:
        dest.write(source.read())
```
</details>

---

## Problem Set 2: CSV Processing (Problems 4-8)

### Problem 4: Count CSV Rows
Read a CSV file and count how many data rows (excluding header) it contains.

<details>
<summary>✅ Solution</summary>
```python
import csv

with open('data.csv', 'r') as f:
    reader = csv.reader(f)
    next(reader)  # Skip header
    count = sum(1 for _ in reader)
    print(f"Data rows: {count}")
```
</details>

---

### Problem 5: Filter CSV by Value
Read a CSV with students (Name, Score) and write only students with score ≥ 90 to a new file.

<details>
<summary>✅ Solution</summary>
```python
import csv

with open('students.csv', 'r') as infile:
    reader = csv.DictReader(infile)
    rows = [r for r in reader if int(r['Score']) >= 90]

with open('honors.csv', 'w', newline='') as outfile:
    writer = csv.DictWriter(outfile, fieldnames=['Name', 'Score'])
    writer.writeheader()
    writer.writerows(rows)
```
</details>

---

### Problem 6: CSV Statistics
Read a CSV with numeric column and compute mean and max.

<details>
<summary>✅ Solution</summary>
```python
import csv

scores = []
with open('scores.csv', 'r') as f:
    reader = csv.DictReader(f)
    for row in reader:
        scores.append(float(row['Score']))

mean = sum(scores) / len(scores)
print(f"Mean: {mean:.2f}, Max: {max(scores)}")
```
</details>

---

### Problem 7: Merge CSV Files
Read two CSV files with different data and merge them into one output file.

<details>
<summary>✅ Solution</summary>
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
</details>

---

### Problem 8: CSV Transformation
Read a CSV with prices and quantities, compute total for each item, write to new CSV.

<details>
<summary>✅ Solution</summary>
```python
import csv

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
</details>

---

## Problem Set 3: JSON Processing (Problems 9-11)

### Problem 9: Parse JSON String
Parse a JSON string containing user data and access a nested value.

<details>
<summary>✅ Solution</summary>
```python
import json

json_str = '{"user": {"name": "Alice", "email": "alice@example.com"}}'
data = json.loads(json_str)
print(data['user']['email'])
```
</details>

---

### Problem 10: Write JSON File
Create a list of products (with name and price) and write to a JSON file.

<details>
<summary>✅ Solution</summary>
```python
import json

products = [
    {"name": "Widget", "price": 19.99},
    {"name": "Gadget", "price": 29.99}
]

with open('products.json', 'w') as f:
    json.dump(products, f, indent=2)
```
</details>

---

### Problem 11: Transform JSON
Read a JSON file with students and their scores, add a grade field (A for 90+, B for 80+, C otherwise), write to new JSON.

<details>
<summary>✅ Solution</summary>
```python
import json

with open('students.json', 'r') as f:
    students = json.load(f)

for student in students:
    score = student['score']
    if score >= 90:
        student['grade'] = 'A'
    elif score >= 80:
        student['grade'] = 'B'
    else:
        student['grade'] = 'C'

with open('students_graded.json', 'w') as f:
    json.dump(students, f, indent=2)
```
</details>

---

## Problem Set 4: Exception Handling (Problems 12-14)

### Problem 12: Safe File Reading
Read a file and handle FileNotFoundError gracefully.

<details>
<summary>✅ Solution</summary>
```python
try:
    with open('file.txt', 'r') as f:
        content = f.read()
    print(content)
except FileNotFoundError:
    print("Error: File not found")
```
</details>

---

### Problem 13: CSV with Error Handling
Read a CSV and skip rows where the numeric column can't be converted.

<details>
<summary>✅ Solution</summary>
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
</details>

---

### Problem 14: Custom Exception Validation
Create a function that raises ValueError if age is invalid.

<details>
<summary>✅ Solution</summary>
```python
def validate_age(age):
    try:
        age_int = int(age)
        if age_int < 0 or age_int > 150:
            raise ValueError("Age must be 0-150")
        return age_int
    except ValueError:
        raise ValueError("Age must be a number")

# Test
try:
    print(validate_age("25"))
    print(validate_age("-5"))
except ValueError as e:
    print(f"Error: {e}")
```
</details>

---

## Problem Set 5: Data Validation and Regex (Problems 15-20)

### Problem 15: Email Validation
Write a function that validates email format using regex.

<details>
<summary>✅ Solution</summary>
```python
import re

def validate_email(email):
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return bool(re.match(pattern, email))

print(validate_email("alice@example.com"))  # True
print(validate_email("invalid-email"))      # False
```
</details>

---

### Problem 16: Phone Number Extraction
Extract all phone numbers in format XXX-XXX-XXXX from text.

<details>
<summary>✅ Solution</summary>
```python
import re

text = "Call 555-123-4567 or 555-987-6543 for info"
phones = re.findall(r'\d{3}-\d{3}-\d{4}', text)
print(phones)  # ['555-123-4567', '555-987-6543']
```
</details>

---

### Problem 17: Data Cleaning
Read CSV, validate each numeric field, skip invalid rows.

<details>
<summary>✅ Solution</summary>
```python
import csv

def is_valid_record(row):
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
</details>

---

### Problem 18: Text Normalization
Read text file, convert to lowercase, remove extra whitespace, write to new file.

<details>
<summary>✅ Solution</summary>
```python
with open('input.txt', 'r') as infile:
    with open('output.txt', 'w') as outfile:
        for line in infile:
            cleaned = ' '.join(line.lower().split())
            outfile.write(cleaned + '\n')
```
</details>

---

### Problem 19: Data Analysis
Read CSV, compute count/mean/max for a column, write report to text file.

<details>
<summary>✅ Solution</summary>
```python
import csv

with open('data.csv', 'r') as f:
    reader = csv.DictReader(f)
    values = [float(r['Value']) for r in reader]

report = f"""DATA REPORT
Count: {len(values)}
Mean: {sum(values)/len(values):.2f}
Max: {max(values):.2f}
"""

with open('report.txt', 'w') as f:
    f.write(report)
```
</details>

---

### Problem 20: Complete Pipeline
Read CSV, validate data, transform values, write JSON.

<details>
<summary>✅ Solution</summary>
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
</details>

---

## Summary Statistics

- **Total Problems:** 20
- **File I/O:** 3 problems
- **CSV:** 5 problems
- **JSON:** 3 problems
- **Exceptions:** 3 problems
- **Validation & Regex:** 6 problems

Practice all problems to master Unit 4!
