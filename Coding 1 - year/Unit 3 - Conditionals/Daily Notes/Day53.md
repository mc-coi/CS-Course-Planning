# Day 53: if/elif/else — Multi-way Branching

**Learning Target:** I can use elif to create multiple conditions and handle more than two paths.

---

## Key Concepts

**elif** (else if) tests additional conditions if the previous ones were False. Conditions are checked **top-to-bottom** and stops at the **first True** match.

Syntax:
```python
if condition1:
    # runs if condition1 True
elif condition2:
    # runs if condition1 False AND condition2 True
elif condition3:
    # runs if condition1 & 2 False AND condition3 True
else:
    # runs if all above are False
```

**Key points:**
- Only ONE branch executes (mutually exclusive)
- Order matters—put more specific conditions first
- `else` is optional; `elif` can appear multiple times
- Must check conditions top-to-bottom

---

## Code Examples

```python
# Grade classifier with elif
score = 85
if score >= 90:
    print("A")
elif score >= 80:
    print("B")  # Runs because 85 >= 80 and 85 < 90
elif score >= 70:
    print("C")
else:
    print("F")

# Time of day
hour = 14  # 2 PM
if hour < 12:
    print("Good morning!")
elif hour < 17:
    print("Good afternoon!")  # Runs
elif hour < 21:
    print("Good evening!")
else:
    print("Good night!")

# Age categories
age = 25
if age < 13:
    print("Child")
elif age < 18:
    print("Teenager")
elif age < 65:
    print("Adult")  # Runs
else:
    print("Senior")

# Season from month
month = int(input("Month (1-12): "))
if month in [12, 1, 2]:
    print("Winter")
elif month in [3, 4, 5]:
    print("Spring")
elif month in [6, 7, 8]:
    print("Summer")
else:  # month in [9, 10, 11]
    print("Fall")

# Menu system
choice = input("Enter A, B, or C: ")
if choice == "A":
    print("You chose A")
elif choice == "B":
    print("You chose B")
elif choice == "C":
    print("You chose C")
else:
    print("Invalid choice")

# Traffic speed
speed = int(input("Speed: "))
if speed > 65:
    print("Speeding!")
elif speed == 65:
    print("Speed limit!")
elif speed > 50:
    print("Safe speed")
else:
    print("Very slow")
```

---

## Order Matters!

**WRONG (overly specific first):**
```python
score = 85
if score >= 70:      # This matches!
    print("Passing")
elif score >= 80:    # Never reaches here
    print("B or higher")
```

Result: prints "Passing" (not intended!)

**CORRECT (most specific first):**
```python
score = 85
if score >= 90:      # No match
    print("A")
elif score >= 80:    # Match! Prints "B or higher"
    print("B or higher")
elif score >= 70:    # Skipped
    print("Passing")
```

Result: prints "B or higher" ✓

---

## Guided Practice (15 minutes)

**Activity:** Build a Grading System

```python
score = int(input("Score (0-100): "))

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
elif score >= 60:
    print("D")
else:
    print("F")
```

**Test with:** 95, 85, 75, 65, 55. Verify output.

**Modify:** Add a + or - to grades (90-92 = A-, 93-96 = A, 97-100 = A+)

---

## Practice Problems

### Problem 1 — Beginner
Classify a number as "Small", "Medium", or "Large".
- Small: < 50
- Medium: 50-99
- Large: >= 100

```python
num = int(input("Number: "))
if num < 50:
    print("Small")
elif :
    print("Medium")
else:
    print("Large")
```

---

### Problem 2 — Intermediate
Ask for a month number (1-12) and print the season.
- Winter: 12, 1, 2
- Spring: 3, 4, 5
- Summer: 6, 7, 8
- Fall: 9, 10, 11

```python
month = int(input("Month (1-12): "))
if :
    print("Winter")
elif :
    print("Spring")
elif :
    print("Summer")
else:
    print("Fall")
```

---

### Problem 3 — Challenge
Build an interactive quiz:
1. Ask a question
2. Get the answer
3. Check if correct
4. Give feedback:
   - Correct → "Excellent!"
   - Off by 1 → "Close!"
   - Way off → "Not even close"

```python
print("What is 2 + 2?")
answer = int(input("Your answer: "))

if answer == 4:
    print("Excellent!")
elif answer == 3 or answer == 5:
    print("Close!")
else:
    print("Not even close")
```

---

## Hints

- **Problem 1:** Second condition: `50 <= num < 100`
- **Problem 2:** Use `in` operator with lists: `if month in [12, 1, 2]:`
- **Problem 3:** Consider edge cases. Is off-by-one always 3 or 5?

---

## Sample Answers

### Problem 1 Example
```python
num = int(input("Number: "))
if num < 50:
    print("Small")
elif num < 100:
    print("Medium")
else:
    print("Large")
```

### Problem 2 Example
```python
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

### Problem 3 Example
```python
print("What is 2 + 2?")
answer = int(input("Your answer: "))

if answer == 4:
    print("Excellent!")
elif abs(answer - 4) == 1:
    print("Close!")
else:
    print("Not even close")
```

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Elif before if | SyntaxError | Every elif must follow an if |
| Overlapping conditions | Wrong condition matches first | Order from most to least specific |
| Forgetting else | Valid, but may want catch-all | Add else for all remaining cases |
| Elif with no colon | SyntaxError | Add `:` after condition |
| Wrong indentation | IndentationError | Match indentation level |

---

## Key Takeaway

if/elif/else chains handle multiple paths. Only ONE path executes. Order matters—more specific conditions first! This is how programs handle real-world decisions with many possibilities.
