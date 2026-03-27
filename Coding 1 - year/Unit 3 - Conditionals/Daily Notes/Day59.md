# Day 59: Input Validation with Conditionals

**Learning Target:** I can validate user input to ensure it's safe and correct before using it in programs.

---

## Key Concepts

**Input validation** checks that user input meets requirements before processing:
- Correct data type (number vs. string)
- Within valid range (0-100, not 150 for age)
- Required format (email has @, phone has dashes, etc.)
- Required fields (not empty)

**Why validate?**
- Prevents crashes (TypeError, ValueError)
- Prevents incorrect calculations
- Improves user experience
- Essential in real-world programs

---

## Code Examples

```python
# Type validation
age_input = input("Age: ")
try:
    age = int(age_input)
except ValueError:
    print("Please enter a number")

# Range validation
score = int(input("Score (0-100): "))
if score < 0 or score > 100:
    print("Invalid score")
else:
    print(f"Your score: {score}")

# Using chained comparison
if 0 <= score <= 100:
    print("Valid")
else:
    print("Invalid")

# Multiple validations
password = input("Password: ")
is_long = len(password) >= 8
has_upper = any(c.isupper() for c in password)
has_digit = any(c.isdigit() for c in password)
has_space = " " not in password

if is_long and has_upper and has_digit and has_space:
    print("✓ Valid password")
else:
    print("✗ Password must be 8+ chars, have uppercase, digit, no spaces")

# Loop until valid (preview of next unit)
while True:
    try:
        age = int(input("Age (0-150): "))
        if 0 <= age <= 150:
            break
        else:
            print("Age must be 0-150")
    except ValueError:
        print("Please enter a number")

# Email validation
email = input("Email: ")
if "@" in email and "." in email:
    print("✓ Valid email format")
else:
    print("✗ Invalid email")

# Non-empty validation
name = input("Name: ")
if name and name.strip():  # Not empty and not just spaces
    print(f"Welcome, {name}")
else:
    print("Name cannot be empty")

# Checking if string contains only digits
phone = input("Phone (digits only): ")
if phone.isdigit():
    print(f"Phone: {phone}")
else:
    print("Phone must contain only digits")

# Username requirements
username = input("Username: ")
is_valid = (
    len(username) >= 3 and
    len(username) <= 20 and
    username.isalnum() and
    not username[0].isdigit()
)
if is_valid:
    print("✓ Valid username")
else:
    print("✗ Username: 3-20 chars, alphanumeric, starts with letter")
```

---

## Validation Patterns

### Pattern 1: Type Validation
```python
try:
    value = int(input("Number: "))
except ValueError:
    print("Not a valid number")
```

### Pattern 2: Range Validation
```python
score = int(input("Score: "))
if not (0 <= score <= 100):
    print("Score must be 0-100")
```

### Pattern 3: Format Validation
```python
email = input("Email: ")
if "@" in email and "." in email:
    print("Valid format")
```

### Pattern 4: Required Field
```python
name = input("Name: ")
if not name or not name.strip():
    print("Name is required")
```

---

## Guided Practice (15 minutes)

**Activity: Build a Validator**

```python
# Validate age input
print("Enter your age")
age_input = input("Age (0-150): ")

try:
    age = int(age_input)
    if age < 0 or age > 150:
        print("Age must be 0-150")
    else:
        print(f"✓ Valid age: {age}")
except ValueError:
    print("Age must be a number")
```

**Try with:** "25" (valid), "abc" (invalid type), "-5" (invalid range), "abc" (error)

**Extend:** Add more validations (is integer, not float, etc.)

---

## Practice Problems

### Problem 1 — Beginner
Validate that a score is between 0 and 100:

```python
score = int(input("Score (0-100): "))
if :
    print("✓ Valid")
else:
    print("✗ Invalid - must be 0-100")
```

---

### Problem 2 — Intermediate
Validate a password:
- At least 8 characters
- Contains at least one uppercase letter
- Contains at least one digit
- No spaces

```python
password = input("Password: ")

has_length = len(password) >= 8
has_upper = any(c.isupper() for c in password)
has_digit = any(c.isdigit() for c in password)
no_space = " " not in password

if :
    print("✓ Strong password")
else:
    print("✗ Weak password")
    if not has_length:
        print("  - Must be at least 8 characters")
    if not has_upper:
        print("  - Must contain uppercase letter")
    if not has_digit:
        print("  - Must contain digit")
    if not no_space:
        print("  - Cannot contain spaces")
```

---

### Problem 3 — Challenge
Validate user registration:
- Username: 3-20 alphanumeric characters, starts with letter
- Email: contains @ and .
- Age: 18-120
- All fields required

```python
username = input("Username: ")
email = input("Email: ")
age_input = input("Age: ")

# Check username
valid_user = (len(username) >= 3 and
              len(username) <= 20 and
              username.isalnum() and
              username[0].isalpha())

# Check email
valid_email = "@" in email and "." in email

# Check age
try:
    age = int(age_input)
    valid_age = 18 <= age <= 120
except ValueError:
    valid_age = False

if valid_user and valid_email and valid_age:
    print("✓ Registration successful")
else:
    print("✗ Invalid input:")
    if not valid_user:
        print("  - Username must be 3-20 alphanumeric, start with letter")
    if not valid_email:
        print("  - Email must contain @ and .")
    if not valid_age:
        print("  - Age must be 18-120")
```

---

## Hints

- **Problem 1:** Use `0 <= score <= 100`
- **Problem 2:** All four conditions must be true: `if has_length and has_upper and has_digit and no_space:`
- **Problem 3:** Combine three validation checks

---

## Sample Answers

### Problem 1 Example
```python
score = int(input("Score (0-100): "))
if 0 <= score <= 100:
    print("✓ Valid")
else:
    print("✗ Invalid - must be 0-100")
```

### Problem 2 Example
```python
password = input("Password: ")

has_length = len(password) >= 8
has_upper = any(c.isupper() for c in password)
has_digit = any(c.isdigit() for c in password)
no_space = " " not in password

if has_length and has_upper and has_digit and no_space:
    print("✓ Strong password")
else:
    print("✗ Weak password - missing:")
    if not has_length:
        print("  - 8+ characters")
    if not has_upper:
        print("  - Uppercase letter")
    if not has_digit:
        print("  - Digit")
    if not no_space:
        print("  - No spaces")
```

### Problem 3 Example
```python
username = input("Username: ")
email = input("Email: ")
age_input = input("Age: ")

valid_user = (len(username) >= 3 and len(username) <= 20 and
              username.isalnum() and username[0].isalpha())
valid_email = "@" in email and "." in email

try:
    age = int(age_input)
    valid_age = 18 <= age <= 120
except ValueError:
    valid_age = False

if valid_user and valid_email and valid_age:
    print("✓ Registration successful")
else:
    print("✗ Invalid input")
```

---

## Key Takeaway

Input validation is critical in real-world programming. Always validate before processing. This prevents crashes and improves reliability!
