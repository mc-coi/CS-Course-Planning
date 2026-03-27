# Day 26: Unit 4 Assessment
**Learning Target:** I can demonstrate mastery of File I/O, exception handling, CSV/JSON processing, and data analysis.

## Part A: Multiple Choice (10 questions)

1. **Which statement correctly opens a file in append mode?**
   - A) open('file.txt', 'a')
   - B) open('file.txt', 'w')
   - C) open('file.txt', 'r+')
   - D) open('file.txt', 'ab')
   **Answer: A**

2. **What does the 'with' statement do when opening files?**
   - A) Creates a backup copy
   - B) Automatically closes the file
   - C) Encrypts the file
   - D) None of the above
   **Answer: B**

3. **Which method would you use to parse a JSON string?**
   - A) json.load()
   - B) json.loads()
   - C) json.dump()
   - D) json.dumps()
   **Answer: B**

4. **What's the difference between json.dump() and json.dumps()?**
   - A) dump() writes to a file, dumps() returns a string
   - B) dumps() is faster than dump()
   - C) No difference, they're aliases
   - D) dump() returns a string, dumps() writes to a file
   **Answer: A**

5. **Which exception is raised when dividing by zero?**
   - A) ValueError
   - B) TypeError
   - C) ZeroDivisionError
   - D) ArithmeticError
   **Answer: C**

6. **What does the 'else' clause in try/except do?**
   - A) Executes if an exception occurs
   - B) Executes if no exception occurs
   - C) Replaces the except block
   - D) Catches all exceptions
   **Answer: B**

7. **Which CSV module class returns rows as dictionaries?**
   - A) csv.reader
   - B) csv.writer
   - C) csv.DictReader
   - D) csv.DictWriter
   **Answer: C**

8. **What file extension is typically used for JSON files?**
   - A) .json
   - B) .js
   - C) .txt
   - D) .data
   **Answer: A**

9. **Which function validates that data meets specific requirements?**
   - A) type()
   - B) str()
   - C) Custom validation function
   - D) int()
   **Answer: C**

10. **What does data cleaning involve?**
    - A) Removing viruses
    - B) Handling missing values and formatting inconsistencies
    - C) Encrypting sensitive data
    - D) Compressing files
    **Answer: B**

## Part B: Short Answer (5 questions, 2 points each)

1. **Explain the difference between read(), readline(), and readlines() methods.**
   - read() returns entire file content as one string
   - readline() returns one line at a time, including newline character
   - readlines() returns a list of all lines

2. **Describe what happens in this code:**
   ```python
   try:
       x = 10 / 0
   except ZeroDivisionError:
       print("Cannot divide by zero")
   else:
       print("Division successful")
   ```
   The ZeroDivisionError is raised, caught, and "Cannot divide by zero" is printed. The else block is skipped.

3. **What is data validation and why is it important?**
   Data validation is checking that data meets format/type/range requirements. It's important to catch errors early and prevent processing invalid data.

4. **How would you access the third element of a nested JSON array?**
   ```python
   data['key'][2]  # or data['key'][2]['field']
   ```

5. **What's the purpose of the finally clause in exception handling?**
   The finally clause executes regardless of whether an exception occurred, typically for cleanup operations like closing files.

## Part C: Coding Problems (3 problems, 5 points each)

**Problem 1: File Reading and Processing**

Write a function that reads a text file (simulated with a string), counts the number of lines, and returns the count and the longest line.

```python
def analyze_file(file_content):
    lines = file_content.strip().split('\n')
    line_count = len(lines)
    longest_line = max(lines, key=len)
    return line_count, longest_line
```

**Problem 2: CSV Processing with Error Handling**

Write a function that reads CSV data (Name, Score), validates that scores are 0-100, and returns only valid records.

```python
import csv
import io

def process_scores_csv(csv_text):
    f = io.StringIO(csv_text)
    reader = csv.DictReader(f)
    valid = []
    
    for row in reader:
        try:
            score = int(row['Score'])
            if 0 <= score <= 100:
                valid.append(row)
        except ValueError:
            continue
    
    return valid
```

**Problem 3: Complete Data Pipeline**

Write a function that:
1. Reads CSV data
2. Cleans field names and values
3. Validates records
4. Computes statistics
5. Returns results

```python
import json

def complete_data_pipeline(csv_text):
    import csv
    import io
    
    # Read and clean
    f = io.StringIO(csv_text)
    reader = csv.DictReader(f)
    cleaned = []
    
    for row in reader:
        cleaned.append({
            'name': row.get('name', '').strip().title(),
            'age': int(row.get('age', 0))
        })
    
    # Validate
    valid = [r for r in cleaned if r['name'] and 0 < r['age'] < 150]
    
    # Analyze
    if valid:
        ages = [r['age'] for r in valid]
        stats = {
            'count': len(valid),
            'avg_age': sum(ages) / len(ages),
            'min_age': min(ages),
            'max_age': max(ages)
        }
    else:
        stats = {}
    
    return {
        'records': valid,
        'statistics': stats
    }
```

## Answer Key

### Multiple Choice
1. A, 2. B, 3. B, 4. A, 5. C, 6. B, 7. C, 8. A, 9. C, 10. B

### Short Answer
[See detailed explanations above in Part B]

### Coding Problems
[See sample solutions above in Part C]

## Grading Rubric

**Part A (Multiple Choice):** 1 point each = 10 points
**Part B (Short Answer):** 2 points each = 10 points
**Part C (Coding):** 5 points each = 15 points
**Total:** 35 points

### Coding Problem Rubric (5 points each)
- Correctness (3 points): Code solves the problem
- Error Handling (1 point): Appropriate try/except or validation
- Code Quality (1 point): Clean, readable, well-organized

## Study Guide

**Key Topics to Review:**
- File modes and operations
- with statement
- Exception types and handling
- CSV reading/writing
- JSON parsing and generation
- Data validation techniques
- Data cleaning methods
- Basic statistics computation

**Common Mistakes to Avoid:**
- Forgetting to close files (use 'with')
- Using wrong JSON method (load vs loads)
- Not handling exceptions properly
- Assuming data is valid without validation
- Off-by-one errors in indexing
- Forgetting newlines when writing

