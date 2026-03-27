# Day 9: Raising Exceptions — raise Statement
**Learning Target:** I can use the raise statement to create custom error conditions and communicate problems to calling code.

### Key Concepts

**raise statement:** Explicitly throws an exception to signal an error condition.

**When to raise:** When a function cannot complete its intended task or receives invalid input.

**Raising specific exceptions:** Using built-in exception types (ValueError, TypeError, FileNotFoundError) with meaningful messages.

**Custom error messages:** Providing clear messages that explain what went wrong.

**Exception propagation:** Raising allows calling code to handle errors.

**Raising and catching:** A function raises an exception; the caller catches it.

### Code Examples

```python
# Example 1: Basic raise with ValueError
def validate_age(age):
    if age < 0 or age > 150:
        raise ValueError("Age must be between 0 and 150")
    return f"Valid age: {age}"

try:
    print(validate_age(25))   # Works
    print(validate_age(-5))   # Raises ValueError
except ValueError as e:
    print(f"Error: {e}")

# Example 2: Raising TypeError for wrong type
def divide(a, b):
    if not isinstance(a, (int, float)) or not isinstance(b, (int, float)):
        raise TypeError("Both arguments must be numbers")
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero")
    return a / b

try:
    print(divide(10, 2))      # Works
    print(divide("10", 2))    # Raises TypeError
except TypeError as e:
    print(f"Error: {e}")

# Example 3: Raising in a function for input validation
def set_password(password):
    if len(password) < 8:
        raise ValueError("Password must be at least 8 characters")
    if not any(c.isupper() for c in password):
        raise ValueError("Password must contain at least one uppercase letter")
    return "Password accepted"

try:
    print(set_password("MyPassword123"))  # Works
except ValueError as e:
    print(f"Password error: {e}")

# Example 4: Raising FileNotFoundError
def read_required_file(filename):
    try:
        with open(filename, 'r') as f:
            return f.read()
    except FileNotFoundError:
        raise FileNotFoundError(f"Required file '{filename}' not found")

try:
    content = read_required_file('config.txt')
except FileNotFoundError as e:
    print(f"Startup error: {e}")

# Example 5: Conditional raising
def process_score(score):
    try:
        score = int(score)
    except ValueError:
        raise ValueError(f"Score must be a number, got '{score}'")

    if score < 0 or score > 100:
        raise ValueError(f"Score must be 0-100, got {score}")

    return f"Score recorded: {score}"

scores = ["85", "110", "abc", "75"]
for score in scores:
    try:
        print(process_score(score))
    except ValueError as e:
        print(f"Error: {e}")

# Example 6: Re-raising exceptions
def safe_divide(a, b):
    try:
        return a / b
    except ZeroDivisionError as e:
        print("Logging error: Division by zero attempted")
        raise  # Re-raise the same exception

try:
    safe_divide(10, 0)
except ZeroDivisionError:
    print("Caught re-raised exception")

# Example 7: Raising with context
def calculate_percentage(part, total):
    if total == 0:
        raise ValueError("Total cannot be zero when calculating percentage")
    if part > total:
        raise ValueError(f"Part ({part}) cannot be greater than total ({total})")
    return (part / total) * 100

try:
    print(calculate_percentage(25, 100))  # Works
    print(calculate_percentage(150, 100)) # Raises ValueError
except ValueError as e:
    print(f"Calculation error: {e}")

# Example 8: Multiple validation checks
def create_user(name, email, age):
    if not name:
        raise ValueError("Name cannot be empty")
    if "@" not in email:
        raise ValueError("Invalid email format")
    if age < 13:
        raise ValueError("User must be at least 13 years old")
    return f"User created: {name} ({email})"

try:
    print(create_user("Alice", "alice@example.com", 25))
    print(create_user("Bob", "invalid-email", 30))
except ValueError as e:
    print(f"Error creating user: {e}")

# Example 9: Raising in data processing
def parse_csv_line(line):
    parts = line.split(',')
    if len(parts) != 3:
        raise ValueError(f"Expected 3 fields, got {len(parts)}")

    name, age_str, score_str = parts
    try:
        age = int(age_str)
        score = int(score_str)
    except ValueError:
        raise ValueError("Age and Score must be integers")

    if age < 0 or score < 0:
        raise ValueError("Age and Score cannot be negative")

    return (name, age, score)

data = ["Alice,25,95", "Bob,abc,87", "Charlie,30"]
for line in data:
    try:
        name, age, score = parse_csv_line(line)
        print(f"✓ {name}: {age} years old, score {score}")
    except ValueError as e:
        print(f"✗ Error parsing '{line}': {e}")

# Example 10: Function that requires non-None values
def process_data(data):
    if data is None:
        raise ValueError("Data cannot be None")
    if isinstance(data, str) and not data.strip():
        raise ValueError("Data cannot be empty string")
    return f"Processing: {data}"

try:
    print(process_data("valid"))
    print(process_data(None))
except ValueError as e:
    print(f"Error: {e}")
```

