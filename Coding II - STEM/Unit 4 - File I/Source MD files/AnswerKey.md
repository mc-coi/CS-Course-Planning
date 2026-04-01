# Unit 4 - File I/O & Data Processing: Answer Key

## Problem 1: Open and read a file

### Solution
```python
# Open and read a file
try:
    with open("data.txt", "r") as file:
        # Read entire file content
        content = file.read()
        print(content)
except FileNotFoundError:
    print("File not found!")

# Alternative: read with error handling
filename = "data.txt"
try:
    f = open(filename, "r")
    content = f.read()
    print(content)
    f.close()
except FileNotFoundError:
    print(f"Error: {filename} not found")
```

### Expected Output
```
(Contents of data.txt file)
```

### Common Mistakes
- Not closing the file (should use with statement)
- Not handling FileNotFoundError exception
- Using absolute paths when relative paths should be used

---

## Problem 2: Write text to a file

### Solution
```python
# Write text to a file
filename = "output.txt"

# Writing mode 'w' (overwrites existing content)
with open(filename, "w") as file:
    file.write("Hello, World!\n")
    file.write("This is line 2\n")
    file.write("This is line 3\n")

print(f"Data written to {filename}")

# Verify by reading back
with open(filename, "r") as file:
    print("\nFile contents:")
    print(file.read())

# Append mode 'a' (adds to existing content)
with open(filename, "a") as file:
    file.write("This line is appended\n")

print("\nAfter appending:")
with open(filename, "r") as file:
    print(file.read())
```

### Expected Output
```
Data written to output.txt

File contents:
Hello, World!
This is line 2
This is line 3

After appending:
Hello, World!
This is line 2
This is line 3
This line is appended
```

### Common Mistakes
- Using 'w' mode when 'a' (append) is intended
- Not including '\n' for newlines
- Forgetting to close the file

---

## Problem 3: Read and print each line of a file

### Solution
```python
# Create a sample file
with open("lines.txt", "w") as file:
    file.write("Line 1: Introduction\n")
    file.write("Line 2: Development\n")
    file.write("Line 3: Conclusion\n")

# Method 1: Using readline() in a loop
print("Method 1: readline()")
with open("lines.txt", "r") as file:
    line = file.readline()
    while line:
        print(line.rstrip())  # rstrip removes trailing newline
        line = file.readline()

# Method 2: Using readlines() (most Pythonic)
print("\nMethod 2: for loop with file object")
with open("lines.txt", "r") as file:
    for line in file:
        print(line.rstrip())

# Method 3: Using readlines()
print("\nMethod 3: readlines()")
with open("lines.txt", "r") as file:
    lines = file.readlines()
    for line in lines:
        print(line.rstrip())

# Method 4: With line numbers
print("\nMethod 4: with line numbers")
with open("lines.txt", "r") as file:
    for i, line in enumerate(file, 1):
        print(f"{i}: {line.rstrip()}")
```

### Expected Output
```
Method 1: readline()
Line 1: Introduction
Line 2: Development
Line 3: Conclusion

Method 2: for loop with file object
Line 1: Introduction
Line 2: Development
Line 3: Conclusion

Method 3: readlines()
Line 1: Introduction
Line 2: Development
Line 3: Conclusion

Method 4: with line numbers
1: Line 1: Introduction
2: Line 2: Development
3: Line 3: Conclusion
```

### Common Mistakes
- Including '\n' in output (should strip it)
- Not closing file after reading
- Not handling empty files properly

---

## Problem 4: Read CSV and process rows

### Solution
```python
import csv

# Create a sample CSV file
with open("students.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Grade", "Score"])
    writer.writerow(["Alice", 11, 95])
    writer.writerow(["Bob", 10, 87])
    writer.writerow(["Charlie", 11, 92])
    writer.writerow(["Diana", 10, 89])

# Method 1: Using csv.reader
print("Method 1: csv.reader")
with open("students.csv", "r") as file:
    reader = csv.reader(file)
    header = next(reader)
    print(f"Header: {header}")
    for row in reader:
        name, grade, score = row
        print(f"{name}: Grade {grade}, Score {score}")

# Method 2: Using csv.DictReader (cleaner)
print("\nMethod 2: csv.DictReader")
with open("students.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(f"{row['Name']}: {row['Score']} points")

# Method 3: Filtering data
print("\nMethod 3: Filter high scorers (>90)")
with open("students.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        if int(row['Score']) > 90:
            print(f"{row['Name']}: {row['Score']}")

# Method 4: Calculate statistics
print("\nMethod 4: Statistics")
with open("students.csv", "r") as file:
    reader = csv.DictReader(file)
    scores = [int(row['Score']) for row in reader]
    print(f"Average: {sum(scores) / len(scores):.2f}")
    print(f"Highest: {max(scores)}")
    print(f"Lowest: {min(scores)}")
```

### Expected Output
```
Method 1: csv.reader
Header: ['Name', 'Grade', 'Score']
Alice: Grade 11, Score 95
Bob: Grade 10, Score 87
Charlie: Grade 11, Score 92
Diana: Grade 10, Score 89

Method 2: csv.DictReader
Alice: 95 points
Bob: 87 points
Charlie: 92 points
Diana: 89 points

Method 3: Filter high scorers (>90)
Alice: 95
Charlie: 92

Method 4: Statistics
Average: 90.75
Highest: 95
Lowest: 87
```

### Common Mistakes
- Forgetting newline="" in open() for CSV writing
- Not converting string values to int/float when needed
- Not handling header row separately if using csv.reader

---

## Problem 5: Write CSV from data

### Solution
```python
import csv

# Data to write
students = [
    {"name": "Alice", "math": 95, "english": 92, "science": 88},
    {"name": "Bob", "math": 87, "english": 90, "science": 85},
    {"name": "Charlie", "math": 92, "english": 88, "science": 91},
    {"name": "Diana", "math": 89, "english": 94, "science": 93}
]

# Method 1: Using csv.writer
print("Writing CSV with csv.writer...")
with open("grades.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Math", "English", "Science"])
    for student in students:
        writer.writerow([student["name"], student["math"],
                        student["english"], student["science"]])

print("✓ grades.csv created")

# Verify
with open("grades.csv", "r") as file:
    print("\nFile contents:")
    print(file.read())

# Method 2: Using csv.DictWriter
print("\nWriting CSV with csv.DictWriter...")
with open("grades2.csv", "w", newline="") as file:
    fieldnames = ["name", "math", "english", "science"]
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(students)

print("✓ grades2.csv created")

# Method 3: Calculate and write statistics
print("\nWriting grades with averages...")
with open("grades_with_avg.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Math", "English", "Science", "Average"])

    for student in students:
        scores = [student["math"], student["english"], student["science"]]
        average = sum(scores) / len(scores)
        writer.writerow([student["name"], student["math"],
                        student["english"], student["science"],
                        f"{average:.2f}"])

print("✓ grades_with_avg.csv created")

with open("grades_with_avg.csv", "r") as file:
    print("\nFile with averages:")
    print(file.read())
```

