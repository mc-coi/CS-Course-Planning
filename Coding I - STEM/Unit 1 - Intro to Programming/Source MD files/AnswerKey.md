# Unit 1: Intro to Programming - Answer Key

---

## Problem 1: Print Your Name 5 Times

### Solution
```python
# Print name 5 times, each on its own line
name = "Alice"
print(name)
print(name)
print(name)
print(name)
print(name)
```

### Expected Output
```
Alice
Alice
Alice
Alice
Alice
```

### Common Mistakes
- Using a loop instead of repetition (while technically correct, misses the point of repetition practice)
- Forgetting that each `print()` automatically adds a newline

---

## Problem 2: Declare Variables for Each Data Type

### Solution
```python
# Declare a variable for each data type
name = "Alice"           # str
age = 25                 # int
height = 5.6             # float
is_student = True        # bool

# Use type() to print each one
print(f"name: {type(name)}")
print(f"age: {type(age)}")
print(f"height: {type(height)}")
print(f"is_student: {type(is_student)}")
```

### Expected Output
```
name: <class 'str'>
age: <class 'int'>
height: <class 'float'>
is_student: <class 'bool'>
```

### Common Mistakes
- Using single quotes vs double quotes (both are correct, but confusing them)
- Forgetting to use `type()` function or calling it incorrectly
- Using 0/1 instead of True/False for boolean

---

## Problem 3: Sum, Difference, Product, and Quotient

### Solution
```python
# Ask for two numbers
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

# Calculate and print operations
print(f"Sum: {num1 + num2}")
print(f"Difference: {num1 - num2}")
print(f"Product: {num1 * num2}")
print(f"Quotient: {num1 / num2}")
```

### Expected Output
```
Enter first number: 10
Enter second number: 3
Sum: 13.0
Difference: 7.0
Product: 30.0
Quotient: 3.3333333333333335
```