### Guided Practice

**Activity: Input Validation Function**

1. Create a function `validate_student_record(name, grade, gpa)` that:
   - Checks that name is not empty
   - Checks that grade is A-F
   - Checks that GPA is between 0.0 and 4.0
   - Raises ValueError with specific messages for each check

2. Create a program that processes a list of students, catching exceptions

**Step-by-step code:**
```python
def validate_student_record(name, grade, gpa):
    if not name or not isinstance(name, str):
        raise ValueError("Name must be a non-empty string")

    if grade not in ['A', 'B', 'C', 'D', 'F']:
        raise ValueError(f"Grade must be A-F, got {grade}")

    try:
        gpa = float(gpa)
    except ValueError:
        raise ValueError(f"GPA must be a number, got {gpa}")

    if gpa < 0.0 or gpa > 4.0:
        raise ValueError(f"GPA must be 0.0-4.0, got {gpa}")

    return True

students = [
    ("Alice", "A", "3.8"),
    ("Bob", "X", "3.5"),
    ("Charlie", "B", "3.2")
]

for name, grade, gpa in students:
    try:
        validate_student_record(name, grade, gpa)
        print(f"✓ {name}: Grade {grade}, GPA {gpa}")
    except ValueError as e:
        print(f"✗ {name}: {e}")
```

### Practice Problems

**Problem 1 — Beginner:** Write a function that takes a number and raises ValueError if it's negative. Test it with both valid and invalid inputs.

**Problem 2 — Intermediate:** Write a function that parses a "key:value" string and raises ValueError if the format is incorrect or the value is not a number.

**Problem 3 — Challenge:** Write a function that reads and validates a CSV line with fields (Name, Email, Phone). Raise specific ValueErrors for: empty fields, invalid email format (must contain @), invalid phone format (must be 10 digits).

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use `if` to check the condition.
- Raise `ValueError` with a message.
- Call the function in a try/except block.

**Problem 2:**
- Split by ':' and check the result.
- Try to convert value to a number.
- Raise `ValueError` for each specific case.

**Problem 3:**
- Split by commas for fields.
- Check each field for emptiness.
- Use `in` to check for '@' in email.
- Check phone length and if all characters are digits.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
def check_positive(num):
    if num < 0:
        raise ValueError("Number must be positive")
    return num

try:
    print(check_positive(5))
    print(check_positive(-3))
except ValueError as e:
    print(f"Error: {e}")

# Problem 2
def parse_key_value(line):
    if ':' not in line:
        raise ValueError("Format must be 'key:value'")
    key, value = line.split(':', 1)
    try:
        num_value = int(value)
    except ValueError:
        raise ValueError(f"Value must be a number, got '{value}'")
    return (key, num_value)

try:
    print(parse_key_value("age:25"))
    print(parse_key_value("name:alice"))
except ValueError as e:
    print(f"Error: {e}")

# Problem 3
def validate_csv_record(line):
    parts = line.split(',')
    if len(parts) != 3:
        raise ValueError("Must have exactly 3 fields")

    name, email, phone = parts

    if not name.strip():
        raise ValueError("Name cannot be empty")
    if not email.strip():
        raise ValueError("Email cannot be empty")
    if not phone.strip():
        raise ValueError("Phone cannot be empty")

    if '@' not in email:
        raise ValueError(f"Invalid email: {email}")

    if not phone.isdigit() or len(phone) != 10:
        raise ValueError(f"Phone must be 10 digits, got {phone}")

    return True

records = ["Alice,alice@example.com,5551234567", "Bob,invalid-email,5551234567"]
for record in records:
    try:
        validate_csv_record(record)
        print(f"✓ {record}")
    except ValueError as e:
        print(f"✗ Error: {e}")
```

</details>
