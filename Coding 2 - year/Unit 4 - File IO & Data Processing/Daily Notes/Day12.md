# Day 12: CSV Files — Reading with csv.reader
**Learning Target:** I can read CSV files using the csv.reader module to parse comma-separated data.

### Key Concepts

**CSV (Comma-Separated Values):** A plain text format for storing tabular data, one row per line, fields separated by commas.

**csv.reader:** A module function that parses CSV data into lists of strings.

**Iterable rows:** csv.reader returns an iterable where each iteration is a list of values.

**Handling special characters:** CSV module handles commas and quotes inside fields automatically.

**Delimiters:** CSV can use other delimiters (tabs, pipes) via the `delimiter` parameter.

**Quoting:** The csv module handles quoted fields containing special characters.

### Code Examples

```python
import csv
import io

# Example 1: Basic CSV reading with csv.reader
csv_content = """Name,Age,Score
Alice,25,95
Bob,23,87
Charlie,24,92"""

f = io.StringIO(csv_content)
reader = csv.reader(f)
for row in reader:
    print(row)  # Each row is a list

# Example 2: Accessing specific columns
f = io.StringIO(csv_content)
reader = csv.reader(f)
header = next(reader)  # Get first row as header
for row in reader:
    name = row[0]
    age = row[1]
    score = row[2]
    print(f"{name}: age {age}, score {score}")

# Example 3: Skipping the header row and processing data
f = io.StringIO(csv_content)
reader = csv.reader(f)
next(reader)  # Skip header
for row in reader:
    print(','.join(row))

# Example 4: Filtering CSV data
f = io.StringIO(csv_content)
reader = csv.reader(f)
header = next(reader)
print(','.join(header))
for row in reader:
    score = int(row[2])
    if score >= 90:
        print(','.join(row))

# Example 5: Handling different delimiters (tab-separated)
tsv_data = """Name\tAge\tScore
Alice\t25\t95
Bob\t23\t87"""

f = io.StringIO(tsv_data)
reader = csv.reader(f, delimiter='\t')
for row in reader:
    print(row)

# Example 6: CSV with quoted fields containing commas
csv_quoted = '''Name,Description,Price
"Product A","A great item, really",19.99
"Product B","Says ""wow""",29.99'''

f = io.StringIO(csv_quoted)
reader = csv.reader(f)
for row in reader:
    print(row)

# Example 7: Building a list of dictionaries from CSV
f = io.StringIO(csv_content)
reader = csv.reader(f)
header = next(reader)
records = []
for row in reader:
    record = {}
    for i, field_name in enumerate(header):
        record[field_name] = row[i]
    records.append(record)

for record in records:
    print(record)

# Example 8: Counting rows and calculating statistics
f = io.StringIO(csv_content)
reader = csv.reader(f)
header = next(reader)
rows = list(reader)

print(f"Total rows: {len(rows)}")
scores = [int(row[2]) for row in rows]
print(f"Average score: {sum(scores) / len(scores):.2f}")

# Example 9: Error handling with CSV
csv_bad = """Name,Age,Score
Alice,25,95
Bob,abc,87
Charlie,24"""

f = io.StringIO(csv_bad)
reader = csv.reader(f)
header = next(reader)

valid = 0
invalid = 0

for row in reader:
    try:
        if len(row) != len(header):
            raise ValueError("Missing fields")
        age = int(row[1])
        score = int(row[2])
        valid += 1
    except ValueError:
        invalid += 1

print(f"Valid: {valid}, Invalid: {invalid}")

# Example 10: Finding max/min values
f = io.StringIO(csv_content)
reader = csv.reader(f)
header = next(reader)
rows = list(reader)

students_with_scores = [(row[0], int(row[2])) for row in rows]
highest = max(students_with_scores, key=lambda x: x[1])
print(f"Highest scorer: {highest[0]} with {highest[1]}")
```

### Guided Practice

**Activity: Simple CSV Report**

1. Create a CSV dataset with students and their scores
2. Use csv.reader to:
   - Read the header
   - Process each row
   - Calculate average score
   - Find highest scorer
   - Count total records

**Step-by-step code:**
```python
import csv
import io

csv_data = """Name,Score
Alice,95
Bob,87
Charlie,92
Diana,88"""

f = io.StringIO(csv_data)
reader = csv.reader(f)
header = next(reader)

scores = []
students = []

for row in reader:
    name = row[0]
    score = int(row[1])
    students.append(name)
    scores.append(score)

average = sum(scores) / len(scores)
print(f"Average score: {average:.2f}")
print(f"Highest: {max(zip(students, scores), key=lambda x: x[1])}")
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that uses csv.reader to read a CSV string and print each row.

**Problem 2 — Intermediate:** Write a program that reads a CSV (Name, Age, Salary), filters for people over 30, and displays them.

**Problem 3 — Challenge:** Write a program that reads a CSV with multiple columns, groups by a category column, and displays totals per group.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use csv.reader() with StringIO for testing.
- Loop through reader to get rows.
- Each row is a list.

**Problem 2:**
- Skip header with next(reader).
- Convert age to int and check if > 30.
- Print matching rows.

**Problem 3:**
- Use a dictionary to group by column.
- Sum or aggregate values per group.
- Display results.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
import csv
import io

# Problem 1
data = "Name,Age\nAlice,25\nBob,30"
f = io.StringIO(data)
reader = csv.reader(f)
for row in reader:
    print(row)

# Problem 2
data = "Name,Age,Salary\nAlice,35,60000\nBob,28,50000\nCarol,32,75000"
f = io.StringIO(data)
reader = csv.reader(f)
next(reader)
for row in reader:
    age = int(row[1])
    if age > 30:
        print(f"{row[0]}: ${row[2]}")

# Problem 3
data = """Product,Category,Sales
Widget,A,100
Gadget,B,150
Widget,A,120
Gadget,B,140"""

f = io.StringIO(data)
reader = csv.reader(f)
next(reader)

totals = {}
for row in reader:
    category = row[1]
    sales = int(row[2])
    totals[category] = totals.get(category, 0) + sales

for cat in sorted(totals.keys()):
    print(f"{cat}: {totals[cat]}")
```

</details>