### Expected Output
```
Writing CSV with csv.writer...
✓ grades.csv created

File contents:
Name,Math,English,Science
Alice,95,92,88
Bob,87,90,85
Charlie,92,88,91
Diana,89,94,93

Writing CSV with csv.DictWriter...
✓ grades2.csv created

Writing grades with averages...
✓ grades_with_avg.csv created

File with averages:
Name,Math,English,Science,Average
Alice,95,92,88,91.67
Bob,87,90,85,87.33
Charlie,92,88,91,90.33
Diana,89,94,93,92.00
```

### Common Mistakes
- Forgetting newline="" parameter
- Not quoting fields that might contain commas
- Incorrect field ordering

---

## Problem 6: Handle FileNotFoundError

### Solution
```python
# Handling FileNotFoundError
def read_file_safe(filename):
    """Read file with error handling"""
    try:
        with open(filename, "r") as file:
            return file.read()
    except FileNotFoundError:
        print(f"Error: File '{filename}' not found")
        return None
    except IOError:
        print(f"Error: Cannot read file '{filename}'")
        return None

# Test with non-existent file
print("Attempting to read non-existent file...")
content = read_file_safe("nonexistent.txt")

# Handling multiple file operations
def process_multiple_files(filenames):
    """Process multiple files with error handling"""
    results = {}

    for filename in filenames:
        try:
            with open(filename, "r") as file:
                results[filename] = file.read()
                print(f"✓ Successfully read {filename}")
        except FileNotFoundError:
            print(f"✗ File not found: {filename}")
            results[filename] = None
        except Exception as e:
            print(f"✗ Error reading {filename}: {e}")
            results[filename] = None

    return results

# Test with multiple files
files_to_read = ["existing.txt", "missing.txt", "also_missing.txt"]

# Create one file for testing
with open("existing.txt", "w") as f:
    f.write("This file exists")

print("\nProcessing multiple files...")
results = process_multiple_files(files_to_read)

# Robust file handling with fallback
def read_with_fallback(primary, fallback):
    """Try to read primary file, fall back to backup"""
    try:
        with open(primary, "r") as file:
            return file.read()
    except FileNotFoundError:
        print(f"Primary file '{primary}' not found, trying fallback...")
        try:
            with open(fallback, "r") as file:
                return file.read()
        except FileNotFoundError:
            print(f"Fallback file '{fallback}' also not found")
            return None

print("\nFallback mechanism:")
content = read_with_fallback("missing.txt", "existing.txt")
if content:
    print(f"Successfully read: {content}")
```

### Expected Output
```
Attempting to read non-existent file...
Error: File 'nonexistent.txt' not found

Processing multiple files...
✓ Successfully read existing.txt
✗ File not found: missing.txt
✗ File not found: also_missing.txt

Fallback mechanism:
Primary file 'missing.txt' not found, trying fallback...
✓ Successfully read: This file exists
```

### Common Mistakes
- Not catching FileNotFoundError specifically
- Not using try-except blocks
- Not providing user-friendly error messages

---

## Problem 7: Parse JSON file

### Solution
```python
import json

# Create a sample JSON file
data = {
    "students": [
        {"id": 1, "name": "Alice", "major": "CS", "gpa": 3.8},
        {"id": 2, "name": "Bob", "major": "Physics", "gpa": 3.6},
        {"id": 3, "name": "Charlie", "major": "CS", "gpa": 3.9}
    ],
    "university": "Tech University",
    "year": 2024
}

# Write JSON to file
with open("students.json", "w") as file:
    json.dump(data, file, indent=2)

print("JSON file created\n")

# Method 1: Read and parse JSON
print("Method 1: Basic JSON parsing")
with open("students.json", "r") as file:
    loaded_data = json.load(file)
    print(f"University: {loaded_data['university']}")
    print(f"Year: {loaded_data['year']}")

# Method 2: Access nested data
print("\nMethod 2: Access nested data")
with open("students.json", "r") as file:
    data = json.load(file)
    for student in data['students']:
        print(f"{student['name']}: {student['major']} (GPA: {student['gpa']})")

# Method 3: Filter data
print("\nMethod 3: Filter CS majors")
with open("students.json", "r") as file:
    data = json.load(file)
    cs_students = [s for s in data['students'] if s['major'] == 'CS']
    for student in cs_students:
        print(f"  {student['name']}: {student['gpa']}")

# Method 4: Error handling
print("\nMethod 4: JSON parsing with error handling")
def load_json_safe(filename):
    try:
        with open(filename, "r") as file:
            return json.load(file)
    except FileNotFoundError:
        print(f"File not found: {filename}")
        return None
    except json.JSONDecodeError:
        print(f"Invalid JSON in {filename}")
        return None

data = load_json_safe("students.json")
if data:
    print(f"✓ Successfully loaded {len(data['students'])} students")

# Method 5: Pretty print JSON
print("\nMethod 5: Pretty print JSON")
with open("students.json", "r") as file:
    data = json.load(file)
    print(json.dumps(data, indent=2))
```

### Expected Output
```
JSON file created

Method 1: Basic JSON parsing
University: Tech University
Year: 2024

Method 2: Access nested data
Alice: CS (GPA: 3.8)
Bob: Physics (GPA: 3.6)
Charlie: CS (GPA: 3.9)

Method 3: Filter CS majors
  Alice: 3.8
  Charlie: 3.9

Method 4: JSON parsing with error handling
✓ Successfully loaded 3 students

Method 5: Pretty print JSON
{
  "students": [
    {
      "id": 1,
      "name": "Alice",
      "major": "CS",
      "gpa": 3.8
    },
    {
      "id": 2,
      "name": "Bob",
      "major": "Physics",
      "gpa": 3.6
    },
    {
      "id": 3,
      "name": "Charlie",
      "major": "CS",
      "gpa": 3.9
    }
  ],
  "university": "Tech University",
  "year": 2024
}
```

