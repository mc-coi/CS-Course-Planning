# Unit 3: Conditionals - Answer Key

---

## Problem 1: Conditional Chain Prediction

### Solution
```python
# Predict the output
x = 15

if x > 10:
    print("Big")
elif x > 5:
    print("Medium")
else:
    print("Small")

# Step-by-step explanation
print("\nStep-by-step:")
print(f"x = {x}")
print(f"Is x > 10? {x > 10} → YES, so print 'Big' and skip the rest")
```

### Expected Output
```
Big

Step-by-step:
x = 15
Is x > 10? True → YES, so print 'Big' and skip the rest
```

### Common Mistakes
- Printing multiple outputs (elif/else are mutually exclusive with if)
- Forgetting that once a condition is true, the rest are skipped
- Evaluating conditions after a true condition

---

## Problem 2: Boolean Expression Step-by-Step

### Solution
```python
# Evaluate: not (5 > 3 and 2 < 1)

print("Expression: not (5 > 3 and 2 < 1)")
print()

# Step 1: Evaluate (5 > 3)
step1 = 5 > 3
print(f"Step 1: 5 > 3 = {step1}")

# Step 2: Evaluate (2 < 1)
step2 = 2 < 1
print(f"Step 2: 2 < 1 = {step2}")

# Step 3: Evaluate (5 > 3 and 2 < 1)
step3 = step1 and step2
print(f"Step 3: {step1} and {step2} = {step3}")

# Step 4: Evaluate not (result)
final = not step3
print(f"Step 4: not {step3} = {final}")

print(f"\nFinal answer: {final}")
```

### Expected Output
```
Expression: not (5 > 3 and 2 < 1)

Step 1: 5 > 3 = True
Step 2: 2 < 1 = False
Step 3: True and False = False
Step 4: not False = True

Final answer: True
```

### Common Mistakes
- Thinking "and" returns True if either is True (it requires both)
- Evaluating expressions in wrong order (parentheses first)
- Forgetting the "not" operator at the end
- Predicting False instead of True

---

## Problem 3: Speed Limit Checker

### Solution
```python
# Speed limit checker
speed_limit = 65
actual_speed = float(input("Enter actual speed: "))

# Calculate how much over the limit
amount_over = actual_speed - speed_limit

# Determine violation status
if amount_over > 10:
    print("Fine")
elif 1 <= amount_over <= 9:
    print("Warning")
else:  # amount_over <= 0
    print("Clear")
```

### Expected Output
```
Enter actual speed: 75
Fine
```

### Common Mistakes
- Using wrong comparison operators (> vs >=)
- Not calculating the difference correctly
- Using separate if statements instead of elif (would check all conditions)
- Not handling the boundary cases (exactly 1 over, exactly 10 over)

---

## Problem 4: Season Finder

### Solution
```python
# Season finder based on month number
month_num = int(input("Enter month number (1-12): "))

if month_num in [12, 1, 2]:
    season = "Winter"
elif month_num in [3, 4, 5]:
    season = "Spring"
elif month_num in [6, 7, 8]:
    season = "Summer"
elif month_num in [9, 10, 11]:
    season = "Fall"
else:
    season = "Invalid month"

print(f"Month {month_num}: {season}")
```

### Expected Output
```
Enter month number (1-12): 3
Month 3: Spring
```

### Common Mistakes
- Using wrong month assignments to seasons
- Forgetting that December is winter (wraps to next year)
- Not handling invalid months (13, 0, -1)
- Using separate if statements instead of elif

---

## Problem 5: Fix Logic Error with elif

### Solution
```python
# ORIGINAL CODE (WRONG):
# if score > 90: print("A")
# if score > 80: print("B")
# Both conditions could be true, printing both!

# FIXED CODE - Use elif:
score = float(input("Enter score: "))

if score > 90:
    print("A")
elif score > 80:
    print("B")
elif score > 70:
    print("C")
elif score > 60:
    print("D")
else:
    print("F")

# Explanation
print("\nExplanation:")
print("Using 'if' for each condition means ALL conditions are checked.")
print("Using 'elif' stops checking once a condition is true.")
```

### Expected Output
```
Enter score: 85
B

Explanation:
Using 'if' for each condition means ALL conditions are checked.
Using 'elif' stops checking once a condition is true.
```

### Common Mistakes
- Using multiple "if" statements instead of "elif"
- Not understanding the difference (if checks all, elif skips rest)
- Printing both "A" and "B" for scores over 90

---

## Problem 6: Triangle Classifier

