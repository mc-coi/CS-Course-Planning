# Day 21: Data Cleaning — Handling Missing/Malformed Data
**Learning Target:** I can clean and normalize data to prepare it for analysis and processing.

### Key Concepts

**Missing data:** Handling empty, null, or undefined values.

**Malformed data:** Fixing incorrect formats (wrong case, extra spaces, etc.).

**Normalization:** Converting data to a consistent format.

**Standardization:** Making all values follow the same rules.

**Data quality:** Improving overall reliability of datasets.

### Code Examples

```python
# Example 1: Handling missing values
def clean_missing_values(data, default='N/A'):
    """Replace None or empty strings with default"""
    cleaned = []
    for record in data:
        clean_record = {}
        for key, value in record.items():
            if value is None or value == '':
                clean_record[key] = default
            else:
                clean_record[key] = value
        cleaned.append(clean_record)
    return cleaned

data = [
    {'name': 'Alice', 'age': 25, 'city': None},
    {'name': '', 'age': 30, 'city': 'NYC'},
    {'name': 'Charlie', 'age': None, 'city': 'LA'}
]

cleaned = clean_missing_values(data)
for record in cleaned:
    print(record)

# Example 2: Trimming whitespace
def clean_whitespace(text):
    """Remove leading/trailing spaces"""
    if isinstance(text, str):
        return text.strip()
    return text

names = ['  Alice  ', 'Bob', '  Carol']
clean_names = [clean_whitespace(n) for n in names]
print(clean_names)

# Example 3: Normalizing case
def normalize_case(text, style='title'):
    """Normalize text case"""
    if not isinstance(text, str):
        return text
    if style == 'title':
        return text.title()
    elif style == 'lower':
        return text.lower()
    elif style == 'upper':
        return text.upper()
    return text

names = ['ALICE', 'bob', 'cArOL']
normalized = [normalize_case(n) for n in names]
print(normalized)

# Example 4: Removing duplicates
def remove_duplicates(data, key):
    """Remove duplicate records based on key"""
    seen = set()
    unique = []
    for record in data:
        value = record[key]
        if value not in seen:
            seen.add(value)
            unique.append(record)
    return unique

data = [
    {'id': 1, 'name': 'Alice'},
    {'id': 2, 'name': 'Bob'},
    {'id': 1, 'name': 'Alice'},
    {'id': 3, 'name': 'Carol'}
]

unique_data = remove_duplicates(data, 'id')
print(f"Original: {len(data)}, Unique: {len(unique_data)}")

# Example 5: Converting types
def convert_type(value, target_type):
    """Safely convert value to target type"""
    try:
        if target_type == 'int':
            return int(float(value))  # Handles "5.0"
        elif target_type == 'float':
            return float(value)
        elif target_type == 'bool':
            return str(value).lower() in ['true', '1', 'yes']
        elif target_type == 'string':
            return str(value)
        return value
    except (ValueError, TypeError):
        return None

values = ['25', '30.5', 'true', 'invalid']
for v in values:
    print(f"{v} -> int: {convert_type(v, 'int')}")

# Example 6: Fixing common spelling/formatting issues
def clean_phone(phone):
    """Standardize phone format"""
    if not phone:
        return None
    # Remove all non-digits
    digits = ''.join(c for c in str(phone) if c.isdigit())
    if len(digits) == 10:
        return f"({digits[:3]}) {digits[3:6]}-{digits[6:]}"
    return None

phones = ['5551234567', '555-123-4567', '(555) 123-4567', 'invalid']
for phone in phones:
    print(f"{phone} -> {clean_phone(phone)}")

# Example 7: Filling missing values with computed defaults
def fill_missing_values(data, field, compute_fn):
    """Fill missing values using a computation"""
    for record in data:
        if not record.get(field):
            record[field] = compute_fn(record)
    return data

data = [
    {'name': 'Alice', 'age': 25, 'birth_year': None},
    {'name': 'Bob', 'age': 30, 'birth_year': None}
]

current_year = 2024
data = fill_missing_values(data, 'birth_year', lambda r: current_year - int(r['age']))
for record in data:
    print(record)

# Example 8: Standardizing categories
def standardize_category(value, mapping):
    """Map variations to standard category"""
    value_lower = str(value).lower().strip()
    return mapping.get(value_lower, value)

grade_mapping = {
    'a': 'A', 'a+': 'A', 'excellent': 'A',
    'b': 'B', 'b+': 'B', 'good': 'B',
    'c': 'C', 'average': 'C'
}

grades = ['A', 'excellent', 'B+', 'good', 'C']
standard = [standardize_category(g, grade_mapping) for g in grades]
print(standard)

# Example 9: Handling outliers
def remove_outliers(numbers, threshold=2):
    """Remove values that deviate significantly from mean"""
    if not numbers:
        return []
    mean = sum(numbers) / len(numbers)
    std_dev = (sum((x - mean) ** 2 for x in numbers) / len(numbers)) ** 0.5
    
    clean = []
    for num in numbers:
        if abs(num - mean) <= threshold * std_dev:
            clean.append(num)
    return clean

scores = [85, 90, 92, 87, 150, 88]  # 150 is outlier
cleaned = remove_outliers(scores)
print(f"Original: {scores}")
print(f"Cleaned: {cleaned}")

# Example 10: Complete data cleaning pipeline
def clean_dataset(data):
    """Complete cleaning pipeline"""
    cleaned = []
    for record in data:
        # Remove whitespace
        name = record.get('name', '').strip()
        if not name:
            continue  # Skip records with no name

        # Convert and validate age
        try:
            age = int(record.get('age', 0))
            if age < 0 or age > 150:
                age = None
        except ValueError:
            age = None

        # Normalize email
        email = record.get('email', '').lower().strip()
        if '@' not in email:
            email = None

        # Standardize grade
        grade = standardize_category(record.get('grade', ''), grade_mapping)

        cleaned.append({
            'name': name,
            'age': age,
            'email': email,
            'grade': grade
        })

    return cleaned

messy_data = [
    {'name': '  Alice  ', 'age': '25', 'email': 'ALICE@EXAMPLE.COM', 'grade': 'A'},
    {'name': '   ', 'age': '30', 'email': 'bob@example.com', 'grade': 'B+'},
    {'name': 'Charlie', 'age': 'twenty', 'email': 'charlie@example', 'grade': 'excellent'},
    {'name': 'Diana', 'age': '28', 'email': 'diana@example.com', 'grade': 'C'}
]

clean_data = clean_dataset(messy_data)
for record in clean_data:
    print(record)
```