### Common Mistakes
- Using json.loads() (string) instead of json.load() (file)
- Not handling JSONDecodeError for malformed JSON
- Not using indent parameter when saving for readability

---

## Problem 8: Read CSV, filter, and write results

### Solution
```python
import csv

# Create sample CSV data
with open("sales.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Date", "Product", "Category", "Quantity", "Price", "Total"])
    writer.writerow(["2024-01-01", "Laptop", "Electronics", 2, 999.99, 1999.98])
    writer.writerow(["2024-01-02", "Mouse", "Electronics", 10, 29.99, 299.90])
    writer.writerow(["2024-01-03", "Desk", "Furniture", 1, 299.99, 299.99])
    writer.writerow(["2024-01-04", "Chair", "Furniture", 3, 149.99, 449.97])
    writer.writerow(["2024-01-05", "Monitor", "Electronics", 4, 299.99, 1199.96])
    writer.writerow(["2024-01-06", "Keyboard", "Electronics", 5, 79.99, 399.95])

# Read and filter
print("Reading and filtering CSV data...\n")

# Filter 1: Only Electronics category with Total > 500
print("Filter 1: Electronics with Total > $500")
high_value_electronics = []

with open("sales.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        if row['Category'] == 'Electronics' and float(row['Total']) > 500:
            high_value_electronics.append(row)
            print(f"  {row['Product']}: ${row['Total']}")

# Filter 2: All sales above average
print("\nFilter 2: Sales above average")
with open("sales.csv", "r") as file:
    reader = csv.DictReader(file)
    rows = list(reader)
    avg_total = sum(float(row['Total']) for row in rows) / len(rows)
    print(f"  Average sale: ${avg_total:.2f}")

    above_avg = [r for r in rows if float(r['Total']) > avg_total]
    for row in above_avg:
        print(f"  {row['Product']}: ${row['Total']}")

# Write filtered results
print("\nWriting filtered results...")

# Write high-value electronics to new file
with open("high_value_sales.csv", "w", newline="") as file:
    if high_value_electronics:
        fieldnames = high_value_electronics[0].keys()
        writer = csv.DictWriter(file, fieldnames=fieldnames)
        writer.writeheader()
        writer.writerows(high_value_electronics)
        print(f"✓ Wrote {len(high_value_electronics)} high-value sales")

# Write sales summary by category
print("\nCategory summary...")
category_totals = {}

with open("sales.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        cat = row['Category']
        total = float(row['Total'])
        if cat not in category_totals:
            category_totals[cat] = 0
        category_totals[cat] += total

with open("category_summary.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Category", "Total Sales"])
    for category, total in sorted(category_totals.items()):
        writer.writerow([category, f"${total:.2f}"])
        print(f"  {category}: ${total:.2f}")

print("\n✓ Summary written to category_summary.csv")
```

### Expected Output
```
Reading and filtering CSV data...

Filter 1: Electronics with Total > $500
  Laptop: $1999.98
  Monitor: $1199.96

Filter 2: Sales above average
  Average sale: $874.95
  Laptop: $1999.98
  Monitor: $1199.96

Writing filtered results...
✓ Wrote 2 high-value sales

Category summary...
  Electronics: $3899.79
  Furniture: $749.96

✓ Summary written to category_summary.csv
```

### Common Mistakes
- Not converting string values to float for numeric comparisons
- Not handling file I/O with proper newline="" for CSV
- Not resetting file pointer after reading (need new with block)

---

## Problem 9: Create custom exceptions for validation

### Solution
```python
# Define custom exceptions
class ValidationError(Exception):
    """Base class for validation errors"""
    pass

class InvalidAgeError(ValidationError):
    """Raised when age is invalid"""
    pass

class InvalidEmailError(ValidationError):
    """Raised when email format is invalid"""
    pass

class InvalidGPAError(ValidationError):
    """Raised when GPA is invalid"""
    pass

class MissingFieldError(ValidationError):
    """Raised when required field is missing"""
    pass

# Validation functions
def validate_age(age):
    """Validate age is between 0 and 150"""
    if not isinstance(age, int):
        raise InvalidAgeError("Age must be an integer")
    if age < 0 or age > 150:
        raise InvalidAgeError(f"Age must be between 0 and 150, got {age}")
    return True

def validate_email(email):
    """Validate email format"""
    if '@' not in email or '.' not in email:
        raise InvalidEmailError(f"Invalid email format: {email}")
    return True

def validate_gpa(gpa):
    """Validate GPA is between 0 and 4.0"""
    if not isinstance(gpa, (int, float)):
        raise InvalidGPAError("GPA must be a number")
    if gpa < 0 or gpa > 4.0:
        raise InvalidGPAError(f"GPA must be between 0 and 4.0, got {gpa}")
    return True

def validate_student(data):
    """Validate student record"""
    required_fields = ['name', 'age', 'email', 'gpa']

    # Check required fields
    for field in required_fields:
        if field not in data:
            raise MissingFieldError(f"Required field missing: {field}")

    # Validate each field
    if not data['name'].strip():
        raise MissingFieldError("Name cannot be empty")

    validate_age(data['age'])
    validate_email(data['email'])
    validate_gpa(data['gpa'])

    return True

# Test validation
test_records = [
    {"name": "Alice", "age": 20, "email": "alice@example.com", "gpa": 3.8},  # Valid
    {"name": "Bob", "age": 25, "email": "bob@example.com", "gpa": 3.5},  # Valid
    {"name": "Charlie", "age": -5, "email": "charlie@example.com", "gpa": 3.7},  # Invalid age
    {"name": "Diana", "age": 22, "email": "invalid-email", "gpa": 3.9},  # Invalid email
    {"name": "Eve", "age": 21, "email": "eve@example.com", "gpa": 4.5},  # Invalid GPA
    {"age": 20, "email": "frank@example.com", "gpa": 3.6},  # Missing name
]

print("Validating student records...\n")
valid_students = []

for i, record in enumerate(test_records, 1):
    try:
        validate_student(record)
        print(f"✓ Record {i}: Valid - {record.get('name', 'Unknown')}")
        valid_students.append(record)
    except InvalidAgeError as e:
        print(f"✗ Record {i}: {e}")
    except InvalidEmailError as e:
        print(f"✗ Record {i}: {e}")
    except InvalidGPAError as e:
        print(f"✗ Record {i}: {e}")
    except MissingFieldError as e:
        print(f"✗ Record {i}: {e}")
    except ValidationError as e:
        print(f"✗ Record {i}: Validation error - {e}")

print(f"\n✓ {len(valid_students)} valid records out of {len(test_records)}")

# Save valid records
import csv
if valid_students:
    with open("validated_students.csv", "w", newline="") as file:
        writer = csv.DictWriter(file, fieldnames=['name', 'age', 'email', 'gpa'])
        writer.writeheader()
        writer.writerows(valid_students)
    print("✓ Valid records saved to validated_students.csv")
```

