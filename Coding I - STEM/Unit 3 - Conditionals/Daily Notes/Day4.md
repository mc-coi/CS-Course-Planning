# Day 4: elif
**Learning Target:** I can use elif for multiple conditions.

### Key Concepts
**elif** (else if) tests additional conditions if the first if is False. Conditions are checked top-to-bottom and **stops at the first True**.

Order matters! Put more specific conditions first.

Syntax: `if ... elif ... elif ... else ...`

### Code Examples
```python
# Grade classifier with elif
score = 85
if score >= 90:
    print("A")
elif score >= 80:
    print("B")  # This runs
elif score >= 70:
    print("C")
else:
    print("F")

# Time of day
hour = 14  # 2 PM
if hour < 12:
    print("Good morning!")
elif hour < 17:
    print("Good afternoon!")  # This runs
elif hour < 21:
    print("Good evening!")
else:
    print("Good night!")

# Multiple elif's — order matters!
age = 25
if age < 13:
    print("Child")
elif age < 18:
    print("Teenager")
elif age < 65:
    print("Adult")  # This runs
else:
    print("Senior")
```

### Guided Practice
Create a program that asks for a test score and prints:
- A (90+), B (80-89), C (70-79), D (60-69), F (<60)

### Practice Problems
**Problem 1 — Beginner:** Use elif to classify a number as "Small", "Medium", or "Large".

```python
num = int(input("Number: "))
if num < 50:
    print()
elif :
    print()
else:
    print()
```

**Problem 2 — Intermediate:** Ask for a month number (1-12) and print the season.

**Problem 3 — Challenge:** Build a simple quiz—ask a question, check answer, print custom message based on correctness and other factors.

<details>
<summary>💡 Hints</summary>

- Problem 1: Split range into 3 categories
- Problem 2: Winter (12,1,2), Spring (3,4,5), Summer (6,7,8), Fall (9,10,11)
- Problem 3: Can add extra elif for "partially correct" or check string length
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num = int(input("Number: "))
if num < 50:
    print("Small")
elif num < 100:
    print("Medium")
else:
    print("Large")

# Problem 2 Example
month = int(input("Month (1-12): "))
if month in [12, 1, 2]:
    print("Winter")
elif month in [3, 4, 5]:
    print("Spring")
elif month in [6, 7, 8]:
    print("Summer")
else:
    print("Fall")
```
</details>

---