### Solution
```python
# Triangle classifier
angle1 = float(input("Enter angle 1: "))
angle2 = float(input("Enter angle 2: "))
angle3 = float(input("Enter angle 3: "))

total_angles = angle1 + angle2 + angle3

# Check if valid triangle (sum = 180)
if total_angles != 180:
    print("Invalid triangle - angles don't sum to 180")
else:
    # Classify the triangle
    if angle1 == angle2 == angle3:
        print("Equilateral triangle")
    elif angle1 == angle2 or angle2 == angle3 or angle1 == angle3:
        print("Isosceles triangle")
    else:
        print("Scalene triangle")

    # Also check by angles
    if angle1 == 90 or angle2 == 90 or angle3 == 90:
        print("Right triangle")
    elif angle1 > 90 or angle2 > 90 or angle3 > 90:
        print("Obtuse triangle")
    else:
        print("Acute triangle")
```

### Expected Output
```
Enter angle 1: 60
Enter angle 2: 60
Enter angle 3: 60
Equilateral triangle
Acute triangle
```

### Common Mistakes
- Not checking if angles sum to 180 first
- Using wrong comparison for equality checks
- Not handling all triangle types (right, acute, obtuse)
- Forgetting that valid angles must be positive

---

## Problem 7: Chained Comparison

### Solution
```python
# ORIGINAL CODE:
# if x >= 0:
#     if x <= 100:
#         # code

# REWRITTEN - Chained comparison:
x = float(input("Enter a number: "))

# Using chained comparison (cleaner):
if 0 <= x <= 100:
    print(f"{x} is between 0 and 100 (inclusive)")
else:
    print(f"{x} is NOT between 0 and 100")

# Both approaches work:
print("\nComparison of approaches:")
print(f"Nested: if x >= 0: if x <= 100:")
print(f"Chained: if 0 <= x <= 100:")
```

### Expected Output
```
Enter a number: 50
50.0 is between 0 and 100 (inclusive)

Comparison of approaches:
Nested: if x >= 0: if x <= 100:
Chained: if 0 <= x <= 100:
```

### Common Mistakes
- Wrong order of values in chained comparison
- Forgetting you can chain multiple comparisons
- Using "and" instead of chained comparison (works but less elegant)
- Not understanding they're equivalent

---

## Problem 8: Assignment vs Comparison

### Solution
```python
# WRONG:
# if x = 5: print("five")
# This is an assignment (=), not a comparison (==)

# CORRECT:
x = 5

if x == 5:
    print("five")

# Explanation
print("\nExplanation:")
print("= is assignment (sets a value)")
print("== is comparison (checks if equal)")
print("Using = in if condition causes SyntaxError")
```

### Expected Output
```
five

Explanation:
= is assignment (sets a value)
== is comparison (checks if equal)
Using = in if condition causes SyntaxError
```

### Common Mistakes
- Using single = instead of == in comparisons
- Not understanding the difference between assignment and comparison
- This is a common syntax error

---

## Problem 9: Leap Year Checker

### Solution
```python
# Leap year checker
year = int(input("Enter a year: "))

# Leap year rules:
# - Divisible by 4 AND not divisible by 100, OR
# - Divisible by 400
is_leap = (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0)

if is_leap:
    print(f"{year} is a leap year")
else:
    print(f"{year} is not a leap year")

# Test with examples
print("\nTest cases:")
test_years = [2000, 1900, 2004, 2001]
for y in test_years:
    is_leap = (y % 4 == 0 and y % 100 != 0) or (y % 400 == 0)
    print(f"{y}: {is_leap}")
```

### Expected Output
```
Enter a year: 2024
2024 is a leap year

Test cases:
2000: True (divisible by 400)
1900: False (divisible by 100 but not 400)
2004: True (divisible by 4, not by 100)
2001: False (not divisible by 4)
```

### Common Mistakes
- Forgetting the 400 rule (century years need to be divisible by 400)
- Using "and" instead of "or" between the two conditions
- Not handling all four test cases correctly
- Logic errors in parentheses

---

## Problem 10: BMI Calculator with Classification

### Solution
```python
# BMI calculator with classification
# BMI = weight (lbs) / (height (in))^2 * 703
# OR: BMI = weight (kg) / (height (m))^2

weight = float(input("Enter weight (kg): "))
height = float(input("Enter height (m): "))

# Calculate BMI
bmi = weight / (height ** 2)

# Classify
if bmi < 18.5:
    classification = "Underweight"
elif 18.5 <= bmi < 25:
    classification = "Normal weight"
elif 25 <= bmi < 30:
    classification = "Overweight"
else:
    classification = "Obese"

# Print results
print(f"\nBMI: {bmi:.2f}")
print(f"Classification: {classification}")
```

### Expected Output
```
Enter weight (kg): 70
Enter height (m): 1.75

BMI: 22.86
Classification: Normal weight
```

### Common Mistakes
- Wrong BMI formula or units
- Wrong classification ranges
- Using exclusive boundaries instead of inclusive
- Not formatting output to 2 decimal places

---

## Problem 11: Boolean Expression with Zero

