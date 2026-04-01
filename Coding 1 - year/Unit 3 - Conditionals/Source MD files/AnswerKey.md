# Unit 3 Answer Key — 25 Problems

## Week 10: Boolean Logic & Comparisons

---

## Problem 1: Prediction - Comparison Results

Write these expressions and predict their output before running:
```python
print(7 > 5)
print(10 == 10)
print("dog" > "cat")
print(100 != 100)
print(3.5 <= 3.5)
```

### Solution
```python
# Evaluate each comparison
print(7 > 5)      # True: 7 is greater than 5
print(10 == 10)   # True: 10 equals 10
print("dog" > "cat")  # True: "dog" comes after "cat" alphabetically
print(100 != 100)     # False: 100 equals 100, so not equal is false
print(3.5 <= 3.5)     # True: 3.5 is equal to 3.5
```

### Expected Output
```
True
True
True
False
True
```

### Common Mistakes
- Confusing < and > (less than vs. greater than)
- Not understanding string comparison (lexicographic order)
- Using = instead of == for comparison

---

## Problem 2: String Comparison

Compare these strings: "apple", "banana", "apricot"
1. Which is smallest alphabetically?
2. Which is largest alphabetically?
3. Write an expression to check if "apricot" is between "apple" and "banana"

### Solution
```python
# 1. Smallest alphabetically
print("apple")  # "apple"

# 2. Largest alphabetically
print("banana")  # "banana"

# 3. Check if "apricot" is between "apple" and "banana"
result = "apple" < "apricot" < "banana"
print(result)  # True
```

### Expected Output
```
apple
banana
True
```

### Common Mistakes
- Not understanding alphabetical ordering (compare first letter, then second, etc.)
- Using wrong comparison operators

---

## Problem 3: Complex Comparison Expressions

Predict the output:
```python
print(5 > 3 == True)
print("5" > "3")
print(len("hi") > 1)
print((10 > 5) == True)
print("abc" < "abd")
```

### Solution
```python
# Evaluate each expression carefully
print(5 > 3 == True)   # True: (5 > 3) is True, True == True is True
print("5" > "3")       # True: "5" comes after "3" in ASCII
print(len("hi") > 1)   # True: len("hi") is 2, 2 > 1 is True
print((10 > 5) == True)  # True: (10 > 5) is True, True == True is True
print("abc" < "abd")   # True: "abc" comes before "abd" alphabetically
```

### Expected Output
```
True
True
True
True
True
```

### Common Mistakes
- Forgetting that comparisons return boolean values
- Not understanding ASCII/alphabetical ordering of strings

---

## Problem 4: Chained Comparisons

Rewrite using chained comparison:
```python
if x >= 0 and x <= 100:
    print("In range")
```

### Solution
```python
# Original (also correct):
# if x >= 0 and x <= 100:

# Chained (cleaner):
if 0 <= x <= 100:
    print("In range")
```

### Expected Output
```
In range
```

### Common Mistakes
- Not understanding that chained comparisons are equivalent to "and"
- Reversing the order (100 <= x <= 0 would always be false)

---

## Problem 5: Lexicographic Order

Order these from smallest to largest alphabetically:
- "zebra", "apple", "mango", "banana", "apricot"

### Solution
```python
# Sort alphabetically
words = ["zebra", "apple", "mango", "banana", "apricot"]
words.sort()
print(words)

# Or simply list them in order:
# "apple", "apricot", "banana", "mango", "zebra"
```

### Expected Output
```
['apple', 'apricot', 'banana', 'mango', 'zebra']
```

### Common Mistakes
- Not understanding alphabetical ordering correctly
- Putting "apricot" before "apple" (both start with "a", but check second letter)

---

## Week 11: if/else Statements

---

## Problem 6: Even/Odd Check

Write an if statement that checks if a number is even (divisible by 2).

### Solution
```python
# Get a number from user
num = int(input("Number: "))

# Check if divisible by 2
if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

### Expected Output
```
Number: 4
Even
```

### Common Mistakes
- Using % incorrectly or not understanding modulo
- Swapping the outputs for even/odd

---

## Problem 7: Voting Eligibility

Ask the user for their age and print "You can vote" if age >= 18.

### Solution
```python
# Ask for age
age = int(input("Age: "))

