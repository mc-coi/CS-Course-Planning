# Day 2: Numeric Types: int & float
**Learning Target:** I can use integer and float types and perform arithmetic.

### Key Concepts
- **Integers** (`int`) are whole numbers: -5, 0, 42, 1000000
- **Floats** (`float`) are decimals: 3.14, -0.5, 2.0 (note the decimal point!)

**Important:** In Python 3, division `/` always returns a float, even if the result is a whole number: `10 / 2 = 5.0`

The `abs()` function returns absolute value (distance from zero).
The `round()` function rounds to a specified decimal place: `round(3.14159, 2)` → `3.14`
The `pow()` function is the same as `**`: `pow(2, 8)` → `256`

**Order of operations** (PEMDAS): Parentheses, Exponents, Multiplication/Division (left-to-right), Addition/Subtraction (left-to-right)

### Code Examples
```python
# Integer arithmetic
print(10 + 3)     # 13
print(10 - 3)     # 7
print(10 * 3)     # 30
print(10 / 3)     # 3.3333... (float)
print(10 // 3)    # 3 (integer division, floor)
print(10 % 3)     # 1 (remainder)
print(2 ** 8)     # 256 (exponentiation)

# Absolute value
print(abs(-5))    # 5
print(abs(3.14))  # 3.14

# Rounding
print(round(3.14159))     # 3 (to nearest whole)
print(round(3.14159, 2))  # 3.14 (to 2 decimals)
print(round(3.14159, 3))  # 3.142 (to 3 decimals)

# Power function
print(pow(2, 8))  # 256 (same as 2**8)
print(pow(5, 3))  # 125

# Working with variables
x = 15
y = 4
print(x + y)      # 19
print(x / y)      # 3.75
print(x // y)     # 3
print(x % y)      # 3 (15 = 4*3 + 3)
```

### Guided Practice
Write a program that:
1. Asks for two numbers
2. Prints their sum, difference, product, quotient, floor quotient, remainder, and power (first to the second)
3. Rounds each result to 2 decimal places

### Practice Problems
**Problem 1 — Beginner:** Write a program that uses at least 5 different arithmetic operators.

```python
x =
y =

print()  # +
print()  # -
print()  # *
print()  # /
print()  # //
```

**Problem 2 — Intermediate:** Create a program that asks for a radius and calculates the area of a circle using π (use `import math` and `math.pi`).

**Problem 3 — Challenge:** Calculate the hypotenuse of a right triangle given two sides using the Pythagorean theorem (a² + b² = c²).

<details>
<summary>💡 Hints</summary>

- Problem 1: Choose any two numbers and show different operations
- Problem 2: Area = π × r²
- Problem 3: c = sqrt(a² + b²) — use `math.sqrt()`
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2 Example
import math
radius = float(input("Radius: "))
area = math.pi * radius ** 2
print(f"Area: {area:.2f}")

# Problem 3 Example
import math
a = float(input("Side a: "))
b = float(input("Side b: "))
c = math.sqrt(a**2 + b**2)
print(f"Hypotenuse: {c:.2f}")
```
</details>

---