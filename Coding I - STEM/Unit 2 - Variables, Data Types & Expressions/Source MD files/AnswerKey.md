# Unit 2: Variables, Data Types & Expressions - Answer Key

---

## Problem 1: Compound Assignment Operators

### Solution
```python
# Create a variable and use +=, -=, *= operators
x = 10
print(f"Initial value: {x}")

# Using +=
x += 5
print(f"After x += 5: {x}")

# Using -=
x -= 3
print(f"After x -= 3: {x}")

# Using *=
x *= 2
print(f"After x *= 2: {x}")
```

### Expected Output
```
Initial value: 10
After x += 5: 15
After x -= 3: 12
After x *= 2: 24
```

### Common Mistakes
- Confusing compound operators with simple assignment (x = x + 5 vs x += 5)
- Forgetting that compound operators modify the variable in place
- Using the wrong operator order (e.g., 5 += x instead of x += 5)

---

## Problem 2: String Indexing and Slicing

### Solution
```python
s = "Hello"
print(f"s = \"{s}\"")
print()

# Index 1 (0-indexed, so second character)
print(f"s[1] = \"{s[1]}\"")  # 'e' (position 1)

# Index -2 (second from the end)
print(f"s[-2] = \"{s[-2]}\"")  # 'l' (position 3, counting backward)

# Slice [1:3] (from index 1 up to, but not including, index 3)
print(f"s[1:3] = \"{s[1:3]}\"")  # 'el'
```

### Expected Output
```
s = "Hello"

s[1] = "e"
s[-2] = "l"
s[1:3] = "el"
```

### Common Mistakes
- Forgetting that Python uses 0-based indexing (s[0] is 'H', not s[1])
- Misunderstanding negative indices (-1 is last, -2 is second-to-last)
- Slicing endpoint is exclusive, so [1:3] includes indices 1 and 2, not 3

---

## Problem 3: Type Difference - "3.14" vs 3.14

### Solution
```python
# Demonstrate the difference
str_result = type("3.14")
float_result = type(3.14)

print(f"type(\"3.14\") = {str_result}")
print(f"type(3.14) = {float_result}")
print()

# Show the practical difference
print("\"3.14\" is a STRING (text):")
print(f"  - You cannot do math with it directly")
print(f"  - \"3.14\" + \"2.0\" = {'3.14' + '2.0'}")  # Concatenation

print("\n3.14 is a FLOAT (number):")
print(f"  - You can do math with it")
print(f"  - 3.14 + 2.0 = {3.14 + 2.0}")  # Addition

# To convert string to float:
num = float("3.14")
print(f"\nfloat(\"3.14\") = {num} (type: {type(num)})")
```

### Expected Output
```
type("3.14") = <class 'str'>
type(3.14) = <class 'float'>

"3.14" is a STRING (text):
  - You cannot do math with it directly
  - "3.14" + "2.0" = 3.142.0

3.14 is a FLOAT (number):
  - You can do math with it
  - 3.14 + 2.0 = 5.14

float("3.14") = 3.14 (type: <class 'float'>)
```

### Common Mistakes
- Not realizing that strings can look like numbers but won't behave like them
- Confusing string concatenation with numeric addition
- Forgetting to convert strings to numbers before doing math

---

## Problem 4: String Reversal Using Slicing

### Solution
```python
# String reversal using negative step in slicing
word = "Python"

# Reverse using [start:stop:step], where step is -1
reversed_word = word[::-1]

print(f"Original: {word}")
print(f"Reversed: {reversed_word}")

# Another example
phrase = "Hello World"
print(f"\nOriginal: {phrase}")
print(f"Reversed: {phrase[::-1]}")

# Explanation of slicing syntax
print("\nSlicing explanation: [start:stop:step]")
print(f"[::1] forward: {word[::1]}")
print(f"[::-1] reverse: {word[::-1]}")
```

### Expected Output
```
Original: Python
Reversed: nohtyP

Original: Hello World
Reversed: dlroW olleH

Slicing explanation: [start:stop:step]
[::1] forward: Python
[::-1] reverse: nohtyP
```

### Common Mistakes
- Forgetting the negative step (step = -1)
- Using indices when they're not needed (omitting start and stop defaults work)
- Not understanding that negative step reverses the direction

---

## Problem 5: String Methods

