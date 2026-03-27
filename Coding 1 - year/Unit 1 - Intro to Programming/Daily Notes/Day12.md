# Day 12: Order of Operations (PEMDAS) in Python
**Learning Target:** I can apply the order of operations correctly in Python expressions.

### Key Concepts
Python follows the standard mathematical order of operations, called **PEMDAS** (or BODMAS in some countries):

1. **Parentheses** (or Brackets) — calculations inside () first
2. **Exponents** (or Orders) — powers like `**`
3. **Multiplication & Division** — left to right (same precedence)
4. **Addition & Subtraction** — left to right (same precedence)

**Important:** Operators with the same precedence are evaluated left to right.

Examples:
- `2 + 3 * 4` = `2 + 12` = `14` (NOT `5 * 4 = 20`)
- `(2 + 3) * 4` = `5 * 4` = `20` (parentheses first!)
- `10 - 5 - 2` = `5 - 2` = `3` (left to right)
- `2 ** 3 ** 2` = `2 ** 9` = `512` (exponents are right to left!)
- `10 / 2 * 5` = `5 * 5` = `25` (division and multiplication left to right)

**Use parentheses** to make your intent clear, even if not strictly necessary:
- `(2 + 3) * 4` is clearer than `2 + 3 * 4`
- `(principal + interest)` is clearer than showing the calculation
- `(1 + rate) ** years` makes compound interest formula clear

### Code Examples
```python
# Order of operations examples
print(2 + 3 * 4)           # 14, not 20
print((2 + 3) * 4)         # 20
print(10 - 3 - 2)          # 5 (left to right)
print(2 ** 3 ** 2)         # 512 (right to left for exponents)
print((2 ** 3) ** 2)       # 64 (8 squared)

# Real-world calculation: compound interest
principal = 1000
rate = 0.05  # 5%
years = 3
amount = principal * (1 + rate) ** years
print(f"Amount after {years} years: ${amount:.2f}")

# Calculating average with proper order
score1, score2, score3 = 85, 92, 78
average = (score1 + score2 + score3) / 3
print(f"Average: {average:.2f}")

# Temperature conversion with proper grouping
fahrenheit = 68
celsius = (fahrenheit - 32) * 5 / 9
print(f"{fahrenheit}°F = {celsius:.1f}°C")
```

### Guided Practice
Create a program that:
1. Calculates the area of a rectangle with complex formula using parentheses
2. Calculates the volume of a rectangular box (length × width × height)
3. Demonstrates why parentheses matter by showing two different results
4. Includes comments explaining the order of operations

### Practice Problems

**Problem 1 — Beginner:** Predict the output of these expressions, then write code to verify:
- `5 + 3 * 2`
- `(5 + 3) * 2`
- `10 / 2 * 5`
- `10 / (2 * 5)`

**Problem 2 — Intermediate:** Write a program that calculates the area of a triangle using the formula: Area = (base × height) / 2. Ensure proper order of operations.

**Problem 3 — Challenge:** Write a program that calculates the future value using compound interest: FV = P(1 + r)^n where P=principal, r=rate, n=years. Use proper parentheses.

<details>
<summary>💡 Hints</summary>

- Problem 1: Remember PEMDAS—multiplication before addition
- Problem 2: Make sure to use parentheses clearly
- Problem 3: The (1 + r) must be calculated before raising to power n
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Verification
print(5 + 3 * 2)          # 11 (multiply first)
print((5 + 3) * 2)        # 16 (parentheses first)
print(10 / 2 * 5)         # 25.0 (left to right)
print(10 / (2 * 5))       # 1.0 (parentheses first)

# Problem 2 Example
base = 8
height = 6
area = (base * height) / 2
print(f"Triangle area: {area}")

# Problem 3 Example
principal = 500
rate = 0.04
years = 10
future_value = principal * (1 + rate) ** years
print(f"Future value: ${future_value:.2f}")
```

</details>

---