### Expected Output
```
Validating student records...

✓ Record 1: Valid - Alice
✓ Record 2: Valid - Bob
✗ Record 3: Age must be between 0 and 150, got -5
✗ Record 4: Invalid email format: invalid-email
✗ Record 5: GPA must be between 0 and 4.0, got 4.5
✗ Record 6: Required field missing: name

✓ 2 valid records out of 6
✓ Valid records saved to validated_students.csv
```

### Common Mistakes
- Not creating a base exception class
- Not validating all required fields
- Not providing informative error messages

---

## Problem 10: Build data cleaning pipeline

### Solution
```python
import csv
import re
from datetime import datetime

# Create messy data file
messy_data = [
    ["Date", "Name", "Email", "Age", "Score"],
    ["2024-01-01", "Alice", "alice@example.com", "25", "95.5"],
    ["2024-01-02", "BOB", "bob@email.com", "  30  ", "87.3"],
    ["2024-01-03", "charlie", "charlie", "22", "92.1"],  # Invalid email
    ["2024-01-04", "Diana Smith", "diana@example.com", "28", ""],  # Missing score
    ["2024-01-05", "Eve", "eve@example.com", "abc", "88.9"],  # Invalid age
]

with open("messy.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerows(messy_data)

print("Building data cleaning pipeline...\n")

# Cleaning functions
def clean_name(name):
    """Clean name: strip, title case"""
    return name.strip().title()

def clean_email(email):
    """Clean and validate email"""
    email = email.strip().lower()
    if not re.match(r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$', email):
        return None
    return email

def clean_age(age):
    """Clean and validate age"""
    try:
        age = int(age.strip())
        if 0 <= age <= 120:
            return age
    except (ValueError, AttributeError):
        pass
    return None

def clean_score(score):
    """Clean and validate score"""
    try:
        score = float(score.strip())
        if 0 <= score <= 100:
            return score
    except (ValueError, AttributeError):
        pass
    return None

def clean_date(date_str):
    """Validate date format"""
    try:
        return datetime.strptime(date_str.strip(), '%Y-%m-%d').strftime('%Y-%m-%d')
    except (ValueError, AttributeError):
        return None

# Pipeline
print("Step 1: Reading messy data")
with open("messy.csv", "r") as file:
    reader = csv.DictReader(file)
    raw_data = list(reader)
    print(f"  Read {len(raw_data)} records\n")

print("Step 2: Cleaning data")
cleaned_data = []
errors = []

for i, row in enumerate(raw_data, 1):
    cleaned_row = {}
    row_errors = []

    # Clean each field
    cleaned_row['date'] = clean_date(row['Date'])
    if not cleaned_row['date']:
        row_errors.append(f"Invalid date: {row['Date']}")

    cleaned_row['name'] = clean_name(row['Name'])

    cleaned_row['email'] = clean_email(row['Email'])
    if not cleaned_row['email']:
        row_errors.append(f"Invalid email: {row['Email']}")

    cleaned_row['age'] = clean_age(row['Age'])
    if cleaned_row['age'] is None:
        row_errors.append(f"Invalid age: {row['Age']}")

    cleaned_row['score'] = clean_score(row['Score'])
    if cleaned_row['score'] is None:
        row_errors.append(f"Invalid score: {row['Score']}")

    if row_errors:
        errors.append({'record': i, 'errors': row_errors})
        print(f"  Record {i} ({cleaned_row['name']}): {', '.join(row_errors)}")
    else:
        cleaned_data.append(cleaned_row)
        print(f"  Record {i} ({cleaned_row['name']}): ✓ Clean")

print(f"\nStep 3: Results")
print(f"  Valid records: {len(cleaned_data)}")
print(f"  Invalid records: {len(errors)}\n")

# Save cleaned data
if cleaned_data:
    print("Step 4: Saving cleaned data")
    with open("cleaned.csv", "w", newline="") as file:
        fieldnames = ['date', 'name', 'email', 'age', 'score']
        writer = csv.DictWriter(file, fieldnames=fieldnames)
        writer.writeheader()
        writer.writerows(cleaned_data)
        print(f"  ✓ Saved to cleaned.csv")

# Save error report
if errors:
    print("Step 5: Saving error report")
    with open("cleaning_errors.txt", "w") as file:
        file.write("Data Cleaning Error Report\n")
        file.write("=" * 40 + "\n\n")
        for error in errors:
            file.write(f"Record {error['record']}:\n")
            for err in error['errors']:
                file.write(f"  - {err}\n")
            file.write("\n")
    print(f"  ✓ Saved error report")
```

### Expected Output
```
Building data cleaning pipeline...

Step 1: Reading messy data
  Read 5 records

Step 2: Cleaning data
  Record 1 (Alice): ✓ Clean
  Record 2 (Bob): ✓ Clean
  Record 3 (Charlie): Invalid email: charlie
  Record 4 (Diana Smith): Invalid score:
  Record 5 (Eve): Invalid age: abc

Step 3: Results
  Valid records: 2
  Invalid records: 3

Step 4: Saving cleaned data
  ✓ Saved to cleaned.csv

Step 5: Saving error report
  ✓ Saved error report
```

### Common Mistakes
- Not handling all edge cases (whitespace, case sensitivity)
- Not validating data before using it
- Not reporting which records failed

---

## Problem 11: Generate statistics report from file

