# Day 41: Comprehensive Review — Vocabulary and Concepts

**Learning Target:** I can identify, explain, and apply all major concepts from Unit 2.

### Review Session Overview

This day focuses on ensuring you understand the **vocabulary** and **core concepts** of Unit 2. We'll do a comprehensive review that will prepare you for the assessment.

### Key Vocabulary Review

Work through these terms. You should be able to define each one and give an example.

**Data Types:**
- **Integer (int):** Whole numbers (positive, negative, or zero)
- **Float:** Decimal numbers; Python 3 `/` always returns float
- **String:** Sequences of characters; immutable; use quotes
- **Boolean:** True or False values; used in comparisons

**Variables & Assignment:**
- **Variable:** A named container for a value
- **Assignment:** Using `=` to give a variable a value
- **Reassignment:** Changing a variable's value
- **Compound assignment:** Operators like `+=`, `-=` that update a variable

**String Operations:**
- **Concatenation:** Combining strings with `+`
- **Repetition:** Repeating a string with `*`
- **Indexing:** Accessing individual characters with `[index]`
- **Slicing:** Extracting portions with `[start:stop:step]`
- **Method:** A function that works on an object (e.g., `.upper()`, `.lower()`)

**Type Conversion:**
- **Type conversion:** Changing a value from one type to another
- **Casting:** Using functions like `int()`, `float()`, `str()` to convert

**Operators:**
- **Arithmetic:** `+`, `-`, `*`, `/`, `//`, `%`, `**`
- **Comparison:** `==`, `!=`, `>`, `<`, `>=`, `<=`
- **Operator precedence:** PEMDAS (Parentheses, Exponents, Mult/Div, Add/Sub)

**Other Concepts:**
- **Import:** Loading a module with `import module_name`
- **Constant:** A value that doesn't change; written in UPPER_CASE by convention
- **F-string:** Formatted string with variables/expressions using `f"...{variable}..."`
- **Input validation:** Checking that user input is valid before using it

### Concept Summary Table

| Concept | Example | Output/Result |
|---------|---------|---------------|
| Concatenation | `"Hello" + " World"` | `"Hello World"` |
| Repetition | `"Ha" * 3` | `"HaHaHa"` |
| Indexing | `"Python"[0]` | `"P"` |
| Negative index | `"Python"[-1]` | `"n"` |
| Slicing | `"Python"[1:4]` | `"yth"` |
| Step slicing | `"Python"[::2]` | `"Pto"` |
| Reversed | `"Python"[::-1]` | `"nohtyP"` |
| `.upper()` | `"hello".upper()` | `"HELLO"` |
| `.lower()` | `"HELLO".lower()` | `"hello"` |
| `.strip()` | `"  hello  ".strip()` | `"hello"` |
| `.replace()` | `"hello".replace("l", "x")` | `"hexxo"` |
| `.find()` | `"hello".find("ll")` | `2` |
| `.count()` | `"banana".count("a")` | `3` |
| Type conversion | `int("42")` | `42` |
| F-string format | `f"${9.5:.2f}"` | `"$9.50"` |
| Comparison | `5 > 3` | `True` |
| math.sqrt() | `math.sqrt(16)` | `4.0` |
| math.pi | `math.pi` | `3.14159...` |

### Practice Problems for Review

**Problem 1: Vocabulary Match**
Match each term to its definition:
1. Slicing ___
2. Type conversion ___
3. String method ___
4. Operator precedence ___

Options:
a) Order in which operations are evaluated
b) Changing a value from one type to another
c) A function that works on a string
d) Extracting a portion of a string

**Problem 2: Code Trace**
Predict the output:
```python
word = "Programming"
print(word[0])
print(word[-1])
print(word[3:6])
print(word[::-1])
```

**Problem 3: Error Identification**
What's wrong with this code?
```python
name = "Alice"
age_str = input("Age: ")
total = name + age_str
result = total * 2
print(f"${result:.2f}")
```

**Problem 4: Concept Application**
Write a line of code that:
- Asks for a temperature in Celsius
- Converts it to Fahrenheit (F = C * 9/5 + 32)
- Displays the result formatted to 1 decimal place

<details>
<summary>✅ Answers</summary>

**Problem 1:**
1. d) Slicing
2. b) Type conversion
3. c) String method
4. a) Operator precedence

**Problem 2:**
```
P
g
gra
gnimmargorP
```

**Problem 3:**
- Can't multiply a string by another string
- Can't use `.2f` format on a string
- Should convert age to float first
- Doesn't make sense logically

**Problem 4:**
```python
celsius = float(input("Celsius: "))
fahrenheit = celsius * 9/5 + 32
print(f"Fahrenheit: {fahrenheit:.1f}")
```

</details>

### Study Guide: Key Formulas & Functions

**Math Formulas:**
- Area of circle: `π * r²`
- Hypotenuse (Pythagorean): `√(a² + b²)`
- Temperature conversion: `F = (C * 9/5) + 32`
- Simple interest: `interest = principal * rate * time`
- Percent increase: `new = original * (1 + percent/100)`

**String Functions:**
- `len(s)` - length
- `s[i]` - character at index i
- `s[start:stop:step]` - slice
- `s.upper()`, `s.lower()` - case conversion
- `s.strip()` - remove whitespace
- `s.replace(old, new)` - replace substring
- `s.find(sub)` - find index (-1 if not found)
- `s.count(sub)` - count occurrences

**Type Conversion:**
- `int(x)` - to integer (truncates)
- `float(x)` - to float
- `str(x)` - to string
- `bool(x)` - to boolean (0/empty = False, else True)

**Math Module:**
- `math.sqrt(x)` - square root
- `math.pi` - π constant
- `math.ceil(x)` - round up
- `math.floor(x)` - round down

---

**Preparation for Assessment:**

Review these areas thoroughly:
1. String indexing and slicing
2. Type conversion and when it's needed
3. Operator precedence (PEMDAS)
4. F-string formatting (decimals, thousands separator)
5. Common string methods
6. Variable naming conventions

You're ready for the assessment!

