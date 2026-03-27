# Day 23: Data Processing Lab — Real Dataset
**Learning Target:** I can apply all File I/O and data processing skills to work with a realistic dataset.

### Key Concepts

**Complete pipeline:** Read → Clean → Validate → Analyze → Export.

**Real-world messiness:** Data contains errors, inconsistencies, and missing values.

**Problem-solving:** Working through issues and adapting approaches.

**Reporting:** Communicating findings effectively.

### Code Examples

```python
import json
import io

# Example 1: Complete processing pipeline
def process_employee_data(data_text):
    """Complete employee data processing"""
    # Parse
    lines = data_text.strip().split('\n')
    employees = []
    
    for line in lines[1:]:  # Skip header
        if not line.strip():
            continue
        parts = line.split(',')
        if len(parts) < 4:
            continue
        
        # Clean and validate
        try:
            name = parts[0].strip().title()
            if not name:
                continue
            
            salary = int(parts[1].strip())
            if salary < 0:
                continue
            
            dept = parts[2].strip().upper()
            if not dept:
                continue
            
            years = int(parts[3].strip())
            if years < 0:
                continue
            
            employees.append({
                'name': name,
                'salary': salary,
                'dept': dept,
                'years': years
            })
        except ValueError:
            continue
    
    return employees

# Example 2: Analysis after processing
def analyze_employees(employees):
    """Analyze processed employee data"""
    if not employees:
        return {}
    
    # Department analysis
    by_dept = {}
    for emp in employees:
        dept = emp['dept']
        if dept not in by_dept:
            by_dept[dept] = []
        by_dept[dept].append(emp['salary'])
    
    dept_stats = {}
    for dept, salaries in by_dept.items():
        dept_stats[dept] = {
            'count': len(salaries),
            'avg_salary': sum(salaries) / len(salaries),
            'min_salary': min(salaries),
            'max_salary': max(salaries)
        }
    
    # Overall stats
    all_salaries = [e['salary'] for e in employees]
    overall = {
        'total_employees': len(employees),
        'avg_salary': sum(all_salaries) / len(all_salaries),
        'total_payroll': sum(all_salaries),
        'avg_tenure': sum(e['years'] for e in employees) / len(employees)
    }
    
    return {'by_department': dept_stats, 'overall': overall}

# Example 3: Processing with error recovery
def process_sales_data(data_text):
    """Process sales data with error handling"""
    sales = []
    errors = []
    
    for line_num, line in enumerate(data_text.strip().split('\n')[1:], 1):
        try:
            parts = line.split(',')
            if len(parts) < 3:
                errors.append(f"Line {line_num}: Missing fields")
                continue
            
            date = parts[0].strip()
            product = parts[1].strip()
            amount = float(parts[2].strip())
            
            if amount < 0:
                errors.append(f"Line {line_num}: Negative amount")
                continue
            
            sales.append({'date': date, 'product': product, 'amount': amount})
        except ValueError:
            errors.append(f"Line {line_num}: Invalid format")
    
    return sales, errors

# Example 4: Grouping and aggregation
def sales_by_product(sales):
    """Aggregate sales by product"""
    by_product = {}
    for sale in sales:
        prod = sale['product']
        if prod not in by_product:
            by_product[prod] = 0
        by_product[prod] += sale['amount']
    
    return sorted(by_product.items(), key=lambda x: x[1], reverse=True)

# Example 5: Data export
def export_report(analysis, format='text'):
    """Export analysis in different formats"""
    if format == 'text':
        lines = []
        lines.append("=== REPORT ===")
        lines.append(f"Total records: {analysis['overall']['total_employees']}")
        lines.append(f"Average salary: ${analysis['overall']['avg_salary']:,.2f}")
        lines.append(f"Total payroll: ${analysis['overall']['total_payroll']:,.2f}")
        return '\n'.join(lines)
    
    elif format == 'json':
        return json.dumps(analysis, indent=2)
    
    return str(analysis)

# Example 6: Complete pipeline execution
def complete_pipeline(input_data):
    """Execute complete data processing pipeline"""
    print("1. Reading data...")
    employees = process_employee_data(input_data)
    print(f"   Loaded {len(employees)} employees")
    
    print("2. Analyzing...")
    analysis = analyze_employees(employees)
    
    print("3. Generating report...")
    report = export_report(analysis, 'text')
    
    return report, employees, analysis

# Example 7: Validation statistics
def validation_report(raw_count, processed_count):
    """Report on validation results"""
    rejected = raw_count - processed_count
    rejection_rate = (rejected / raw_count * 100) if raw_count > 0 else 0
    
    return {
        'input_records': raw_count,
        'output_records': processed_count,
        'rejected': rejected,
        'acceptance_rate': f"{100 - rejection_rate:.1f}%"
    }

# Example 8: Data quality checks
def data_quality_report(employees):
    """Check data quality"""
    checks = {}
    
    # Missing values
    missing_count = sum(1 for e in employees if None in e.values())
    checks['missing_values'] = missing_count
    
    # Outliers (very high salaries)
    avg_salary = sum(e['salary'] for e in employees) / len(employees)
    high_salaries = [e for e in employees if e['salary'] > avg_salary * 2]
    checks['outliers'] = len(high_salaries)
    
    # Tenure range
    tenures = [e['years'] for e in employees]
    checks['tenure_range'] = (min(tenures), max(tenures))
    
    return checks

# Example 9: Comparative analysis
def compare_departments(analysis):
    """Compare department statistics"""
    depts = analysis['by_department']
    
    # Highest paying department
    highest = max(depts.items(), key=lambda x: x[1]['avg_salary'])
    
    # Most employees
    largest = max(depts.items(), key=lambda x: x[1]['count'])
    
    return {
        'highest_paying': highest[0],
        'largest_dept': largest[0],
        'dept_count': len(depts)
    }

# Example 10: Summary generation
def generate_summary(employees, analysis, errors):
    """Generate executive summary"""
    summary = []
    summary.append("EXECUTIVE SUMMARY")
    summary.append("=" * 40)
    summary.append(f"Records processed: {len(employees)}")
    summary.append(f"Errors encountered: {len(errors)}")
    summary.append(f"")
    summary.append(f"Total employees: {analysis['overall']['total_employees']}")
    summary.append(f"Average salary: ${analysis['overall']['avg_salary']:,.0f}")
    summary.append(f"Total payroll: ${analysis['overall']['total_payroll']:,.0f}")
    summary.append(f"Average tenure: {analysis['overall']['avg_tenure']:.1f} years")
    
    return '\n'.join(summary)

# Sample data
sample_data = """Name,Salary,Department,Years
Alice Smith,75000,Engineering,5
Bob Johnson,65000,Sales,3
Charlie Brown,85000,Engineering,7
Diana Prince,60000,Sales,2
Eve Wilson,90000,Engineering,8
Frank Castle,55000,Support,1"""

# Run complete pipeline
employees, analysis = process_employee_data(sample_data), None
analysis = analyze_employees(employees)
print(generate_summary(employees, analysis, []))
```