# Check voting eligibility
if age >= 18:
    print("You can vote")
else:
    print("You cannot vote yet")
```

### Expected Output
```
Age: 20
You can vote
```

### Common Mistakes
- Using > instead of >= (18 year olds should be able to vote)
- Not converting input to int

---

## Problem 8: Grade Classifier

Ask for a test score and print the letter grade:
- A (90+), B (80-89), C (70-79), D (60-69), F (<60)

### Solution
```python
# Get test score
score = int(input("Score: "))

# Determine letter grade
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

### Expected Output
```
Score: 85
B
```

### Common Mistakes
- Checking ranges incorrectly (e.g., score >= 80 and score < 90 instead of just >= 80)
- Not using elif properly (extra if statements cause all conditions to be checked)

---

## Problem 9: Season Finder

Ask for a month number (1-12) and print the season:
- Winter: 12, 1, 2
- Spring: 3, 4, 5
- Summer: 6, 7, 8
- Fall: 9, 10, 11

### Solution
```python
# Get month number
month = int(input("Month: "))

# Determine season
if month in [12, 1, 2]:
    print("Winter")
elif month in [3, 4, 5]:
    print("Spring")
elif month in [6, 7, 8]:
    print("Summer")
else:
    print("Fall")
```

### Expected Output
```
Month: 3
Spring
```

### Common Mistakes
- Not grouping months correctly (e.g., putting 3 in winter)
- Using multiple if statements instead of elif

---

## Problem 10: Number Guessing Game

Build a guessing game:
1. Pick a random number 1-10
2. Ask user to guess
3. Print "Correct!" or "Wrong! It was [number]"

### Solution
```python
# Import random module
import random

# Pick a random number 1-10
secret = random.randint(1, 10)

# Ask user to guess
guess = int(input("Guess (1-10): "))

# Check if correct
if guess == secret:
    print("Correct!")
else:
    print(f"Wrong! It was {secret}")
```

### Expected Output
```
Guess (1-10): 7
Wrong! It was 3
```

### Common Mistakes
- Forgetting to import random
- Using randint(1, 11) instead of randint(1, 10)

---

## Week 12: Nested Conditionals & Complex Logic

---

## Problem 11: Nested Positive/Even Check

Check if a number is positive. If yes, check if it's even.

### Solution
```python
# Get a number
num = int(input("Number: "))

# First check if positive
if num > 0:
    # If positive, check if even
    if num % 2 == 0:
        print("Positive and even")
    else:
        print("Positive and odd")
else:
    print("Not positive")
```

### Expected Output
```
Number: 8
Positive and even
```

### Common Mistakes
- Not indenting the nested if statement properly
- Checking both conditions at once instead of nesting

---

## Problem 12: Login System

Create a login program:
1. Check username (must be "admin")
2. If correct, check password (must be "pass123")
3. If both correct, print "Login successful"
4. Different messages for each failure

### Solution
```python
# Ask for username
username = input("Username: ")

# Check username first
if username == "admin":
    # If username is correct, check password
    password = input("Password: ")
    if password == "pass123":
        print("Login successful")
    else:
        print("Wrong password")
else:
    print("User not found")
```

### Expected Output
```
Username: admin
Password: pass123
Login successful
```

### Common Mistakes
- Checking both conditions with "and" instead of nesting
- Not providing different error messages

---

## Problem 13: Eligibility Checker

Check if a user can borrow a book. They can if:
- They are a student AND
- Book is not overdue AND
- They haven't maxed out (5 books)

### Solution
```python
# Define conditions
is_student = True
is_overdue = False
books_owned = 3
max_books = 5

# Check all conditions with AND
if is_student and not is_overdue and books_owned < max_books:
    print("Can borrow")
else:
    print("Cannot borrow")
```

### Expected Output
```
Can borrow
```

### Common Mistakes
- Using OR instead of AND (requires all conditions to be true)
- Not using "not" for the overdue check

---

## Problem 14: Game Purchase Logic

Check if player can buy equipment:
1. Has enough gold (>= 100)
2. Has inventory space (< 5 items)

If can buy: purchase and update stats
If can't: explain why

