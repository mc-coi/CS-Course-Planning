# Day 47: Logical Operators (and, or, not)

**Learning Target:** I can combine Boolean expressions using logical operators (and, or, not) and understand truth tables.

---

## Key Concepts

**Logical operators** combine multiple Boolean expressions:

- **`and`:** Both conditions must be True for the result to be True
- **`or`:** At least one condition must be True for the result to be True
- **`not`:** Reverses the Boolean value (True becomes False, False becomes True)

**Short-circuit evaluation:** Python stops evaluating as soon as the result is determined:
- With `and`: if the first condition is False, the second is not checked
- With `or`: if the first condition is True, the second is not checked

This saves time and can prevent errors!

---

## Code Examples

```python
# and operator — both must be True
age = 17
has_license = True
if age >= 16 and has_license:
    print("Can drive!")  # Runs because both are True

# or operator — at least one True
day = "Sunday"
has_homework = False
if day == "Saturday" or day == "Sunday" or has_homework == False:
    print("No school!")  # Runs because day is Sunday

# not operator — reverses the Boolean
is_raining = False
if not is_raining:
    print("Let's go outside!")  # Runs (not False = True)

# Complex expression with all three
age = 20
has_id = True
is_member = False
if (age >= 18 and has_id) or is_member:
    print("Access granted")  # Runs because (True and True) or False = True

# Short-circuit evaluation example
x = 5
if x > 0 and x < 10:
    print("In range")  # Both checked, both True

# Example where short-circuit helps
numbers = []
if len(numbers) > 0 and numbers[0] > 5:
    print("First is big")  # Won't error—first condition False stops second check

# Chaining with or
favorite = input("Favorite color? ")
if favorite == "red" or favorite == "blue" or favorite == "green":
    print("Nice choice!")
```

---

## Truth Tables

### AND Truth Table
| and | T | F |
|-----|---|---|
| T   | T | F |
| F   | F | F |

Both must be True for and to return True.

### OR Truth Table
| or | T | F |
|----|---|---|
| T  | T | T |
| F  | T | F |

At least one must be True for or to return True.

### NOT Truth Table
| Input | not Input |
|-------|-----------|
| T     | F         |
| F     | T         |

Not reverses the Boolean.

---

## Guided Practice (15 minutes)

**Activity:** Boolean Detective

Evaluate these expressions step-by-step:

1. `5 > 3 and 2 < 1`
   - Is `5 > 3` True? YES
   - Is `2 < 1` True? NO
   - Result: True and False = **False**

2. `10 == 10 or "hello" == "goodbye"`
   - Is `10 == 10` True? YES
   - Does the second matter? NO (or stops at first True)
   - Result: **True**

3. `not (5 < 10)`
   - Is `5 < 10` True? YES
   - not True = **False**

4. Write your own: Create an expression that evaluates to True using all three operators.

---

## Practice Problems

### Problem 1 — Beginner
Create a condition with `and`: check if a number is between 1 and 10 (inclusive).

```python
num = int(input("Number: "))
if :
    print("In range")
else:
    print("Out of range")
```

**Requirement:** Use the `and` operator to check both bounds.

---

### Problem 2 — Intermediate
Check if a password is strong. A strong password has:
- At least 8 characters AND
- At least one uppercase letter AND
- At least one digit

```python
password = input("Password: ")
# Write condition here
if :
    print("Strong password")
else:
    print("Weak password")
```

**Hint:** Use `len()`, `.isupper()`, and `.isdigit()` on strings.

---

### Problem 3 — Challenge
Create a "can borrow a book" checker with these conditions:
- User is a student AND
- Book is not overdue AND
- User hasn't reached max books (5)

Model the logic with variables and logical operators.

```python
is_student = True
book_overdue = False
books_owned = 3
max_books = 5

# Write the condition here
if :
    print("You can borrow this book")
else:
    print("You cannot borrow this book")
```

---

## Hints

- **Problem 1:** You need: `num >= 1 and num <= 10` (or use chained comparison: `1 <= num <= 10`)
- **Problem 2:** Check each requirement with `and`. For digits: `any(c.isdigit() for c in password)` or check manually
- **Problem 3:** Combine three conditions with `and`. The third condition checks remaining capacity

---

## Sample Answers

### Problem 1 Example
```python
num = int(input("Number: "))
if num >= 1 and num <= 10:
    print("In range")
else:
    print("Out of range")

# Pythonic way with chained comparison
if 1 <= num <= 10:
    print("In range")
else:
    print("Out of range")
```

### Problem 2 Example
```python
password = input("Password: ")
has_upper = any(c.isupper() for c in password)
has_digit = any(c.isdigit() for c in password)

if len(password) >= 8 and has_upper and has_digit:
    print("Strong password")
else:
    print("Weak password")
```

### Problem 3 Example
```python
is_student = True
book_overdue = False
books_owned = 3
max_books = 5

if is_student and not book_overdue and books_owned < max_books:
    print("You can borrow this book")
else:
    print("You cannot borrow this book")
```

---

## Key Takeaway

Logical operators let you combine multiple conditions to create sophisticated decision-making. Remember: `and` requires all True, `or` requires at least one True, and `not` reverses. Use truth tables to debug!