### Guided Practice

**Activity: Process a Complete Dataset**

1. Read sample CSV data
2. Clean and validate
3. Perform analysis
4. Generate report

**Step-by-step code:**
```python
data = """Product,Q1,Q2,Q3,Q4
Widget,1000,1200,1100,1300
Gadget,800,900,950,1050
Device,600,700,750,800"""

products = {}
lines = data.strip().split('\n')
header = lines[0].split(',')

for line in lines[1:]:
    parts = line.split(',')
    product = parts[0]
    sales = [int(x) for x in parts[1:]]
    products[product] = {
        'quarters': sales,
        'total': sum(sales),
        'average': sum(sales) / len(sales)
    }

for product, data in products.items():
    print(f"{product}: Total {data['total']}, Avg {data['average']:.0f}")
```

### Practice Problems

**Problem 1 — Beginner:** Process CSV data, clean it, and display basic statistics.

**Problem 2 — Intermediate:** Process data from multiple sources, validate, clean, and generate a report.

**Problem 3 — Challenge:** Create a complete data system that reads, validates, analyzes, and exports results.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Read CSV line by line.
- Validate each field.
- Calculate statistics.

**Problem 2:**
- Process each source.
- Validate all data.
- Combine and analyze.

**Problem 3:**
- Build modular functions.
- Test each step.
- Create clear output.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
def process_simple_csv(data_text):
    lines = data_text.strip().split('\n')
    numbers = []
    for line in lines[1:]:
        try:
            num = int(line.split(',')[1])
            numbers.append(num)
        except:
            pass
    return {
        'count': len(numbers),
        'avg': sum(numbers) / len(numbers),
        'min': min(numbers),
        'max': max(numbers)
    }

# Problem 2
def merge_and_analyze(data1, data2):
    all_records = []
    for line in data1.split('\n')[1:]:
        if line.strip():
            all_records.append(line)
    for line in data2.split('\n')[1:]:
        if line.strip():
            all_records.append(line)
    return len(all_records)

# Problem 3
class DataProcessor:
    def __init__(self):
        self.data = []
    
    def read_csv(self, csv_text):
        for line in csv_text.strip().split('\n')[1:]:
            if line.strip():
                self.data.append(line)
    
    def validate(self):
        return [r for r in self.data if len(r.split(',')) > 2]
    
    def analyze(self):
        return len(self.data)
    
    def export(self):
        return '\n'.join(self.data)
```

</details>
