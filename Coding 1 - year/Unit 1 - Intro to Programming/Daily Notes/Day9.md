# Day 9: Type Conversion — int(), float(), str() with input()
**Learning Target:** I can convert user input to numeric data types for calculations.

### Key Concepts
Since `input()` always returns a string, you must **convert** the string to a number before using it in calculations. This is called **type conversion** or **casting**.

Three main conversion functions:
- `int()` - Converts a value to an integer (whole number)
- `float()` - Converts a value to a float (decimal number)
- `str()` - Converts a value to a string (text)

**Important notes:**
- `int("5")` works → 5
- `int("5.5")` fails → error (can't convert string with decimal directly to int)
- `int(5.9)` works → 5 (truncates/removes the decimal)
- `float("5")` works → 5.0
- `float("5.5")` works → 5.5
- `str(5)` works → "5" (now it's text)

**Common pattern:** `variable = int(input("Prompt: "))` or `variable = float(input("Prompt: "))`

### Code Examples
```python
# Converting input to int
age = int(input("How old are you? "))
print(age)         # Now it's a number, not text

# Converting input to float
height = float(input("How tall are you (in feet)? "))
print(height)      # Now it's a decimal number

# Converting numbers to strings for concatenation
score = 95
message = "Your score: " + str(score)
print(message)     # Concatenation works now!

# Using converted input in calculations
hours = int(input("Hours worked: "))
pay = hours * 15   # This works because hours is an int
print(f"You earned: ${pay}")

# Multiple conversions
num1 = int(input("First number: "))
num2 = int(input("Second number: "))
sum_result = num1 + num2
print(f"Sum: {sum_result}")
```

### Guided Practice
Create a simple calculator program that:
1. Asks the user for two numbers using `input()`
2. Converts both to integers or floats
3. Calculates the sum, difference, and product
4. Prints the results with labels

### Practice Problems

**Problem 1 — Beginner:** Write a program that asks for two numbers and prints their sum, difference, product, and quotient.

```python
# Starter code
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))

print("Sum:", )
print("Difference:", )
print("Product:", )
print("Quotient:", )
```

**Problem 2 — Intermediate:** Write a miles-to-kilometers converter. Ask the user for miles (as a float) and print the equivalent in km (1 mile = 1.60934 km).

**Problem 3 — Challenge:** Write a program that asks for a principal amount (starting money), interest rate (as a decimal), and years, then calculates compound interest.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use the arithmetic operators to combine num1 and num2
- Problem 2: Remember to convert input to float, then multiply
- Problem 3: Formula: New Amount = Principal × (1 + rate)^years
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))
print("Sum:", num1 + num2)
print("Difference:", num1 - num2)
print("Product:", num1 * num2)
print("Quotient:", num1 / num2)

# Problem 2 Example
miles = float(input("Enter miles: "))
kilometers = miles * 1.60934
print(f"{miles} miles = {kilometers:.2f} km")

# Problem 3 Example
principal = float(input("Principal: $"))
rate = float(input("Interest rate (as decimal): "))
years = int(input("Years: "))
new_amount = principal * ((1 + rate) ** years)
print(f"After {years} years: ${new_amount:.2f}")
```

</details>

---
