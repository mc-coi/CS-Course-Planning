# Day 9: Project Day — Student Data Analyzer
**Learning Target:** I can build a complete data analysis program.

### Project Overview
Analyze student data from CSV files:
- Read student records (name, grade, GPA)
- Calculate class statistics
- Identify top/bottom performers
- Generate reports
- Handle errors gracefully

### Requirements
- Read CSV file with error handling
- Calculate mean, median, min, max
- Filter data by criteria
- Write results to output file
- Handle invalid/missing data

### Scaffold & Starter Code
```python
import csv
from statistics import mean, median

class StudentAnalyzer:
    def __init__(self, filename):
        self.filename = filename
        self.students = []
        self.load_data()

    def load_data(self):
        try:
            with open(self.filename, 'r') as f:
                reader = csv.DictReader(f)
                for row in reader:
                    try:
                        self.students.append({
                            'name': row['Name'],
                            'grade': float(row['Grade'])
                        })
                    except ValueError:
                        print(f"Skipping invalid grade for {row['Name']}")
        except FileNotFoundError:
            print(f"File {self.filename} not found!")

    def get_statistics(self):
        if not self.students:
            return None
        grades = [s['grade'] for s in self.students]
        return {
            'mean': mean(grades),
            'median': median(grades),
            'min': min(grades),
            'max': max(grades),
            'count': len(self.students)
        }

    def generate_report(self, output_file):
        stats = self.get_statistics()
        with open(output_file, 'w') as f:
            f.write("STUDENT ANALYSIS REPORT\n")
            f.write(f"Students: {stats['count']}\n")
            f.write(f"Average Grade: {stats['mean']:.2f}\n")
            f.write(f"Median Grade: {stats['median']:.2f}\n")

# Usage
analyzer = StudentAnalyzer("students.csv")
analyzer.generate_report("report.txt")
```

### Enhancement Ideas
- Letter grade distribution
- Student rankings
- Trend analysis over time
- Export to JSON/Excel
- Data visualization

---

# Unit Practice Bank

1. **Beginner:** Open and read a file.
2. **Beginner:** Write text to a file.
3. **Beginner:** Read and print each line of a file.
4. **Intermediate:** Read CSV and process rows.
5. **Intermediate:** Write CSV from data.
6. **Intermediate:** Handle FileNotFoundError.
7. **Intermediate:** Parse JSON file.
8. **Challenge:** Read CSV, filter, and write results.
9. **Challenge:** Create custom exceptions for validation.
10. **Challenge:** Build data cleaning pipeline.
11. **Challenge:** Generate statistics report from file.
12. **Challenge:** Merge multiple data files.
13. **Challenge:** Create interactive data analyzer.
14. **Challenge:** Build robust file processor with error handling.
15. **Challenge:** Process and visualize data from files.

---

# Common Mistakes & How to Fix Them
| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Forgetting to close file | Resource leak | Use `with` statement |
| Using 'w' mode when 'a' needed | Overwrites file | Choose correct mode |
| csv.writer with no newline='' | Extra blank lines | Use `newline=""` parameter |
| Catching all exceptions generically | Hides real errors | Catch specific exceptions |
| No try/except for file operations | Crashes on missing file | Always use exception handling |
| Assuming file format | Crashes on different format | Validate/handle variations |

---

# Unit Assessment Prep

**Review Questions:**

1. What are the three main file modes in Python?
2. Why use the `with` statement for files?
3. What's the difference between `read()` and `readlines()`?
4. How do you read a CSV file?
5. What's JSON used for?
6. Explain try/except/else/finally.
7. What are custom exceptions?
8. How do you calculate mean and median?
9. When should you use `DictReader` vs `reader`?
10. How do you handle missing data?

**Answers:**

1. `'r'` (read), `'w'` (write/overwrite), `'a'` (append)
2. It automatically closes the file, even if errors occur
3. `read()` returns entire string; `readlines()` returns list of lines
4. `csv.reader()` or `csv.DictReader()` from csv module
5. Lightweight format for storing/exchanging structured data
6. try runs code, except catches errors, else runs if no error, finally always runs
7. Custom classes inheriting from Exception for application-specific errors
8. Mean: sum/count; Median: middle value of sorted data
9. DictReader when you want dict access (column names); reader for list access
10. Use defaults, skip rows, validate before use

---

# Vocabulary & Quick Reference

**Key Terms:**
- **File mode:** How file is opened (r, w, a)
- **CSV:** Comma-separated values (tabular format)
- **JSON:** JavaScript Object Notation (structured text)
- **Exception:** Error that can be caught and handled
- **Validation:** Checking data is correct/safe
- **Normalization:** Converting data to standard format
- **Statistic:** Mathematical summary of data

**Key Syntax:**
```python
# File operations
with open("file.txt", "r") as f:
    data = f.read()

# CSV
import csv
reader = csv.DictReader(file)

# JSON
import json
data = json.load(file)

# Exception handling
try:
    # code
except SpecificError as e:
    # handle
finally:
    # cleanup
```

---
