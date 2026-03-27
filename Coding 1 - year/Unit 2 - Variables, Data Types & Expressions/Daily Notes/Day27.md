# Day 27: Boolean Data Type — True/False, Comparison Operators

**Learning Target:** I can evaluate Boolean expressions and use comparison operators to build conditional logic.

### Key Concepts

**Booleans** are values that are either `True` or `False` (always capitalized in Python). They're the foundation of conditional logic (if/else statements, which you'll use heavily in Unit 3).

**Comparison operators** compare two values and return a Boolean result (True or False):
- `==` : equal to
- `!=` : not equal to
- `>` : greater than
- `<` : less than
- `>=` : greater than or equal to
- `<=` : less than or equal to

**Comparisons work on different types:**
- Numbers: `5 > 3` is `True`
- Strings: `"apple" < "banana"` is `True` (alphabetical order)
- Mixed types can cause errors, so be careful

**Important:** Do NOT confuse `=` (assignment) with `==` (comparison). `if x = 5` will cause an error; use `if x == 5`.

The **`bool()` function** converts any value to Boolean:
- `bool(0)` → `False` (0 is "falsy")
- `bool(1)` → `True` (non-zero is "truthy")
- `bool("")` → `False` (empty string is "falsy")
- `bool("hello")` → `True` (non-empty string is "truthy")
- `bool([])` → `False` (empty list is "falsy")

### Code Examples

```python
# Basic comparison operators
print(5 > 3)       # True
print(5 < 3)       # False
print(5 == 5)      # True
print(5 != 3)      # True
print(5 >= 5)      # True
print(5 <= 3)      # False

# String comparisons (alphabetical)
print("apple" < "banana")    # True (a comes before b)
print("zebra" > "apple")     # True
print("hello" == "hello")    # True
print("Hello" == "hello")    # False (case-sensitive!)

# Storing Boolean values
is_adult = True
is_raining = False
print(type(is_adult))   # <class 'bool'>

# Comparing variables
age = 16
print(age >= 18)    # False
print(age < 21)     # True

# Converting to Boolean
print(bool(0))          # False
print(bool(1))          # True
print(bool(100))        # True
print(bool(-5))         # True (any non-zero is True)
print(bool(""))         # False (empty string)
print(bool("hello"))    # True (non-empty string)

# Practical examples
score = 85
passing = score >= 60
print(passing)  # True

user_input = input("Continue? (yes/no): ").strip().lower()
is_yes = user_input == "yes"
print(is_yes)
```

### Guided Practice

1. Ask the user for a number.
2. Check if it's greater than 10, equal to 10, and less than 10 using comparison operators.
3. Store the results in Boolean variables.
4. Print each comparison result.
5. Ask the user for two words and check if they're equal (case-insensitive).

### Practice Problems

**Problem 1 — Beginner:**
- Declare variable `x = 15` and `y = 20`
- Print the results of `x > y`, `x < y`, `x == y`, `x != y`

```python
x = 15
y = 20

print()  # x > y
print()  # x < y
print()  # x == y
print()  # x != y
```

**Problem 2 — Intermediate:**
- Ask the user for their age
- Create Boolean variables to check:
  - Is age 18 or older?
  - Is age less than 65?
  - Is age exactly 21?
- Print meaningful messages for each

**Problem 3 — Challenge:**
- Ask the user for a number
- Check if it's positive, negative, or zero
- Check if it's even or odd (hint: use `%` operator)
- Print all results

<details>
<summary>💡 Hints</summary>

- Problem 1: Just evaluate the expressions; they'll return True or False.
- Problem 2: Use `>=`, `<`, `==` and store results in variables like `is_adult = age >= 18`.
- Problem 3: Use `> 0`, `< 0`, `== 0` for sign. For even/odd, use `num % 2 == 0` (even if remainder is 0).

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
x = 15
y = 20
print(x > y)    # False
print(x < y)    # True
print(x == y)   # False
print(x != y)   # True

# Problem 2 Example
age = int(input("Age: "))
is_adult = age >= 18
is_young = age < 65
is_legal_drinking = age == 21
print(f"Adult? {is_adult}")
print(f"Young? {is_young}")
print(f"Legal drinking age? {is_legal_drinking}")

# Problem 3 Example
num = int(input("Enter a number: "))
is_positive = num > 0
is_negative = num < 0
is_zero = num == 0
is_even = num % 2 == 0
print(f"Positive? {is_positive}")
print(f"Negative? {is_negative}")
print(f"Zero? {is_zero}")
print(f"Even? {is_even}")
```

</details>

---
