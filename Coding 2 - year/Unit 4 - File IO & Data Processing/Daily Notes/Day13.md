# Day 13: CSV Files — Writing with csv.writer
**Learning Target:** I can write CSV files using the csv.writer module to save tabular data.

### Key Concepts

**csv.writer:** A module function that creates a CSV writer object for writing data to CSV format.

**Writerow vs writerows:** `writerow()` writes a single row; `writerows()` writes multiple rows.

**Proper CSV format:** The writer handles formatting, including quoting fields with special characters.

**File modes:** Use `'w'` to create/overwrite, `'a'` to append.

**with statement:** Always use for proper file closure.

**CSV dialects:** You can specify formatting rules (quoting, delimiters, etc.).

### Code Examples

```python
import csv
import io

# Example 1: Basic CSV writing
output = io.StringIO()
writer = csv.writer(output)
writer.writerow(['Name', 'Age', 'Score'])
writer.writerow(['Alice', '25', '95'])
writer.writerow(['Bob', '23', '87'])

csv_text = output.getvalue()
print(csv_text)

# Example 2: Writing multiple rows with writerows
output = io.StringIO()
writer = csv.writer(output)
rows = [
    ['Name', 'Age', 'Score'],
    ['Alice', '25', '95'],
    ['Bob', '23', '87'],
    ['Charlie', '24', '92']
]
writer.writerows(rows)
print(output.getvalue())

# Example 3: Converting list of lists to CSV
output = io.StringIO()
writer = csv.writer(output)
data = [
    ['Product', 'Category', 'Price'],
    ['Widget', 'Hardware', '19.99'],
    ['Gadget', 'Electronics', '29.99']
]
writer.writerows(data)
print(output.getvalue())

# Example 4: Writing with different delimiter
output = io.StringIO()
writer = csv.writer(output, delimiter='\t')
writer.writerow(['Name', 'Age', 'Score'])
writer.writerow(['Alice', '25', '95'])
print(output.getvalue())

# Example 5: Handling fields with commas
output = io.StringIO()
writer = csv.writer(output)
writer.writerow(['Product', 'Description', 'Price'])
writer.writerow(['Item A', 'Great product, highly recommended', '19.99'])
print(output.getvalue())

# Example 6: Writing dictionary data as CSV
output = io.StringIO()
writer = csv.writer(output)

students = [
    {'name': 'Alice', 'age': 25, 'score': 95},
    {'name': 'Bob', 'age': 23, 'score': 87}
]

writer.writerow(['name', 'age', 'score'])
for student in students:
    writer.writerow([student['name'], student['age'], student['score']])

print(output.getvalue())

# Example 7: Appending to existing CSV data
output = io.StringIO()
writer = csv.writer(output)
writer.writerow(['Name', 'Score'])
writer.writerow(['Alice', '95'])
writer.writerow(['Bob', '87'])

initial = output.getvalue()

output2 = io.StringIO()
writer2 = csv.writer(output2)
writer2.writerow(['Charlie', '92'])

final = initial + output2.getvalue()
print(final)

# Example 8: Building CSV from user input simulation
output = io.StringIO()
writer = csv.writer(output)
writer.writerow(['Name', 'Email', 'Phone'])

contacts = [
    ('Alice', 'alice@example.com', '555-1234'),
    ('Bob', 'bob@example.com', '555-5678'),
]

writer.writerows(contacts)
print(output.getvalue())

# Example 9: Quote handling
output = io.StringIO()
writer = csv.writer(output, quoting=csv.QUOTE_ALL)
writer.writerow(['Name', 'Description'])
writer.writerow(['Item', 'Product with "quotes"'])
print(output.getvalue())

# Example 10: Writing with error handling
def write_csv_safe(data, output_var):
    try:
        writer = csv.writer(output_var)
        for row in data:
            # Ensure all fields are strings
            string_row = [str(item) for item in row]
            writer.writerow(string_row)
        return True
    except Exception as e:
        print(f"Error writing CSV: {e}")
        return False

output = io.StringIO()
data = [['Name', 'Age'], ['Alice', 25], ['Bob', 30]]
if write_csv_safe(data, output):
    print(output.getvalue())
```

### Guided Practice

**Activity: Create a Student Records CSV**

1. Create a program that:
   - Stores student data (name, age, grade, gpa)
   - Uses csv.writer to create a CSV file
   - Writes header and 5 student records
   - Reads back the file to verify

**Step-by-step code:**
```python
import csv
import io

# Create data
header = ['Name', 'Age', 'Grade', 'GPA']
students = [
    ['Alice', '18', 'A', '3.9'],
    ['Bob', '19', 'B', '3.5'],
    ['Charlie', '18', 'A', '3.8'],
    ['Diana', '20', 'A', '3.95'],
    ['Eve', '19', 'B', '3.4']
]

# Write to CSV
output = io.StringIO()
writer = csv.writer(output)
writer.writerow(header)
writer.writerows(students)

csv_content = output.getvalue()
print("CSV Content:")
print(csv_content)

# Verify by reading back
import io
f = io.StringIO(csv_content)
reader = csv.reader(f)
print("\nVerification (reading back):")
for row in reader:
    print(row)
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that creates a CSV with 3 rows of data (Name, Age) and displays the output.

**Problem 2 — Intermediate:** Write a program that converts a list of dictionaries to CSV format using csv.writer.

**Problem 3 — Challenge:** Write a program that reads CSV data, filters it (e.g., scores > 85), and writes the filtered results to a new CSV.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Create a StringIO object.
- Use csv.writer() to create a writer.
- Use writerow() for each row.
- Print the result with .getvalue().

**Problem 2:**
- Get the keys from the first dictionary for the header.
- Use writerow() for header.
- Loop through dictionaries and writerow() each.

**Problem 3:**
- Read original CSV with csv.reader.
- Filter rows based on condition.
- Write filtered rows with csv.writer.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
import csv
import io

# Problem 1
output = io.StringIO()
writer = csv.writer(output)
writer.writerow(['Name', 'Age'])
writer.writerow(['Alice', '25'])
writer.writerow(['Bob', '30'])
print(output.getvalue())

# Problem 2
data = [
    {'name': 'Alice', 'city': 'NYC'},
    {'name': 'Bob', 'city': 'LA'}
]

output = io.StringIO()
writer = csv.writer(output)
writer.writerow(data[0].keys())
for item in data:
    writer.writerow(item.values())
print(output.getvalue())

# Problem 3
input_data = """Name,Score
Alice,95
Bob,80
Charlie,92"""

filtered = io.StringIO()
writer = csv.writer(filtered)

f = io.StringIO(input_data)
reader = csv.reader(f)
header = next(reader)
writer.writerow(header)

for row in reader:
    score = int(row[1])
    if score > 85:
        writer.writerow(row)

print(filtered.getvalue())
```

</details>