### Guided Practice

**Activity: Clean Real-World-like Data**

Create a function that cleans student records with common issues:
- Extra whitespace
- Missing/empty fields
- Inconsistent case
- Invalid age values

**Step-by-step code:**
```python
def clean_student_records(data):
    cleaned = []
    for record in data:
        # Clean name
        name = record.get('name', '').strip().title()

        # Clean age
        try:
            age = int(record.get('age', ''))
            if age < 5 or age > 100:
                age = None
        except (ValueError, TypeError):
            age = None

        # Clean email
        email = record.get('email', '').strip().lower()
        if '@' not in email:
            email = None

        # Only keep records with name and age
        if name and age:
            cleaned.append({'name': name, 'age': age, 'email': email})

    return cleaned

messy_records = [
    {'name': '  ALICE  ', 'age': 18, 'email': 'ALICE@SCHOOL.EDU'},
    {'name': '  bob  ', 'age': 'nineteen', 'email': 'bob@school.edu'},
    {'name': '', 'age': 20, 'email': 'carol@school.edu'},
    {'name': 'Diana', 'age': 250, 'email': 'diana@school.edu'},
]

clean = clean_student_records(messy_records)
for record in clean:
    print(record)
```

### Practice Problems

**Problem 1 — Beginner:** Create a function that removes leading/trailing whitespace from all string values in a list of dicts.

**Problem 2 — Intermediate:** Create a function that cleans a list of records by removing duplicates and handling missing values.

**Problem 3 — Challenge:** Create a comprehensive data cleaning function that handles multiple data quality issues.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Loop through dict items.
- Use str.strip() on string values.
- Return cleaned dict.

**Problem 2:**
- Keep track of seen values (for duplicates).
- Check for None/empty values.
- Provide reasonable defaults.

**Problem 3:**
- Normalize case.
- Convert types.
- Remove outliers.
- Handle missing values.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
def remove_whitespace(records):
    cleaned = []
    for record in records:
        clean_record = {}
        for key, value in record.items():
            if isinstance(value, str):
                clean_record[key] = value.strip()
            else:
                clean_record[key] = value
        cleaned.append(clean_record)
    return cleaned

# Problem 2
def clean_records(records):
    seen_ids = set()
    cleaned = []
    for record in records:
        if record.get('id') in seen_ids:
            continue
        seen_ids.add(record.get('id'))

        clean_record = record.copy()
        for key in clean_record:
            if clean_record[key] is None or clean_record[key] == '':
                clean_record[key] = 'N/A'
        cleaned.append(clean_record)
    return cleaned

# Problem 3
def comprehensive_clean(records):
    cleaned = []
    for record in records:
        # Normalize strings
        name = record.get('name', '').strip().title()
        if not name:
            continue

        # Convert age
        try:
            age = int(record.get('age', 0))
        except ValueError:
            age = None

        # Normalize category
        category = record.get('category', '').lower()

        cleaned.append({'name': name, 'age': age, 'category': category})
    return cleaned
```

</details>
