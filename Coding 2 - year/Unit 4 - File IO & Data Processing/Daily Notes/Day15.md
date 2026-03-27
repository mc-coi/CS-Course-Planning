# Day 15: CSV Lab — Student Records System
**Learning Target:** I can apply CSV reading/writing skills to build a functional data system.

### Key Concepts

**Complete workflow:** Read input → validate → process → write output.

**Data persistence:** Saving data to CSV for later use.

**CRUD operations:** Create, Read, Update, Delete records.

**Merging files:** Combining data from multiple sources.

**Data integrity:** Ensuring data quality throughout the process.

### Code Examples

```python
import csv
import io

# Example 1: Simple student records system
def create_student_record(name, grade, gpa):
    """Create a new student record"""
    return {'Name': name, 'Grade': grade, 'GPA': gpa}

def add_to_csv(records, new_record):
    """Add a record to existing records"""
    records.append(new_record)
    return records

def write_students_csv(records):
    """Write records to CSV format"""
    output = io.StringIO()
    fieldnames = ['Name', 'Grade', 'GPA']
    writer = csv.DictWriter(output, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(records)
    return output.getvalue()

# Example 2: Reading and updating records
input_csv = """Name,Grade,GPA
Alice,A,3.9
Bob,B,3.5
Charlie,A,3.8"""

def read_students(csv_content):
    """Read students from CSV"""
    f = io.StringIO(csv_content)
    reader = csv.DictReader(f)
    return list(reader)

students = read_students(input_csv)
# Add new student
students.append({'Name': 'Diana', 'Grade': 'A', 'GPA': '3.95'})
output = write_students_csv(students)
print(output)

# Example 3: Filtering and statistics
def get_honors_students(students, min_gpa=3.8):
    """Filter students with GPA >= min_gpa"""
    return [s for s in students if float(s['GPA']) >= min_gpa]

honors = get_honors_students(students)
print(f"Honors students: {len(honors)}")
for student in honors:
    print(f"  {student['Name']}: {student['GPA']}")

# Example 4: Sorting and ranking
def rank_students(students):
    """Sort students by GPA (descending)"""
    return sorted(students, key=lambda s: float(s['GPA']), reverse=True)

ranked = rank_students(students)
print("Class ranking:")
for i, student in enumerate(ranked, 1):
    print(f"{i}. {student['Name']}: {student['GPA']}")

# Example 5: Merging data from multiple sources
attendance_csv = """Name,Present,Absent
Alice,45,5
Bob,40,10
Charlie,44,6"""

def merge_student_data(students_csv, attendance_csv):
    """Merge student info with attendance"""
    students_f = io.StringIO(students_csv)
    attendance_f = io.StringIO(attendance_csv)

    students = {r['Name']: r for r in csv.DictReader(students_f)}
    attendance = {r['Name']: r for r in csv.DictReader(attendance_f)}

    merged = []
    for name, student in students.items():
        record = student.copy()
        if name in attendance:
            record['Present'] = attendance[name]['Present']
            record['Absent'] = attendance[name]['Absent']
        merged.append(record)

    return merged

merged = merge_student_data(input_csv, attendance_csv)
for record in merged:
    print(record)

# Example 6: Data transformation and export
def create_transcript(students):
    """Create a formatted transcript"""
    output = io.StringIO()
    output.write("=== STUDENT TRANSCRIPT ===\n")
    for student in sorted(students, key=lambda s: s['Name']):
        gpa = float(student['GPA'])
        standing = "Good" if gpa >= 3.5 else "Satisfactory"
        output.write(f"{student['Name']}: Grade {student['Grade']}, GPA {gpa:.2f} ({standing})\n")
    return output.getvalue()

transcript = create_transcript(students)
print(transcript)

# Example 7: Data validation with CSV
def validate_student_record(record):
    """Validate a student record"""
    errors = []
    if not record.get('Name') or not record['Name'].strip():
        errors.append("Name cannot be empty")
    if record.get('Grade') not in ['A', 'B', 'C', 'D', 'F']:
        errors.append(f"Invalid grade: {record.get('Grade')}")
    try:
        gpa = float(record.get('GPA', 0))
        if gpa < 0 or gpa > 4.0:
            errors.append(f"GPA out of range: {gpa}")
    except ValueError:
        errors.append(f"GPA must be a number: {record.get('GPA')}")
    return errors

# Example 8: Export with filtering and formatting
def export_honors_list(students_csv):
    """Create an honors list export"""
    f = io.StringIO(students_csv)
    students = list(csv.DictReader(f))

    output = io.StringIO()
    output.write("NAME,GPA,GRADE\n")
    for s in students:
        if float(s['GPA']) >= 3.8:
            output.write(f"{s['Name'].upper()},{s['GPA']},{s['Grade']}\n")

    return output.getvalue()

honors_export = export_honors_list(input_csv)
print("Honors Export:")
print(honors_export)

# Example 9: Summary statistics
def generate_summary(students):
    """Generate statistics about student body"""
    gpas = [float(s['GPA']) for s in students]
    grades = {}
    for s in students:
        grade = s['Grade']
        grades[grade] = grades.get(grade, 0) + 1

    return {
        'total_students': len(students),
        'avg_gpa': sum(gpas) / len(gpas),
        'max_gpa': max(gpas),
        'min_gpa': min(gpas),
        'grade_distribution': grades
    }

summary = generate_summary(students)
print(f"Summary: {summary['total_students']} students, Avg GPA: {summary['avg_gpa']:.2f}")

# Example 10: Complete pipeline: read, process, validate, write
def process_student_records(input_csv_text):
    """Complete processing pipeline"""
    # Read
    f = io.StringIO(input_csv_text)
    students = list(csv.DictReader(f))

    # Validate and filter
    valid_students = []
    invalid_count = 0
    for student in students:
        errors = validate_student_record(student)
        if not errors:
            valid_students.append(student)
        else:
            invalid_count += 1

    # Process (add computed fields)
    for student in valid_students:
        gpa = float(student['GPA'])
        student['Standing'] = 'Good' if gpa >= 3.5 else 'Satisfactory'

    # Write
    output = io.StringIO()
    fieldnames = ['Name', 'Grade', 'GPA', 'Standing']
    writer = csv.DictWriter(output, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(valid_students)

    return output.getvalue(), valid_students, invalid_count

result_csv, valid, invalid = process_student_records(input_csv)
print(f"Processed: {len(valid)} valid, {invalid} invalid")
print(result_csv)
```