### Solution
```python
# Evaluate: a=5; b=0; if a and not b: print("yes") else: print("no")
a = 5
b = 0

# Step through the logic
print("Evaluate: if a and not b:")
print(f"a = {a} → {bool(a)} (non-zero is truthy)")
print(f"b = {b} → {bool(b)} (zero is falsy)")
print(f"not b = not {b} = {not b}")
print(f"a and not b = {a} and {not b} = {a and not b}")
print()

if a and not b:
    print("yes")
else:
    print("no")
```

### Expected Output
```
Evaluate: if a and not b:
a = 5 → True (non-zero is truthy)
b = 0 → False (zero is falsy)
not b = not 0 = True
a and not b = 5 and True = True

yes
```

### Common Mistakes
- Thinking 0 is True (it's falsy)
- Forgetting that non-zero numbers are truthy
- Not understanding "not" operator on booleans
- Predicting "no" instead of "yes"

---

## Problem 12: Simple Login

### Solution
```python
# Simple login checker
username = input("Enter username: ")
password = input("Enter password: ")

# Both must match specific values
correct_username = "admin"
correct_password = "password123"

if username == correct_username and password == correct_password:
    print("Login successful!")
else:
    print("Login failed!")
```

### Expected Output
```
Enter username: admin
Enter password: password123
Login successful!
```

### Common Mistakes
- Using "or" instead of "and" (both must match, not either)
- Using = instead of == for comparison
- Storing wrong credentials
- Not handling case sensitivity

---

## Problem 13: Rock-Paper-Scissors Outcome

### Solution
```python
# Rock-paper-scissors outcome checker
player1 = input("Player 1 - Enter choice (rock/paper/scissors): ").lower()
player2 = input("Player 2 - Enter choice (rock/paper/scissors): ").lower()

if player1 == player2:
    print("It's a tie!")
elif player1 == "rock" and player2 == "scissors":
    print("Player 1 wins! Rock beats scissors")
elif player1 == "scissors" and player2 == "paper":
    print("Player 1 wins! Scissors beats paper")
elif player1 == "paper" and player2 == "rock":
    print("Player 1 wins! Paper beats rock")
else:
    print("Player 2 wins!")
```

### Expected Output
```
Player 1 - Enter choice (rock/paper/scissors): rock
Player 2 - Enter choice (rock/paper/scissors): scissors
Player 1 wins! Rock beats scissors
```

### Common Mistakes
- Forgetting all three winning conditions
- Not checking for ties
- Using wrong logic (rock beats scissors, not the reverse)
- Not using .lower() to handle case sensitivity

---

## Problem 14: Shipping Cost Calculator

### Solution
```python
# Shipping cost calculator
weight = float(input("Enter weight (lbs): "))
wants_express = input("Want express shipping? (yes/no): ").lower() == "yes"
is_us = input("Is destination in US? (yes/no): ").lower() == "yes"

# Base rate by weight
if weight <= 5:
    base_rate = 5.00
elif weight <= 10:
    base_rate = 8.00
elif weight <= 20:
    base_rate = 12.00
else:
    base_rate = 15.00

# Total cost
total_cost = base_rate

# Add express fee if requested
if wants_express:
    total_cost += 5.00

# Add international fee if outside US
if not is_us:
    total_cost += 10.00

# Print results
print(f"\nShipping Cost:")
print(f"Base rate: ${base_rate:.2f}")
print(f"Express: {'$5.00' if wants_express else '$0.00'}")
print(f"International: {'$10.00' if not is_us else '$0.00'}")
print(f"Total: ${total_cost:.2f}")
```

### Expected Output
```
Enter weight (lbs): 8
Want express shipping? (yes/no): yes
Is destination in US? (yes/no): no

Shipping Cost:
Base rate: $8.00
Express: $5.00
International: $10.00
Total: $23.00
```

### Common Mistakes
- Not calculating each fee separately
- Using wrong weight thresholds
- Forgetting to add international fee when applicable
- Not formatting output as currency

---

## Problem 15: Debug Grade Assignment

### Solution
```python
# ORIGINAL CODE (3 ERRORS):
# grade=75; if grade>=90: letter="A" elif grade>=80: letter="B" elif grade>=70 letter="C" print(letter)

# ERROR 1: Missing colon after elif grade>=70
# ERROR 2: Missing colon after elif grade>=80 (actually OK)
# ERROR 3: indent/syntax after if statements

# FIXED CODE:
grade = 75

if grade >= 90:
    letter = "A"
elif grade >= 80:
    letter = "B"
elif grade >= 70:
    letter = "C"
elif grade >= 60:
    letter = "D"
else:
    letter = "F"

print(letter)

# Explanation
print("\nErrors found:")
print("1. Missing colon after 'elif grade>=70'")
print("2. Indentation issues")
print("3. Missing elif conditions for D and F")
```

### Expected Output
```
C

Errors found:
1. Missing colon after 'elif grade>=70'
2. Indentation issues
3. Missing elif conditions for D and F
```

### Common Mistakes
- Forgetting colons at the end of if/elif lines
- Indentation errors
- Not handling all grade ranges (D and F)
- Case sensitivity in variable names

---
