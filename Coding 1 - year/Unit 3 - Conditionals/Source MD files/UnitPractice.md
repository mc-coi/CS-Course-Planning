# Unit 3: Conditionals — Practice Bank

25 practice problems organized by difficulty and topic.

---

## Week 10: Boolean Logic & Comparisons (5 problems)

### Problem 1 — Beginner: Prediction
Write these expressions and predict their output before running:
```python
print(7 > 5)
print(10 == 10)
print("dog" > "cat")
print(100 != 100)
print(3.5 <= 3.5)
```

**Answer:**
```
True
True
True
False
True
```

---

### Problem 2 — Beginner: String Comparison
Compare these strings: "apple", "banana", "apricot"
1. Which is smallest alphabetically?
2. Which is largest alphabetically?
3. Write an expression to check if "apricot" is between "apple" and "banana"

**Answer:**
1. "apple" (smallest)
2. "banana" (largest)
3. `"apple" < "apricot" < "banana"` → True

---

### Problem 3 — Intermediate: Complex Expressions
Predict the output:
```python
print(5 > 3 == True)
print("5" > "3")
print(len("hi") > 1)
print((10 > 5) == True)
print("abc" < "abd")
```

**Answer:**
```
True
True
True
True
True
```

---

### Problem 4 — Intermediate: Chained Comparisons
Rewrite using chained comparison:
```python
if x >= 0 and x <= 100:
    print("In range")
```

**Answer:**
```python
if 0 <= x <= 100:
    print("In range")
```

---

### Problem 5 — Challenge: Lexicographic Order
Order these from smallest to largest alphabetically:
- "zebra", "apple", "mango", "banana", "apricot"

**Answer:** apple, apricot, banana, mango, zebra

---

## Week 11: if/else Statements (5 problems)

### Problem 6 — Beginner: Even/Odd
Write an if statement that checks if a number is even (divisible by 2).

**Answer:**
```python
num = int(input("Number: "))
if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

---

### Problem 7 — Beginner: Voting
Ask the user for their age and print "You can vote" if age >= 18.

**Answer:**
```python
age = int(input("Age: "))
if age >= 18:
    print("You can vote")
else:
    print("You cannot vote yet")
```

---

### Problem 8 — Intermediate: Grade Classifier
Ask for a test score and print the letter grade:
- A (90+), B (80-89), C (70-79), D (60-69), F (<60)

**Answer:**
```python
score = int(input("Score: "))
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

---

### Problem 9 — Intermediate: Season Finder
Ask for a month number (1-12) and print the season:
- Winter: 12, 1, 2
- Spring: 3, 4, 5
- Summer: 6, 7, 8
- Fall: 9, 10, 11

**Answer:**
```python
month = int(input("Month: "))
if month in [12, 1, 2]:
    print("Winter")
elif month in [3, 4, 5]:
    print("Spring")
elif month in [6, 7, 8]:
    print("Summer")
else:
    print("Fall")
```

---

### Problem 10 — Challenge: Number Guessing Game
Build a guessing game:
1. Pick a random number 1-10
2. Ask user to guess
3. Print "Correct!" or "Wrong! It was [number]"

**Answer:**
```python
import random
secret = random.randint(1, 10)
guess = int(input("Guess (1-10): "))
if guess == secret:
    print("Correct!")
else:
    print(f"Wrong! It was {secret}")
```

---

## Week 12: Nested Conditionals & Complex Logic (5 problems)

### Problem 11 — Beginner: Nested Check
Check if a number is positive. If yes, check if it's even.

**Answer:**
```python
num = int(input("Number: "))
if num > 0:
    if num % 2 == 0:
        print("Positive and even")
    else:
        print("Positive and odd")
else:
    print("Not positive")
```

---

### Problem 12 — Intermediate: Login System
Create a login program:
1. Check username (must be "admin")
2. If correct, check password (must be "pass123")
3. If both correct, print "Login successful"
4. Different messages for each failure

**Answer:**
```python
username = input("Username: ")
if username == "admin":
    password = input("Password: ")
    if password == "pass123":
        print("Login successful")
    else:
        print("Wrong password")
else:
    print("User not found")
```

---

### Problem 13 — Intermediate: Eligibility Checker
Check if a user can borrow a book. They can if:
- They are a student AND
- Book is not overdue AND
- They haven't maxed out (5 books)

**Answer:**
```python
is_student = True
is_overdue = False
books_owned = 3
max_books = 5

if is_student and not is_overdue and books_owned < max_books:
    print("Can borrow")
else:
    print("Cannot borrow")
```

---

### Problem 14 — Challenge: Game Purchase Logic
Check if player can buy equipment:
1. Has enough gold (>= 100)
2. Has inventory space (< 5 items)

If can buy: purchase and update stats
If can't: explain why

**Answer:**
```python
gold = 150
inventory = 3
sword_cost = 100

if gold >= sword_cost:
    if inventory < 5:
        print("Purchase successful!")
        gold -= sword_cost
        inventory += 1
        print(f"Gold: {gold}, Items: {inventory}")
    else:
        print("Inventory full!")
else:
    print("Not enough gold")
```

---

### Problem 15 — Challenge: BMI Calculator
Calculate BMI: weight(lb) / height(in)² × 703
Classify:
- < 18.5: Underweight
- 18.5-24.9: Normal
- 25-29.9: Overweight
- 30+: Obese

**Answer:**
```python
weight = float(input("Weight (lbs): "))
height = float(input("Height (inches): "))
bmi = (weight / (height ** 2)) * 703

if bmi < 18.5:
    print("Underweight")
elif bmi < 25:
    print("Normal weight")
elif bmi < 30:
    print("Overweight")
else:
    print("Obese")
```

