# Unit 2 Answer Key — 25 Problems

## Tier 1: Beginner Problems

---

## Problem 1: Variable Declaration & Reassignment

Declare a variable `color` with the value `"blue"`, reassign it to `"red"`, then print it.

### Solution
```python
# Declare variable with initial value
color = "blue"

# Reassign to a new value
color = "red"

# Print the current value
print(color)
```

### Expected Output
```
red
```

### Common Mistakes
- Only printing "blue" because you forgot to reassign
- Not understanding that reassignment overwrites the old value

---

## Problem 2: Basic Arithmetic and PEMDAS

Calculate `(15 + 5) * 2 - 10` step by step, showing operator precedence.

### Solution
```python
# Calculate step by step following PEMDAS
# Step 1: Parentheses first: (15 + 5) = 20
# Step 2: Multiply: 20 * 2 = 40
# Step 3: Subtract: 40 - 10 = 30

result = (15 + 5) * 2 - 10
print(result)
```

### Expected Output
```
30
```

### Common Mistakes
- Calculating left-to-right without following PEMDAS (would give wrong answer)
- Not using parentheses correctly

---

## Problem 3: String Concatenation

Combine three strings: `"Hello"`, `" "`, `"World"` into a single string and print.

### Solution
```python
# Concatenate three strings
result = "Hello" + " " + "World"

# Print the combined string
print(result)
```

### Expected Output
```
Hello World
```

### Common Mistakes
- Forgetting the space string in the middle
- Using commas instead of plus signs (which would add spaces automatically)

---

## Problem 4: String Indexing

Given `word = "Programming"`, print the character at index 3.

### Solution
```python
# Create the string
word = "Programming"

# Access character at index 3 (remember: indexing starts at 0)
# P(0) r(1) o(2) g(3) r(4) a(5) m(6) m(7) i(8) n(9) g(10)
print(word[3])
```

### Expected Output
```
g
```

### Common Mistakes
- Using index 4 instead of 3 (forgetting that indexing starts at 0)
- Trying to print word[3] without understanding how indexing works

---

## Problem 5: String Length

Find and print the length of the string `"Computer Science"`.

### Solution
```python
# Use len() to find the length of the string
text = "Computer Science"
print(len(text))
```

### Expected Output
```
16
```

### Common Mistakes
- Miscounting the characters manually instead of using len()
- Forgetting to count the space character

---

## Problem 6: String Slicing

Given `text = "Python"`, extract and print `"tho"` using slicing.

### Solution
```python
# Create the string
text = "Python"

# Slice to get "tho" (characters at indices 2, 3, 4)
# P(0) y(1) t(2) h(3) o(4) n(5)
print(text[2:5])
```

### Expected Output
```
tho
```

### Common Mistakes
- Using [2:4] instead of [2:5] (forgetting that the end index is exclusive)
- Not understanding slice notation correctly

---

## Problem 7: Type Conversion

Convert the string `"99"` to an integer, add 1, and print the result.

### Solution
```python
# Convert string to integer
num = int("99")

# Add 1
result = num + 1

# Print the result
print(result)
```

### Expected Output
```
100
```

### Common Mistakes
- Trying to add 1 to the string "99" directly (which would cause an error)
- Forgetting to use int() for conversion

---

## Problem 8: String Method - Uppercase

Take the string `"hello world"` and print it in uppercase.

### Solution
```python
# Use the upper() method to convert to uppercase
text = "hello world"
print(text.upper())
```

### Expected Output
```
HELLO WORLD
```

### Common Mistakes
- Trying to use UPPER() (wrong capitalization)
- Not calling the method with parentheses

---

## Problem 9: Comparison Operator

Evaluate `10 < 15` and print the result (should be `True`).

### Solution
```python
# Evaluate the comparison
result = 10 < 15

# Print the boolean result
print(result)
```

### Expected Output
```
True
```

### Common Mistakes
- Using = (assignment) instead of < (comparison)
- Expecting a number instead of True/False

---

## Problem 10: Simple F-String

Format the price `19.99` as currency using an f-string: `f"${price:.2f}"`.

### Solution
```python
# Create the price variable
price = 19.99

# Use f-string with currency formatting
print(f"${price:.2f}")
```

### Expected Output
```
$19.99
```

### Common Mistakes
- Forgetting the `.2f` formatting specifier
- Not understanding that .2f means 2 decimal places

---

## Tier 2: Intermediate Problems

---

## Problem 11: Compound Assignment Operators

Starting with `x = 50`, use `+=`, `-=`, and `*=` to modify it, printing after each operation.

### Solution
```python
# Start with initial value
x = 50

# Add 10 using +=
x += 10
print(x)  # 60

# Subtract 5 using -=
x -= 5
print(x)  # 55

# Multiply by 2 using *=
x *= 2
print(x)  # 110
```

### Expected Output
```
60
55
110
```

