# Day 3: Variables & Data Types
**Learning Target:** I can store information in variables and identify Python's four basic data types.

### Key Concepts
A **variable** is a named container that stores a value in the computer's memory. Think of it like a labeled box—you put something inside and give it a name so you can refer to it later.

Python has four main data types:
1. **str (string):** Text, enclosed in quotes. Examples: `"Alice"`, `'hello'`, `"123 Main St"`
2. **int (integer):** Whole numbers without decimals. Examples: `42`, `-7`, `0`
3. **float (floating-point):** Numbers with decimals. Examples: `3.14`, `-0.5`, `99.99`
4. **bool (boolean):** True or False (always capitalized in Python)

**Variable naming rules:**
- Cannot contain spaces; use underscores instead: `first_name` not `first name`
- Cannot start with a number: `age1` is okay, `1age` is not
- Cannot use special characters like `!@#$%`
- Cannot be Python keywords like `print`, `if`, `while`
- Are case-sensitive: `score` and `Score` are different variables

The `type()` function tells you what data type a value is.

### Code Examples
```python
# String variables
name = "Alex"
city = "Nashville"
print(name)        # Alex
print(city)        # Nashville

# Integer variables
age = 17
score = 95
print(age)         # 17

# Float variables
gpa = 3.85
price = 19.99
print(gpa)         # 3.85

# Boolean variables
is_enrolled = True
is_absent = False
print(is_enrolled) # True

# Check data types
print(type("hello"))     # <class 'str'>
print(type(42))          # <class 'int'>
print(type(3.14))        # <class 'float'>
print(type(True))        # <class 'bool'>

# Variables can be reassigned
x = 5
print(x)           # 5
x = 10
print(x)           # 10 — the value changed!

# Multiple assignment
a, b, c = 1, 2, 3
print(a, b, c)     # 1 2 3
```

### Guided Practice
Create a student profile with at least 5 variables of different data types. Print each variable and its type. Then change one variable's value and print it again.

### Practice Problems
**Problem 1 — Beginner:** Declare one variable of each data type (str, int, float, bool) and print them all.

```python
# Starter code
name =
age =
height =
is_student =

print()
```

**Problem 2 — Intermediate:** Create variables for a student: name, age, GPA, and whether they're on the honor roll. Print a sentence using all four variables.

**Problem 3 — Challenge:** What does `type("3.14")` return vs. `type(3.14)`? Write code to demonstrate and explain the difference.

<details>
<summary>💡 Hints</summary>
- Problem 1: Strings need quotes, booleans are True or False (capitalized)<br>
- Problem 2: Use f-strings or + to combine strings and variables<br>
- Problem 3: Quotes make it text, not a number
</details>

<details>
<summary>✅ Sample Answers</summary>

## Problem 1 Example
```python
name = "Jordan"
age = 16
height = 5.75
is_student = True
print(name, age, height, is_student)
print(type(name), type(age), type(height), type(is_student))
```

## Problem 2 Example
```python
name = "Sam"
age = 17
gpa = 3.9
is_honors = True
print(f"{name} is {age}, has a {gpa} GPA, and honors: {is_honors}")
```

</details>

---