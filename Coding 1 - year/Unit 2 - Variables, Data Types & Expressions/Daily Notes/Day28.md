# Day 28: Compound Expressions — Combining Math and String Operations

**Learning Target:** I can combine multiple operations in a single expression and understand operator precedence.

### Key Concepts

**Compound expressions** use multiple operators to perform complex calculations in one line. Understanding **operator precedence** (order of operations) is crucial.

**PEMDAS/BODMAS** — the order of operations:
1. **Parentheses** (highest priority)
2. **Exponents** (`**`)
3. **Multiplication, Division** (left to right)
4. **Addition, Subtraction** (left to right)

Without parentheses, `2 + 3 * 4` gives `14` (multiply first, then add), NOT `20`.

**String operations in expressions:**
- Concatenation: `"Hello" + " " + "World"`
- Repetition: `"Ha" * 3`
- Indexing: `"Python"[0]`
- Slicing: `"Python"[1:4]`
- Methods: `"hello".upper()`

You can combine these: `"Hello, " + name.title() + "!"` or `word.upper() + word.lower()`.

**Type mixing:**
- Arithmetic requires numbers: `"5" + 3` will error; use `int("5") + 3` or `"5" + str(3)`
- Concatenation requires strings: `"Score: " + str(95)`
- Comparisons: `5 > "3"` will error (can't compare int to string)

### Code Examples

```python
# Order of operations
print(2 + 3 * 4)        # 14 (not 20!)
print((2 + 3) * 4)      # 20 (parentheses change order)
print(10 - 5 + 2)       # 7 (left to right)
print(10 - (5 + 2))     # 3 (parentheses change order)

# Exponents come before multiplication
print(2 * 3 ** 2)       # 18 (not 36; exponent first)
print((2 * 3) ** 2)     # 36

# String operations in expressions
name = "alice"
greeting = "Hello, " + name.title() + "!"
print(greeting)  # "Hello, Alice!"

word = "Python"
new_word = word.upper() + word.lower()
print(new_word)  # "PYTHONpython"

# Complex arithmetic
radius = 5
area = 3.14159 * radius ** 2
print(area)  # 78.53975

# Type conversion in expressions
score1 = "85"
score2 = "90"
average = (int(score1) + int(score2)) / 2
print(f"Average: {average}")

# Combining string methods
text = "  HELLO WORLD  "
clean = text.strip().lower()
result = "First 5 chars: " + clean[0:5]
print(result)  # "First 5 chars: hello"

# Complex expression with multiple operations
age = 25
years_to_retirement = 65 - age
years_worked = age - 18
print(f"Years until retirement: {years_to_retirement}")
print(f"Years working: {years_worked}")

# String repetition in expressions
line = "-" * 20
print(line)  # "--------------------"
print(line + "+" + line)  # Long separator line
```

### Guided Practice

1. Write an expression that calculates the area of a circle (radius is 5): `π * r²`
2. Write an expression that concatenates a greeting with a cleaned user input
3. Write an expression using parentheses that changes the result of `10 - 3 * 2`
4. Predict the output of `"Code" * 3` and `"Code"[0:2]`
5. Calculate simple interest: `P * (1 + r * t)` where P=1000, r=0.05, t=3

### Practice Problems

**Problem 1 — Beginner:**
Calculate the perimeter of a rectangle:
- Ask for length and width
- Calculate: `perimeter = 2 * (length + width)`
- Print the result

```python
length = float(input("Length: "))
width = float(input("Width: "))

perimeter =

print(f"Perimeter: {perimeter}")
```

**Problem 2 — Intermediate:**
Create a name tag generator:
- Ask for first name, last name
- Create output: "[FIRST LAST] --- [FIRST LAST]" (both uppercase and lowercase versions)
- Use string operations to make this in one expression

**Problem 3 — Challenge:**
Calculate the discriminant of a quadratic equation: `b² - 4ac`
- Ask for a, b, c
- Calculate the discriminant
- If discriminant > 0, print "Two real solutions"
- If discriminant == 0, print "One solution"
- If discriminant < 0, print "No real solutions"

<details>
<summary>💡 Hints</summary>

- Problem 1: `perimeter = 2 * (length + width)` (parentheses ensure addition happens first).
- Problem 2: Concatenate with `+`, use `.upper()`, `.lower()`, and `.title()`.
- Problem 3: `discriminant = b**2 - 4*a*c`. Then use comparisons to check the value.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
length = float(input("Length: "))
width = float(input("Width: "))
perimeter = 2 * (length + width)
print(f"Perimeter: {perimeter}")

# Problem 2 Example
first = input("First name: ").strip().title()
last = input("Last name: ").strip().title()
tag = first + " " + last + " --- " + (first + " " + last).upper()
print(tag)

# Problem 3 Example
a = float(input("a: "))
b = float(input("b: "))
c = float(input("c: "))
discriminant = b**2 - 4*a*c
if discriminant > 0:
    print("Two real solutions")
elif discriminant == 0:
    print("One solution")
else:
    print("No real solutions")
```

</details>

---
