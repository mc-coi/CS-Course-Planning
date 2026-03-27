# Day 24: Review Day — File I/O & Data Processing
**Learning Target:** I can demonstrate mastery of all File I/O and data processing concepts through problem-solving.

### Key Review Topics

**File I/O Fundamentals:**
- open() modes (r, w, a)
- with statement for safe file handling
- Reading methods (read(), readline(), readlines())
- Writing methods (write(), writelines())
- File paths with os.path

**Exception Handling:**
- try/except/else/finally
- Specific exception types
- Raising exceptions
- Custom exceptions

**CSV Processing:**
- csv.reader and csv.writer
- csv.DictReader and csv.DictWriter
- Handling different delimiters
- Processing tabular data

**JSON Processing:**
- json.loads() and json.dumps()
- json.load() and json.dump()
- Nested JSON structures
- API-like responses

**Data Processing:**
- Validation
- Cleaning
- Analysis
- Statistics

### Review Code Examples

```python
# Example 1: Complete file operations review
import os
import csv
import json
import io

# File mode review
def demonstrate_file_modes():
    data = io.StringIO()
    # Write mode (create/overwrite)
    data.write("Initial content\n")
    
    # Read content
    data.seek(0)
    content = data.read()
    print(f"Content: {content}")
    
    return content

# Example 2: Exception handling review
def process_with_error_handling(data_list):
    results = []
    errors = []
    
    for item in data_list:
        try:
            num = int(item)
            if num < 0:
                raise ValueError("Negative number")
            results.append(num)
        except ValueError as e:
            errors.append((item, str(e)))
        except TypeError:
            errors.append((item, "Type error"))
    
    return results, errors

# Example 3: CSV operations review
def csv_round_trip(data_list):
    # Write CSV
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(['Name', 'Score'])
    for name, score in data_list:
        writer.writerow([name, score])
    
    # Read CSV
    csv_content = output.getvalue()
    f = io.StringIO(csv_content)
    reader = csv.DictReader(f)
    
    results = []
    for row in reader:
        results.append(row)
    
    return results

# Example 4: JSON operations review
def json_round_trip(data_dict):
    # Convert to JSON string
    json_str = json.dumps(data_dict, indent=2)
    
    # Parse back
    parsed = json.loads(json_str)
    
    return json_str, parsed

# Example 5: Data validation review
def validate_record(record):
    errors = []
    
    # Name validation
    if not record.get('name'):
        errors.append("Name required")
    
    # Age validation
    try:
        age = int(record.get('age', 0))
        if age < 0 or age > 150:
            errors.append("Age out of range")
    except ValueError:
        errors.append("Age must be a number")
    
    # Email validation
    email = record.get('email', '')
    if '@' not in email:
        errors.append("Invalid email")
    
    return len(errors) == 0, errors

# Example 6: Data cleaning review
def clean_record(record):
    cleaned = {}
    
    # Clean name
    cleaned['name'] = record.get('name', '').strip().title()
    
    # Clean age
    try:
        cleaned['age'] = int(record.get('age', 0))
    except ValueError:
        cleaned['age'] = None
    
    # Clean email
    cleaned['email'] = record.get('email', '').lower().strip()
    
    return cleaned

# Example 7: Analysis review
def analyze_scores(scores):
    if not scores:
        return {}
    
    sorted_scores = sorted(scores)
    n = len(scores)
    
    return {
        'count': n,
        'mean': sum(scores) / n,
        'median': sorted_scores[n // 2],
        'min': min(scores),
        'max': max(scores),
        'range': max(scores) - min(scores)
    }

# Example 8: Complete pipeline review
def complete_process_pipeline(csv_text):
    # Read
    f = io.StringIO(csv_text)
    reader = csv.DictReader(f)
    records = list(reader)
    
    # Clean
    cleaned = []
    for record in records:
        cleaned.append(clean_record(record))
    
    # Validate
    valid = []
    for record in cleaned:
        is_valid, errors = validate_record(record)
        if is_valid:
            valid.append(record)
    
    # Analyze
    if valid:
        ages = [r['age'] for r in valid if r['age']]
        stats = analyze_scores(ages)
    else:
        stats = {}
    
    return valid, stats

# Example 9: Error recovery review
def robust_file_reading(csv_content):
    """Read with comprehensive error handling"""
    try:
        f = io.StringIO(csv_content)
        reader = csv.DictReader(f)
        data = []
        
        for row_num, row in enumerate(reader, 1):
            try:
                # Validate row
                if not all(row.values()):
                    print(f"Row {row_num}: Missing values")
                    continue
                data.append(row)
            except KeyError as e:
                print(f"Row {row_num}: Missing column {e}")
                continue
        
        return data
    
    except csv.Error as e:
        print(f"CSV parsing error: {e}")
        return []
    except IOError as e:
        print(f"File error: {e}")
        return []

# Example 10: Reporting review
def generate_processing_report(input_count, output_count, stats):
    report = []
    report.append("=" * 50)
    report.append("PROCESSING REPORT")
    report.append("=" * 50)
    report.append(f"Input records: {input_count}")
    report.append(f"Valid records: {output_count}")
    report.append(f"Rejection rate: {(1 - output_count/input_count)*100:.1f}%")
    
    if stats:
        report.append(f"\nStatistics:")
        for key, value in stats.items():
            if isinstance(value, float):
                report.append(f"  {key}: {value:.2f}")
            else:
                report.append(f"  {key}: {value}")
    
    return "\n".join(report)
```

### Review Checklist

Students should be able to:
- Create and use with statements
- Handle multiple exception types
- Read/write CSV files with reader/writer and DictReader/DictWriter
- Parse and generate JSON
- Validate and clean data
- Compute statistics
- Handle errors gracefully

### Sample Review Problems

**Problem 1:** Write a function that reads a CSV, validates data, and writes valid records to a new CSV.

**Problem 2:** Write a function that processes JSON API responses and computes statistics.

**Problem 3:** Write a complete data pipeline that reads, cleans, validates, analyzes, and reports.

<details>
<summary>💡 Review Tips</summary>

- Remember the difference between load/loads and dump/dumps
- Always use with statements for files
- Catch specific exception types
- Validate early, clean often
- Test error cases as well as happy paths

</details>
