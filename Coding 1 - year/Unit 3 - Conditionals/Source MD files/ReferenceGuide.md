# Unit 3: Conditionals — Reference Guide

Quick reference for all essential conditional concepts and syntax.

---

## Comparison Operators

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `==` | Equal to | `5 == 5` | True |
| `!=` | Not equal to | `5 != 3` | True |
| `<` | Less than | `3 < 5` | True |
| `>` | Greater than | `5 > 3` | True |
| `<=` | Less than or equal | `5 <= 5` | True |
| `>=` | Greater than or equal | `5 >= 5` | True |

---

## Logical Operators

| Operator | Meaning | True When | Example |
|----------|---------|-----------|---------|
| `and` | Logical AND | Both conditions True | `5 > 3 and 3 < 10` → True |
| `or` | Logical OR | At least one True | `5 > 10 or 3 < 10` → True |
| `not` | Logical NOT | Reverses Boolean | `not (5 > 10)` → True |

---

## Truth Tables

### AND Truth Table
```
A     | B     | A and B
------|-------|----------
True  | True  | True
True  | False | False
False | True  | False
False | False | False
```
**Both must be True**

### OR Truth Table
```
A     | B     | A or B
------|-------|----------
True  | True  | True
True  | False | True
False | True  | True
False | False | False
```
**At least one must be True**

### NOT Truth Table
```
A     | not A
------|-------
True  | False
False | True
```
**Reverses the value**

---

## Conditional Statements

### Basic if
```python
if condition:
    # Execute if condition is True
```

### if/else
```python
if condition:
    # Execute if True
else:
    # Execute if False
```

### if/elif/else
```python
if condition1:
    # Execute if condition1 is True
elif condition2:
    # Execute if condition1 False and condition2 True
elif condition3:
    # Execute if condition1 & condition2 False and condition3 True
else:
    # Execute if all above are False
```

### Nested if
```python
if condition1:
    if condition2:
        # Execute if both conditions True
```

---

## Common Patterns

### Chained Comparisons
```python
1 <= x <= 10      # x is between 1 and 10
```
Equivalent to: `x >= 1 and x <= 10`

### Checking Membership
```python
if color in ["red", "blue", "green"]:
    # color is one of these values
```

### Checking Substring
```python
if "hello" in "hello world":
    # substring exists
    print("Found it!")  # Runs
```

### Negating Complex Conditions (DeMorgan's Law)
```python
# Original
if not (x >= 0 and x <= 100):
    # x is NOT in range

# Equivalent
if x < 0 or x > 100:
    # x is NOT in range
```

### Default Values with OR
```python
name = input("Name: ") or "Guest"
# If input is empty (falsy), use "Guest"
```

### Safe Indexing with AND
```python
if data and data[0] > 5:
    # data is not empty AND first element > 5
    # Won't error on empty list
```

---

## Truthy and Falsy Values

### Falsy Values (evaluate as False)
- `False` — Boolean False
- `0` — Integer zero
- `0.0` — Float zero
- `""` — Empty string
- `[]` — Empty list
- `None` — No value

### Truthy Values (evaluate as True)
- `True` — Boolean True
- Any non-zero number (1, -5, 3.14)
- Any non-empty string ("hello", "0", " ")
- Any non-empty list, dict, set

---

## Short-Circuit Evaluation

### AND Short-Circuit
```python
if False and something():
    pass
# something() is NOT called (already False)
```

### OR Short-Circuit
```python
if True or something():
    pass
# something() is NOT called (already True)
```

---

## Input Validation Patterns

### Type Validation
```python
try:
    age = int(input("Age: "))
except ValueError:
    print("Please enter a number")
```

### Range Validation
```python
if 0 <= age <= 150:
    print("Valid age")
else:
    print("Invalid age")
```

### String Validation
```python
if len(password) >= 8:
    print("Long enough")

if "@" in email:
    print("Valid email format")

if password.isdigit():
    print("All digits")
```

### Required Field
```python
if name and name.strip():
    print("Name provided")
else:
    print("Name required")
```

---

