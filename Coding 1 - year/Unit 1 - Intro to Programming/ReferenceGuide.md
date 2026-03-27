# Unit 1 Reference Guide — Vocabulary & Quick Reference

## Key Terms & Definitions

**Algorithm:** A step-by-step procedure to solve a problem. Must be precise, unambiguous, finite, and effective.

**Computer Science:** The study of problem-solving using computers. It's about breaking down complex problems into simple instructions.

**Data Type:** A category of data that Python recognizes:
- str (string) = text in quotes
- int (integer) = whole numbers
- float = decimal numbers
- bool = True or False

**Variable:** A named container that stores a value in memory. Created with the assignment operator `=`.

**Input:** Information the user provides to the program using the `input()` function.

**Output:** Information the program displays to the user using the `print()` function.

**Syntax:** The rules for writing code correctly in Python.

**Comment:** A note in code that Python ignores. Starts with `#`. Used to explain code to humans.

**Operator:** A symbol representing an operation: `+`, `-`, `*`, `/`, `//`, `%`, `**`

**Function:** Reusable code that performs a specific task. Examples: `print()`, `input()`, `type()`

**Type Conversion:** Converting from one data type to another using functions like `int()`, `float()`, `str()`

**String Concatenation:** Combining strings using the `+` operator.

**F-string:** A formatted string literal that allows embedding variables. Starts with `f"..."`

**Pseudocode:** English-like description of an algorithm, used for planning.

**Flowchart:** Visual diagram using shapes to represent an algorithm.

**Escape Character:** Special sequence representing a character you can't easily type. Examples: `\n`, `\t`, `\\`

**5-Step Development Process:** Define → Plan → Code → Test → Refine

---

## Key Syntax Reference

### Basic Print & Variables
```python
# Printing text
print("Hello, World!")

# Creating variables
name = "Alex"
age = 17
gpa = 3.85
is_enrolled = True

# Printing variables
print(name)
print(age)

# Checking data types
print(type(name))      # <class 'str'>
print(type(age))       # <class 'int'>
```

### Comments & Formatting
```python
# This is a comment
print("Hello")  # Comment can be inline too

# Escape characters
print("Line 1\nLine 2")  # \n = newline
print("Name\tAge")      # \t = tab
print("C:\\Users\\Documents")  # \\ = backslash
```

### Input & Type Conversion
```python
name = input("What's your name? ")
age = int(input("Age: "))
height = float(input("Height: "))

# Converting types
text_num = str(42)     # "42"
number = int("42")     # 42
decimal = float("3.14") # 3.14
```

### String Concatenation
```python
first = "Alex"
last = "Smith"
full_name = first + " " + last  # "Alex Smith"
print("Hello, " + name + "!")
```

### Arithmetic Operators
```python
# Basic operations
print(10 + 3)    # 13 (addition)
print(10 - 3)    # 7 (subtraction)
print(10 * 3)    # 30 (multiplication)
print(10 / 3)    # 3.333... (division, returns float)
print(10 // 3)   # 3 (floor division)
print(10 % 3)    # 1 (modulus/remainder)
print(2 ** 3)    # 8 (exponentiation)
```

### F-Strings & Formatting
```python
name = "Alex"
age = 17
gpa = 3.857

# Basic f-string
print(f"Name: {name}")

# Formatting decimals
print(f"GPA: {gpa:.2f}")  # 3.86

# Expressions in f-strings
print(f"Next year: {age + 1}")

# Alignment
print(f"{name:>10}")     # Right-align in 10 spaces
print(f"{name:<10}")     # Left-align in 10 spaces
```

### Order of Operations (PEMDAS)
```python
# Parentheses first
print((2 + 3) * 4)      # 20, not 14

# Exponents
print(2 ** 3 ** 2)      # 512 (right to left for exponents)

# Multiplication & Division (left to right)
print(10 / 2 * 5)       # 25.0

# Addition & Subtraction (left to right)
print(10 - 3 - 2)       # 5
```

### Common Functions
```python
# round() - rounds to decimal places
round(3.14159, 2)       # 3.14

# type() - returns data type
type("hello")           # <class 'str'>

# abs() - absolute value
abs(-5)                 # 5

# int(), float(), str() - type conversion
int("42")               # 42
float("3.14")           # 3.14
str(42)                 # "42"
```

---

## Common Mistakes & How to Fix Them

