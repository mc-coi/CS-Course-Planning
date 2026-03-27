# Unit 4: File I/O & Data Processing — Unit Assessment

**Duration:** 45-60 minutes
**Total Points:** 100

---

## Section A: Multiple Choice (10 points, 1 point each)

Choose the best answer for each question.

**1.** Which statement is the safest way to open and read a file in Python?

A) `file = open('data.txt'); content = file.read()`
B) `with open('data.txt') as f: content = f.read()`
C) `open('data.txt').read()`
D) `file = open('data.txt'); content = file.read(); file.close()`

**Answer: B**

---

**2.** What does `json.loads()` do?

A) Loads a JSON file from disk
B) Parses a JSON string into a Python object
C) Loads and saves JSON
D) Lists all JSON attributes

**Answer: B**

---

**3.** Which exception is raised when a file doesn't exist?

A) ValueError
B) TypeError
C) FileNotFoundError
D) IOError

**Answer: C**

---

**4.** What is the purpose of the `with` statement in file operations?

A) It's optional but faster
B) It automatically closes the file
C) It prevents all errors
D) It encrypts the file

**Answer: B**

---

**5.** Which csv module function reads data as dictionaries with column names as keys?

A) csv.reader()
B) csv.DictReader()
C) csv.dict_reader()
D) csv.parse()

**Answer: B**

---

**6.** What does this regex pattern match: `\d{3}-\d{3}-\d{4}`?

A) Any sequence of 10 digits
B) 3 digits, dash, 3 digits, dash, 4 digits
C) A phone number
D) A credit card

**Answer: B**

---

**7.** How do you add a new key-value pair to a Python dictionary?

A) `dict.add('key', 'value')`
B) `dict['key'] = 'value'`
C) `dict.update('key')`
D) `dict.insert('key', 'value')`

**Answer: B**

---

**8.** What's the difference between `f.read()` and `f.readlines()`?

A) No difference; they're identical
B) `read()` returns entire file as string; `readlines()` returns list of lines
C) They work on different file types
D) `readlines()` is faster

**Answer: B**

---

**9.** Which code correctly validates an email address?

A) `if '@' in email: valid = True`
B) `if re.match(r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$', email): valid = True`
C) `if email.isvalid(): valid = True`
D) `if len(email) > 3: valid = True`

**Answer: B**

---

**10.** What does `os.path.exists(filename)` return?

A) The file path if it exists
B) True if the file exists, False otherwise
C) The file size
D) A file object

**Answer: B**

---

## Section B: Short Answer (20 points, 4 points each)

Answer each question in 2-3 sentences or a short code snippet.

**1. Explain the difference between `json.load()` and `json.loads()`. When would you use each?**

Expected Answer: `json.load()` reads from a file (no 's'), while `json.loads()` parses a JSON string (has 's' for string). Use `load()` when reading from a file, and `loads()` when you have JSON as a string.

---

**2. Write code showing the recommended way to read a file with error handling.**

Expected Answer:
```python
try:
    with open('file.txt', 'r') as f:
        content = f.read()
except FileNotFoundError:
    print("File not found")
```

---

**3. Name three things you should validate when reading CSV data.**

Expected Answer: Any three of:
- Data types (numeric fields are actually numbers)
- Required fields are present
- Value ranges (e.g., ages 0-150)
- Format validation (e.g., email has @)
- Field count matches expected columns
- Empty files

---

**4. Write a regex pattern that validates a date in MM/DD/YYYY format.**

Expected Answer: `\d{2}/\d{2}/\d{4}` or `(0[1-9]|1[0-2])/(0[1-9]|[12]\d|3[01])/\d{4}` (more strict)

---

**5. Describe one advantage of using `csv.DictReader` instead of `csv.reader`.**

Expected Answer: `DictReader` accesses columns by name (like `row['Name']`) instead of by index (like `row[0]`), making code more readable and less error-prone.

---

## Section C: Coding Challenges (70 points)

### Challenge 1: CSV Data Filtering (20 points)

**Task:** Write a program that:
1. Reads a CSV file with student records (Name, Age, Grade)
2. Validates that Age is numeric and 5-100
3. Validates that Grade is A-F
4. Writes valid records to an output CSV file
5. Reports how many records were valid/invalid

**Sample Input CSV:**
```
Name,Age,Grade
Alice,18,A
Bob,twenty,B
Charlie,19,X
Diana,18,A
```

**Expected Output CSV:**
```
Name,Age,Grade
Alice,18,A
Diana,18,A
```

**Output to Console:**
```
Valid: 2
Invalid: 2
```

**Grading:**
- File I/O (reading): 5 points
- Validation logic: 8 points
- File output: 5 points
- Error handling: 2 points

---

### Challenge 2: JSON Data Transformation (25 points)

**Task:** Write a program that:
1. Reads a JSON file containing a list of products with name, category, and price
2. Groups products by category
3. For each category, calculate:
   - Total value (sum of all prices)
   - Count of products
   - Average price
4. Write results to a JSON file
5. Generate a text report

**Sample Input JSON:**
```json
[
  {"name": "Widget", "category": "Tools", "price": 19.99},
  {"name": "Gadget", "category": "Electronics", "price": 29.99},
  {"name": "Wrench", "category": "Tools", "price": 14.99},
  {"name": "Cable", "category": "Electronics", "price": 9.99}
]
```

