# Unit 2: Variables, Data Types & Expressions
> Master Python's data types, master string manipulation, and learn to format output like a professional.

##  Unit Overview
- **Duration:** 9 days / 3 weeks
- **Key Concepts:** Variable assignment and reassignment, numeric types (int/float), string operations, Boolean values, type conversion, f-string formatting, math module, and constants
- **Big Idea:** Different data types and operators allow you to manipulate and display information in powerful ways

##  Learning Targets
- I can declare and reassign variables using assignment and compound assignment operators
- I can use integer and float types and perform accurate arithmetic
- I can create strings and use concatenation, repetition, indexing, and slicing
- I can use common string methods to analyze and transform text
- I can evaluate Boolean expressions and use comparison operators
- I can convert between different data types
- I can use f-strings to create clean, formatted output
- I can write complex expressions and use the math module
- I can build a complete program using multiple data types and calculations

---

# Day 1: Introduction to Variables & Assignment
**Learning Target:** I can declare variables and explain how assignment works.

### Key Concepts
The assignment operator `=` gives a variable a value. It does NOT mean equality (that's `==`, which you'll learn later). Variables can be reassigned—the old value is replaced.

**Compound assignment operators** let you update a variable using its current value:
- `x += 5` means `x = x + 5` (add 5 to x)
- `x -= 3` means `x = x - 3` (subtract 3)
- `x *= 2` means `x = x * 2` (multiply by 2)
- `x /= 4` means `x = x / 4` (divide by 4)
- `x //= 2` means `x = x // 2` (integer divide)

**Multiple assignment** lets you assign several variables at once: `a, b, c = 1, 2, 3`

### Code Examples
```python
# Basic assignment
score = 0
print(score)      # 0

# Reassignment
score = 100
print(score)      # 100

# Compound assignment
score += 10       # score = score + 10; now 110
print(score)      # 110

score -= 5        # score = score - 5; now 105
print(score)      # 105

score *= 2        # score = score * 2; now 210
print(score)      # 210

# Multiple assignment (same value)
a = b = c = 0
print(a, b, c)    # 0 0 0

# Multiple assignment (different values)
x, y, z = 1, 2, 3
print(x, y, z)    # 1 2 3

# Swapping variables
a = 5
b = 10
a, b = b, a       # Swap!
print(a, b)       # 10 5
```

### Guided Practice
Create a game score tracker. Start with a score of 0, then use compound assignment to add 10 points, subtract 3 points, multiply by 2, and divide by 2. Print the score after each operation.

### Practice Problems
**Problem 1 — Beginner:** Declare a variable, assign it a value, reassign it to a different value, then print it.

```python
# Starter code
name =

name =

print()
```

**Problem 2 — Intermediate:** Create a score variable starting at 50. Use all 5 compound assignment operators on it and print the score after each.

**Problem 3 — Challenge:** Swap the values of three variables using multiple assignment. Print before and after.

<details>
<summary>💡 Hints</summary>

- Problem 1: Simple—just choose any value and change it
- Problem 2: Start at 50, then +=, -=, *=, /=, //=
- Problem 3: You can do `x, y, z = y, z, x` to rotate values
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = "Alice"
print(name)       # Alice
name = "Bob"
print(name)       # Bob

