# Day 5: Boolean Data Type & Comparison Operators
**Learning Target:** I can evaluate comparison expressions and explain Boolean values.

### Key Concepts
**Booleans** are values that are either `True` or `False` (always capitalized in Python).

**Comparison operators** produce Boolean results:
- `==` equal to
- `!=` not equal to
- `>` greater than
- `<` less than
- `>=` greater than or equal to
- `<=` less than or equal to

Comparisons work on strings too—they compare alphabetically: `"apple" < "banana"` is `True`

The `bool()` function converts values to Boolean:
- `bool(0)` → `False`
- `bool(1)` → `True` (any non-zero number)
- `bool("")` → `False` (empty string)
- `bool("hello")` → `True` (non-empty string)
- `bool([])` → `False` (empty list, learned later)

### Code Examples
```python
# Comparison operators
print(5 > 3)       # True
print(5 < 3)       # False
print(5 == 5)      # True
print(5 != 3)      # True
print(5 >= 5)      # True
print(5 <= 3)      # False

# Comparing strings (alphabetically)
print("apple" < "banana")    # True
print("zebra" > "apple")     # True
print("hello" == "hello")    # True

# Boolean type
x = True
y = False
print(type(x))     # <class 'bool'>
print(type(y))     # <class 'bool'>

# Converting to Boolean
print(bool(0))         # False
print(bool(1))         # True
print(bool(5))         # True
print(bool(""))        # False
print(bool("hello"))   # True
```

### Guided Practice
Write a program that asks for the user's age and prints:
- Is the age exactly 18? (using ==)
- Is the age at least 16? (using >=)
- Is the age less than 21? (using <)
- Is the age not 18? (using !=)

### Practice Problems
**Problem 1 — Beginner:** Write comparisons (don't assign to variables, just print the results):
- Is 10 > 5?
- Is "cat" == "dog"?
- Is 3.5 <= 3.5?

```python
print()
print()
print()
```

**Problem 2 — Intermediate:** Ask the user for two numbers and print whether the first is greater than, less than, or equal to the second.

**Problem 3 — Challenge:** Ask for a password and print True if it's exactly "secret123", False otherwise. Then convert 0, 1, "", "password" to Boolean and explain each result.

<details>
<summary>💡 Hints</summary>

- Problem 1: Just use print() with the comparison
- Problem 2: Use ==, <, > for the three cases
- Problem 3: Use input() and == to compare; then use bool() function
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
print(10 > 5)           # True
print("cat" == "dog")   # False
print(3.5 <= 3.5)       # True

# Problem 2 Example
num1 = int(input("First number: "))
num2 = int(input("Second number: "))
if num1 > num2:
    print(f"{num1} is greater")
elif num1 < num2:
    print(f"{num2} is greater")
else:
    print("They are equal")
```
</details>

---