### Solution
```python
# Demonstrate 6+ string methods
text = input("Enter a word or sentence: ")

# .upper() - convert to uppercase
print(f"Upper: {text.upper()}")

# .lower() - convert to lowercase
print(f"Lower: {text.lower()}")

# .replace(old, new) - replace substring
print(f"Replace 'o' with '0': {text.replace('o', '0')}")

# .split() - split string into list
words = text.split()
print(f"Split into words: {words}")

# .find(substring) - find index of substring
index = text.find('l')
print(f"Index of 'l': {index}")

# .count(substring) - count occurrences
count = text.count('l')
print(f"Count of 'l': {count}")

# Bonus methods:
# .strip() - remove whitespace from ends
# .startswith() - check if starts with
# .endswith() - check if ends with
```

### Expected Output
```
Enter a word or sentence: Hello World
Upper: HELLO WORLD
Lower: hello world
Replace 'o' with '0': Hell0 W0rld
Split into words: ['Hello', 'World']
Index of 'l': 2
Count of 'l': 3
```

### Common Mistakes
- Forgetting that strings are immutable (methods return new strings, don't modify originals)
- Using wrong syntax for methods (forgot parentheses or arguments)
- Not storing result of method call (e.g., text = text.upper())
- Using wrong method name (.toUpper() instead of .upper())

---

## Problem 6: Boolean Expression Prediction

### Solution
```python
# Predict the output of boolean expression
a = 5
b = 0

# Expression: if a and not b: print("yes") else: print("no")
print("Expression: if a and not b: print('yes') else: print('no')")
print()

# Step through the logic
print("Step 1: Evaluate 'a'")
print(f"  a = {a} → truthy (non-zero number)")

print("\nStep 2: Evaluate 'not b'")
print(f"  b = {b} → falsy (zero)")
print(f"  not b = not {b} = {not b}")

print("\nStep 3: Evaluate 'a and not b'")
print(f"  {a} and {not b} = {a and not b}")

print("\nStep 4: Print result")
if a and not b:
    print("yes")
else:
    print("no")
```

### Expected Output
```
Expression: if a and not b: print('yes') else: print('no')

Step 1: Evaluate 'a'
  a = 5 → truthy (non-zero number)

Step 2: Evaluate 'not b'
  b = 0 → falsy (zero)
  not b = not 0 = True

Step 3: Evaluate 'a and not b'
  5 and True = True

Step 4: Print result
yes
```

### Common Mistakes
- Thinking 0 is True (it's actually falsy)
- Not understanding `and` requires both conditions to be True
- Confusing `not b` logic (not 0 is True)
- Predicting "no" instead of "yes"

---

## Problem 7: Circle Calculator

### Solution
```python
import math

# Get radius from user
radius = float(input("Enter the radius of the circle: "))

# Calculate area and circumference using math.pi
area = math.pi * radius ** 2
circumference = 2 * math.pi * radius

# Print results
print(f"Radius: {radius}")
print(f"Area: {area:.4f}")
print(f"Circumference: {circumference:.4f}")
```

### Expected Output
```
Enter the radius of the circle: 5
Radius: 5.0
Area: 78.5398
Circumference: 31.4159
```

### Common Mistakes
- Forgetting to import math module
- Using wrong formula for area (radius² instead of π*radius²)
- Not using math.pi (using approximation 3.14 is less accurate)
- Forgetting to format output decimal places

---

## Problem 8: Fix String Concatenation with Type Conversion

### Solution
```python
# ORIGINAL CODE (ERROR):
# name = input("Name: ")
# print("Hello " + name + " you are " + 17 + " years old")
# Error: cannot concatenate str and int (17 is an integer)

# FIXED CODE - Option 1: Convert 17 to string
name = input("Name: ")
print("Hello " + name + " you are " + str(17) + " years old")

# FIXED CODE - Option 2: Use f-string (preferred)
name = input("Name: ")
print(f"Hello {name} you are 17 years old")

# FIXED CODE - Option 3: Use commas in print
name = input("Name: ")
print("Hello", name, "you are", 17, "years old")
```

### Expected Output
```
Name: Alice
Hello Alice you are 17 years old
```

### Common Mistakes
- Forgetting to convert integer to string with str()
- Not knowing alternative approaches (f-strings or commas)
- Thinking the error is somewhere else in the code

---

## Problem 9: Distance Formula

### Solution
```python
import math

# Get coordinates from user
x1 = float(input("Enter x1: "))
y1 = float(input("Enter y1: "))
x2 = float(input("Enter x2: "))
y2 = float(input("Enter y2: "))

# Calculate distance using formula: d = sqrt((x2-x1)² + (y2-y1)²)
distance = math.sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2)

# Print with 2 decimal places
print(f"Distance: {distance:.2f}")
```

### Expected Output
```
Enter x1: 0
Enter y1: 0
Enter x2: 3
Enter y2: 4
Distance: 5.00
```

### Common Mistakes
- Forgetting to import math module for sqrt()
- Wrong formula (using addition instead of Pythagorean theorem)
- Not formatting output to 2 decimal places
- Forgetting parentheses around differences before squaring

---

## Problem 10: F-String with Alignment

### Solution
```python
# Create a formatted table with f-strings and alignment
print("=== Expense Report ===")
print()

# Header
print(f"{'Item':<15} {'Price':>10} {'Quantity':>10} {'Total':>10}")
print("-" * 50)

# Data rows
items = [
    ("Apple", 1.50, 5),
    ("Banana", 0.75, 8),
    ("Orange", 2.00, 3),
]

total_spent = 0
for item, price, qty in items:
    line_total = price * qty
    total_spent += line_total
    print(f"{item:<15} ${price:>9.2f} {qty:>10} ${line_total:>9.2f}")

print("-" * 50)
print(f"{'TOTAL':<15} {'':>10} {'':>10} ${total_spent:>9.2f}")
```

### Expected Output
```
=== Expense Report ===

Item            Price   Quantity      Total
--------------------------------------------------
Apple             $1.50          5     $7.50
Banana            $0.75          8     $6.00
Orange            $2.00          3     $6.00
--------------------------------------------------
TOTAL                                  $19.50
```

### Common Mistakes
- Forgetting alignment operators (< for left, > for right, ^ for center)
- Wrong width specification
- Not formatting numbers with .2f for currency
- Inconsistent spacing between columns

---

## Problem 11: Slice Notation with Negative Step

### Solution
```python
# Demonstrate slice notation: [start:stop:step]
text = "Python"

print(f"Original string: {text}")
print()

# [::-1] reverses the string (step = -1, start and stop omitted)
print(f"text[::-1] = {text[::-1]}")

print("\nSlice notation breakdown [start:stop:step]:")
print(f"  start: where to begin (default: 0 for forward, -1 for backward)")
print(f"  stop: where to end (exclusive)")
print(f"  step: direction and increment")
print()

# More examples
print("Examples:")
print(f"text[::1]   = {text[::1]}    (forward, all)")
print(f"text[::-1]  = {text[::-1]}   (backward, all)")
print(f"text[::2]   = {text[::2]}    (forward, every 2nd)")
print(f"text[1:5]   = {text[1:5]}    (index 1 to 4)")
print(f"text[:3]    = {text[:3]}     (first 3 characters)")
print(f"text[2:]    = {text[2:]}     (from index 2 to end)")
```

### Expected Output
```
Original string: Python

text[::-1] = nohtyP

Slice notation breakdown [start:stop:step]:
  start: where to begin (default: 0 for forward, -1 for backward)
  stop: where to end (exclusive)
  step: direction and increment

Examples:
text[::1]   = Python    (forward, all)
text[::-1]  = nohtyP   (backward, all)
text[::2]   = Pto    (forward, every 2nd)
text[1:5]   = ytho    (index 1 to 4)
text[:3]    = Pyt     (first 3 characters)
text[2:]    = thon     (from index 2 to end)
```

### Common Mistakes
- Not understanding that negative step means reverse direction
- Forgetting that omitted start/stop use sensible defaults
- Confusing the parameters (step is third, not first)
- Using negative indices incorrectly

---

## Problem 12: Word Analyzer

### Solution
```python
# Word analyzer - input a word and analyze it
word = input("Enter a word: ").strip()

# Length
length = len(word)

# First and last letter
first_letter = word[0] if length > 0 else "N/A"
last_letter = word[-1] if length > 0 else "N/A"

# Reversed
reversed_word = word[::-1]

# Uppercase
uppercase = word.upper()

# Check if starts with vowel
vowels = "aeiouAEIOU"
starts_with_vowel = word[0] in vowels if length > 0 else False

# Print results
print(f"\nWord: {word}")
print(f"Length: {length}")
print(f"First letter: {first_letter}")
print(f"Last letter: {last_letter}")
print(f"Reversed: {reversed_word}")
print(f"Uppercase: {uppercase}")
print(f"Starts with vowel: {starts_with_vowel}")
```

### Expected Output
```
Enter a word: Python

Word: Python
Length: 6
First letter: P
Last letter: n
Reversed: nohtyP
Uppercase: PYTHON
Starts with vowel: False
```

### Common Mistakes
- Not checking if word is empty before accessing indices
- Forgetting to convert to uppercase (or lowercase)
- Using wrong method to reverse
- Not checking vowels correctly (forgetting both upper and lower case)

---

## Problem 13: Type Conversion Prediction

### Solution
```python
# Predict the outputs of type conversion
a = "5"
b = 3

print(f"a = \"{a}\" (string)")
print(f"b = {b} (integer)")
print()

# int(a) + b
result1 = int(a) + b
print(f"int(a) + b = int(\"{a}\") + {b} = {result1}")

# a * b (string repetition)
result2 = a * b
print(f"a * b = \"{a}\" * {b} = \"{result2}\"")

# a + str(b) (string concatenation)
result3 = a + str(b)
print(f"a + str(b) = \"{a}\" + str({b}) = \"{result3}\"")
```

### Expected Output
```
a = "5" (string)
b = 3 (integer)

int(a) + b = int("5") + 3 = 8
a * b = "5" * 3 = "555"
a + str(b) = "5" + str(3) = "53"
```

### Common Mistakes
- Thinking "5" * 3 equals 15 (it actually repeats the string, "555")
- Confusing string concatenation with addition ("5" + "3" = "53", not "8")
- Forgetting to convert between types when needed
- Predicting "8" for the first one but not the others

---

## Problem 14: Password Strength Checker

### Solution
```python
# Password strength checker using string methods
password = input("Enter a password: ")

# Check 1: 8+ characters
has_min_length = len(password) >= 8

# Check 2: Contains at least one digit
has_digit = any(char.isdigit() for char in password)

# Check 3: Contains at least one uppercase letter
has_uppercase = any(char.isupper() for char in password)

# Determine strength
is_strong = has_min_length and has_digit and has_uppercase

# Print results
print(f"\nPassword: {password}")
print(f"Length >= 8: {has_min_length}")
print(f"Contains digit: {has_digit}")
print(f"Contains uppercase: {has_uppercase}")
print(f"Strong password: {is_strong}")

if is_strong:
    print("✓ Password is strong!")
else:
    missing = []
    if not has_min_length:
        missing.append("at least 8 characters")
    if not has_digit:
        missing.append("a digit")
    if not has_uppercase:
        missing.append("an uppercase letter")
    print(f"✗ Password needs: {', '.join(missing)}")
```

### Expected Output
```
Enter a password: MyPass123

Password: MyPass123
Length >= 8: True
Contains digit: True
Contains uppercase: True
Strong password: True
✓ Password is strong!
```

### Common Mistakes
- Using .isdigit() on entire string instead of checking each character
- Forgetting to check all three criteria
- Not providing helpful feedback on what's missing
- Using complicated loops instead of string methods

---

## Problem 15: Loan Payment Calculator

### Solution
```python
# Loan payment calculator
# Formula: M = P[r(1+r)ⁿ]/[(1+r)ⁿ-1]

principal = float(input("Enter principal (loan amount): $"))
annual_rate = float(input("Enter annual interest rate (%): "))
years = int(input("Enter loan period (years): "))

# Convert annual rate to monthly rate (as decimal)
monthly_rate = annual_rate / 100 / 12

# Convert years to months
num_months = years * 12

# Apply formula: M = P[r(1+r)ⁿ]/[(1+r)ⁿ-1]
numerator = principal * monthly_rate * ((1 + monthly_rate) ** num_months)
denominator = ((1 + monthly_rate) ** num_months) - 1

if denominator != 0:
    monthly_payment = numerator / denominator
else:
    monthly_payment = principal / num_months

# Calculate total paid and interest paid
total_paid = monthly_payment * num_months
total_interest = total_paid - principal

# Print results
print(f"\nLoan Summary:")
print(f"Principal: ${principal:.2f}")
print(f"Annual Rate: {annual_rate}%")
print(f"Loan Period: {years} years ({num_months} months)")
print(f"\nMonthly Payment: ${monthly_payment:.2f}")
print(f"Total Paid: ${total_paid:.2f}")
print(f"Total Interest: ${total_interest:.2f}")
```

### Expected Output
```
Enter principal (loan amount): $200000
Enter annual interest rate (%): 5
Enter loan period (years): 30

Loan Summary:
Principal: $200000.00
Annual Rate: 5%
Loan Period: 30 years (360 months)

Monthly Payment: $1073.64
Total Paid: $386510.34
Total Interest: $186510.34
```

### Common Mistakes
- Not converting annual rate to monthly rate (divide by 12 and by 100)
- Wrong formula implementation or missing parentheses
- Not converting years to months (multiply by 12)
- Forgetting to format output as currency with 2 decimals
- Confusing numerator and denominator in the formula

---
