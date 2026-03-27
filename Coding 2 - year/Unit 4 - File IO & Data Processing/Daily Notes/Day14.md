# Day 14: CSV DictReader & DictWriter
**Learning Target:** I can use DictReader and DictWriter to work with CSV files as dictionaries, making it easier to access fields by name.

### Key Concepts

**DictReader:** Reads CSV files and returns each row as an OrderedDict (or dict) with column names as keys.

**DictWriter:** Writes dictionaries to CSV format, automatically handling column names.

**Advantages over reader/writer:** Access fields by name instead of index; more readable code.

**Fieldnames:** Header row that defines column names for DictWriter.

**Accessing fields:** Use `row['ColumnName']` instead of `row[index]`.

**Easier data manipulation:** Dictionaries are often easier to work with than lists.

### Code Examples

```python
import csv
import io

# Example 1: Basic DictReader
csv_content = """Name,Age,Score
Alice,25,95
Bob,23,87
Charlie,24,92"""

f = io.StringIO(csv_content)
reader = csv.DictReader(f)
for row in reader:
    print(row)  # Each row is a dict

# Example 2: Accessing specific fields by name
f = io.StringIO(csv_content)
reader = csv.DictReader(f)
for row in reader:
    name = row['Name']
    score = row['Score']
    print(f"{name}: {score}")

# Example 3: Basic DictWriter
output = io.StringIO()
fieldnames = ['Name', 'Age', 'Score']
writer = csv.DictWriter(output, fieldnames=fieldnames)

writer.writeheader()
writer.writerow({'Name': 'Alice', 'Age': '25', 'Score': '95'})
writer.writerow({'Name': 'Bob', 'Age': '23', 'Score': '87'})

print(output.getvalue())

# Example 4: Writing multiple rows with DictWriter
output = io.StringIO()
fieldnames = ['Name', 'Age', 'Score']
writer = csv.DictWriter(output, fieldnames=fieldnames)

writer.writeheader()
rows = [
    {'Name': 'Alice', 'Age': '25', 'Score': '95'},
    {'Name': 'Bob', 'Age': '23', 'Score': '87'},
    {'Name': 'Charlie', 'Age': '24', 'Score': '92'}
]
writer.writerows(rows)

print(output.getvalue())

# Example 5: Converting DictReader data to a list
f = io.StringIO(csv_content)
reader = csv.DictReader(f)
records = list(reader)

for record in records:
    print(f"{record['Name']}: {record['Score']}")

# Example 6: Filtering with DictReader
f = io.StringIO(csv_content)
reader = csv.DictReader(f)

for row in reader:
    score = int(row['Score'])
    if score >= 90:
        print(f"{row['Name']}: {score}")

# Example 7: Transforming and writing data
input_data = """Name,Score
Alice,95
Bob,87
Charlie,92"""

input_f = io.StringIO(input_data)
reader = csv.DictReader(input_f)

output = io.StringIO()
fieldnames = ['Name', 'Score', 'Grade']
writer = csv.DictWriter(output, fieldnames=fieldnames)

writer.writeheader()
for row in reader:
    score = int(row['Score'])
    grade = 'A' if score >= 90 else 'B' if score >= 80 else 'C'
    writer.writerow({
        'Name': row['Name'],
        'Score': row['Score'],
        'Grade': grade
    })

print(output.getvalue())

# Example 8: Working with dictionaries from DictReader
f = io.StringIO(csv_content)
reader = csv.DictReader(f)

students = []
for row in reader:
    students.append({
        'name': row['Name'].lower(),
        'age': int(row['Age']),
        'score': int(row['Score'])
    })

for student in students:
    print(student)

# Example 9: DictReader with custom fieldnames
data_no_header = """Alice,25,95
Bob,23,87"""

f = io.StringIO(data_no_header)
fieldnames = ['Name', 'Age', 'Score']
reader = csv.DictReader(f, fieldnames=fieldnames)

for row in reader:
    print(row)

# Example 10: Filtering and writing filtered results
input_csv = """Name,Department,Salary
Alice,Sales,60000
Bob,Engineering,80000
Charlie,Sales,55000
Diana,Engineering,85000"""

input_f = io.StringIO(input_csv)
reader = csv.DictReader(input_f)

output = io.StringIO()
writer = csv.DictWriter(output, fieldnames=['Name', 'Department', 'Salary'])
writer.writeheader()

for row in reader:
    salary = int(row['Salary'])
    if salary > 60000:
        writer.writerow(row)

print(output.getvalue())
```

### Guided Practice

**Activity: Transform CSV Data**

1. Read a CSV file with Name and Score
2. Add a new column calculating the Grade (A for 90+, B for 80+, C otherwise)
3. Write to a new CSV with Name, Score, Grade

**Step-by-step code:**
```python
import csv
import io

input_data = """Name,Score
Alice,95
Bob,87
Charlie,92
Diana,78"""

# Read with DictReader
input_f = io.StringIO(input_data)
reader = csv.DictReader(input_f)

# Write with DictWriter
output = io.StringIO()
fieldnames = ['Name', 'Score', 'Grade']
writer = csv.DictWriter(output, fieldnames=fieldnames)

writer.writeheader()
for row in reader:
    score = int(row['Score'])
    grade = 'A' if score >= 90 else 'B' if score >= 80 else 'C'
    writer.writerow({
        'Name': row['Name'],
        'Score': row['Score'],
        'Grade': grade
    })

print(output.getvalue())
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that uses DictReader to read CSV data and print each row with field names.

**Problem 2 — Intermediate:** Write a program that reads CSV with Name/Age/City, filters for age > 25, and writes results using DictWriter.

**Problem 3 — Challenge:** Write a program that reads two CSV files (students and grades) and joins them, writing a combined output.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use csv.DictReader on a StringIO.
- Loop through reader.
- Print each row (dict).

**Problem 2:**
- Use DictReader to read.
- Filter based on age.
- Use DictWriter with same fieldnames.

**Problem 3:**
- Read both CSVs into lists of dicts.
- Match rows by a key (student ID or name).
- Combine matching records.
- Write combined output.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
import csv
import io

# Problem 1
data = "Name,Age\nAlice,25\nBob,30"
f = io.StringIO(data)
reader = csv.DictReader(f)
for row in reader:
    print(row)

# Problem 2
input_data = "Name,Age,City\nAlice,35,NYC\nBob,28,LA\nCarol,32,Chicago"
input_f = io.StringIO(input_data)
reader = csv.DictReader(input_f)

output = io.StringIO()
writer = csv.DictWriter(output, fieldnames=['Name', 'Age', 'City'])
writer.writeheader()

for row in reader:
    if int(row['Age']) > 25:
        writer.writerow(row)

print(output.getvalue())

# Problem 3
students_data = "ID,Name\n1,Alice\n2,Bob"
grades_data = "ID,Grade\n1,A\n2,B"

students_f = io.StringIO(students_data)
grades_f = io.StringIO(grades_data)

students_reader = csv.DictReader(students_f)
students = {row['ID']: row for row in students_reader}

grades_reader = csv.DictReader(grades_f)
grades = {row['ID']: row for row in grades_reader}

output = io.StringIO()
writer = csv.DictWriter(output, fieldnames=['ID', 'Name', 'Grade'])
writer.writeheader()

for student_id, student in students.items():
    grade = grades.get(student_id, {}).get('Grade', 'N/A')
    writer.writerow({'ID': student_id, 'Name': student['Name'], 'Grade': grade})

print(output.getvalue())
```

</details>
