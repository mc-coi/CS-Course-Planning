# Day 54: Practice with if/elif/else

**Learning Target:** I can apply if/elif/else patterns to real-world problems like grade calculators and menu systems.

---

## Learning Summary

You now know:
1. Boolean expressions (True/False)
2. Comparison operators (==, !=, <, >, <=, >=)
3. Logical operators (and, or, not)
4. if statements (single condition)
5. if/else (two paths)
6. if/elif/else (multiple paths)

---

## Real-World Applications

### Pattern 1: Grading Systems

```python
# Get score and calculate grade
score = int(input("Enter score (0-100): "))

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

# Calculate GPA
if grade == "A":
    gpa = 4.0
elif grade == "B":
    gpa = 3.0
elif grade == "C":
    gpa = 2.0
elif grade == "D":
    gpa = 1.0
else:
    gpa = 0.0

print(f"Score: {score}, Grade: {grade}, GPA: {gpa}")
```

### Pattern 2: Menu Systems

```python
# Simple menu
print("=== Game Menu ===")
print("1. Start Game")
print("2. Load Game")
print("3. Settings")
print("4. Exit")

choice = input("Choose (1-4): ")

if choice == "1":
    print("Starting new game...")
elif choice == "2":
    print("Loading game...")
elif choice == "3":
    print("Opening settings...")
elif choice == "4":
    print("Goodbye!")
else:
    print("Invalid choice")
```

### Pattern 3: Range Classification

```python
# BMI (Body Mass Index) classifier
weight = float(input("Weight (lbs): "))
height = float(input("Height (inches): "))

bmi = (weight / (height ** 2)) * 703

if bmi < 18.5:
    category = "Underweight"
elif bmi < 25:
    category = "Normal weight"
elif bmi < 30:
    category = "Overweight"
else:
    category = "Obese"

print(f"BMI: {bmi:.1f} - {category}")
```

---

## Guided Practice (20 minutes)

**Activity 1: Grade Calculator**

Build a program that:
1. Asks for student name and score
2. Calculates grade (A/B/C/D/F)
3. Calculates GPA (4.0/3.0/2.0/1.0/0.0)
4. Prints results

```python
name = input("Student name: ")
score = int(input("Score: "))

# Calculate grade
if score >= 90:
    grade = "A"
    gpa = 4.0
elif score >= 80:
    grade = "B"
    gpa = 3.0
elif score >= 70:
    grade = "C"
    gpa = 2.0
elif score >= 60:
    grade = "D"
    gpa = 1.0
else:
    grade = "F"
    gpa = 0.0

print(f"{name}: {score} → {grade} (GPA: {gpa})")
```

**Activity 2: Simple Menu**

Build a menu that asks the user what they want to do, then simulates doing it.

---

## Practice Problems

### Problem 1 — Beginner
Create a simple temperature classifier:
- < 32°F: Freezing
- 32-60°F: Cold
- 61-75°F: Comfortable
- 76-90°F: Hot
- > 90°F: Very Hot

```python
temp = int(input("Temperature (°F): "))

if :
    print("Freezing")
elif :
    print("Cold")
elif :
    print("Comfortable")
elif :
    print("Hot")
else:
    print("Very Hot")
```

---

### Problem 2 — Intermediate
Build a discount calculator:
- 0-4 items: 0% discount
- 5-9 items: 5% discount
- 10-19 items: 10% discount
- 20+ items: 15% discount

```python
items = int(input("Number of items: "))
price = float(input("Price per item: "))

# Calculate discount
if :
    discount = 0.0
elif :
    discount = 0.05
elif :
    discount = 0.10
else:
    discount = 0.15

total = items * price
savings = total * discount
final = total - savings

print(f"Subtotal: ${total:.2f}")
print(f"Discount: ${savings:.2f}")
print(f"Total: ${final:.2f}")
```

---

### Problem 3 — Challenge
Build a ticket price calculator for a movie theater:
- Child (< 13): $6
- Student (13-17): $8
- Adult (18-64): $10
- Senior (65+): $7

Also apply a weekday discount:
- Monday-Thursday: 25% off
- Friday-Sunday: 10% off

```python
age = int(input("Your age: "))
day = input("Day of week: ").lower()

# Determine base price
if age < 13:
    base_price = 6
elif age < 18:
    base_price = 8
elif age < 65:
    base_price = 10
else:
    base_price = 7

# Apply weekday discount
if day in ["monday", "tuesday", "wednesday", "thursday"]:
    discount = 0.25
else:
    discount = 0.10

final_price = base_price * (1 - discount)
print(f"Price: ${final_price:.2f}")
```

---

## Hints

- **Problem 1:** Use inequalities: `< 32`, `32 <= temp <= 60`, etc.
- **Problem 2:** Check item count ranges
- **Problem 3:** Combine two if/elif chains; multiply by (1 - discount)

---

## Sample Answers

### Problem 1 Example
```python
temp = int(input("Temperature (°F): "))

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

### Problem 2 Example
```python
items = int(input("Number of items: "))
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
savings = total * discount
final = total - savings

print(f"Subtotal: ${total:.2f}")
print(f"Discount: ${savings:.2f}")
print(f"Total: ${final:.2f}")
```

### Problem 3 Example
```python
age = int(input("Your age: "))
day = input("Day of week: ").lower()

if age < 13:
    base_price = 6
elif age < 18:
    base_price = 8
elif age < 65:
    base_price = 10
else:
    base_price = 7

if day in ["monday", "tuesday", "wednesday", "thursday"]:
    discount = 0.25
else:
    discount = 0.10

final_price = base_price * (1 - discount)
print(f"Price: ${final_price:.2f}")
```

---

## Key Takeaway

if/elif/else patterns solve real problems. Recognize the pattern: range classification, menu selection, tiered pricing. These are everywhere in software!