### Solution
```python
# Player status
gold = 150
inventory = 3
sword_cost = 100

# Check if can purchase
if gold >= sword_cost:
    if inventory < 5:
        # Purchase successful
        print("Purchase successful!")
        gold -= sword_cost
        inventory += 1
        print(f"Gold: {gold}, Items: {inventory}")
    else:
        # Inventory full
        print("Inventory full!")
else:
    # Not enough gold
    print("Not enough gold")
```

### Expected Output
```
Purchase successful!
Gold: 50, Items: 4
```

### Common Mistakes
- Not nesting the conditions properly
- Updating stats even when purchase fails

---

## Problem 15: BMI Calculator

Calculate BMI: weight(lb) / height(in)² × 703
Classify:
- < 18.5: Underweight
- 18.5-24.9: Normal
- 25-29.9: Overweight
- 30+: Obese

### Solution
```python
# Get weight and height
weight = float(input("Weight (lbs): "))
height = float(input("Height (inches): "))

# Calculate BMI
bmi = (weight / (height ** 2)) * 703

# Classify BMI
if bmi < 18.5:
    print("Underweight")
elif bmi < 25:
    print("Normal weight")
elif bmi < 30:
    print("Overweight")
else:
    print("Obese")
```

### Expected Output
```
Weight (lbs): 150
Height (inches): 70
Normal weight
```

### Common Mistakes
- Using wrong formula for BMI
- Overlapping ranges (e.g., checking bmi >= 18.5 and bmi <= 24.9 separately)

---

## Week 13: Real-World Applications

---

## Problem 16: Temperature Classifier

Classify temperature:
- < 32°F: Freezing
- 32-60°F: Cold
- 61-75°F: Comfortable
- 76-90°F: Hot
- > 90°F: Very Hot

### Solution
```python
# Get temperature
temp = int(input("Temperature: "))

# Classify
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

### Expected Output
```
Temperature: 72
Comfortable
```

### Common Mistakes
- Overlapping ranges or missing edge cases
- Not using <= for inclusive comparisons

---

## Problem 17: Discount Calculator

Apply discounts based on quantity:
- 0-4 items: 0%
- 5-9 items: 5%
- 10-19 items: 10%
- 20+ items: 15%

### Solution
```python
# Get items and price per item
items = int(input("Items: "))
price = float(input("Price per item: "))

# Determine discount
if items < 5:
    discount = 0.0
elif items < 10:
    discount = 0.05
elif items < 20:
    discount = 0.10
else:
    discount = 0.15

# Calculate final price
total = items * price
final = total * (1 - discount)
print(f"Total: ${final:.2f}")
```

### Expected Output
```
Items: 15
Price per item: 10.00
Total: $135.00
```

### Common Mistakes
- Using >= instead of < for ranges
- Not calculating the discount correctly (should be 1 - discount)

---

## Problem 18: Movie Ticket Pricing

Price by age + weekday discount:
- Child (< 13): $6
- Student (13-17): $8
- Adult (18-64): $10
- Senior (65+): $7
Discount: Mon-Thu 25%, Fri-Sun 10%

### Solution
```python
# Get age and day
age = int(input("Age: "))
day = input("Day: ").lower()

# Determine base price
if age < 13:
    base = 6
elif age < 18:
    base = 8
elif age < 65:
    base = 10
else:
    base = 7

# Determine discount
if day in ["monday", "tuesday", "wednesday", "thursday"]:
    discount = 0.25
else:
    discount = 0.10

# Calculate final price
final = base * (1 - discount)
print(f"${final:.2f}")
```

### Expected Output
```
Age: 25
Day: monday
$7.50
```

### Common Mistakes
- Not considering both age and day factors
- Using wrong discount percentages

---

## Problem 19: College Admission

Check eligibility. Person can attend if:
- GPA >= 3.0 AND SAT >= 1000
Print approved/denied with details

### Solution
```python
# Get GPA and SAT score
gpa = float(input("GPA: "))
sat = int(input("SAT: "))

# Check eligibility
if gpa >= 3.0 and sat >= 1000:
    print("APPROVED")
else:
    print("DENIED")
    if gpa < 3.0:
        print(f"  GPA low (have {gpa}, need 3.0)")
    if sat < 1000:
        print(f"  SAT low (have {sat}, need 1000)")
```

### Expected Output
```
GPA: 2.8
SAT: 1050
DENIED
  GPA low (have 2.8, need 3.0)
