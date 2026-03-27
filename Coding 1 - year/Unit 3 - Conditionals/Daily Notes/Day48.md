# Day 48: Combining Comparisons

**Learning Target:** I can combine multiple comparison operators to create sophisticated Boolean expressions.

---

## Key Concepts

You can combine comparison operators in several ways:

1. **Separate conditions with logical operators:**
   ```python
   if x > 5 and x < 10:  # x is between 5 and 10
   ```

2. **Chained comparisons (Pythonic!):**
   ```python
   if 5 < x < 10:  # More readable and elegant
   ```

3. **Multiple conditions with `or`:**
   ```python
   if score < 60 or score > 100:  # Out of valid range
   ```

4. **Negating a compound condition:**
   ```python
   if not (x == 1 or x == 2):  # x is NOT 1 or 2
   ```

**DeMorgan's Law:** These are equivalent:
- `not (A and B)` = `(not A) or (not B)`
- `not (A or B)` = `(not A) and (not B)`

---

## Code Examples

```python
# Chained comparisons (most elegant)
x = 50
if 1 <= x <= 100:
    print("In range")  # Runs

# Equivalent using and (also fine)
if x >= 1 and x <= 100:
    print("In range")  # Runs

# Multiple comparisons with or
age = 5
if age < 13 or age > 65:
    print("Senior or child discount applies")  # Runs

# Complex: three comparisons
score = 85
if score >= 70 and score <= 100 and score != 0:
    print("Valid passing score")  # Runs

# Negating a compound condition
day = "Monday"
if not (day == "Saturday" or day == "Sunday"):
    print("It's a weekday")  # Runs

# Grade classification
score = 85
if 90 <= score <= 100:
    print("A")
elif 80 <= score < 90:
    print("B")
elif 70 <= score < 80:
    print("C")
else:
    print("F")

# Checking if value is in one of several ranges
x = 15
if (0 <= x < 10) or (20 <= x < 30) or (40 <= x < 50):
    print("In valid range")  # Runs

# Multiple string comparisons
color = input("Favorite color: ")
if color == "red" or color == "blue" or color == "green":
    print("Primary color!")

# Pythonic way: use 'in' with list
if color in ["red", "blue", "green"]:
    print("Primary color!")  # More efficient
```

---

## Guided Practice (15 minutes)

**Activity:** Fix the Logic

Each of these is trying to check something. Some are correct, some are wrong. Fix the incorrect ones:

1. **Check if number is between 1 and 10:**
   ```python
   if 1 <= x <= 10:  # CORRECT ✓
   if x >= 1 and x <= 10:  # CORRECT ✓
   if x > 1 and x < 10:  # WRONG (doesn't include 1 and 10)
   ```

2. **Check if it's a weekend:**
   ```python
   if day == "Saturday" and day == "Sunday":  # WRONG (one var can't be both)
   if day == "Saturday" or day == "Sunday":  # CORRECT ✓
   ```

3. **Check if age is NOT a teenager (NOT between 13-19):**
   ```python
   if not (13 <= age <= 19):  # CORRECT ✓
   if age < 13 or age > 19:  # CORRECT ✓
   if age < 13 and age > 19:  # WRONG (nothing satisfies both)
   ```

**Partner Activity:** Create your own compound comparison and explain it to a partner.

---

## Practice Problems

### Problem 1 — Beginner
Check if a number is NOT between 1 and 100. Write the condition two different ways:

```python
num = int(input("Number: "))

# Method 1: Using not and chained comparison
if :
    print("Out of range")

# Method 2: Using or
if :
    print("Out of range")
```

---

### Problem 2 — Intermediate
A test score is valid if it's between 0 and 100. Rewrite this to use chained comparison:

```python
score = int(input("Score: "))
if score >= 0 and score <= 100:
    print("Valid score")
else:
    print("Invalid score")
```

**Requirement:** Use chained comparison instead of `and`.

---

### Problem 3 — Challenge
A player can use a weapon if they:
- Have enough gold (>= 100) AND
- Have inventory space (< 5 items) AND
- Are at least level 5

Write a compound condition. Then rewrite it using DeMorgan's Law to check when they CANNOT use the weapon.

```python
gold = 150
items = 3
level = 6

# Can use weapon?
if :
    print("Can use weapon")

# Cannot use weapon? (opposite of above)
if :
    print("Cannot use weapon")
```

---

## Hints

- **Problem 1:** Method 1: `not (num >= 1 and num <= 100)` or `not (1 <= num <= 100)`; Method 2: `num < 1 or num > 100`
- **Problem 2:** Replace `and` with a single chained comparison: `0 <= score <= 100`
- **Problem 3:** For cannot-use: Apply DeMorgan's Law or just negate the entire condition

---

## Sample Answers

### Problem 1 Example
```python
num = int(input("Number: "))

# Method 1: Using not
if not (1 <= num <= 100):
    print("Out of range")

# Method 2: Using or
if num < 1 or num > 100:
    print("Out of range")
```

### Problem 2 Example
```python
score = int(input("Score: "))
if 0 <= score <= 100:
    print("Valid score")
else:
    print("Invalid score")
```

### Problem 3 Example
```python
gold = 150
items = 3
level = 6

# Can use weapon?
if gold >= 100 and items < 5 and level >= 5:
    print("Can use weapon")

# Cannot use weapon? (opposite)
if not (gold >= 100 and items < 5 and level >= 5):
    print("Cannot use weapon")

# Using DeMorgan's Law (all three conditions reversed with or)
if gold < 100 or items >= 5 or level < 5:
    print("Cannot use weapon")
```

---

## Key Takeaway

Combining comparisons creates powerful conditions. Learn to use chained comparisons for readability and `and`/`or` for flexibility. Understand DeMorgan's Law to switch between equivalent forms!