### Solution
```python
import csv
from statistics import mean, median, stdev

# Create sample data
with open("test_scores.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Student", "Math", "English", "Science", "History"])
    writer.writerow(["Alice", 95, 92, 88, 91])
    writer.writerow(["Bob", 87, 90, 85, 88])
    writer.writerow(["Charlie", 92, 88, 91, 89])
    writer.writerow(["Diana", 89, 94, 93, 95])
    writer.writerow(["Eve", 88, 91, 87, 86])

print("Generating Statistics Report\n")
print("=" * 50)

# Read data
with open("test_scores.csv", "r") as file:
    reader = csv.DictReader(file)
    students = list(reader)

# Convert numeric values
for student in students:
    student['Math'] = int(student['Math'])
    student['English'] = int(student['English'])
    student['Science'] = int(student['Science'])
    student['History'] = int(student['History'])

# Calculate student statistics
print("\nStudent Individual Statistics:")
print("-" * 50)

for student in students:
    name = student['Student']
    scores = [student['Math'], student['English'],
              student['Science'], student['History']]

    avg = mean(scores)
    max_score = max(scores)
    min_score = min(scores)

    print(f"\n{name}:")
    print(f"  Scores: {scores}")
    print(f"  Average: {avg:.2f}")
    print(f"  Highest: {max_score}")
    print(f"  Lowest: {min_score}")

# Calculate subject statistics
print("\n" + "=" * 50)
print("\nSubject Statistics:")
print("-" * 50)

subjects = ['Math', 'English', 'Science', 'History']
subject_stats = {}

for subject in subjects:
    scores = [student[subject] for student in students]

    avg = mean(scores)
    med = median(scores)
    std = stdev(scores) if len(scores) > 1 else 0
    max_score = max(scores)
    min_score = min(scores)

    subject_stats[subject] = {
        'average': avg,
        'median': med,
        'stdev': std,
        'max': max_score,
        'min': min_score
    }

    print(f"\n{subject}:")
    print(f"  Average: {avg:.2f}")
    print(f"  Median: {med:.2f}")
    print(f"  Std Dev: {std:.2f}")
    print(f"  Range: {min_score}-{max_score}")

# Overall class statistics
print("\n" + "=" * 50)
print("\nClass Overall Statistics:")
print("-" * 50)

all_scores = []
for student in students:
    all_scores.extend([student['Math'], student['English'],
                      student['Science'], student['History']])

print(f"\nTotal scores: {len(all_scores)}")
print(f"Class average: {mean(all_scores):.2f}")
print(f"Class median: {median(all_scores):.2f}")
print(f"Std deviation: {stdev(all_scores):.2f}")
print(f"Highest score: {max(all_scores)}")
print(f"Lowest score: {min(all_scores)}")

# Save report
with open("statistics_report.txt", "w") as file:
    file.write("Test Scores Statistics Report\n")
    file.write("=" * 50 + "\n\n")

    file.write("Subject Statistics:\n")
    file.write("-" * 50 + "\n")
    for subject, stats in subject_stats.items():
        file.write(f"\n{subject}:\n")
        file.write(f"  Average: {stats['average']:.2f}\n")
        file.write(f"  Median: {stats['median']:.2f}\n")
        file.write(f"  Std Dev: {stats['stdev']:.2f}\n")
        file.write(f"  Range: {stats['min']}-{stats['max']}\n")

    file.write("\n" + "=" * 50 + "\n")
    file.write("Class Overall:\n")
    file.write(f"  Average: {mean(all_scores):.2f}\n")
    file.write(f"  Median: {median(all_scores):.2f}\n")
    file.write(f"  Std Dev: {stdev(all_scores):.2f}\n")

print("\n✓ Report saved to statistics_report.txt")
```

### Expected Output
```
Generating Statistics Report

==================================================

Student Individual Statistics:
--------------------------------------------------

Alice:
  Scores: [95, 92, 88, 91]
  Average: 91.50
  Highest: 95
  Lowest: 88

Bob:
  Scores: [87, 90, 85, 88]
  Average: 87.50
  Highest: 90
  Lowest: 85

Charlie:
  Scores: [92, 88, 91, 89]
  Average: 90.00
  Highest: 92
  Lowest: 88

Diana:
  Scores: [89, 94, 93, 95]
  Average: 92.75
  Highest: 95
  Lowest: 89

Eve:
  Scores: [88, 91, 87, 86]
  Average: 88.00
  Highest: 91
  Lowest: 86

==================================================

Subject Statistics:
--------------------------------------------------

Math:
  Average: 90.20
  Median: 89.00
  Std Dev: 3.11
  Range: 87-95

English:
  Average: 91.00
  Median: 91.00
  Std Dev: 2.00
  Range: 88-94

Science:
  Average: 88.80
  Median: 88.00
  Std Dev: 3.35
  Range: 85-93

History:
  Average: 89.80
  Median: 89.00
  Std Dev: 3.70
  Range: 86-95

==================================================

Class Overall Statistics:
--------------------------------------------------

Total scores: 20
Class average: 90.00
Class median: 90.00
Std deviation: 2.74
Highest score: 95
Lowest score: 85

✓ Report saved to statistics_report.txt
```

### Common Mistakes
- Not converting string values to numbers before calculations
- Not handling empty files or missing data
- Dividing by zero when calculating statistics

---

## Problem 12: Merge multiple data files

