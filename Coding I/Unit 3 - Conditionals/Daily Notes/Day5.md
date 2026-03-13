# Day 5: Logical Operators
**Learning Target:** I can combine conditions using logical operators (and, or, not).

### Key Concepts
**Logical operators** combine Boolean expressions:
- **and:** Both conditions must be True
- **or:** At least one condition must be True
- **not:** Reverses the Boolean (True becomes False, False becomes True)

**Short-circuit evaluation:** With `and`, if first condition is False, the second isn't checked. With `or`, if first is True, second isn't checked.

### Code Examples
```python
# and operator — both must be True
age = 17
has_license = True
if age >= 16 and has_license:
    print("Can drive!")  # Runs

# or operator — at least one True
day = "Sunday"
has_homework = False
if day == "Saturday" or day == "Sunday" or has_homework == False:
    print("No school!")  # Runs

# not operator — reverses
is_raining = False
if not is_raining:
    print("Let's go outside!")  # Runs (not False = True)

# Complex expression
score = 85
attendance = 0.9
if score >= 80 and attendance >= 0.8:
    print("Passing grade")  # Runs

# Combining all three
age = 20
has_id = True
is_member = False
if (age >= 18 and has_id) or is_member:
    print("Access granted")  # Runs
```

### Guided Practice
Write conditions for:
1. "You can apply for college" if age >= 18 AND you have a diploma
2. "Discount applies" if age < 13 OR age > 65
3. "Not allowed" if you're NOT an adult (age < 18)

### Practice Problems
**Problem 1 — Beginner:** Create a condition with `and`: check if a number is between 1 and 10.

```python
num = int(input("Number: "))
if :
    print("In range")
else:
    print("Out of range")
```

**Problem 2 — Intermediate:** Check if a password is strong (8+ chars AND contains a digit and uppercase).

**Problem 3 — Challenge:** Create a "can borrow a book" checker: student AND not overdue AND not maxed out books.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `num >= 1 and num <= 10`
- Problem 2: Use `.isdigit()` and `.isupper()` on strings, or check characters
- Problem 3: Use multiple conditions with `and`
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num = int(input("Number: "))
if num >= 1 and num <= 10:
    print("In range")
else:
    print("Out of range")

# Pythonic way with chained comparison
if 1 <= num <= 10:
    print("In range")
```
</details>

---