```

### Common Mistakes
- Not providing specific feedback for why denied
- Using OR instead of AND

---

## Problem 20: Leap Year Checker

Year is leap if:
- Divisible by 4 AND
- NOT divisible by 100 OR divisible by 400

### Solution
```python
# Get year
year = int(input("Year: "))

# Check leap year logic
if year % 400 == 0:
    print(f"{year} is a leap year")
elif year % 100 == 0:
    print(f"{year} is not a leap year")
elif year % 4 == 0:
    print(f"{year} is a leap year")
else:
    print(f"{year} is not a leap year")
```

### Expected Output
```
Year: 2024
2024 is a leap year
```

### Common Mistakes
- Simplifying the logic too much (just checking divisible by 4)
- Getting the exception for centuries wrong

---

## Week 14: Review & Assessment

---

## Problem 21: Input Validation

Validate test score is 0-100:

### Solution
```python
# Get score
score = int(input("Score: "))

# Validate range
if 0 <= score <= 100:
    print("Valid")
else:
    print("Invalid")
```

### Expected Output
```
Score: 85
Valid
```

### Common Mistakes
- Using separate conditions instead of chained comparison
- Not handling out-of-range values

---

## Problem 22: Password Strength

Check password:
- >= 8 chars AND has uppercase AND has digit

### Solution
```python
# Get password
pw = input("Password: ")

# Check all requirements
if len(pw) >= 8 and any(c.isupper() for c in pw) and any(c.isdigit() for c in pw):
    print("Strong")
else:
    print("Weak")
```

### Expected Output
```
Password: MyPass123
Strong
```

### Common Mistakes
- Not using all three conditions
- Not using any() with generator expressions for character checks

---

## Problem 23: Rock-Paper-Scissors

Single round game with random computer choice

### Solution
```python
import random

# Get player choice
player = input("rock/paper/scissors: ").lower()

# Computer picks randomly
computer = random.choice(["rock", "paper", "scissors"])

# Determine winner
if player == computer:
    print("Tie")
elif (player == "rock" and computer == "scissors") or \
     (player == "scissors" and computer == "paper") or \
     (player == "paper" and computer == "rock"):
    print("You win!")
else:
    print("Computer wins!")
```

### Expected Output
```
rock/paper/scissors: rock
You win!
```

### Common Mistakes
- Not checking all winning combinations
- Not handling ties

---

## Problem 24: Access Control

Determine permissions by role:
- guest: view only
- user: view + comment
- moderator: view + comment + delete
- admin: all

### Solution
```python
# Get role
role = input("Role: ").lower()

# Set permissions based on role
if role == "guest":
    can_view, can_comment, can_delete = True, False, False
elif role == "user":
    can_view, can_comment, can_delete = True, True, False
elif role == "moderator":
    can_view, can_comment, can_delete = True, True, True
elif role == "admin":
    can_view, can_comment, can_delete = True, True, True

# Display permissions
if can_view:
    print("Can view")
if can_comment:
    print("Can comment")
if can_delete:
    print("Can delete")
```

### Expected Output
```
Role: moderator
Can view
Can comment
Can delete
```

### Common Mistakes
- Not setting all permissions correctly
- Using if instead of elif (inefficient)

---

## Problem 25: Game Character Creation

Create character with:
1. Age check (must be 13+)
2. Experience level determines difficulty
3. Difficulty determines starting health and equipment

### Solution
```python
# Get age
age = int(input("Age: "))

# Check age requirement
if age < 13:
    print("Too young")
else:
    # Get experience level
    exp = int(input("Experience (1-10): "))

    # Determine difficulty based on experience
    if exp <= 3:
        difficulty, health = "Easy", 150
        weapon = "Wooden Sword"
    elif exp <= 6:
        difficulty, health = "Normal", 100
        weapon = "Iron Sword"
    else:
        difficulty, health = "Hard", 75
        weapon = "Steel Sword"

    # Display character stats
    print(f"Difficulty: {difficulty}")
    print(f"Health: {health}")
    print(f"Weapon: {weapon}")
```

### Expected Output
```
Age: 16
Experience (1-10): 7
Difficulty: Hard
Health: 75
Weapon: Steel Sword
```

### Common Mistakes
- Not checking age first
- Not properly linking experience to difficulty settings
- Not displaying all information

---