### Solution
```python
import csv
import os

# Create sample data files
print("Creating sample data files...\n")

# Q1 sales
with open("sales_q1.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Month", "Product", "Quantity", "Revenue"])
    writer.writerow(["January", "Laptop", 5, 4999.95])
    writer.writerow(["February", "Monitor", 8, 2399.92])
    writer.writerow(["March", "Keyboard", 15, 1199.85])

# Q2 sales
with open("sales_q2.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Month", "Product", "Quantity", "Revenue"])
    writer.writerow(["April", "Mouse", 20, 599.80])
    writer.writerow(["May", "Headphones", 12, 1799.88])
    writer.writerow(["June", "Laptop", 8, 7999.92])

# Q3 sales
with open("sales_q3.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Month", "Product", "Quantity", "Revenue"])
    writer.writerow(["July", "Monitor", 6, 1799.94])
    writer.writerow(["August", "Keyboard", 10, 799.90])
    writer.writerow(["September", "Mouse", 18, 539.82])

print("Sample files created.\n")

# Method 1: Simple merge
print("Method 1: Simple merge of all files")
print("=" * 50)

files_to_merge = ["sales_q1.csv", "sales_q2.csv", "sales_q3.csv"]
all_data = []
headers = None

for filename in files_to_merge:
    try:
        with open(filename, "r") as file:
            reader = csv.DictReader(file)
            if headers is None:
                headers = reader.fieldnames
            all_data.extend(list(reader))
            print(f"✓ Read {filename}")
    except FileNotFoundError:
        print(f"✗ {filename} not found")

# Save merged file
if all_data:
    with open("sales_all_quarters.csv", "w", newline="") as file:
        writer = csv.DictWriter(file, fieldnames=headers)
        writer.writeheader()
        writer.writerows(all_data)
    print(f"✓ Merged data saved to sales_all_quarters.csv")
    print(f"  Total records: {len(all_data)}\n")

# Method 2: Merge with aggregation
print("Method 2: Merge with aggregation")
print("=" * 50)

product_totals = {}

for filename in files_to_merge:
    with open(filename, "r") as file:
        reader = csv.DictReader(file)
        for row in reader:
            product = row['Product']
            quantity = int(row['Quantity'])
            revenue = float(row['Revenue'])

            if product not in product_totals:
                product_totals[product] = {'quantity': 0, 'revenue': 0}

            product_totals[product]['quantity'] += quantity
            product_totals[product]['revenue'] += revenue

# Save aggregated report
with open("product_summary.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Product", "Total Quantity", "Total Revenue"])
    for product, data in sorted(product_totals.items()):
        writer.writerow([product, data['quantity'], f"${data['revenue']:.2f}"])

print("\nProduct Summary:")
for product, data in sorted(product_totals.items()):
    print(f"  {product}: {data['quantity']} units, ${data['revenue']:.2f}")

print("\n✓ Product summary saved to product_summary.csv\n")

# Method 3: Merge with data transformation
print("Method 3: Merge with validation and cleaning")
print("=" * 50)

valid_records = []
error_count = 0

for filename in files_to_merge:
    with open(filename, "r") as file:
        reader = csv.DictReader(file)
        for i, row in enumerate(reader, 1):
            try:
                # Validate data
                int(row['Quantity'])
                float(row['Revenue'])
                valid_records.append(row)
            except (ValueError, KeyError):
                error_count += 1
                print(f"✗ {filename} row {i}: Invalid data")

print(f"✓ {len(valid_records)} valid records")
print(f"✗ {error_count} invalid records")

# Clean up temporary files
print("\nCleaning up temporary files...")
for filename in files_to_merge:
    if os.path.exists(filename):
        os.remove(filename)
        print(f"  Deleted {filename}")
```

### Expected Output
```
Creating sample files...

Sample files created.

Method 1: Simple merge of all files
==================================================
✓ Read sales_q1.csv
✓ Read sales_q2.csv
✓ Read sales_q3.csv
✓ Merged data saved to sales_all_quarters.csv
  Total records: 9

Method 2: Merge with aggregation
==================================================

Product Summary:
  Headphones: 12 units, $1799.88
  Keyboard: 25 units, $1999.75
  Laptop: 13 units, $12999.87
  Monitor: 14 units, $4199.86
  Mouse: 38 units, $1139.62

✓ Product summary saved to product_summary.csv

Method 3: Merge with validation and cleaning
==================================================
✓ 9 valid records
✗ 0 invalid records

Cleaning up temporary files...
  Deleted sales_q1.csv
  Deleted sales_q2.csv
  Deleted sales_q3.csv
```

### Common Mistakes
- Not resetting headers/reader between files
- Not validating data while merging
- Not handling missing files gracefully

---

## Problem 13: Create interactive data analyzer

### Solution
```python
import csv

class DataAnalyzer:
    """Interactive data analyzer for CSV files"""

    def __init__(self, filename):
        self.filename = filename
        self.data = []
        self.load_data()

    def load_data(self):
        """Load data from CSV file"""
        try:
            with open(self.filename, "r") as file:
                reader = csv.DictReader(file)
                self.data = list(reader)
                print(f"✓ Loaded {len(self.data)} records\n")
        except FileNotFoundError:
            print(f"✗ File {self.filename} not found")

    def display_menu(self):
        """Display interactive menu"""
        while True:
            print("\n" + "=" * 40)
            print("Data Analyzer Menu")
            print("=" * 40)
            print("1. View summary")
            print("2. Filter data")
            print("3. Search records")
            print("4. Sort data")
            print("5. Export filtered data")
            print("6. Exit")
            print("-" * 40)

            choice = input("Enter choice (1-6): ").strip()

            if choice == "1":
                self.show_summary()
            elif choice == "2":
                self.filter_data()
            elif choice == "3":
                self.search_records()
            elif choice == "4":
                self.sort_data()
            elif choice == "5":
                self.export_data()
            elif choice == "6":
                print("Goodbye!")
                break
            else:
                print("Invalid choice")

    def show_summary(self):
        """Show data summary"""
        if not self.data:
            print("No data to analyze")
            return

        print(f"\nTotal records: {len(self.data)}")
        print(f"Fields: {list(self.data[0].keys())}")
        print("\nFirst 3 records:")
        for i, record in enumerate(self.data[:3], 1):
            print(f"  {i}. {record}")

    def filter_data(self):
        """Filter data by field value"""
        if not self.data:
            return

        fields = list(self.data[0].keys())
        print(f"\nAvailable fields: {fields}")

        field = input("Enter field to filter: ").strip()
        value = input("Enter value to match: ").strip()

        filtered = [r for r in self.data if r.get(field, "") == value]
        print(f"\n✓ Found {len(filtered)} records:")
        for record in filtered:
            print(f"  {record}")

    def search_records(self):
        """Search records by partial match"""
        search_term = input("\nEnter search term: ").strip().lower()

        results = []
        for record in self.data:
            if any(search_term in str(v).lower() for v in record.values()):
                results.append(record)

        print(f"\n✓ Found {len(results)} matching records:")
        for record in results[:5]:
            print(f"  {record}")
        if len(results) > 5:
            print(f"  ... and {len(results) - 5} more")

    def sort_data(self):
        """Sort data by a field"""
        if not self.data:
            return

        fields = list(self.data[0].keys())
        print(f"\nAvailable fields: {fields}")

        field = input("Enter field to sort by: ").strip()
        order = input("Sort order (asc/desc): ").strip().lower()

        try:
            sorted_data = sorted(self.data,
                               key=lambda x: float(x.get(field, 0)),
                               reverse=(order == "desc"))
            print(f"\n✓ Sorted by {field} ({order}):")
            for record in sorted_data[:5]:
                print(f"  {record}")
            if len(sorted_data) > 5:
                print(f"  ... and {len(sorted_data) - 5} more")
        except ValueError:
            print("Cannot sort non-numeric field")

    def export_data(self):
        """Export filtered data to CSV"""
        filename = input("\nEnter output filename: ").strip()

        if not self.data:
            print("No data to export")
            return

        try:
            with open(filename, "w", newline="") as file:
                writer = csv.DictWriter(file, fieldnames=self.data[0].keys())
                writer.writeheader()
                writer.writerows(self.data)
            print(f"✓ Exported {len(self.data)} records to {filename}")
        except Exception as e:
            print(f"✗ Error: {e}")

# Create sample data and run analyzer
with open("products.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Product", "Category", "Price", "Stock"])
    writer.writerow(["Laptop", "Electronics", 999.99, 5])
    writer.writerow(["Mouse", "Electronics", 29.99, 50])
    writer.writerow(["Desk", "Furniture", 299.99, 12])
    writer.writerow(["Chair", "Furniture", 149.99, 20])
    writer.writerow(["Monitor", "Electronics", 299.99, 8])

print("Sample file created: products.csv\n")

# Note: In actual use, this would run interactively
# For demonstration, showing the class structure and methods
analyzer = DataAnalyzer("products.csv")
analyzer.show_summary()
```

