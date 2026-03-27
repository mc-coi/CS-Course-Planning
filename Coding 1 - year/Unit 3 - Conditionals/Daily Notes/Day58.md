# Day 58: Short-Circuit Evaluation & Truthy/Falsy Values

**Learning Target:** I can understand short-circuit evaluation and use truthy/falsy values in conditionals.

---

## Key Concepts

### Short-Circuit Evaluation

Python stops evaluating as soon as the result is determined:

**With `and`:** If first condition is False, second is not checked (already False)
```python
if False and something():
    pass  # something() is NOT called
```

**With `or`:** If first condition is True, second is not checked (already True)
```python
if True or something():
    pass  # something() is NOT called
```

**Benefit:** Prevents errors and saves time.

### Truthy and Falsy Values

In Python, any value can be used in a Boolean context:

**Falsy values** (evaluate as False):
- `False` (the Boolean)
- `0` (zero)
- `0.0` (zero float)
- `""` (empty string)
- `[]` (empty list)
- `None` (no value)

**Truthy values** (evaluate as True):
- `True` (the Boolean)
- Any non-zero number (1, -5, 3.14, etc.)
- Any non-empty string ("hello", " ", "0", etc.)
- Any non-empty list, dict, etc.

---

## Code Examples

```python
# Short-circuit with and
password = ""
if password and len(password) >= 8:
    print("Strong")  # password is falsy, so second not checked

# Short-circuit with or
username = input("Username: ") or "Guest"
# If input is empty string (falsy), use "Guest"

# Truthy values in conditionals
x = 5
if x:  # Non-zero is truthy
    print("x is truthy")  # Runs

name = "Alice"
if name:  # Non-empty string is truthy
    print("Name exists")  # Runs

# Falsy values in conditionals
count = 0
if count:  # Zero is falsy
    print("We have items")  # Doesn't run

text = ""
if text:  # Empty string is falsy
    print("Text exists")  # Doesn't run

# Using not with truthy/falsy
if not username:
    print("No username provided")

# Checking if list is not empty
items = [1, 2, 3]
if items:
    print(f"Found {len(items)} items")  # Runs

# Short-circuit prevents index error
data = []
if data and data[0] > 5:
    print("First item > 5")  # data is empty (falsy), so data[0] not accessed

# Real-world: Get user input with default
name = input("Name: ") or "Anonymous"
age_input = input("Age: ")
age = int(age_input) if age_input else 0

# Checking if file was opened successfully
file_content = ""
if file_content:
    print("File has content")
else:
    print("File is empty or not loaded")

# Testing multiple conditions safely
nums = [10, 20, 30]
if len(nums) > 0 and nums[0] > 5:
    print("First number is > 5")  # len check prevents index error

# Common pattern: check if variable exists
user = None
if user:
    print(f"Hello, {user.name}")
else:
    print("No user logged in")
```

---

## Guided Practice (15 minutes)

**Activity 1: Identify Truthy/Falsy**

```python
print(bool(5))        # True (non-zero)
print(bool(0))        # False (zero)
print(bool("hello"))  # True (non-empty string)
print(bool(""))       # False (empty string)
print(bool([1,2]))    # True (non-empty list)
print(bool([]))       # False (empty list)
```

**Activity 2: Short-Circuit Behavior**

```python
# Predict what prints:
x = 0
if x and print("A"):  # print() is NOT called
    print("B")
# Output: (nothing - x is falsy, so print never runs)

# What about this?
x = 1
if x or print("A"):   # print() is NOT called
    print("B")
# Output: B (x is truthy, so print never checked)
```

---

## Practice Problems

### Problem 1 — Beginner
Check if a list has items without getting an IndexError:

```python
items = []
# Check if list has items AND first item > 5
if  and items[0] > 5:
    print("First item is > 5")
else:
    print("List empty or first item <= 5")
```

---

### Problem 2 — Intermediate
Get user input with a default value:

```python
name = input("Your name (or press Enter for 'Guest'): ")
# If empty, use "Guest"; otherwise use input

name =  or "Guest"

print(f"Hello, {name}")
```

---

### Problem 3 — Challenge
Check if password is valid (non-empty and >= 8 chars) without redundant checks:

```python
password = input("Password: ")

# Should check: password is not empty AND length >= 8
if  and len(password) >= 8:
    print("✓ Valid password")
else:
    print("✗ Invalid (empty or too short)")
```

---

## Hints

- **Problem 1:** Check if `items` is truthy (non-empty) first
- **Problem 2:** Use `or` operator: empty string is falsy
- **Problem 3:** Check `password` first (non-empty), then length

---

## Sample Answers

### Problem 1 Example
```python
items = []
if items and items[0] > 5:
    print("First item is > 5")
else:
    print("List empty or first item <= 5")
```

### Problem 2 Example
```python
name = input("Your name (or press Enter for 'Guest'): ")
name = name or "Guest"
print(f"Hello, {name}")
```

### Problem 3 Example
```python
password = input("Password: ")

if password and len(password) >= 8:
    print("✓ Valid password")
else:
    print("✗ Invalid (empty or too short)")
```

---

## Common Patterns

**Pattern 1: Default values**
```python
username = input("Name: ") or "Guest"
```

**Pattern 2: Safe indexing**
```python
if data and data[0]:
    first = data[0]
```

**Pattern 3: Check before processing**
```python
if email and "@" in email:
    send_welcome(email)
```

---

## Key Takeaway

Short-circuit evaluation saves time and prevents errors. Truthy/falsy values make conditionals more concise. Understanding these patterns makes you write more Pythonic code!