# Problem 2 Example
score = 50
score += 10; print(score)     # 60
score -= 5; print(score)      # 55
score *= 2; print(score)      # 110
score /= 5; print(score)      # 22.0
score //= 2; print(score)     # 11.0
```
</details>

---

# Day 2: Numeric Types: int & float
**Learning Target:** I can use integer and float types and perform arithmetic.

### Key Concepts
- **Integers** (`int`) are whole numbers: -5, 0, 42, 1000000
- **Floats** (`float`) are decimals: 3.14, -0.5, 2.0 (note the decimal point!)

**Important:** In Python 3, division `/` always returns a float, even if the result is a whole number: `10 / 2 = 5.0`

The `abs()` function returns absolute value (distance from zero).
The `round()` function rounds to a specified decimal place: `round(3.14159, 2)` → `3.14`
The `pow()` function is the same as `**`: `pow(2, 8)` → `256`

**Order of operations** (PEMDAS): Parentheses, Exponents, Multiplication/Division (left-to-right), Addition/Subtraction (left-to-right)

### Code Examples
```python
# Integer arithmetic
print(10 + 3)     # 13
print(10 - 3)     # 7
print(10 * 3)     # 30
print(10 / 3)     # 3.3333... (float)
print(10 // 3)    # 3 (integer division, floor)
print(10 % 3)     # 1 (remainder)
print(2 ** 8)     # 256 (exponentiation)

# Absolute value
print(abs(-5))    # 5
print(abs(3.14))  # 3.14

# Rounding
print(round(3.14159))     # 3 (to nearest whole)
print(round(3.14159, 2))  # 3.14 (to 2 decimals)
print(round(3.14159, 3))  # 3.142 (to 3 decimals)

# Power function
print(pow(2, 8))  # 256 (same as 2**8)
print(pow(5, 3))  # 125

# Working with variables
x = 15
y = 4
print(x + y)      # 19
print(x / y)      # 3.75
print(x // y)     # 3
print(x % y)      # 3 (15 = 4*3 + 3)
```

### Guided Practice
Write a program that:
1. Asks for two numbers
2. Prints their sum, difference, product, quotient, floor quotient, remainder, and power (first to the second)
3. Rounds each result to 2 decimal places

### Practice Problems
**Problem 1 — Beginner:** Write a program that uses at least 5 different arithmetic operators.

```python
x =
y =

print()  # +
print()  # -
print()  # *
print()  # /
print()  # //
```

**Problem 2 — Intermediate:** Create a program that asks for a radius and calculates the area of a circle using π (use `import math` and `math.pi`).

**Problem 3 — Challenge:** Calculate the hypotenuse of a right triangle given two sides using the Pythagorean theorem (a² + b² = c²).

<details>
<summary>💡 Hints</summary>

- Problem 1: Choose any two numbers and show different operations
- Problem 2: Area = π × r²
- Problem 3: c = sqrt(a² + b²) — use `math.sqrt()`
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2 Example
import math
radius = float(input("Radius: "))
area = math.pi * radius ** 2
print(f"Area: {area:.2f}")

# Problem 3 Example
import math
a = float(input("Side a: "))
b = float(input("Side b: "))
c = math.sqrt(a**2 + b**2)
print(f"Hypotenuse: {c:.2f}")
```
</details>

---

# Day 3: String Data Type & Operations
**Learning Target:** I can create strings and use concatenation, indexing, and slicing.

### Key Concepts
**Strings** are sequences of characters (text). They can use single quotes `'hello'` or double quotes `"hello"`.

**Concatenation** combines strings using `+`:
```python
first = "John"
last = "Doe"
full = first + " " + last  # "John Doe"
```

**Repetition** repeats a string using `*`:
```python
print("Ha" * 3)  # "HaHaHa"
```

**Length** finds how many characters are in a string:
```python
word = "Python"
print(len(word))  # 6
```

**Indexing** accesses individual characters. Indexing starts at 0:
```python
word = "Python"
print(word[0])    # "P" (first character)
print(word[1])    # "y" (second character)
print(word[-1])   # "n" (last character)
print(word[-2])   # "o" (second-to-last)
```

**Slicing** extracts portions of a string using `[start:stop]` (stop is exclusive):
```python
word = "Python"
print(word[0:3])   # "Pyt" (chars 0,1,2)
print(word[2:5])   # "tho" (chars 2,3,4)
print(word[:3])    # "Pyt" (from start to 3)
print(word[3:])    # "hon" (from 3 to end)
print(word[::-1])  # "nohtyP" (reversed!)
```

### Code Examples
```python
# Concatenation
name = "Alex"
greeting = "Hello, " + name + "!"
print(greeting)    # "Hello, Alex!"

# Repetition
print("*" * 10)    # "**********"

# Length
word = "Programming"
print(len(word))   # 11

# Indexing
sentence = "Python is fun"
print(sentence[0])    # "P"
print(sentence[-1])   # "n"

# Slicing
print(sentence[0:6])   # "Python"
print(sentence[10:13]) # "fun"
print(sentence[:6])    # "Python"
print(sentence[7:])    # "is fun"
print(sentence[::-1])  # "nuf si nohtyP" (reversed)
```

### Guided Practice
Write a program that:
1. Asks the user for a word
2. Prints the first character, last character, middle character
3. Prints the word reversed
4. Prints the length of the word

### Practice Problems
**Problem 1 — Beginner:** Create a string with your name and print the first 3 characters, last 3 characters, and the whole string reversed.

```python
name =

print()  # first 3
print()  # last 3
print()  # reversed
```

**Problem 2 — Intermediate:** Write a program that asks for a sentence and counts how many characters are in it.

**Problem 3 — Challenge:** Predict the output of `"Python"[1:5:2]` (slicing with step). Explain what the third number in `[start:stop:step]` does.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use indexing with [0], [-1], [::-1], or slicing
- Problem 2: Use `len()` function
- Problem 3: Step skips characters; `[1:5:2]` takes chars 1 and 3
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = "Alexandra"
print(name[0:3])      # "Ale"
print(name[-3:])      # "dra"
print(name[::-1])     # "ardnaxelA"

# Problem 2 Example
sentence = input("Enter sentence: ")
print(f"Character count: {len(sentence)}")

# Problem 3
print("Python"[1:5:2])  # "yo" (indices 1 and 3)
```
</details>

---

# Day 4: String Methods
**Learning Target:** I can use common string methods to manipulate text.

### Key Concepts
**String methods** are built-in functions that work on strings. Use syntax: `string.method()`

Common methods:
- `.upper()` - return uppercase version
- `.lower()` - return lowercase version
- `.title()` - return title case (first letter of each word capitalized)
- `.strip()` - remove leading/trailing whitespace
- `.replace(old, new)` - replace all occurrences
- `.split()` - split into a list of words
- `.find(substring)` - return index of substring (-1 if not found)
- `.count(substring)` - count occurrences
- `.startswith(prefix)` - True if starts with prefix
- `.endswith(suffix)` - True if ends with suffix

Methods can be **chained**: `input().strip().lower().title()`

### Code Examples
```python
msg = "  Hello World  "

# Case methods
print(msg.upper())          # "  HELLO WORLD  "
print(msg.lower())          # "  hello world  "
print(msg.title())          # "  Hello World  "
print(msg.strip())          # "Hello World" (no spaces)
print(msg.strip().upper())  # "HELLO WORLD" (chaining)

# Replace and split
text = "hello world"
print(text.replace("world", "Python"))  # "hello Python"
print(text.split())         # ['hello', 'world']

# Find and count
word = "programming"
print(word.find("ram"))     # 3 (index where "ram" starts)
print(word.count("m"))      # 2 (two m's)

# Starts/ends with
print("hello.txt".endswith(".txt"))      # True
print("alice@email.com".startswith("alice"))  # True

# Chaining methods
user_input = "  ZACH  "
clean = user_input.strip().lower().title()
print(clean)                # "Zach"
```

### Guided Practice
Write a program that asks the user for a sentence and performs these operations:
1. Print uppercase and lowercase versions
2. Replace all spaces with hyphens
3. Print the first word using `.split()`
4. Count how many times the letter 'e' appears
5. Check if it starts with a capital letter

### Practice Problems
**Problem 1 — Beginner:** Use string methods on the phrase "PYTHON IS FUN": lowercase, titlecase, and replace "FUN" with "AWESOME".

```python
phrase = "PYTHON IS FUN"

print()  # lowercase
print()  # titlecase
print()  # replace
```

**Problem 2 — Intermediate:** Write a program that asks for a word and tells the user if it's a palindrome (reads the same forwards and backwards) using string methods.

**Problem 3 — Challenge:** Chain 4+ string methods together to clean user input: remove whitespace, convert to lowercase, replace punctuation, and check if a word is in it.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use .lower(), .title(), .replace()
- Problem 2: Use .lower() to make comparison case-insensitive, then compare to [::-1]
- Problem 3: Strip, lower, replace, then find or endswith
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
phrase = "PYTHON IS FUN"
print(phrase.lower())                    # "python is fun"
print(phrase.title())                    # "Python Is Fun"
print(phrase.replace("FUN", "AWESOME"))  # "PYTHON IS AWESOME"

# Problem 2 Example
word = input("Enter word: ").strip().lower()
if word == word[::-1]:
    print("It's a palindrome!")
else:
    print("Not a palindrome.")
```
</details>

---

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

# Day 7: String Formatting with f-strings
**Learning Target:** I can use f-strings to create clean formatted output.

### Key Concepts
**f-strings** (formatted string literals) let you embed variables and expressions directly in strings. Use an `f` before the quote and put variables in `{curly braces}`.

Formatting options:
- `{variable}` - plain value
- `{expression}` - math or function calls
- `{value:.2f}` - float with 2 decimals
- `{value:10}` - right-aligned in 10-character width
- `{value:<10}` - left-aligned in 10-character width
- `{value:>10}` - right-aligned (explicit)
- `{value:^10}` - centered in 10-character width

### Code Examples
```python
# Basic f-strings
name = "Alex"
age = 17
print(f"My name is {name}")        # "My name is Alex"
print(f"I am {age} years old")     # "I am 17 years old"

# Expressions in f-strings
print(f"Next year I'll be {age + 1}")  # "Next year I'll be 18"
print(f"3 + 4 = {3 + 4}")          # "3 + 4 = 7"

# Decimal formatting
price = 19.5
print(f"Price: ${price:.2f}")      # "Price: $19.50"
gpa = 3.9467
print(f"GPA: {gpa:.2f}")           # "GPA: 3.95"

# Width and alignment
name = "Bob"
print(f"Name: {name:10}")          # "Name: Bob       " (10 chars, right-aligned)
print(f"Name: {name:<10}")         # "Name: Bob       " (left-aligned)
print(f"Name: {name:>10}")         # "Name:        Bob" (right-aligned)
print(f"Name: {name:^10}")         # "Name:    Bob    " (centered)

# Report example
print(f"{'Item':<15} {'Price':>10} {'Qty':>5}")
print(f"{'Apple':<15} {'$1.50':>10} {'3':>5}")
print(f"{'Banana':<15} {'$0.75':>10} {'6':>5}")
```

### Guided Practice
Create a receipt formatter that:
1. Asks for item name, price, and quantity
2. Calculates subtotal
3. Calculates tax (8%)
4. Calculates total
5. Prints a nicely formatted receipt using f-strings

### Practice Problems
**Problem 1 — Beginner:** Use an f-string to print: "Hello [name], you are [age] years old" where name and age are variables.

```python
name =
age =

print()
```

**Problem 2 — Intermediate:** Create a simple invoice for a purchase. Use f-strings to format prices to 2 decimals and align items in columns.

**Problem 3 — Challenge:** Print a table of squares (1-10) using f-strings with proper alignment and formatting.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use f"Hello {name}, you are {age}" syntax
- Problem 2: Use :.2f for prices and :10 or :<15 for alignment
- Problem 3: Print a header row, then loop and format each number and its square
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2 Example
item = "Laptop"
price = 999.5
quantity = 1
subtotal = price * quantity
tax = subtotal * 0.08
total = subtotal + tax

print(f"{'Item':<20} {'Price':>10}")
print(f"{item:<20} ${price:>9.2f}")
print(f"{'Subtotal:':<20} ${subtotal:>9.2f}")
print(f"{'Tax (8%):':<20} ${tax:>9.2f}")
print(f"{'Total:':<20} ${total:>9.2f}")

# Problem 3 Example
print(f"{'Number':<10} {'Square':>10}")
for i in range(1, 11):
    print(f"{i:<10} {i**2:>10}")
```
</details>

---

# Day 8: Expressions, Constants & math Module
**Learning Target:** I can write complex expressions and use the math module.

### Key Concepts
**Constants** are variables whose values should never change. By convention, use ALL_CAPS: `MAX_ATTEMPTS = 3`, `TAX_RATE = 0.0925`

The **math module** provides mathematical functions and constants:
- `math.sqrt(x)` - square root
- `math.ceil(x)` - round up
- `math.floor(x)` - round down
- `math.pi` - π (3.14159...)
- `math.e` - Euler's number (2.71828...)
- `math.pow(x, y)` - x to the power of y (same as `x ** y`)

To use: `import math` at the top of your program.

### Code Examples
```python
import math

# Constants (use ALL_CAPS)
TAX_RATE = 0.0925
DISCOUNT = 0.15
MAX_ATTEMPTS = 3
SPEED_OF_LIGHT = 299_792_458  # underscores for readability

# Using constants
price = 100
tax = price * TAX_RATE
print(f"Tax: ${tax:.2f}")

# Math module
print(math.sqrt(144))    # 12.0
print(math.sqrt(2))      # 1.414...
print(math.ceil(3.2))    # 4 (round up)
print(math.floor(3.9))   # 3 (round down)
print(math.pi)           # 3.14159...
print(math.e)            # 2.71828...

# Practical example: Circle area
radius = 5
area = math.pi * radius ** 2
print(f"Area: {area:.2f}")  # Area: 78.54

# Distance between two points
x1, y1 = 0, 0
x2, y2 = 3, 4
distance = math.sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2)
print(f"Distance: {distance}")  # Distance: 5.0
```

### Guided Practice
Write a program that:
1. Defines constants for tax rate and discount
2. Asks for a price
3. Calculates and prints price with tax applied
4. Calculates area and circumference of a circle using `math.pi`

### Practice Problems
**Problem 1 — Beginner:** Use `math.sqrt()` and `math.pi` to calculate the area of a circle with radius 5.

```python
import math

radius = 5

print()
```

**Problem 2 — Intermediate:** Write a distance calculator using the distance formula: d = √((x₂-x₁)² + (y₂-y₁)²)

**Problem 3 — Challenge:** Create a program with at least 3 constants and use `math.ceil()` and `math.floor()` to demonstrate rounding up/down.

<details>
<summary>💡 Hints</summary>

- Problem 1: area = math.pi × r²
- Problem 2: Use math.sqrt() and the formula with variables
- Problem 3: Define MAX_PRICE, MIN_WAGE, TAX_RATE, then use ceil/floor on calculations
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
import math
radius = 5
area = math.pi * radius ** 2
print(f"Area: {area:.2f}")

# Problem 2 Example
import math
x1 = float(input("X1: "))
y1 = float(input("Y1: "))
x2 = float(input("X2: "))
y2 = float(input("Y2: "))
distance = math.sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2)
print(f"Distance: {distance:.2f}")
```
</details>

---

# Day 9: Unit 2 Project
**Learning Target:** I can build a complete program using multiple data types and calculations.

### Project: Personal Finance Tracker

Create a program that tracks personal finances. Your program must include:

**Requirements:**
- At least 4 different data types (str, int, float, bool)
- At least 3 inputs from the user
- At least 2 calculations
- At least 1 constant (ALL_CAPS)
- At least 2 string methods or formatting operations
- Clean output using f-strings with proper formatting
- At least 4 comments

**Example:**
```
=== FINANCE TRACKER ===
Name: Alex
Monthly income: 1500
Monthly expenses: 1200
Are you saving? yes

=== SUMMARY ===
Name:  Alex
Income: $1500.00
Expenses: $1200.00
Monthly Savings: $300.00
Savings Percentage: 20.00%
Status: SAVING SUCCESSFULLY!
```

**Submission Checklist:**
- [ ] Code runs without errors
- [ ] Has 4+ different data types
- [ ] Has 3+ inputs
- [ ] Has 2+ calculations
- [ ] Has 1+ constant
- [ ] Uses 2+ string methods or f-string formatting
- [ ] Has 4+ comments
- [ ] Clean, professional output

---

## Unit Practice Bank

1. **Beginner:** Create a variable and use +=, -=, *= on it, printing after each operation.
2. **Beginner:** Predict output: `s = "Hello"`; print(s[1]); print(s[-2]); print(s[1:3])
3. **Beginner:** What does `type("3.14")` return vs `type(3.14)`? Write code showing the difference.
4. **Intermediate:** Write a string reversal using slicing with negative step.
5. **Intermediate:** Use 6+ different string methods (.upper(), .lower(), .replace(), .split(), .find(), .count()) on user input.
6. **Intermediate:** Predict: `a=5; b=0; if a and not b: print("yes") else: print("no")` — what prints and why?
7. **Intermediate:** Create a circle calculator: area and circumference using `math.pi`.
8. **Intermediate:** Fix this code: `name = input("Name: "); print("Hello " + name + " you are " + 17 + " years old")`
9. **Intermediate:** Write the distance formula program: inputs (x₁,y₁,x₂,y₂), output distance with 2 decimals.
10. **Challenge:** Create an f-string that prints a table with proper alignment (headers, rows, totals).
11. **Challenge:** What does `"Python"[::-1]` produce? Explain slice notation with negative step [start:stop:step].
12. **Challenge:** Write a word analyzer: accept a word, print length, first/last letter, reversed, uppercase, and check if starts with vowel.
13. **Challenge:** Predict: `a = "5"; b = 3; print(int(a) + b); print(a * b); print(a + str(b))`
14. **Challenge:** Write a password strength checker (8+ chars, contain digit, uppercase) using string methods only.
15. **Challenge:** Create a loan payment calculator: principal, annual rate, years → monthly payment using M = P[r(1+r)ⁿ]/[(1+r)ⁿ-1]

---

## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Using `=` for comparison: `if x = 5:` | SyntaxError | Use `==` for comparison: `if x == 5:` |
| Forgetting quotes on string: `name = Alex` | NameError: Alex is undefined | Add quotes: `name = "Alex"` |
| `print("Hello" + 5)` | TypeError: can't add str and int | Convert: `print("Hello " + str(5))` |
| `name[0] = "J"` — trying to change string | TypeError: 'str' is immutable | Strings can't be changed; create new: `name = "J" + name[1:]` |
| Using wrong quotes: `name = "Alex'` | SyntaxError: unterminated string | Match quotes: `name = "Alex"` or `name = 'Alex'` |
| `int("3.14")` — trying to convert float string to int | ValueError | Convert to float first: `int(float("3.14"))` |
| Division returns float: `10 / 2` gives `5.0` not `5` | Not really an error, but unexpected | Use `//` for integer division: `10 // 2` returns `5` |
| Forgetting `import math` then using `math.sqrt()` | NameError: name 'math' is undefined | Add `import math` at the top |

---

## Unit Assessment Prep

**Review Questions:**

1. What is the difference between `=` and `==`?
2. Explain compound assignment: what does `x += 10` do?
3. What does `/` division return vs `//` floor division?
4. Demonstrate indexing and slicing on the string "Python".
5. List and explain 5 string methods.
6. What is the difference between `"5"` and `5`?
7. How do you convert a string to a number in Python?
8. Write an f-string that prints a number with 2 decimal places.
9. How do you import the math module and use `math.sqrt()`?
10. What is a constant and why use ALL_CAPS?

**Answers:**
1. `=` assigns; `==` compares for equality
2. `x += 10` means `x = x + 10` (add 10 to x)
3. `/` always returns float (3.0); `//` returns integer (3)
4. `"Python"[0]` = "P", `"Python"[-1]` = "n", `"Python"[1:4]` = "yth"
5. `.upper()`, `.lower()`, `.strip()`, `.replace()`, `.split()` (or others)
6. `"5"` is text (string); `5` is a number (integer)
7. `int("5")` or `float("3.14")`
8. `f"{price:.2f}"`
9. `import math` at top; then `math.sqrt(16)` returns `4.0`
10. Constants are values that shouldn't change; ALL_CAPS makes this clear: `MAX_ATTEMPTS = 3`

---

## Vocabulary & Quick Reference

**Key Terms:**
- **Casting:** Converting from one data type to another
- **Concatenation:** Joining strings with +
- **Slicing:** Extracting a portion of a string with [start:stop]
- **Method:** A function that belongs to a data type, used with dot notation
- **f-string:** Formatted string literal for clean output
- **Constant:** A variable that never changes (use ALL_CAPS)
- **Operator Precedence:** Order that operations are performed (PEMDAS)

**Key Operators & Methods:**
```python
# Compound assignment
+=, -=, *=, /=, //=

# Arithmetic
+, -, *, /, //, %, **

# String operations
concatenation (+), repetition (*), len(), indexing [n], slicing [a:b], [a:b:c]

# String methods
.upper(), .lower(), .title(), .strip(), .replace(), .split(), .find(), .count(), .startswith(), .endswith()

# Comparison
==, !=, <, >, <=, >=

# Type conversion
int(), float(), str(), bool()

# Formatting
f"text {variable}" or f"{value:.2f}"

# Math module
import math; math.sqrt(), math.pi, math.ceil(), math.floor()
```

**Common Formulas:**
- Circle area: π × r²
- Circle circumference: 2π × r
- Distance: √((x₂-x₁)² + (y₂-y₁)²)
