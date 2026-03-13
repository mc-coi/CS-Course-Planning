# Day 7: Conditional Applications
**Learning Target:** I can validate input and handle complex conditions.

### Key Concepts
**Input validation** ensures user input is safe and correct before using it. Validate with if statements.

**Chained comparisons** (Pythonic): `1 <= x <= 10` instead of `x >= 1 and x <= 10`

### Code Examples
```python
# Input validation — loop until valid
while True:
    try:
        age = int(input("Age (0-150): "))
        if 0 <= age <= 150:
            break
        else:
            print("Age must be 0-150")
    except ValueError:
        print("Please enter a number")

# Chained comparison (Pythonic)
score = 85
if 80 <= score <= 90:
    print("In the 80s range")

# Range check
x = 50
if 1 <= x <= 100:
    print("In valid range")

# Complex validation
password = input("Password: ")
if len(password) >= 8:
    print("Password long enough")
else:
    print("Too short (min 8 chars)")
```

### Guided Practice
Create an age checker that asks for age and prints:
- If < 13: "Child"
- If 13-19: "Teenager"
- If 20-64: "Adult"
- If 65+: "Senior"

### Practice Problems
**Problem 1 — Beginner:** Ask for test score, validate it's 0-100, print "Valid" or "Invalid".

**Problem 2 — Intermediate:** Ask for password, validate it's 8+ chars, has uppercase, has digit.

**Problem 3 — Challenge:** Ask for height and weight, calculate BMI, classify (underweight/normal/overweight/obese).

<details>
<summary>💡 Hints</summary>

- Problem 1: Check `0 <= score <= 100`
- Problem 2: Use string methods like `.isupper()` or loop to check
- Problem 3: BMI = weight(lb) / height(in)² × 703
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
score = int(input("Score (0-100): "))
if 0 <= score <= 100:
    print("Valid")
else:
    print("Invalid")

# Problem 2 Example
pw = input("Password: ")
if len(pw) >= 8 and any(c.isupper() for c in pw) and any(c.isdigit() for c in pw):
    print("Strong password")
else:
    print("Weak password")
```
</details>

---