## Flag Variables

Boolean variables that track state:

```python
# Examples
is_logged_in = True
has_permission = False
can_vote = age >= 18
is_valid = score >= 0 and score <= 100

# Use in conditions
if is_logged_in and has_permission:
    access_resource()
```

---

## Common Mistakes to Avoid

| Mistake | Wrong | Correct |
|---------|-------|---------|
| Assignment vs Comparison | `if x = 5:` | `if x == 5:` |
| Missing colon | `if x > 5` | `if x > 5:` |
| Wrong indentation | Code not indented | 4 spaces indented |
| AND instead of OR | `day == "Sat" and day == "Sun"` | `day == "Sat" or day == "Sun"` |
| Wrong boundary | `score > 90` (excludes 90) | `score >= 90` (includes 90) |
| Order in elif | General before specific | Specific before general |
| Comparing string to number | `"18" >= 18` | `int(input()) >= 18` |

---

## Debugging Checklist

When code doesn't work:
- [ ] Check for `=` instead of `==`
- [ ] Verify all colons present
- [ ] Check indentation (4 spaces)
- [ ] Verify correct operators (and vs or)
- [ ] Check condition order in elif
- [ ] Validate input types
- [ ] Test with print() statements
- [ ] Trace code line-by-line

---

## DeMorgan's Law

Converting between forms:

```python
# Original form 1
not (A and B)

# Equivalent form 1
(not A) or (not B)

# Original form 2
not (A or B)

# Equivalent form 2
(not A) and (not B)
```

---

## Quick Reference: if/elif/else Order

```python
# Order matters! Most specific first:

if score >= 90:
    print("A")          # Most specific
elif score >= 80:
    print("B")          # More general
elif score >= 70:
    print("C")          # More general
elif score >= 60:
    print("D")          # More general
else:
    print("F")          # Catch-all
```

---

## Essential String Methods for Validation

| Method | Returns | Example |
|--------|---------|---------|
| `.isdigit()` | True if all digits | `"123".isdigit()` → True |
| `.isalpha()` | True if all letters | `"abc".isalpha()` → True |
| `.isalnum()` | True if alphanumeric | `"abc123".isalnum()` → True |
| `.isupper()` | True if uppercase | `"A".isupper()` → True |
| `.islower()` | True if lowercase | `"a".islower()` → True |
| `.strip()` | Remove whitespace | `" hello ".strip()` → "hello" |
| `.lower()` | Convert to lowercase | `"HELLO".lower()` → "hello" |
| `.upper()` | Convert to uppercase | `"hello".upper()` → "HELLO" |

---

## The `in` Operator

**Check membership in sequences:**

```python
# Strings
"e" in "hello"              # True
"x" in "hello"              # False

# Lists
5 in [1, 2, 3, 5, 10]       # True
5 in [1, 2, 3]              # False

# Ranges (with range())
5 in range(1, 10)           # True
15 in range(1, 10)          # False
```

---

## Indentation Rules

**Python uses indentation (4 spaces) to define blocks:**

```python
if x > 5:               # Condition ends with :
    print("Big")       # INDENTED (4 spaces) - part of if
    print("Really big")  # Still indented - part of if
print("Done")           # NOT indented - outside if, always runs

# Wrong indentation causes errors!
if x > 5:
print("Big")            # ERROR! Not indented
```

---

## When to Use Which Conditional

| Situation | Use | Example |
|-----------|-----|---------|
| Yes/No decision | if/else | `if age >= 18: ...` |
| Multiple options | if/elif/else | Grade classification |
| Dependent decisions | Nested if | Check username, then password |
| Independent checks | and/or | Check multiple requirements |
| State tracking | Flag variables | `is_logged_in = True` |

---

## Practice Command

When you're unsure:
1. Write the condition in English
2. Break it into parts
3. Evaluate each part
4. Combine with and/or
5. Test with examples

Example:
- English: "If age is at least 18 AND has a license"
- Condition: `age >= 18 and has_license`
- Test: age=20, has_license=True → True ✓

---

*Keep this reference handy while coding!*
