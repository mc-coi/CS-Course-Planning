# Day 6: Type Conversion
**Learning Target:** I can convert between data types using casting functions.

### Key Concepts
**Casting** (or type conversion) changes a value from one data type to another:
- `int()` converts to integer
- `float()` converts to float
- `str()` converts to string
- `bool()` converts to Boolean

**Important:** `int(3.9)` → `3` (truncates/cuts off decimal, does NOT round!)

Common casting scenarios:
- `int("42")` → `42` ✓
- `int("hello")` → ValueError ✗
- `float("3.14")` → `3.14` ✓
- `str(100)` → `"100"` ✓
- `int(True)` → `1`, `int(False)` → `0`

### Code Examples
```python
# String to integer
print(int("42"))       # 42
print(int("-7"))       # -7

# String to float
print(float("3.14"))   # 3.14
print(float("2"))      # 2.0

# Number to string
print(str(100))        # "100"
print(str(3.14))       # "3.14"

# Float to int (truncates!)
print(int(3.9))        # 3 (NOT rounded!)
print(int(-5.8))       # -5

# Boolean conversion
print(int(True))       # 1
print(int(False))      # 0
print(bool(1))         # True
print(bool(0))         # False

# Common pattern: get numeric input
age = int(input("Age: "))
gpa = float(input("GPA: "))
print(f"You are {age} and your GPA is {gpa}")

# Error handling (preview)
try:
    num = int("hello")
except ValueError:
    print("Cannot convert 'hello' to integer")
```

### Guided Practice
Write a program that:
1. Asks for a number as a string
2. Converts it to int and float
3. Prints all three versions with their types
4. Shows the difference between int(3.9) and round(3.9)

### Practice Problems
**Problem 1 — Beginner:** Convert these values and print the results with their types:
- `int("123")`
- `float("45.67")`
- `str(999)`

```python
print()
print()
print()
```

**Problem 2 — Intermediate:** Ask the user for a number as a string, convert to int, then print it doubled and squared.

**Problem 3 — Challenge:** Explain and demonstrate the difference between `int(3.9)` and `round(3.9)`. Show 3 more examples of each.

<details>
<summary>💡 Hints</summary>

- Problem 1: Just use the conversion functions and print with type()
- Problem 2: Convert first, then do math
- Problem 3: int() cuts off decimals; round() rounds mathematically
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2 Example
num_str = input("Enter a number: ")
num = int(num_str)
print(f"Doubled: {num * 2}")
print(f"Squared: {num ** 2}")

# Problem 3 Examples
print(int(5.8))        # 5 (truncates)
print(round(5.8))      # 6 (rounds)
print(int(2.2))        # 2 (truncates)
print(round(2.2))      # 2 (rounds)
```
</details>

---