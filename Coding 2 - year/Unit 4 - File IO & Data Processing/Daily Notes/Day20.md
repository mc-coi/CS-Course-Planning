# Day 20: Data Validation — Checking Input
**Learning Target:** I can validate data to ensure it meets requirements before processing.

### Key Concepts

**Data validation:** Checking that data meets expected format, range, and type requirements.

**Validation rules:** Defining what makes data acceptable.

**Early validation:** Catching errors before they cause problems downstream.

**Meaningful error messages:** Telling users what's wrong and how to fix it.

**Validation patterns:** Common checks (not empty, within range, proper format, etc.).

### Code Examples

```python
# Example 1: Basic value range validation
def validate_age(age):
    try:
        age_int = int(age)
        if age_int < 0 or age_int > 150:
            return False, "Age must be between 0 and 150"
        return True, age_int
    except ValueError:
        return False, "Age must be a number"

# Example 2: Email validation
def validate_email(email):
    if not email or '@' not in email:
        return False, "Invalid email format"
    if '.' not in email.split('@')[1]:
        return False, "Email domain must contain a dot"
    return True, email

# Example 3: String validation
def validate_name(name):
    if not name or not name.strip():
        return False, "Name cannot be empty"
    if len(name) < 2:
        return False, "Name must be at least 2 characters"
    if not name.replace(' ', '').isalpha():
        return False, "Name can only contain letters and spaces"
    return True, name.strip()

# Example 4: Multiple field validation
def validate_student_record(name, age, gpa):
    errors = []

    valid, msg = validate_name(name)
    if not valid:
        errors.append(f"Name: {msg}")

    valid, msg = validate_age(age)
    if not valid:
        errors.append(f"Age: {msg}")

    try:
        gpa_float = float(gpa)
        if gpa_float < 0 or gpa_float > 4.0:
            errors.append("GPA: Must be 0.0 to 4.0")
    except ValueError:
        errors.append("GPA: Must be a number")

    return len(errors) == 0, errors

# Example 5: Pattern matching validation
def validate_phone(phone):
    if not phone:
        return False, "Phone cannot be empty"
    digits = ''.join(c for c in phone if c.isdigit())
    if len(digits) != 10:
        return False, "Phone must have 10 digits"
    return True, phone

# Example 6: Enum validation
def validate_grade(grade):
    valid_grades = ['A', 'B', 'C', 'D', 'F']
    if grade not in valid_grades:
        return False, f"Grade must be one of {valid_grades}"
    return True, grade

# Example 7: Date validation
def validate_date(date_str):
    try:
        parts = date_str.split('-')
        if len(parts) != 3:
            return False, "Date must be MM-DD-YYYY"
        month, day, year = int(parts[0]), int(parts[1]), int(parts[2])
        if month < 1 or month > 12:
            return False, "Month must be 1-12"
        if day < 1 or day > 31:
            return False, "Day must be 1-31"
        if year < 1900 or year > 2100:
            return False, "Year must be 1900-2100"
        return True, date_str
    except ValueError:
        return False, "Date values must be numbers"

# Example 8: List validation
def validate_scores(scores_str):
    try:
        scores = [int(x.strip()) for x in scores_str.split(',')]
        if len(scores) == 0:
            return False, "Must provide at least one score"
        for score in scores:
            if score < 0 or score > 100:
                return False, "All scores must be 0-100"
        return True, scores
    except ValueError:
        return False, "Scores must be comma-separated numbers"

# Example 9: Unique value validation
def validate_unique_ids(ids):
    unique_ids = set(ids)
    if len(unique_ids) != len(ids):
        return False, "Duplicate IDs found"
    return True, unique_ids

# Example 10: Conditional validation
def validate_application(data):
    errors = []

    if not data.get('name'):
        errors.append("Name is required")

    age = data.get('age')
    if age and int(age) < 18:
        errors.append("Must be 18 or older")
        # If under 18, require parent permission
        if not data.get('parent_permission'):
            errors.append("Parent permission required for under 18")

    if not data.get('email'):
        errors.append("Email is required")

    return len(errors) == 0, errors
```

### Guided Practice

**Activity: Create a Validation System**

1. Create validation functions for common fields:
   - Username (3-20 chars, alphanumeric)
   - Password (8+ chars, must have letter and number)
   - Email (valid format)

2. Test with various inputs

**Step-by-step code:**
```python
def validate_username(username):
    if not username or len(username) < 3 or len(username) > 20:
        return False, "Username must be 3-20 characters"
    if not username.isalnum():
        return False, "Username can only contain letters and numbers"
    return True, username

def validate_password(password):
    if not password or len(password) < 8:
        return False, "Password must be at least 8 characters"
    has_letter = any(c.isalpha() for c in password)
    has_digit = any(c.isdigit() for c in password)
    if not (has_letter and has_digit):
        return False, "Password must contain letters and numbers"
    return True, password

def validate_email(email):
    if '@' not in email or '.' not in email.split('@')[-1]:
        return False, "Invalid email format"
    return True, email

# Test data
test_cases = [
    ("alice123", "SecurePass1", "alice@example.com"),
    ("ab", "password", "invalid-email"),
    ("validuser", "onlyletters", "bob@test.com")
]

for username, password, email in test_cases:
    u_valid, u_msg = validate_username(username)
    p_valid, p_msg = validate_password(password)
    e_valid, e_msg = validate_email(email)

    print(f"Username: {u_msg if not u_valid else '✓'}")
    print(f"Password: {p_msg if not p_valid else '✓'}")
    print(f"Email: {e_msg if not e_valid else '✓'}")
    print()
```

### Practice Problems

**Problem 1 — Beginner:** Create a validation function for numbers in a specific range.

**Problem 2 — Intermediate:** Create validation functions for multiple fields and test with sample data.

**Problem 3 — Challenge:** Create a comprehensive validation system that validates a complete user registration form.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Accept min and max parameters.
- Check if value is a number.
- Check if it's within range.

**Problem 2:**
- Create separate functions for each field.
- Return tuple: (is_valid, message_or_value).
- Test with various valid/invalid inputs.

**Problem 3:**
- Validate all fields.
- Return list of all errors found.
- Check for cross-field dependencies if needed.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
def validate_range(value, min_val, max_val):
    try:
        num = int(value)
        if num < min_val or num > max_val:
            return False, f"Must be {min_val}-{max_val}"
        return True, num
    except ValueError:
        return False, "Must be a number"

# Problem 2
def validate_fields(name, age, email):
    errors = []

    if not name or len(name) < 2:
        errors.append("Name too short")

    try:
        age_int = int(age)
        if age_int < 0 or age_int > 150:
            errors.append("Age out of range")
    except ValueError:
        errors.append("Age must be a number")

    if '@' not in email:
        errors.append("Invalid email")

    return len(errors) == 0, errors

# Problem 3
def validate_registration(data):
    errors = []

    if not data.get('username') or len(data['username']) < 3:
        errors.append("Username must be 3+ chars")

    password = data.get('password', '')
    if len(password) < 8:
        errors.append("Password must be 8+ chars")
    if not any(c.isdigit() for c in password):
        errors.append("Password must include a digit")

    if '@' not in data.get('email', ''):
        errors.append("Invalid email")

    try:
        age = int(data.get('age', 0))
        if age < 13:
            errors.append("Must be 13 or older")
    except ValueError:
        errors.append("Age must be a number")

    return len(errors) == 0, errors
```

</details>
