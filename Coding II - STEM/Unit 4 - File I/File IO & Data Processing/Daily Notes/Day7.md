# Day 7: Data Cleaning
**Learning Target:** I can validate, clean, and normalize data from files.

### Key Concepts
Data cleaning: handling missing data, type conversion, normalization, removing duplicates.

### Code Examples
```python
# Remove duplicates
data = [1, 2, 2, 3, 3, 3]
cleaned = list(set(data))

# Handle missing data
data = {"name": "Alice", "age": None}
age = data.get("age", 0)  # Default to 0 if missing

# Validate types
def validate_number(value):
    try:
        return float(value)
    except ValueError:
        return None

# Normalize data
names = ["alice", "Bob", "  charlie  "]
normalized = [name.strip().lower() for name in names]

# Remove empty values
data = ["item1", "", "item2", None, "item3"]
cleaned = [x for x in data if x]

# Data validation class
class DataValidator:
    @staticmethod
    def validate_email(email):
        return "@" in email and "." in email

    @staticmethod
    def validate_age(age):
        try:
            return 0 <= int(age) <= 150
        except ValueError:
            return False
```

### Guided Practice
Clean messy CSV data.

### Practice Problems
**Problem 1 — Beginner:** Remove duplicates from a list.

**Problem 2 — Intermediate:** Clean and validate CSV data.

**Problem 3 — Challenge:** Create a data cleaning pipeline.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
data = [1, 1, 2, 3, 3]
cleaned = list(dict.fromkeys(data))  # Preserves order

# Problem 2
import csv
with open("messy.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        if row["age"]:  # Check not empty
            age = int(row["age"])
            if 0 <= age <= 150:
                print(row)
```
</details>

---

---
