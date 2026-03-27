# Day 25: Practice Day — Data Challenges
**Learning Target:** I can solve complex data processing problems using all Unit 4 skills.

### Challenges

**Challenge 1: CSV Data Merge**
Given two CSV files with overlapping data, merge them and remove duplicates.

**Challenge 2: JSON Transformation**
Read nested JSON, extract specific data, and create a new JSON structure.

**Challenge 3: Data Quality Audit**
Analyze a dataset for quality issues and generate a report.

**Challenge 4: Complete Pipeline**
Build a system that reads messy data, cleans it, validates it, analyzes it, and exports results.

### Challenge Solutions

```python
import csv
import json
import io

# Challenge 1: CSV Data Merge
def merge_csv_files(csv1_text, csv2_text):
    """Merge two CSV files, removing duplicates"""
    
    # Read both files
    f1 = io.StringIO(csv1_text)
    f2 = io.StringIO(csv2_text)
    
    reader1 = csv.DictReader(f1)
    reader2 = csv.DictReader(f2)
    
    # Merge with duplicate removal
    seen = set()
    merged = []
    
    for row in reader1:
        key = tuple(sorted(row.items()))
        if key not in seen:
            seen.add(key)
            merged.append(row)
    
    for row in reader2:
        key = tuple(sorted(row.items()))
        if key not in seen:
            seen.add(key)
            merged.append(row)
    
    # Write merged data
    if merged:
        output = io.StringIO()
        fieldnames = merged[0].keys()
        writer = csv.DictWriter(output, fieldnames=fieldnames)
        writer.writeheader()
        writer.writerows(merged)
        return output.getvalue()
    
    return ""

# Challenge 2: JSON Transformation
def transform_json(json_input):
    """Transform nested JSON to different structure"""
    
    f = io.StringIO(json_input)
    data = json.load(f)
    
    # Extract and transform
    if 'records' in data:
        transformed = []
        for record in data['records']:
            transformed.append({
                'id': record.get('id'),
                'name': record.get('details', {}).get('name', 'N/A'),
                'active': record.get('status') == 'active'
            })
        
        output = io.StringIO()
        json.dump(transformed, output, indent=2)
        return output.getvalue()
    
    return "{}"

# Challenge 3: Data Quality Audit
def audit_data_quality(csv_text):
    """Audit dataset for quality issues"""
    
    f = io.StringIO(csv_text)
    reader = csv.DictReader(f)
    
    issues = {
        'missing_fields': 0,
        'invalid_emails': 0,
        'invalid_ages': 0,
        'duplicates': 0,
        'total_records': 0
    }
    
    seen = set()
    
    for row in reader:
        issues['total_records'] += 1
        
        # Check for missing fields
        if any(not v or v.strip() == '' for v in row.values()):
            issues['missing_fields'] += 1
        
        # Check for invalid email
        if '@' not in row.get('email', ''):
            issues['invalid_emails'] += 1
        
        # Check for invalid age
        try:
            age = int(row.get('age', '0'))
            if age < 0 or age > 150:
                issues['invalid_ages'] += 1
        except ValueError:
            issues['invalid_ages'] += 1
        
        # Check for duplicates
        key = (row.get('id'), row.get('name'))
        if key in seen:
            issues['duplicates'] += 1
        seen.add(key)
    
    return issues

# Challenge 4: Complete Pipeline
class DataPipeline:
    def __init__(self):
        self.raw_data = []
        self.cleaned_data = []
        self.valid_data = []
        self.analysis = {}
    
    def read_csv(self, csv_text):
        """Step 1: Read CSV"""
        f = io.StringIO(csv_text)
        reader = csv.DictReader(f)
        self.raw_data = list(reader)
        return len(self.raw_data)
    
    def clean_data(self):
        """Step 2: Clean data"""
        self.cleaned_data = []
        for record in self.raw_data:
            cleaned = {
                'name': record.get('name', '').strip().title(),
                'email': record.get('email', '').lower().strip(),
                'age': self._convert_age(record.get('age', ''))
            }
            self.cleaned_data.append(cleaned)
        return len(self.cleaned_data)
    
    def validate_data(self):
        """Step 3: Validate data"""
        self.valid_data = []
        for record in self.cleaned_data:
            if self._is_valid(record):
                self.valid_data.append(record)
        return len(self.valid_data)
    
    def analyze_data(self):
        """Step 4: Analyze data"""
        if not self.valid_data:
            return {}
        
        ages = [r['age'] for r in self.valid_data if r['age'] is not None]
        
        self.analysis = {
            'total': len(self.valid_data),
            'avg_age': sum(ages) / len(ages) if ages else None,
            'min_age': min(ages) if ages else None,
            'max_age': max(ages) if ages else None
        }
        return self.analysis
    
    def export_json(self):
        """Step 5: Export as JSON"""
        output = io.StringIO()
        json.dump(self.valid_data, output, indent=2)
        return output.getvalue()
    
    def generate_report(self):
        """Generate processing report"""
        report = []
        report.append("PIPELINE REPORT")
        report.append("=" * 50)
        report.append(f"Raw records: {len(self.raw_data)}")
        report.append(f"Cleaned records: {len(self.cleaned_data)}")
        report.append(f"Valid records: {len(self.valid_data)}")
        report.append(f"Rejection rate: {(1 - len(self.valid_data)/len(self.raw_data))*100:.1f}%")
        
        if self.analysis:
            report.append(f"\nAnalysis:")
            for key, value in self.analysis.items():
                if isinstance(value, float):
                    report.append(f"  {key}: {value:.2f}")
                else:
                    report.append(f"  {key}: {value}")
        
        return "\n".join(report)
    
    def _convert_age(self, age_str):
        """Helper: Convert age string to int"""
        try:
            return int(age_str)
        except ValueError:
            return None
    
    def _is_valid(self, record):
        """Helper: Check if record is valid"""
        if not record['name']:
            return False
        if '@' not in record['email']:
            return False
        if record['age'] is None or record['age'] < 0 or record['age'] > 150:
            return False
        return True
```

### Practice Scenarios

**Scenario 1: Sales Data Processing**
- Read quarterly sales CSV
- Clean values (remove $ signs, convert to numbers)
- Calculate totals and averages
- Identify top performers

**Scenario 2: Student Records System**
- Read student CSV
- Validate all fields
- Calculate GPA averages
- Generate honors list
- Export results

**Scenario 3: API Response Processing**
- Parse JSON API response
- Extract student data
- Validate fields
- Compute statistics
- Generate report

### Solutions by Difficulty

See the complete Challenge Solutions section above for code examples.