### Expected Output
```
Sample file created: products.csv

✓ Loaded 5 records

Total records: 5
Fields: ['Product', 'Category', 'Price', 'Stock']

First 3 records:
  1. {'Product': 'Laptop', 'Category': 'Electronics', 'Price': '999.99', 'Stock': '5'}
  2. {'Product': 'Mouse', 'Category': 'Electronics', 'Price': '29.99', 'Stock': '50'}
  3. {'Product': 'Desk', 'Category': 'Furniture', 'Price': '299.99', 'Stock': '12'}
```

### Common Mistakes
- Not properly validating user input
- Not handling exceptions in interactive menus
- Not properly closing files after operations

---

## Problem 14: Build robust file processor with error handling

### Solution
```python
import csv
import json
import os
from pathlib import Path

class RobustFileProcessor:
    """Robust file processor with comprehensive error handling"""

    def __init__(self, filename):
        self.filename = filename
        self.errors = []
        self.warnings = []

    def add_error(self, error_msg):
        """Log an error"""
        self.errors.append(error_msg)
        print(f"✗ ERROR: {error_msg}")

    def add_warning(self, warning_msg):
        """Log a warning"""
        self.warnings.append(warning_msg)
        print(f"⚠ WARNING: {warning_msg}")

    def file_exists(self):
        """Check if file exists"""
        if not os.path.exists(self.filename):
            self.add_error(f"File not found: {self.filename}")
            return False
        return True

    def file_readable(self):
        """Check if file is readable"""
        if not os.access(self.filename, os.R_OK):
            self.add_error(f"File not readable: {self.filename}")
            return False
        return True

    def get_file_size(self):
        """Get file size in MB"""
        try:
            size_bytes = os.path.getsize(self.filename)
            size_mb = size_bytes / (1024 * 1024)
            return size_mb
        except Exception as e:
            self.add_error(f"Cannot get file size: {e}")
            return None

    def validate_csv(self):
        """Validate CSV file structure"""
        try:
            with open(self.filename, "r", encoding="utf-8") as file:
                reader = csv.reader(file)
                rows = list(reader)

                if not rows:
                    self.add_warning("CSV file is empty")
                    return False

                header_length = len(rows[0])

                for i, row in enumerate(rows[1:], 2):
                    if len(row) != header_length:
                        self.add_warning(f"Row {i} has {len(row)} columns, expected {header_length}")

                print(f"✓ CSV structure valid ({len(rows)} rows)")
                return True

        except Exception as e:
            self.add_error(f"CSV validation failed: {e}")
            return False

    def validate_json(self):
        """Validate JSON file"""
        try:
            with open(self.filename, "r", encoding="utf-8") as file:
                json.load(file)
                print("✓ JSON is valid")
                return True
        except json.JSONDecodeError as e:
            self.add_error(f"Invalid JSON: {e}")
            return False
        except Exception as e:
            self.add_error(f"JSON validation failed: {e}")
            return False

    def process_csv_safe(self):
        """Process CSV with error handling"""
        try:
            valid_rows = 0
            invalid_rows = 0

            with open(self.filename, "r", encoding="utf-8-sig") as file:
                reader = csv.DictReader(file)

                if reader.fieldnames is None:
                    self.add_error("CSV has no header row")
                    return None

                processed_data = []

                for i, row in enumerate(reader, 2):
                    try:
                        # Validate row
                        if not row or all(v == '' for v in row.values()):
                            self.add_warning(f"Row {i} is empty")
                            invalid_rows += 1
                            continue

                        processed_data.append(row)
                        valid_rows += 1

                    except Exception as e:
                        self.add_error(f"Error processing row {i}: {e}")
                        invalid_rows += 1

                print(f"\n✓ Processed {valid_rows} valid rows")
                if invalid_rows > 0:
                    print(f"⚠ Skipped {invalid_rows} invalid rows")

                return processed_data

        except UnicodeDecodeError:
            self.add_error("File encoding error (try different encoding)")
            return None
        except Exception as e:
            self.add_error(f"CSV processing failed: {e}")
            return None

    def generate_report(self):
        """Generate error and warning report"""
        print("\n" + "=" * 50)
        print("Processing Report")
        print("=" * 50)
        print(f"File: {self.filename}")
        print(f"Size: {self.get_file_size():.2f} MB" if self.get_file_size() else "Size: Unknown")
        print(f"Errors: {len(self.errors)}")
        print(f"Warnings: {len(self.warnings)}")

        if self.errors:
            print("\nErrors:")
            for error in self.errors:
                print(f"  - {error}")

        if self.warnings:
            print("\nWarnings:")
            for warning in self.warnings:
                print(f"  - {warning}")

# Test the processor
print("Creating test CSV file...\n")

with open("test_data.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Age", "Email"])
    writer.writerow(["Alice", "25", "alice@example.com"])
    writer.writerow(["Bob", "30", "bob@example.com"])
    writer.writerow(["", "", ""])  # Empty row
    writer.writerow(["Charlie", "invalid", "charlie@example.com"])

print("Test file created\n")

# Process with robust processor
processor = RobustFileProcessor("test_data.csv")

print("Checking file...")
if processor.file_exists() and processor.file_readable():
    print("✓ File exists and is readable\n")

    print("Validating structure...")
    processor.validate_csv()

    print("\nProcessing data...")
    data = processor.process_csv_safe()

    processor.generate_report()
```

