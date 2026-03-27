# Day 57: Complex Conditions with and/or

**Learning Target:** I can use complex compound conditions with and/or to replace nested conditionals and simplify logic.

---

## Key Concepts

Nested conditionals can often be **simplified using logical operators**:

```python
# Nested version
if x > 5:
    if y < 10:
        print("Both conditions true")

# Simplified with and
if x > 5 and y < 10:
    print("Both conditions true")
```

**When to flatten nesting:**
- Both conditions are independent (don't depend on each other)
- You want clearer, more readable code
- Similar logic block for both cases

**When to keep nesting:**
- Conditions are dependent (inner checks based on outer)
- Different blocks for different cases
- Hierarchical decision-making

---

## Code Examples

```python
# Nested version (hierarchical)
is_student = True
if is_student:
    gpa = 3.5
    if gpa >= 3.0:
        print("Honor student")

# Flattened version (independent checks)
is_student = True
gpa = 3.5
if is_student and gpa >= 3.0:
    print("Honor student")

# Complex with and
age = 20
has_license = True
if age >= 16 and has_license:
    print("Can drive")

# Complex with or
day = "Saturday"
if day == "Saturday" or day == "Sunday":
    print("Weekend!")

# Multiple and/or
score = 85
attendance = 0.9
if score >= 80 and attendance >= 0.8 and score < 90:
    print("Good performance, room to improve")

# Using parentheses for clarity
age = 15
if (age < 13) or (age >= 13 and age < 18):
    print("Child or teenager")

# Negating complex conditions (DeMorgan's Law)
has_permission = False
is_admin = False

# NOT (A or B) = (NOT A) and (NOT B)
if not (has_permission or is_admin):
    print("Access denied")

# Equivalent:
if not has_permission and not is_admin:
    print("Access denied")

# Real-world: Password validation
password = "MyPass123!"
is_long = len(password) >= 8
has_upper = any(c.isupper() for c in password)
has_digit = any(c.isdigit() for c in password)

if is_long and has_upper and has_digit:
    print("Strong password")

# File access rules
is_owner = True
is_group_member = False
is_public = False

if is_owner or (is_group_member and is_public):
    print("Can access")
```

---

## Guided Practice (15 minutes)

**Activity: Simplify Complex Conditions**

Rewrite each nested version as a flattened version with logical operators:

1. **Nested:**
   ```python
   if age >= 18:
       if has_license:
           print("Can drive")
   ```
   **Flattened:**
   ```python
   if age >= 18 and has_license:
       print("Can drive")
   ```

2. **Nested:**
   ```python
   if score >= 90:
       if grade == "A":
           print("Perfect!")
   ```
   **Flattened:**
   ```python
   if score >= 90 and grade == "A":
       print("Perfect!")
   ```

3. **Complex with or:**
   ```python
   if day == "Saturday":
       print("Weekend")
   if day == "Sunday":
       print("Weekend")
   ```
   **Combined:**
   ```python
   if day == "Saturday" or day == "Sunday":
       print("Weekend")
   ```

---

## Practice Problems

### Problem 1 — Beginner
Rewrite this nested version using `and`:

```python
# Nested
age = 25
if age >= 18:
    if age < 65:
        print("Working age")

# Flattened version
if :
    print("Working age")
```

---

### Problem 2 — Intermediate
Rewrite using logical operators:

```python
# Original nested version
is_student = True
has_scholarship = False
if is_student:
    if has_scholarship:
        print("Get tuition discount")

# Flattened version
if :
    print("Get tuition discount")
```

---

### Problem 3 — Challenge
Check if a user can access a document:
- Owner can always access
- Admin can access
- Others can access if document is public

Write with logical operators:

```python
is_owner = False
is_admin = True
is_public = False

if :
    print("Access granted")
else:
    print("Access denied")
```

---

## Hints

- **Problem 1:** Use `and` to combine two conditions: `age >= 18 and age < 65`
- **Problem 2:** What single condition checks both? `is_student and has_scholarship`
- **Problem 3:** Owner OR admin OR (public document): `is_owner or is_admin or is_public`

---

## Sample Answers

### Problem 1 Example
```python
age = 25
if age >= 18 and age < 65:
    print("Working age")
```

### Problem 2 Example
```python
is_student = True
has_scholarship = False
if is_student and has_scholarship:
    print("Get tuition discount")
```

### Problem 3 Example
```python
is_owner = False
is_admin = True
is_public = False

if is_owner or is_admin or is_public:
    print("Access granted")
else:
    print("Access denied")
```

---

## Truth Evaluation Order

Python evaluates left-to-right with **short-circuit** behavior:

```python
# AND: stops at first False
if False and something_expensive():
    pass  # something_expensive() NOT called

# OR: stops at first True
if True or something_expensive():
    pass  # something_expensive() NOT called
```

This is efficient and can prevent errors!

---

## Key Takeaway

Complex conditions with `and`/`or` can replace nested ifs when conditions are independent. Choose what's most readable. More options = more flexibility!
