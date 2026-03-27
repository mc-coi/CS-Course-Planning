# Day 26: Type Conversion — int(), float(), str(), bool()

**Learning Target:** I can convert between different data types and explain when and why type conversion is necessary.

### Key Concepts

**Type conversion** changes a value from one data type to another. Python provides functions to convert:

**`int(x)`** converts to an integer:
- `int("42")` → `42`
- `int(3.7)` → `3` (truncates, doesn't round)
- `int("3.5")` → ERROR (can't directly convert string with decimal to int)

**`float(x)`** converts to a float:
- `float("3.14")` → `3.14`
- `float(42)` → `42.0`
- `float("hello")` → ERROR

**`str(x)`** converts to a string:
- `str(42)` → `"42"`
- `str(3.14)` → `"3.14"`
- `str(True)` → `"True"`

**`bool(x)`** converts to a boolean:
- `bool(0)` → `False` (0 is falsy)
- `bool(1)` → `True` (non-zero is truthy)
- `bool("")` → `False` (empty string is falsy)
- `bool("hello")` → `True` (non-empty string is truthy)

**When do you need type conversion?**
1. `input()` returns a string, so you need `int(input())` to get a number.
2. Concatenation requires strings: `"Score: " + str(100)`.
3. Arithmetic requires numbers: `int("5") + int("3")`.

### Code Examples

```python
# Converting strings to numbers
num_str = "42"
num_int = int(num_str)
print(num_int + 8)  # 50

price_str = "9.99"
price_float = float(price_str)
print(price_float * 2)  # 19.98

# Converting numbers to strings
score = 95
print("Score: " + str(score))  # "Score: 95"

# Using input with conversion
age = int(input("How old are you? "))
print(f"Next year you'll be {age + 1}")

# Float to int (truncates)
print(int(3.7))    # 3 (not 4!)
print(int(3.2))    # 3

# Type conversion for calculations
x = "10"
y = "3"
result = int(x) + int(y)
print(result)      # 13

# Converting to boolean
print(bool(0))          # False
print(bool(1))          # True
print(bool(-5))         # True (any non-zero number is True)
print(bool(""))         # False
print(bool("hello"))    # True
print(bool([]))         # False (empty list)

# Practical example: user input with conversion
name = input("What's your name? ").strip()
age = int(input("How old are you? "))
height = float(input("How tall are you (meters)? "))
print(f"{name} is {age} years old and {height}m tall")
```

### Guided Practice

1. Ask the user for a number as a string.
2. Convert it to an integer and add 10 to it.
3. Display the result.
4. Ask the user for a price (with a decimal point).
5. Convert to float, multiply by 1.1 (10% increase), and display formatted.

### Practice Problems

**Problem 1 — Beginner:**
- Ask the user for a number
- Convert it to an integer
- Add 5 and print the result

```python
# Starter code
num_str = input("Enter a number: ")
num_int =

print()
```

**Problem 2 — Intermediate:**
- Ask the user for their name and age
- Convert age to an integer
- Calculate what their age will be in 10 years
- Print: "[Name] will be [age] in 10 years"

**Problem 3 — Challenge:**
Write a program that asks for three test scores (with possible decimals), converts them to floats, calculates the average, converts to an integer for display, and prints "Your average is [X]%"

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `int()` to convert the string input to an integer.
- Problem 2: Use `.strip()` on the name and `int()` on the age.
- Problem 3: Add three `float()` conversions, calculate average, then use `int()` to convert for display.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num_str = input("Enter a number: ")
num_int = int(num_str)
print(num_int + 5)

# Problem 2 Example
name = input("What's your name? ").strip()
age_str = input("How old are you? ")
age = int(age_str)
future_age = age + 10
print(f"{name} will be {future_age} in 10 years")

# Problem 3 Example
score1 = float(input("Score 1: "))
score2 = float(input("Score 2: "))
score3 = float(input("Score 3: "))
average = (score1 + score2 + score3) / 3
average_int = int(average)
print(f"Your average is {average_int}%")
```

</details>

---