### Common Mistakes
- Using `int()` instead of `float()` (loses decimal precision)
- Attempting integer division (//) instead of regular division (/)
- Not handling division by zero

---

## Problem 4: Miles to Kilometers Converter

### Solution
```python
# Miles to kilometers converter
miles = float(input("Enter miles: "))
kilometers = miles * 1.60934

print(f"{miles} miles = {kilometers} kilometers")
```

### Expected Output
```
Enter miles: 5
5.0 miles = 8.0467 kilometers
```

### Common Mistakes
- Using the wrong conversion factor
- Not storing the conversion factor as a named constant
- Printing too many or too few decimal places without rounding

---

## Problem 5: Rectangle Area and Perimeter

### Solution
```python
# Ask for dimensions
length = float(input("Enter length: "))
width = float(input("Enter width: "))

# Calculate area and perimeter
area = length * width
perimeter = 2 * (length + width)

# Print results
print(f"Area: {area}")
print(f"Perimeter: {perimeter}")
```

### Expected Output
```
Enter length: 4
Enter width: 6
Area: 24.0
Perimeter: 20.0
```

### Common Mistakes
- Confusing area (length × width) with perimeter
- Using wrong perimeter formula (e.g., 2*length + 2*width works, but 2*(length + width) is cleaner)
- Not converting input to float

---

## Problem 6: Type Comparison - String vs Float

### Solution
```python
# Demonstrate type difference
result1 = type("3.14")
result2 = type(3.14)

print(f"type('3.14') = {result1}")
print(f"type(3.14) = {result2}")

# Explanation: "3.14" is text (str), while 3.14 is a number (float)
print("\n'3.14' is a string (text), so it has quotes and won't do math")
print("3.14 is a float (number), so it can be used in calculations")

# Demonstrate:
print(f"\n'3.14' + '2.0' = {('3.14' + '2.0')}")  # String concatenation
print(f"3.14 + 2.0 = {3.14 + 2.0}")              # Numeric addition
```

### Expected Output
```
type('3.14') = <class 'str'>
type(3.14) = <class 'float'>

'3.14' is a string (text), so it has quotes and won't do math
3.14 is a float (number), so it can be used in calculations

'3.14' + '2.0' = 3.142.0
3.14 + 2.0 = 5.14
```

### Common Mistakes
- Not understanding the practical difference (both look like 3.14)
- Confusing when to use quotes vs when not to
- Not recognizing that strings cannot be used in math operations

---

## Problem 7: Fix Input and Type Conversion Error

### Solution
```python
# ORIGINAL CODE (BROKEN):
# num = input("Enter: ")
# print(num + 10)  # ERROR: cannot add string + int

# FIXED CODE:
num = input("Enter: ")
num = int(num)  # Convert string to integer
print(num + 10)

# EXPLANATION:
# input() always returns a string, even if user types a number
# We must explicitly convert it using int() before doing math
```

### Expected Output
```
Enter: 5
15
```

### Common Mistakes
- Not converting `input()` to an integer before math operations
- Using `float()` when an integer is needed (works but unnecessary)
- Forgetting that `input()` returns a string, not a number

---

## Problem 8: Price and Quantity with Tax

### Solution
```python
# Ask for price and quantity
price = float(input("Enter price per item: "))
quantity = float(input("Enter quantity: "))

# Calculate subtotal
subtotal = price * quantity

# Apply 8% tax
tax = subtotal * 0.08
total = subtotal + tax

# Print results
print(f"Subtotal: ${subtotal:.2f}")
print(f"Tax (8%): ${tax:.2f}")
print(f"Total: ${total:.2f}")
```

### Expected Output
```
Enter price per item: 12.99
Enter quantity: 3
Subtotal: $38.97
Tax (8%): $3.12
Total: $42.09
```

### Common Mistakes
- Calculating tax on the total instead of the subtotal
- Forgetting to add tax to subtotal
- Not formatting output with 2 decimal places

---

## Problem 9: Modulo Operator - 17 % 5

### Solution
```python
# Calculate modulo
result = 17 % 5
print(f"17 % 5 = {result}")

# Explanation
print("\n17 divided by 5:")
print("17 ÷ 5 = 3 remainder 2")
print("So 17 % 5 = 2")

# Real-world example: checking if number is even or odd
number = 17
if number % 2 == 0:
    print(f"{number} is even")
else:
    print(f"{number} is odd")

# Another example: checking time
total_minutes = 97
hours = total_minutes // 60
minutes = total_minutes % 60
print(f"\n97 minutes = {hours} hours and {minutes} minutes")
```

### Expected Output
```
17 % 5 = 2

17 divided by 5:
17 ÷ 5 = 3 remainder 2
So 17 % 5 = 2

17 is odd

97 minutes = 1 hours and 37 minutes
```

### Common Mistakes
- Thinking modulo is division (confusing with // operator)
- Misunderstanding that it returns the remainder
- Real-world applications: used for divisibility checks, cycling patterns, time conversions

---

## Problem 10: Variable Assignment and Prediction

### Solution
```python
# Step through the code
x = 5
y = x + 3  # y = 5 + 3 = 8
x = 10     # x changes, but y stays the same
print(x, y)

# Explanation print
print("\nStep-by-step:")
print("1. x = 5")
print("2. y = x + 3 → y = 5 + 3 = 8")
print("3. x = 10 (x changes, but y was already calculated)")
print("4. x is now 10, y is still 8")
```

### Expected Output
```
10 8

Step-by-step:
1. x = 5
2. y = x + 3 → y = 5 + 3 = 8
3. x = 10 (x changes, but y was already calculated)
4. x is now 10, y is still 8
```

### Common Mistakes
- Thinking y will change to 13 when x changes (y was already calculated and stored)
- Not understanding that variables store values, not references to other variables
- Predicting output as "10 13"

---

## Problem 11: Savings Calculator

### Solution
```python
# Savings calculator
starting_balance = float(input("Enter starting balance: $"))
monthly_savings = float(input("Enter monthly savings: $"))
months = int(input("Enter number of months: "))

# Calculate total
total_saved = starting_balance + (monthly_savings * months)

# Calculate average per month
total_deposited = monthly_savings * months
average_per_month = total_deposited / months  # This is just monthly_savings

# Print results
print(f"\nStarting balance: ${starting_balance:.2f}")
print(f"Monthly savings: ${monthly_savings:.2f}")
print(f"Number of months: {months}")
print(f"Total saved: ${total_saved:.2f}")
print(f"Average per month: ${average_per_month:.2f}")
```

### Expected Output
```
Enter starting balance: $1000
Enter monthly savings: $200
Enter number of months: 6

Starting balance: $1000.00
Monthly savings: $200.00
Number of months: 6
Total saved: $2200.00
Average per month: $200.00
```

### Common Mistakes
- Confusing total savings with money deposited (need to include starting balance)
- Calculating average incorrectly (should be total_deposited / months)
- Not formatting currency with 2 decimal places

---

## Problem 12: String Concatenation Error

### Solution
```python
# ORIGINAL CODE (ERROR):
# print("Hello" + 5)  # TypeError: cannot concatenate str and int

# EXPLANATION AND FIXES:
print("ERROR: TypeError: can only concatenate str (not 'int') to str")
print("\nFix 1: Convert the number to string")
print("Hello" + str(5))

print("\nFix 2: Use f-string or format()")
print(f"Hello {5}")

print("\nFix 3: Use comma in print (automatic space)")
print("Hello", 5)
```

### Expected Output
```
ERROR: TypeError: can only concatenate str (not 'int') to str

Fix 1: Convert the number to string
Hello5

Fix 2: Use f-string or format()
Hello 5

Fix 3: Use comma in print (automatic space)
Hello 5
```

### Common Mistakes
- Not understanding that strings and numbers need explicit conversion to combine
- Forgetting `str()` conversion
- Not knowing alternative approaches (f-strings, format(), commas in print)

---

## Problem 13: Study Hours Tracker

### Solution
```python
# Ask for study hours Monday through Friday
monday = float(input("Hours studied Monday: "))
tuesday = float(input("Hours studied Tuesday: "))
wednesday = float(input("Hours studied Wednesday: "))
thursday = float(input("Hours studied Thursday: "))
friday = float(input("Hours studied Friday: "))

# Calculate total and average
total_hours = monday + tuesday + wednesday + thursday + friday
daily_average = total_hours / 5

# Print results
print(f"\nWeekly study summary:")
print(f"Total hours studied: {total_hours}")
print(f"Daily average: {daily_average}")
```

### Expected Output
```
Hours studied Monday: 2
Hours studied Tuesday: 3
Hours studied Wednesday: 1.5
Hours studied Thursday: 2.5
Hours studied Friday: 1

Weekly study summary:
Total hours studied: 10.0
Daily average: 2.0
```

### Common Mistakes
- Using only 4 days instead of 5 when calculating average
- Dividing by the wrong number (should be 5, not 7)
- Not storing all values before calculating

---

## Problem 14: Currency Converter

### Solution
```python
# Currency converter - USD to other currencies
# Exchange rates (approximate as of 2024)
usd_to_eur = 0.92
usd_to_jpy = 150.00
usd_to_gbp = 0.79

# Ask for USD amount
usd = float(input("Enter amount in USD: $"))

# Convert to other currencies
eur = usd * usd_to_eur
jpy = usd * usd_to_jpy
gbp = usd * usd_to_gbp

# Print results
print(f"\n${usd} USD equals:")
print(f"€{eur:.2f} EUR (Euro)")
print(f"¥{jpy:.2f} JPY (Japanese Yen)")
print(f"£{gbp:.2f} GBP (British Pound)")
```

### Expected Output
```
Enter amount in USD: $100
$100.0 USD equals:
€92.00 EUR (Euro)
¥15000.00 JPY (Japanese Yen)
£79.00 GBP (British Pound)
```

### Common Mistakes
- Using outdated or incorrect exchange rates
- Not storing rates as variables (hardcoding)
- Forgetting to format output with proper symbols and decimal places
- Converting in the wrong direction (JPY to USD instead of USD to JPY)

---

## Problem 15: Debug GPA Input

### Solution
```python
# ORIGINAL CODE (3 ERRORS):
# gpa = Float(input("GPA: "))           # ERROR 1: Float should be float (lowercase)
# print("Your gpa is" gpa)              # ERROR 2: Missing + operator for concatenation
#                                        # ERROR 3: Line above has syntax error

# FIXED CODE:
gpa = float(input("GPA: "))
print("Your gpa is " + str(gpa))

# OR using f-string (preferred):
gpa = float(input("GPA: "))
print(f"Your gpa is {gpa}")
```

### Expected Output
```
GPA: 3.5
Your gpa is 3.5
```

### Common Mistakes
- Using `Float()` instead of `float()` (Python is case-sensitive for built-in functions)
- Forgetting the `+` operator when concatenating strings
- Missing space in the output string
- Not converting the number to a string for concatenation

---
