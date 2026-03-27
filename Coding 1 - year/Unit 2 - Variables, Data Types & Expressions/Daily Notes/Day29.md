# Day 29: The Math Module — import math, math.sqrt(), math.pi, math.ceil/floor

**Learning Target:** I can import and use the math module to perform advanced mathematical operations.

### Key Concepts

The **math module** provides mathematical functions and constants that aren't built into Python by default. You access it using the `import` statement.

**`import math`** loads the math module. Then use dot notation: `math.sqrt()`, `math.pi`, etc.

**Common math functions:**
- `math.sqrt(x)` : square root
- `math.pow(x, y)` : x to the power of y (same as `x ** y`)
- `math.ceil(x)` : round UP to nearest integer
- `math.floor(x)` : round DOWN to nearest integer
- `math.fabs(x)` : absolute value (like `abs()`)

**Math constants:**
- `math.pi` : π ≈ 3.14159...
- `math.e` : e ≈ 2.71828...

**Important:** Before using a function from the math module, you MUST import it first. If you forget `import math`, you'll get a NameError.

You can also use `from math import pi` to import specific items, then use `pi` directly without the `math.` prefix.

### Code Examples

```python
import math

# Square root
print(math.sqrt(16))    # 4.0
print(math.sqrt(2))     # 1.414...
print(math.sqrt(25))    # 5.0

# Power function
print(math.pow(2, 8))   # 256.0
print(math.pow(5, 3))   # 125.0

# Using the constant pi
print(math.pi)          # 3.14159...
radius = 5
area = math.pi * radius ** 2
print(area)             # 78.5398...

# Rounding functions
print(math.ceil(3.2))   # 4 (round up)
print(math.ceil(3.9))   # 4
print(math.floor(3.2))  # 3 (round down)
print(math.floor(3.9))  # 3

# Absolute value
print(math.fabs(-5))    # 5.0
print(math.fabs(3.14))  # 3.14

# Practical example: distance formula
import math
x1, y1 = 0, 0
x2, y2 = 3, 4
distance = math.sqrt((x2 - x1)**2 + (y2 - y1)**2)
print(distance)  # 5.0

# Pythagorean theorem
a = 3
b = 4
c = math.sqrt(a**2 + b**2)
print(f"Hypotenuse: {c}")  # 5.0

# Circle calculations
radius = float(input("Radius: "))
area = math.pi * radius ** 2
circumference = 2 * math.pi * radius
print(f"Area: {area:.2f}")
print(f"Circumference: {circumference:.2f}")

# Alternative: import specific items
from math import pi, sqrt
print(pi)       # 3.14159...
print(sqrt(16)) # 4.0
```

### Guided Practice

1. Import the math module.
2. Calculate the hypotenuse of a right triangle with sides 5 and 12.
3. Calculate the area of a circle with radius 7 (use `math.pi`).
4. Use `math.ceil()` and `math.floor()` on the number 3.7.
5. Use the distance formula to find distance between points (0,0) and (6,8).

### Practice Problems

**Problem 1 — Beginner:**
- Ask for the radius of a circle
- Calculate area using `math.pi * r ** 2`
- Calculate circumference using `2 * math.pi * r`
- Print both with 2 decimal places

```python
import math

radius = float(input("Radius: "))

area =
circumference =

print(f"Area: {area:.2f}")
print(f"Circumference: {circumference:.2f}")
```

**Problem 2 — Intermediate:**
- Ask the user for two numbers (sides of a right triangle)
- Calculate the hypotenuse using `math.sqrt(a**2 + b**2)`
- Print the hypotenuse with 2 decimal places
- Also print the perimeter of the triangle

**Problem 3 — Challenge:**
- Ask the user for a number
- Calculate its square root using `math.sqrt()`
- Round the square root UP using `math.ceil()`
- Round the square root DOWN using `math.floor()`
- Print both rounded values and the exact square root
- Calculate the distance between the original number and the rounded values

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `import math` at the top. Formula: area = π * r², circumference = 2 * π * r.
- Problem 2: Use `math.sqrt(a**2 + b**2)` for hypotenuse. Perimeter = a + b + c.
- Problem 3: Use `math.sqrt()`, `math.ceil()`, `math.floor()`. Distance is `|original - rounded|`.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
import math
radius = float(input("Radius: "))
area = math.pi * radius ** 2
circumference = 2 * math.pi * radius
print(f"Area: {area:.2f}")
print(f"Circumference: {circumference:.2f}")

# Problem 2 Example
import math
a = float(input("Side a: "))
b = float(input("Side b: "))
c = math.sqrt(a**2 + b**2)
perimeter = a + b + c
print(f"Hypotenuse: {c:.2f}")
print(f"Perimeter: {perimeter:.2f}")

# Problem 3 Example
import math
num = float(input("Number: "))
sqrt_val = math.sqrt(num)
ceil_val = math.ceil(sqrt_val)
floor_val = math.floor(sqrt_val)
print(f"Square root: {sqrt_val}")
print(f"Rounded up: {ceil_val}")
print(f"Rounded down: {floor_val}")
```

</details>

---