---

## Week 13: Real-World Applications (5 problems)

### Problem 16 — Beginner: Temperature Classifier
Classify temperature:
- < 32°F: Freezing
- 32-60°F: Cold
- 61-75°F: Comfortable
- 76-90°F: Hot
- > 90°F: Very Hot

**Answer:**
```python
temp = int(input("Temperature: "))
if temp < 32:
    print("Freezing")
elif temp <= 60:
    print("Cold")
elif temp <= 75:
    print("Comfortable")
elif temp <= 90:
    print("Hot")
else:
    print("Very Hot")
```

---

### Problem 17 — Intermediate: Discount Calculator
Apply discounts based on quantity:
- 0-4 items: 0%
- 5-9 items: 5%
- 10-19 items: 10%
- 20+ items: 15%

**Answer:**
```python
items = int(input("Items: "))
price = float(input("Price per item: "))

if items < 5:
    discount = 0.0
elif items < 10:
    discount = 0.05
elif items < 20:
    discount = 0.10
else:
    discount = 0.15

total = items * price
final = total * (1 - discount)
print(f"Total: ${final:.2f}")
```

---

### Problem 18 — Intermediate: Movie Ticket Pricing
Price by age + weekday discount:
- Child (< 13): $6
- Student (13-17): $8
- Adult (18-64): $10
- Senior (65+): $7
Discount: Mon-Thu 25%, Fri-Sun 10%

**Answer:**
```python
age = int(input("Age: "))
day = input("Day: ").lower()

if age < 13:
    base = 6
elif age < 18:
    base = 8
elif age < 65:
    base = 10
else:
    base = 7

if day in ["monday", "tuesday", "wednesday", "thursday"]:
    discount = 0.25
else:
    discount = 0.10

final = base * (1 - discount)
print(f"${final:.2f}")
```

---

### Problem 19 — Challenge: College Admission
Check eligibility. Person can attend if:
- GPA >= 3.0 AND SAT >= 1000
Print approved/denied with details

**Answer:**
```python
gpa = float(input("GPA: "))
sat = int(input("SAT: "))

if gpa >= 3.0 and sat >= 1000:
    print("APPROVED")
else:
    print("DENIED")
    if gpa < 3.0:
        print(f"  GPA low (have {gpa}, need 3.0)")
    if sat < 1000:
        print(f"  SAT low (have {sat}, need 1000)")
```

---

### Problem 20 — Challenge: Leap Year Checker
Year is leap if:
- Divisible by 4 AND
- NOT divisible by 100 OR divisible by 400

**Answer:**
```python
year = int(input("Year: "))

if year % 400 == 0:
    print(f"{year} is a leap year")
elif year % 100 == 0:
    print(f"{year} is not a leap year")
elif year % 4 == 0:
    print(f"{year} is a leap year")
else:
    print(f"{year} is not a leap year")
```

---

## Week 14: Review & Assessment (5 problems)

### Problem 21 — Beginner: Validation
Validate test score is 0-100:

**Answer:**
```python
score = int(input("Score: "))
if 0 <= score <= 100:
    print("Valid")
else:
    print("Invalid")
```

---

### Problem 22 — Intermediate: Password Strength
Check password:
- >= 8 chars AND has uppercase AND has digit

**Answer:**
```python
pw = input("Password: ")
if len(pw) >= 8 and any(c.isupper() for c in pw) and any(c.isdigit() for c in pw):
    print("Strong")
else:
    print("Weak")
```

---

### Problem 23 — Intermediate: Rock-Paper-Scissors
Single round game with random computer choice

**Answer:**
```python
import random
player = input("rock/paper/scissors: ").lower()
computer = random.choice(["rock", "paper", "scissors"])

if player == computer:
    print("Tie")
elif (player == "rock" and computer == "scissors") or \
     (player == "scissors" and computer == "paper") or \
     (player == "paper" and computer == "rock"):
    print("You win!")
else:
    print("Computer wins!")
```

---

### Problem 24 — Challenge: Access Control
Determine permissions by role:
- guest: view only
- user: view + comment
- moderator: view + comment + delete
- admin: all

**Answer:**
```python
role = input("Role: ").lower()

if role == "guest":
    can_view, can_comment, can_delete = True, False, False
elif role == "user":
    can_view, can_comment, can_delete = True, True, False
elif role == "moderator":
    can_view, can_comment, can_delete = True, True, True
elif role == "admin":
    can_view, can_comment, can_delete = True, True, True

if can_view:
    print("Can view")
if can_comment:
    print("Can comment")
if can_delete:
    print("Can delete")
```

---

### Problem 25 — Challenge: Game Character Creation
Create character with:
1. Age check (must be 13+)
2. Experience level determines difficulty
3. Difficulty determines starting health and equipment

**Answer:**
```python
age = int(input("Age: "))

if age < 13:
    print("Too young")
else:
    exp = int(input("Experience (1-10): "))

    if exp <= 3:
        difficulty, health = "Easy", 150
        weapon = "Wooden Sword"
    elif exp <= 6:
        difficulty, health = "Normal", 100
        weapon = "Iron Sword"
    else:
        difficulty, health = "Hard", 75
        weapon = "Steel Sword"

    print(f"Difficulty: {difficulty}")
    print(f"Health: {health}")
    print(f"Weapon: {weapon}")
```

---

## How to Use This Practice Bank

1. **Start with Beginner problems** to build confidence
2. **Move to Intermediate** once you understand basics
3. **Challenge problems** stretch your skills
4. **Code all solutions** — don't just read them
5. **Test with multiple inputs** — edge cases matter
6. **Review mistakes** — learn from errors

---

*Practice is how you master programming. Work through these problems!*