### Guided Practice

**Activity: Build a Student Records System**

1. Create functions to:
   - Read student CSV (Name, Age, Major)
   - Add new students
   - Find students by major
   - Calculate class statistics
   - Export filtered results

2. Test the system with sample data

**Step-by-step code:**
```python
import csv
import io

# Student data
student_data = """Name,Age,Major
Alice,18,CS
Bob,19,Math
Charlie,18,CS
Diana,20,Physics
Eve,19,Math"""

# Read
f = io.StringIO(student_data)
students = list(csv.DictReader(f))

# Function to find by major
def find_by_major(students, major):
    return [s for s in students if s['Major'] == major]

# Get CS majors
cs_students = find_by_major(students, 'CS')
print(f"CS majors ({len(cs_students)}):")
for s in cs_students:
    print(f"  {s['Name']}")

# Export CS students
output = io.StringIO()
writer = csv.DictWriter(output, fieldnames=['Name', 'Age', 'Major'])
writer.writeheader()
writer.writerows(cs_students)
print("\nCS Export:")
print(output.getvalue())
```

### Practice Problems

**Problem 1 — Beginner:** Read a student CSV and write out only students with grade A.

**Problem 2 — Intermediate:** Read two CSV files (students and test scores) and merge them into one output file.

**Problem 3 — Challenge:** Create a complete student management system that can add, filter, and generate reports from student data.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Read CSV with DictReader.
- Filter for Grade == 'A'.
- Write with DictWriter.

**Problem 2:**
- Read both files into dicts.
- Use a common field (ID/Name) to match rows.
- Combine matching records.
- Write merged output.

**Problem 3:**
- Create functions for each operation.
- Maintain a list of students.
- Allow reading from file, adding, filtering.
- Generate reports and export.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
import csv
import io

# Problem 1
students_csv = "Name,Grade\nAlice,A\nBob,B\nCharlie,A"
f = io.StringIO(students_csv)
reader = csv.DictReader(f)

output = io.StringIO()
writer = csv.DictWriter(output, fieldnames=['Name', 'Grade'])
writer.writeheader()

for row in reader:
    if row['Grade'] == 'A':
        writer.writerow(row)

print(output.getvalue())

# Problem 2
students_csv = "ID,Name\n1,Alice\n2,Bob"
scores_csv = "ID,Score\n1,95\n2,87"

students_f = io.StringIO(students_csv)
scores_f = io.StringIO(scores_csv)

students = {r['ID']: r for r in csv.DictReader(students_f)}
scores = {r['ID']: r for r in csv.DictReader(scores_f)}

output = io.StringIO()
writer = csv.DictWriter(output, fieldnames=['ID', 'Name', 'Score'])
writer.writeheader()

for sid, student in students.items():
    score = scores.get(sid, {}).get('Score', 'N/A')
    writer.writerow({'ID': sid, 'Name': student['Name'], 'Score': score})

print(output.getvalue())

# Problem 3
class StudentRecords:
    def __init__(self):
        self.students = []

    def add_student(self, name, age, major):
        self.students.append({'Name': name, 'Age': age, 'Major': major})

    def filter_by_major(self, major):
        return [s for s in self.students if s['Major'] == major]

    def export_csv(self):
        output = io.StringIO()
        writer = csv.DictWriter(output, fieldnames=['Name', 'Age', 'Major'])
        writer.writeheader()
        writer.writerows(self.students)
        return output.getvalue()

system = StudentRecords()
system.add_student('Alice', 18, 'CS')
system.add_student('Bob', 19, 'Math')
system.add_student('Charlie', 18, 'CS')

cs_majors = system.filter_by_major('CS')
print(f"CS majors: {[s['Name'] for s in cs_majors]}")
print(system.export_csv())
```

</details>
