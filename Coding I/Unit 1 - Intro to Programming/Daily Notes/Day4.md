# Day 4: User Input & Simple Calculations
**Learning Target:** I can collect user input and perform basic arithmetic.

### Key Concepts
The `input()` function pauses the program and waits for the user to type something, then press Enter. **Important:** `input()` always returns a **string**, even if the user types numbers.

To use a number entered by the user in calculations, you must **convert** it using `int()` for whole numbers or `float()` for decimals.

**Arithmetic operators:**
- `+` addition
- `-` subtraction
- `*` multiplication
- `/` division (always returns a float, even if result is whole)
- `//` integer division (floor division, discards remainder)
- `%` modulus (returns the remainder)
- `**` exponentiation (power)

### Code Examples
```python
# Getting user input
name = input("What is your name? ")
print(f"Hello, {name}!")

# Converting input to numbers
age = int(input("How old are you? "))
gpa = float(input("What is your GPA? "))

# Arithmetic
print(10 + 3)      # 13
print(10 - 3)      # 7
print(10 * 3)      # 30
print(10 / 3)      # 3.333... (always float)
print(10 // 3)     # 3 (floor division)
print(10 % 3)      # 1 (remainder)
print(2 ** 8)      # 256 (2 to the power of 8)

# Tip calculator
bill = float(input("Enter bill amount: $"))
tip_percent = 0.20
tip = bill * tip_percent
total = bill + tip
print(f"Tip: ${tip:.2f}")
print(f"Total: ${total:.2f}")
```

### Guided Practice
Create a tip calculator that asks the user for:
1. The bill amount (float)
2. The tip percentage (as a decimal like 0.18 for 18%)
Then calculate and print the tip amount and total (including tip).

### Practice Problems
**Problem 1 — Beginner:** Write a program that asks for two numbers and prints their sum, difference, product, and quotient.

```python
# Starter code
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))

print("Sum:", )
print("Difference:", )
print("Product:", )
print("Quotient:", )
```

**Problem 2 — Intermediate:** Write a miles-to-kilometers converter. Ask the user for miles and print the equivalent in km (1 mile = 1.60934 km).

**Problem 3 — Challenge:** Write a program that asks for a rectangle's length and width, then prints its area, perimeter, and diagonal (use `import math` and `math.sqrt()`).

<details>
<summary>💡 Hints</summary>

- Problem 1: Use the arithmetic operators to combine num1 and num2
- Problem 2: Remember to convert input to float, then multiply
- Problem 3: Diagonal = sqrt(length² + width²)
</details>

<details>

<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))
print("Sum:", num1 + num2)
print("Difference:", num1 - num2)
print("Product:", num1 * num2)
print("Quotient:", num1 / num2)

# Problem 2 Example
miles = float(input("Enter miles: "))
kilometers = miles * 1.60934
print(f"{miles} miles = {kilometers:.2f} km")
```
</details>

---