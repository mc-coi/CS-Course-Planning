# Day 3: CSV Files
**Learning Target:** I can read and write CSV files using the csv module.

### Key Concepts
CSV (Comma-Separated Values) format for tabular data.

`csv.reader()` and `csv.writer()` for simple access.
`csv.DictReader()` and `csv.DictWriter()` for dict-based access.

### Code Examples
```python
import csv

# Reading CSV
with open("students.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)

# Writing CSV
with open("output.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Age", "Grade"])
    writer.writerow(["Alice", 25, "A"])
    writer.writerow(["Bob", 23, "B"])

# Using DictReader (returns dicts)
with open("students.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row["Name"], row["Grade"])

# Using DictWriter
with open("output.csv", "w", newline="") as file:
    fieldnames = ["Name", "Age"]
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerow({"Name": "Zach", "Age": 17})
```

### Guided Practice
Read a CSV, filter rows, write filtered data.

### Practice Problems
**Problem 1 — Beginner:** Read a CSV and print all rows.

**Problem 2 — Intermediate:** Read CSV and calculate statistics.

**Problem 3 — Challenge:** Merge multiple CSV files.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
import csv
with open("data.csv", "r") as f:
    reader = csv.DictReader(f)
    grades = [float(row["Grade"]) for row in reader]
    avg = sum(grades) / len(grades)
```
</details>

---

---