### Common Mistakes
- Using += incorrectly (should be x += 10, not x + 10)
- Not tracking the value through each operation

---

## Problem 12: String Slicing with Step

Given `word = "Programming"`, use slicing with step to print every 2nd character.

### Solution
```python
# Create the string
word = "Programming"

# Slice with step of 2 to get every 2nd character
# P(0) r(1) o(2) g(3) r(4) a(5) m(6) m(7) i(8) n(9) g(10)
# Getting indices 0, 2, 4, 6, 8, 10: P, o, r, m, i, g
print(word[::2])
```

### Expected Output
```
Pormig
```

### Common Mistakes
- Using [2::2] which starts at index 2 instead of 0
- Not understanding the third parameter in slicing (start:stop:step)

---

## Problem 13: Method Chaining

Apply three string methods in sequence: `.strip()`, `.lower()`, `.title()` to `"  HELLO  "`.

### Solution
```python
# Chain multiple methods on the same string
text = "  HELLO  "
result = text.strip().lower().title()
print(result)
```

### Expected Output
```
Hello
```

### Common Mistakes
- Applying methods one at a time instead of chaining
- Not understanding the order of operations (strip removes spaces, lower converts, title capitalizes first letter)

---

## Problem 14: Multiple Assignment & Swapping

Create two variables, swap their values using `a, b = b, a`, and print before/after.

### Solution
```python
# Create two variables
a = 10
b = 20

# Print before swap
print(f"Before: a={a}, b={b}")

# Swap using tuple assignment
a, b = b, a

# Print after swap
print(f"After: a={a}, b={b}")
```

### Expected Output
```
Before: a=10, b=20
After: a=20, b=10
```

### Common Mistakes
- Using a temporary variable when Python's tuple assignment works directly
- Not printing before and after to show the swap

---

## Problem 15: Operator Precedence

Calculate `2 + 3 * 4 - 5 // 2`. Show step-by-step with correct order of operations.

### Solution
```python
# Step-by-step evaluation following operator precedence
# (*, /, //, % before +, -)
# Step 1: 3 * 4 = 12
# Step 2: 5 // 2 = 2
# Step 3: 2 + 12 = 14
# Step 4: 14 - 2 = 12

result = 2 + 3 * 4 - 5 // 2
print(result)
```

### Expected Output
```
12
```

### Common Mistakes
- Calculating left-to-right: 2+3=5, 5*4=20, 20-5=15, 15//2=7 (wrong)
- Not knowing the precedence order

---

## Problem 16: Float to Integer Conversion

Convert `7.8` to an integer using `int()`. Explain why the result is 7, not 8.

### Solution
```python
# Convert float to integer
value = 7.8
result = int(value)
print(result)

# Explanation: int() truncates (cuts off) the decimal part.
# It does NOT round - it simply removes everything after the decimal point.
# So 7.8 becomes 7, and 7.2 would also become 7.
```

### Expected Output
```
7
```