| Mistake | Error | Fix |
|---------|-------|-----|
| `Print("Hello")` | NameError: uppercase P | Python is case-sensitive; use `print()` (lowercase) |
| `name = input()` then `print(name + 5)` | TypeError: can't add str and int | Convert input: `name = int(input())` or `print(str(5))` |
| `print(Hello)` | NameError: name not defined | Strings need quotes: `print("Hello")` |
| `age = "17"` then use in math | Wrong result (string concatenation) | Convert: `age = int(input(...))` or use `int("17")` |
| `my age = 25` | SyntaxError: invalid syntax | Use underscores: `my_age = 25` |
| `print 5` | SyntaxError: invalid syntax | Python 3 requires parentheses: `print(5)` |
| Forgetting to convert `input()` | Can't do math on strings | Always use `int()` or `float()`: `num = int(input("Number: "))` |
| `Print = 5` | Will break print function | Variable names should be lowercase; use `print_value = 5` |
| `print("Hi"` | SyntaxError: missing closing paren | Count your parentheses and quotes |
| `print("Hi')` | SyntaxError: mismatched quotes | Match quotes: opening and closing must be same type |
| `num = "5.5"` then `int(num)` | ValueError | Can't convert string with decimal directly to int; use `float()` first |
| `print(f"Hi {name}")` without f prefix | TypeError: can't format non-strings | Add `f` before the quote: `f"Hi {name}"` |
| Using undefined variable | NameError: name not defined | Make sure you've assigned the variable before using it |
| Wrong operator: `a = 5` then `if a = 3` | SyntaxError | Use `==` for comparison, `=` for assignment |

---

## Quick Formula Reference

**Temperature Conversions:**
- Celsius to Fahrenheit: F = C × 9/5 + 32
- Fahrenheit to Celsius: C = (F - 32) × 5/9

**Area & Perimeter:**
- Rectangle area: A = length × width
- Rectangle perimeter: P = 2L + 2W
- Triangle area: A = (base × height) / 2

**Interest:**
- Simple interest: I = principal × rate × time / 100
- Compound interest: A = P(1 + r/100)^n

**Other:**
- BMI: weight(lbs) / height(in)² × 703
- Distance conversions: 1 mile = 1.60934 km
- Weight conversions: 1 lb = 0.453592 kg

---

## Data Type Quick Reference

| Type | Examples | When to Use |
|------|----------|------------|
| str | `"Alice"`, `'hello'`, `"123 Main St"` | Text, names, addresses |
| int | `42`, `-7`, `0`, `1000000` | Counting, ages, scores, whole numbers |
| float | `3.14`, `-0.5`, `99.99`, `2.0` | Measurements, prices, decimals |
| bool | `True`, `False` | Yes/no, on/off, true/false situations |

---

## Escape Characters

| Character | What It Does | Example |
|-----------|-------------|---------|
| `\n` | Newline (new line) | `print("Hi\nBye")` prints Hi, then Bye |
| `\t` | Tab (indentation) | `print("Name\tAge")` creates space between columns |
| `\\` | Backslash (literal \) | `print("C:\\Users\\Documents")` |
| `\'` | Single quote inside quotes | `print('It\'s nice')` prints It's nice |
| `\"` | Double quote inside quotes | `print("He said \"Hi\"")` prints He said "Hi" |

---

## Variable Naming Rules

**Valid Variable Names:**
- `age`, `name`, `score`
- `my_age`, `first_name`, `total_cost`
- `age1`, `score2`, `attempt_1`

**Invalid Variable Names:**
- `my age` (spaces not allowed)
- `1age` (can't start with number)
- `age!` (special characters not allowed)
- `if`, `print`, `while` (Python keywords)
- `My Age` vs `my_age` (use lowercase with underscores)

**Best Practices:**
- Use descriptive names: `student_grade` not `x`
- Use lowercase with underscores: `my_variable`
- Be specific: `total_score` not `number`
- Avoid single letters except for loop counters

---

## Operator Precedence (Order of Operations)

1. **Parentheses** — `()` — Highest priority
2. **Exponents** — `**`
3. **Multiplication, Division** — `*`, `/`, `//`, `%` — Left to right
4. **Addition, Subtraction** — `+`, `-` — Lowest priority, left to right

**Memory Tip:** PEMDAS (Please Excuse My Dear Aunt Sally)

Example:
```python
2 + 3 * 4          # 14 (multiply first: 3*4=12, then 2+12=14)
(2 + 3) * 4        # 20 (parentheses first: 2+3=5, then 5*4=20)
10 - 5 - 2         # 3 (left to right: 10-5=5, then 5-2=3)
2 ** 3 ** 2        # 512 (right to left: 3**2=9, then 2**9=512)
```

---

## The 5-Step Development Process

1. **Define (Ask):** Understand the problem. What are inputs? What's the output?
2. **Plan (Design):** Break into steps. Write pseudocode. Make a flowchart.
3. **Code (Implement):** Write the Python program. Use clear variable names.
4. **Test (Verify):** Run with different inputs. Check for errors.
5. **Refine (Debug/Improve):** Fix bugs. Make code cleaner. Improve output.

---

## Debugging Checklist

When your program doesn't work:
- [ ] Check for syntax errors (red underlines in editor)
- [ ] Verify all parentheses are matched
- [ ] Check all quotes are matched
- [ ] Verify colons are in the right places
- [ ] Check variable names are spelled correctly
- [ ] Verify all variables are defined before using them
- [ ] Check that types match (not adding strings and numbers)
- [ ] Verify input is converted to the right type
- [ ] Check order of operations is correct
- [ ] Test with multiple inputs to find logic errors
- [ ] Read the error message—it usually tells you the problem!

---
