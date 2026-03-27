# Day 11: Arithmetic Operators & Their Uses
**Learning Target:** I can use arithmetic operators to solve mathematical problems.

### Key Concepts
Python has seven main arithmetic operators:
- `+` **Addition:** combines two numbers
- `-` **Subtraction:** finds the difference
- `*` **Multiplication:** combines groups
- `/` **Division:** splits a quantity, always returns float even for whole numbers (10 / 2 = 5.0)
- `//` **Floor Division:** divides and rounds down to the nearest whole number (10 // 3 = 3)
- `%` **Modulus (Remainder):** returns what's left over after division (10 % 3 = 1)
- `**` **Exponentiation (Power):** raises a number to a power (2 ** 3 = 8)

**Key points:**
- `/` always returns a float: `10 / 2` = `5.0` (not 5)
- `//` returns an integer (floor division): `10 // 3` = `3`
- `%` is useful for checking if numbers are divisible or finding patterns
- `**` is used for powers and roots: `9 ** 0.5` = `3.0` (square root)

**Real-world uses:**
- Addition: total cost, total time, total distance
- Subtraction: change due, time remaining, difference
- Multiplication: total cost (price × quantity), area, compound calculations
- Division: average, unit price, splitting
- Modulus: checking if even/odd, cycling through patterns, remainders
- Exponentiation: compound interest, area/volume calculations, physics

### Code Examples
```python
# Basic arithmetic
print(10 + 3)      # 13
print(10 - 3)      # 7
print(10 * 3)      # 30
print(10 / 3)      # 3.3333... (float)
print(10 // 3)     # 3 (floor division)
print(10 % 3)      # 1 (remainder)
print(2 ** 8)      # 256 (2 to the power of 8)

# Using variables
principal = 1000
rate = 0.05
interest = principal * rate
print(f"Interest: ${interest:.2f}")

# Modulus for practical use (converting minutes to hours and minutes)
minutes = 95
hours = minutes // 60
remaining_minutes = minutes % 60
print(f"{minutes} minutes = {hours}h {remaining_minutes}m")

# Exponentiation
base = 5
exponent = 3
result = base ** exponent
print(f"{base} to the power of {exponent} = {result}")
```

### Guided Practice
Create a program that:
1. Uses all 7 arithmetic operators with the same two numbers
2. Shows the result of each operation with a label
3. Includes comments explaining what each operator does
4. Demonstrates a real-world use of modulus (e.g., converting time or checking even/odd)

### Practice Problems

**Problem 1 — Beginner:** Write a program that asks for two numbers and prints their sum, difference, product, and quotient.

**Problem 2 — Intermediate:** Convert 365 minutes to hours and remaining minutes using `//` and `%`. Display the result clearly.

**Problem 3 — Challenge:** Write a program that calculates the area and perimeter of a rectangle given length and width. (Area = L × W, Perimeter = 2L + 2W)

<details>
<summary>💡 Hints</summary>

- Problem 1: Use all four basic operators with the same two numbers
- Problem 2: Use // to get hours, % to get remaining minutes
- Problem 3: Make sure your output is labeled and formatted nicely with $ or units
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num1 = 15
num2 = 4
print(f"{num1} + {num2} = {num1 + num2}")
print(f"{num1} - {num2} = {num1 - num2}")
print(f"{num1} * {num2} = {num1 * num2}")
print(f"{num1} / {num2} = {num1 / num2:.2f}")

# Problem 2 Example
total_minutes = 365
hours = total_minutes // 60
remaining = total_minutes % 60
print(f"{total_minutes} minutes = {hours} hours and {remaining} minutes")

# Problem 3 Example
length = 12
width = 5
area = length * width
perimeter = 2 * length + 2 * width
print(f"Rectangle: {length} × {width}")
print(f"Area: {area} sq units")
print(f"Perimeter: {perimeter} units")
```

</details>

---