**Expected Output JSON:**
```json
{
  "Tools": {
    "count": 2,
    "total": 34.98,
    "average": 17.49
  },
  "Electronics": {
    "count": 2,
    "total": 39.98,
    "average": 19.99
  }
}
```

**Grading:**
- JSON reading: 5 points
- Grouping logic: 8 points
- Calculations: 7 points
- Output (JSON + report): 5 points

---

### Challenge 3: Complete Data Processing Pipeline (25 points)

**Task:** Create a complete program that:
1. Reads a CSV file with sales data (Date, Product, Quantity, Price)
2. Validates all fields (Quantity and Price must be numeric, Quantity > 0)
3. Calculates total sale amount for each record
4. Computes statistics (total sales, average, highest product by revenue)
5. Generates a formatted text report
6. Handles errors gracefully

**Sample Input CSV:**
```
Date,Product,Quantity,Price
2024-03-01,Widget,5,19.99
2024-03-01,Gadget,3,29.99
2024-03-02,Widget,-2,19.99
2024-03-02,Cable,10,9.99
```

**Expected Report:**
```
==== SALES REPORT ====
Total Records: 3 valid, 1 invalid
Total Revenue: $449.66
Average Sale: $149.89
Top Product: Widget ($199.90)
```

**Requirements:**
- Use proper file I/O with error handling
- Validate all data before processing
- Compute multiple statistics
- Generate formatted report
- Add comments explaining logic

**Grading:**
- File I/O and error handling: 6 points
- Data validation: 6 points
- Calculations: 6 points
- Report generation: 4 points
- Code quality/comments: 3 points

---

## Answer Key

### Section A: Multiple Choice
1. B | 2. B | 3. C | 4. B | 5. B | 6. B | 7. B | 8. B | 9. B | 10. B

### Section B: Short Answer
(See expected answers above)

### Section C: Sample Solutions

**Challenge 1:**
```python
import csv

valid = []
invalid = 0

try:
    with open('input.csv', 'r') as f:
        reader = csv.DictReader(f)
        for row in reader:
            try:
                age = int(row['Age'])
                grade = row['Grade']
                if 5 <= age <= 100 and grade in 'ABCDEF':
                    valid.append(row)
                else:
                    invalid += 1
            except ValueError:
                invalid += 1

    with open('output.csv', 'w', newline='') as f:
        writer = csv.DictWriter(f, fieldnames=['Name', 'Age', 'Grade'])
        writer.writeheader()
        writer.writerows(valid)

    print(f"Valid: {len(valid)}")
    print(f"Invalid: {invalid}")

except FileNotFoundError:
    print("Input file not found")
```

**Challenge 2:**
```python
import json

try:
    with open('products.json', 'r') as f:
        products = json.load(f)

    categories = {}
    for product in products:
        cat = product['category']
        if cat not in categories:
            categories[cat] = {'count': 0, 'total': 0}
        categories[cat]['count'] += 1
        categories[cat]['total'] += product['price']

    for cat in categories:
        categories[cat]['average'] = round(categories[cat]['total'] / categories[cat]['count'], 2)

    with open('output.json', 'w') as f:
        json.dump(categories, f, indent=2)

    print("==== CATEGORY REPORT ====")
    for cat, stats in categories.items():
        print(f"{cat}: {stats['count']} items, Total: ${stats['total']:.2f}")

except FileNotFoundError:
    print("File not found")
```

**Challenge 3:**
```python
import csv

valid_records = []
invalid_count = 0

try:
    with open('sales.csv', 'r') as f:
        reader = csv.DictReader(f)
        for row in reader:
            try:
                qty = int(row['Quantity'])
                price = float(row['Price'])
                if qty > 0:
                    row['total'] = qty * price
                    valid_records.append(row)
                else:
                    invalid_count += 1
            except ValueError:
                invalid_count += 1

    if valid_records:
        total_revenue = sum(float(r['total']) for r in valid_records)
        avg_sale = total_revenue / len(valid_records)

        products = {}
        for record in valid_records:
            prod = record['Product']
            if prod not in products:
                products[prod] = 0
            products[prod] += float(record['total'])

        top_product = max(products, key=products.get)

        report = f"""==== SALES REPORT ====
Total Records: {len(valid_records)} valid, {invalid_count} invalid
Total Revenue: ${total_revenue:.2f}
Average Sale: ${avg_sale:.2f}
Top Product: {top_product} (${products[top_product]:.2f})
"""
        print(report)

        with open('report.txt', 'w') as f:
            f.write(report)

except FileNotFoundError:
    print("Error: File not found")
except Exception as e:
    print(f"Error: {e}")
```

---

## Scoring Rubric

| Category | Excellent (A) | Good (B) | Satisfactory (C) | Needs Improvement (D/F) |
|----------|---------------|----------|------------------|------------------------|
| **File I/O** | Proper use of `with`, error handling | Mostly correct file handling | Basic file operations work | Missing error handling, unclosed files |
| **Data Validation** | Comprehensive validation, meaningful errors | Most fields validated | Basic validation present | Little or no validation |
| **Logic/Algorithms** | Efficient, correct solutions | Correct solutions with minor issues | Works but inefficient | Incorrect logic |
| **Code Quality** | Clear, well-commented, proper names | Generally clear and organized | Readable but sparse comments | Difficult to understand |

---

## Passing Score: 70 points (70%)

Good luck!
