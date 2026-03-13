# Day 8: Expressions, Constants & math Module
**Learning Target:** I can write complex expressions and use the math module.

### Key Concepts
**Constants** are variables whose values should never change. By convention, use ALL_CAPS: `MAX_ATTEMPTS = 3`, `TAX_RATE = 0.0925`

The **math module** provides mathematical functions and constants:
- `math.sqrt(x)` - square root
- `math.ceil(x)` - round up
- `math.floor(x)` - round down
- `math.pi` - π (3.14159...)
- `math.e` - Euler's number (2.71828...)
- `math.pow(x, y)` - x to the power of y (same as `x ** y`)

To use: `import math` at the top of your program.

### Code Examples
```python
import math

# Constants (use ALL_CAPS)
TAX_RATE = 0.0925
DISCOUNT = 0.15
MAX_ATTEMPTS = 3
SPEED_OF_LIGHT = 299_792_458  # underscores for readability

# Using constants
price = 100
tax = price * TAX_RATE
print(f"Tax: ${tax:.2f}")

# Math module
print(math.sqrt(144))    # 12.0
print(math.sqrt(2))      # 1.414...
print(math.ceil(3.2))    # 4 (round up)
print(math.floor(3.9))   # 3 (round down)
print(math.pi)           # 3.14159...
print(math.e)            # 2.71828...

# Practical example: Circle area
radius = 5
area = math.pi * radius ** 2
print(f"Area: {area:.2f}")  # Area: 78.54

# Distance between two points
x1, y1 = 0, 0
x2, y2 = 3, 4
distance = math.sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2)
print(f"Distance: {distance}")  # Distance: 5.0
```

### Guided Practice
Write a program that:
1. Defines constants for tax rate and discount
2. Asks for a price
3. Calculates and prints price with tax applied
4. Calculates area and circumference of a circle using `math.pi`

### Practice Problems
**Problem 1 — Beginner:** Use `math.sqrt()` and `math.pi` to calculate the area of a circle with radius 5.

```python
import math

radius = 5

print()
```

**Problem 2 — Intermediate:** Write a distance calculator using the distance formula: d = √((x₂-x₁)² + (y₂-y₁)²)

**Problem 3 — Challenge:** Create a program with at least 3 constants and use `math.ceil()` and `math.floor()` to demonstrate rounding up/down.

<details>
<summary>💡 Hints</summary>

- Problem 1: area = math.pi × r²
- Problem 2: Use math.sqrt() and the formula with variables
- Problem 3: Define MAX_PRICE, MIN_WAGE, TAX_RATE, then use ceil/floor on calculations
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
import math
radius = 5
area = math.pi * radius ** 2
print(f"Area: {area:.2f}")

# Problem 2 Example
import math
x1 = float(input("X1: "))
y1 = float(input("Y1: "))
x2 = float(input("X2: "))
y2 = float(input("Y2: "))
distance = math.sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2)
print(f"Distance: {distance:.2f}")
```
</details>

---