### Expected Output
```
Creating test CSV file...

Test file created

Checking file...
✓ File exists and is readable

Validating structure...
✓ CSV structure valid (5 rows)

Processing data...
⚠ WARNING: Row 4 is empty
✓ Processed 3 valid rows
⚠ Skipped 1 invalid rows

==================================================
Processing Report
==================================================
File: test_data.csv
Size: 0.00 MB
Errors: 0
Warnings: 1

Warnings:
  - Row 4 is empty
```

### Common Mistakes
- Not handling different file encodings
- Not validating data structure before processing
- Not providing detailed error messages for debugging

---

## Problem 15: Process and visualize data from files

### Solution
```python
import csv
import matplotlib.pyplot as plt
from statistics import mean

# Create sample sales data
with open("sales_data.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Month", "Sales", "Expenses", "Profit"])
    writer.writerow(["January", 5000, 3000, 2000])
    writer.writerow(["February", 6200, 3500, 2700])
    writer.writerow(["March", 5800, 3200, 2600])
    writer.writerow(["April", 7100, 4000, 3100])
    writer.writerow(["May", 8300, 4500, 3800])
    writer.writerow(["June", 9200, 5000, 4200])

print("Processing and visualizing sales data...\n")

# Read and process data
months = []
sales = []
expenses = []
profits = []

with open("sales_data.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        months.append(row['Month'])
        sales.append(int(row['Sales']))
        expenses.append(int(row['Expenses']))
        profits.append(int(row['Profit']))

# Calculate statistics
print("Sales Statistics:")
print(f"  Average Sales: ${mean(sales):.2f}")
print(f"  Average Expenses: ${mean(expenses):.2f}")
print(f"  Average Profit: ${mean(profits):.2f}")
print(f"  Total Profit: ${sum(profits):.2f}")
print(f"  Best Month: {months[profits.index(max(profits))]} (${max(profits)})")

# Create visualizations
fig, axes = plt.subplots(2, 2, figsize=(12, 10))
fig.suptitle('Sales Analysis Dashboard', fontsize=16, fontweight='bold')

# 1. Sales trend line chart
ax1 = axes[0, 0]
ax1.plot(months, sales, marker='o', color='blue', linewidth=2)
ax1.set_title('Sales Trend')
ax1.set_ylabel('Sales ($)')
ax1.grid(True, alpha=0.3)

# 2. Expenses vs Sales bar chart
ax2 = axes[0, 1]
x_pos = range(len(months))
width = 0.35
ax2.bar([i - width/2 for i in x_pos], sales, width, label='Sales', color='green')
ax2.bar([i + width/2 for i in x_pos], expenses, width, label='Expenses', color='red')
ax2.set_title('Sales vs Expenses')
ax2.set_ylabel('Amount ($)')
ax2.set_xticks(x_pos)
ax2.set_xticklabels(months, rotation=45)
ax2.legend()

# 3. Profit over time
ax3 = axes[1, 0]
colors = ['green' if p > mean(profits) else 'orange' for p in profits]
ax3.bar(months, profits, color=colors)
ax3.axhline(y=mean(profits), color='blue', linestyle='--', label='Average Profit')
ax3.set_title('Monthly Profit')
ax3.set_ylabel('Profit ($)')
ax3.set_xticklabels(months, rotation=45)
ax3.legend()

# 4. Profit margin pie chart
ax4 = axes[1, 1]
profit_margin = [(p/s)*100 for p, s in zip(profits, sales)]
ax4.plot(months, profit_margin, marker='s', color='purple', linewidth=2)
ax4.set_title('Profit Margin Trend')
ax4.set_ylabel('Profit Margin (%)')
ax4.set_xticklabels(months, rotation=45)
ax4.grid(True, alpha=0.3)

plt.tight_layout()
print("\n✓ Chart shows sales trend, expenses comparison, profit analysis, and profit margins")
print("  The line chart displays monthly sales trends")
print("  The bar chart compares sales vs expenses side-by-side")
print("  The profit chart shows monthly profits with average line")
print("  The profit margin chart shows profitability trends over time")

# Save report
with open("sales_report.txt", "w") as file:
    file.write("Sales Analysis Report\n")
    file.write("=" * 40 + "\n\n")
    file.write("Monthly Data:\n")
    file.write(f"{'Month':<12} {'Sales':>10} {'Expenses':>10} {'Profit':>10}\n")
    file.write("-" * 40 + "\n")
    for m, s, e, p in zip(months, sales, expenses, profits):
        file.write(f"{m:<12} ${s:>9} ${e:>9} ${p:>9}\n")
    file.write("\n" + "=" * 40 + "\n")
    file.write(f"Average Sales: ${mean(sales):.2f}\n")
    file.write(f"Average Expenses: ${mean(expenses):.2f}\n")
    file.write(f"Average Profit: ${mean(profits):.2f}\n")
    file.write(f"Total Profit: ${sum(profits):.2f}\n")

print("✓ Report saved to sales_report.txt")
```

### Expected Output
```
Processing and visualizing sales data...

Sales Statistics:
  Average Sales: $7108.33
  Average Expenses: $3866.67
  Average Profit: $3241.67
  Total Profit: $19450.00
  Best Month: June ($4200)

✓ Chart shows sales trend, expenses comparison, profit analysis, and profit margins
  The line chart displays monthly sales trends
  The bar chart compares sales vs expenses side-by-side
  The profit chart shows monthly profits with average line
  The profit margin chart shows profitability trends over time
✓ Report saved to sales_report.txt
```

### Common Mistakes
- Not converting string data to numeric types before processing
- Not setting proper labels and titles on charts
- Not handling missing or empty data values