### Common Mistakes
- Thinking int() rounds (it doesn't, it truncates)
- Using round() instead of int() for conversion

---

## Problem 17: Circle Area Calculation

Ask the user for a radius and calculate area using `π * r²`. Display with 2 decimal places.

### Solution
```python
# Import math module to access pi
import math

# Ask for radius
radius = float(input("Radius: "))

# Calculate area using the formula A = π * r²
area = math.pi * radius ** 2

# Display with 2 decimal places
print(f"Area: {area:.2f}")
```

### Expected Output
```
Radius: 5
Area: 78.54
```

### Common Mistakes
- Forgetting to import math to use math.pi
- Using r * 2 instead of r ** 2 (multiply by 2 vs. square)

---

## Problem 18: String Finding

Use `.find()` to locate the first occurrence of `"an"` in `"banana"`.

### Solution
```python
# Use find() to locate substring
text = "banana"
index = text.find("an")

# Print the index where "an" is first found
print(index)
```

### Expected Output
```
1
```

### Common Mistakes
- Expecting to find "an" at index 0 or 3
- Not understanding that find() returns the starting index

---

## Problem 19: String Counting

Use `.count()` to count how many times `"l"` appears in `"hello world"`.

### Solution
```python
# Use count() to count occurrences
text = "hello world"
count = text.count("l")

# Print the count
print(count)
```

### Expected Output
```
3
```

### Common Mistakes
- Miscounting manually (forgetting one of the l's)
- Not realizing count() is case-sensitive

---

## Problem 20: Formatted Currency Output

Format these amounts as currency with thousands separator: `1234.5`, `50.1`, `999999.99`.

### Solution
```python
# Create a list of amounts
amounts = [1234.5, 50.1, 999999.99]

# Format each with currency and thousands separator
for amount in amounts:
    print(f"${amount:,.2f}")
```

### Expected Output
```
$1,234.50
$50.10
$999,999.99
```

### Common Mistakes
- Using .2f without the comma for thousands separator
- Not understanding the formatting specifier syntax: {:,.2f}

---

## Tier 3: Challenge Problems

---

## Problem 21: String Manipulation Program

Write a program that:
- Asks for a sentence
- Prints it in uppercase
- Prints the first 5 characters
- Prints the last 5 characters
- Prints it reversed

### Solution
```python
# Ask for a sentence
sentence = input("Enter a sentence: ")

# Print in uppercase
print(sentence.upper())

# Print first 5 characters
print(sentence[:5])

# Print last 5 characters
print(sentence[-5:])

# Print reversed
print(sentence[::-1])
```

### Expected Output
```
Enter a sentence: Hello World
HELLO WORLD
Hello
World
dlroW olleH
```

### Common Mistakes
- Not using proper slicing notation
- Forgetting that negative indices count from the end

---

## Problem 22: Temperature Converter

Write a program that:
- Asks for temperature in Celsius
- Converts to Fahrenheit: F = (C × 9/5) + 32
- Displays result formatted to 1 decimal place

### Solution
```python
# Ask for temperature in Celsius
celsius = float(input("Celsius: "))

# Convert to Fahrenheit
fahrenheit = (celsius * 9/5) + 32

# Display with 1 decimal place
print(f"Fahrenheit: {fahrenheit:.1f}")
```

### Expected Output
```
Celsius: 0
Fahrenheit: 32.0
```

### Common Mistakes
- Using the wrong conversion formula
- Not using the .1f formatting specifier

---

## Problem 23: Discount Calculator

Write a program that:
- Asks for original price and discount percentage
- Calculates discount amount
- Calculates final price
- Displays itemized breakdown with proper currency formatting

### Solution
```python
# Ask for original price and discount
original = float(input("Original price: $"))
discount_pct = float(input("Discount (%): "))

# Calculate discount amount
discount_amt = original * (discount_pct / 100)

# Calculate final price
final = original - discount_amt

# Display itemized breakdown
print(f"Original: ${original:.2f}")
print(f"Discount ({discount_pct}%): ${discount_amt:.2f}")
print(f"Final: ${final:.2f}")
```

### Expected Output
```
Original price: $100.00
Discount (%): 20
Original: $100.00
Discount (20.0%): $20.00
Final: $80.00
```

### Common Mistakes
- Calculating discount_amt incorrectly
- Not formatting currency values with .2f

---

## Problem 24: Pythagorean Theorem Solver

Write a program that:
- Asks for two sides of a right triangle (a and b)
- Calculates hypotenuse: c = √(a² + b²)
- Uses `math.sqrt()`
- Displays result with 2 decimal places

### Solution
```python
# Import math module for sqrt
import math

# Ask for the two sides
a = float(input("Side a: "))
b = float(input("Side b: "))

# Calculate hypotenuse using Pythagorean theorem
c = math.sqrt(a**2 + b**2)

# Display result with 2 decimal places
print(f"Hypotenuse: {c:.2f}")
```

### Expected Output
```
Side a: 3
Side b: 4
Hypotenuse: 5.00
```

### Common Mistakes
- Trying to use ** 0.5 instead of math.sqrt()
- Forgetting to square both sides before adding

---

## Problem 25: Comprehensive Calculator

Write a program that:
- Asks user to choose: Temperature, Distance, or Price calculation
- Performs the selected conversion/calculation
- Displays formatted results
- Asks if user wants another calculation
- Repeats until user quits

### Solution
```python
# Main loop - continue until user chooses to exit
while True:
    print("\n=== Calculator Menu ===")
    print("1) Temperature")
    print("2) Distance")
    print("3) Price")
    print("4) Exit")

    choice = input("Choose (1-4): ")

    if choice == "1":
        # Temperature conversion C to F
        c = float(input("Celsius: "))
        f = (c * 9/5) + 32
        print(f"Fahrenheit: {f:.1f}")
    elif choice == "2":
        # Distance conversion Meters to Feet
        m = float(input("Meters: "))
        ft = m * 3.28084
        print(f"Feet: {ft:.2f}")
    elif choice == "3":
        # Price with tax
        price = float(input("Price: $"))
        tax = price * 0.08
        total = price + tax
        print(f"Total: ${total:.2f}")
    elif choice == "4":
        # Exit the program
        break
    else:
        # Handle invalid choice
        print("Invalid choice")
```

### Expected Output
```
=== Calculator Menu ===
1) Temperature
2) Distance
3) Price
4) Exit
Choose (1-4): 1
Celsius: 25
Fahrenheit: 77.0

=== Calculator Menu ===
1) Temperature
2) Distance
3) Price
4) Exit
Choose (1-4): 4
```

### Common Mistakes
- Not implementing the loop correctly
- Not handling invalid input choices
- Not formatting output correctly

---
