# Day 21: Review of Variables & Types; int vs float in Depth

**Learning Target:** I can declare variables, explain different numeric types, and understand the distinction between integers and floats in Python.

### Key Concepts

Variables are named containers for values. The **assignment operator** `=` gives a variable a value—this is different from the comparison operator `==` (which you'll use later). Once assigned, a variable can be reassigned to a new value, and the old value is discarded.

Python supports multiple **data types**. Two fundamental numeric types are:

**Integers (`int`)** are whole numbers with no decimal point: -42, 0, 5, 1000000. Operations on integers can produce unexpected results if you're not careful. For example, `10 / 3` does NOT return `3` (as in some languages)—it returns `3.3333...` (a float).

**Floats (`float`)** represent decimal numbers: 3.14, -0.5, 2.0, 0.0. Notice that `2.0` is a float, even though it's a whole number. The decimal point makes it a float. In Python 3, the division operator `/` **always returns a float**, even when dividing evenly: `10 / 2` gives `5.0`, not `5`.

To perform **integer division** (divide and discard the remainder), use `//`. For example, `10 // 3` gives `3` (an integer). To get the remainder, use the **modulo operator** `%`: `10 % 3` gives `1` because 10 = (3 × 3) + 1.

The **`type()` function** tells you what type a value is: `type(42)` returns `<class 'int'>`, and `type(3.14)` returns `<class 'float'>`.

### Code Examples

```python
# Basic variable assignment
name = "Alice"
age = 25
height = 5.7
print(name)      # Alice
print(age)       # 25
print(height)    # 5.7

# Reassignment
score = 0
print(score)     # 0
score = 100
print(score)     # 100

# Types of numbers
num_int = 42
num_float = 3.14
print(type(num_int))      # <class 'int'>
print(type(num_float))    # <class 'float'>

# Division in Python 3
print(10 / 2)    # 5.0 (float, not 5!)
print(10 // 2)   # 5 (integer division)
print(10 / 3)    # 3.3333...
print(10 // 3)   # 3
print(10 % 3)    # 1 (remainder)

# The decimal point matters
print(type(5))      # <class 'int'>
print(type(5.0))    # <class 'float'>

# Arithmetic with mixed types
result = 5 + 2.0
print(result)       # 7.0 (when you mix int and float, result is float)
print(type(result)) # <class 'float'>
```

### Guided Practice

1. Declare three variables: one for an integer, one for a float, and one for a string.
2. Use `type()` to check each variable's type and print the results.
3. Perform these operations and predict the type of each result:
   - `10 + 5`
   - `10 + 5.0`
   - `10 / 2`
   - `10 // 2`
4. Explain to a partner why `10 / 2` gives `5.0` instead of `5`.

### Practice Problems

**Problem 1 — Beginner:** Create variables for your name, age, and height. Use `type()` on each and print the results.

```python
# Starter code
name =
age =
height =

print(type(name))
print(type(age))
print(type(height))
```

**Problem 2 — Intermediate:** Given two integers `a = 20` and `b = 3`, print the results of `+`, `-`, `*`, `/`, `//`, `%`, and `**` (exponentiation). Identify which operations return integers and which return floats.

**Problem 3 — Challenge:** Explain what happens when you compute `0.1 + 0.2` and compare it to `0.3`. Why might `0.1 + 0.2 == 0.3` return `False`? (Hint: This is about how computers store decimals.)

<details>
<summary>💡 Hints</summary>

- Problem 1: Remember to declare variables with `=` and use the `type()` function.
- Problem 2: Division `/` always gives float; integer division `//` gives int; modulo `%` gives int; exponentiation `**` gives int if both operands are int.
- Problem 3: Try running `print(0.1 + 0.2)` and `print(0.3)` separately to see the difference.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = "Alex"
age = 16
height = 5.8

print(type(name))     # <class 'str'>
print(type(age))      # <class 'int'>
print(type(height))   # <class 'float'>

# Problem 2 Example
a = 20
b = 3
print(a + b)    # 23 (int)
print(a - b)    # 17 (int)
print(a * b)    # 60 (int)
print(a / b)    # 6.666... (float)
print(a // b)   # 6 (int)
print(a % b)    # 2 (int)
print(a ** b)   # 8000 (int)

# Problem 3: Floating-point precision
print(0.1 + 0.2)   # 0.30000000000000004 (not exactly 0.3!)
print(0.1 + 0.2 == 0.3)  # False
```

</details>

---
