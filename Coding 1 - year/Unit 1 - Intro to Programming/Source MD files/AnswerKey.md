# Unit 1 Answer Key — 30 Problems

## Beginner Problems

---

## Problem 1: Personal Information

Write a program that prints your name, grade, and age on three separate lines.

### Solution
```python
# Print personal information
print("Alex")
print("10")
print("17")
```

### Expected Output
```
Alex
10
17
```

### Common Mistakes
- Forgetting to put each item on a separate line using separate print statements
- Using commas in a single print statement (which adds spaces between values)

---

## Problem 2: Data Types

Create variables for each data type (str, int, float, bool) and use `type()` to print each one.

### Solution
```python
# Create variables of different data types
name = "Jordan"
age = 16
height = 5.75
is_student = True

# Print the type of each variable
print(type(name))
print(type(age))
print(type(height))
print(type(is_student))
```

### Expected Output
```
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
```

### Common Mistakes
- Not storing variables before calling type() on them
- Forgetting that type() returns a type object, not a string

---

## Problem 3: User Input and Greeting

Write a program that asks the user for their name and favorite color, then prints "Hello, [name]! I like [color] too!"

### Solution
```python
# Ask user for input
name = input("What is your name? ")
color = input("What is your favorite color? ")

# Print personalized greeting
print(f"Hello, {name}! I like {color} too!")
```

### Expected Output
```
What is your name? Alex
What is your favorite color? blue
Hello, Alex! I like blue too!
```

### Common Mistakes
- Forgetting to use f-strings or concatenation to combine variables with text
- Not calling input() for each piece of information separately

---

## Problem 4: Integer Division and Modulo

Convert 300 minutes into hours and remaining minutes using `//` and `%`.

### Solution
```python
# Store the total minutes
minutes = 300

# Calculate hours using integer division
hours = minutes // 60

# Calculate remaining minutes using modulo
remaining = minutes % 60

# Display the result
print(f"{minutes} minutes = {hours} hours and {remaining} minutes")
```

### Expected Output
```
300 minutes = 5 hours and 0 minutes
```

### Common Mistakes
- Using `/` (regular division) instead of `//` (integer division)
- Confusing which operator gives the remainder (it's `%`, not `/`)

---

## Problem 5: PEMDAS Order of Operations

Calculate 15 + 8 * 3 by hand, then write code to verify your answer demonstrates PEMDAS.

### Solution
```python
# By hand: 8 * 3 = 24, then 15 + 24 = 39
# Python follows PEMDAS (multiplication before addition)
result = 15 + 8 * 3
print(result)  # Should be 39
```

### Expected Output
```
39
```

### Common Mistakes
- Calculating left-to-right as 15 + 8 = 23, then 23 * 3 = 69 (wrong order)
- Not understanding that multiplication has higher precedence than addition

---

## Problem 6: Four Operations

Write a program that asks for two numbers and prints their sum, difference, product, and quotient.

### Solution
```python
# Ask user for two numbers
num1 = float(input("First number: "))
num2 = float(input("Second number: "))

# Calculate all four operations
print(f"Sum: {num1 + num2}")
print(f"Difference: {num1 - num2}")
print(f"Product: {num1 * num2}")
print(f"Quotient: {num1 / num2}")
```

### Expected Output
```
First number: 10
Second number: 5
Sum: 15.0
Difference: 5.0
Product: 50.0
Quotient: 2.0
```

### Common Mistakes
- Using int() instead of float() (doesn't allow decimal input)
- Forgetting to use f-strings to display the operations clearly

---

## Problem 7: Height and Weight Storage

Ask the user for their height (in inches) and weight (in pounds), then store both in variables and print them.

### Solution
```python
# Ask user for height and weight
height = int(input("Height (inches): "))
weight = int(input("Weight (pounds): "))

# Store and display the values
print(f"Height: {height} inches")
print(f"Weight: {weight} pounds")
```

### Expected Output
```
Height (inches): 72
Weight (pounds): 150
Height: 72 inches
Weight: 150 pounds
```

### Common Mistakes
- Not converting input to int (input always returns a string)
- Not providing clear labels in the output

---

## Problem 8: Celsius to Fahrenheit

Create a program that converts 32 Celsius to Fahrenheit using the formula F = C * 9/5 + 32.

### Solution
```python
# Store the Celsius temperature
celsius = 32

# Apply the conversion formula
fahrenheit = celsius * 9/5 + 32

# Display the result
print(f"{celsius}°C = {fahrenheit}°F")
```

### Expected Output
```
32°C = 89.6°F
```

### Common Mistakes
- Using integer division (`//`) instead of regular division (`/`)
- Getting the formula wrong (e.g., multiplying by 5/9 instead of 9/5)

---

## Problem 9: Code with Comments

Write a program with at least 3 comments explaining what it does.

### Solution
```python
# This program asks for a student's name and age
name = input("What is your name? ")
age = int(input("What is your age? "))

# Calculate next year's age by adding 1
next_year_age = age + 1

# Display a greeting with the calculated age
print(f"Hello {name}! Next year you'll be {next_year_age}!")
```

### Expected Output
```
What is your name? Sam
What is your age? 16
Hello Sam! Next year you'll be 17!
```

### Common Mistakes
- Comments that are too obvious or don't add value
- Forgetting that comments should explain the "why," not just the "what"

---

## Problem 10: Multiplication with Label

Ask the user for a number, multiply it by 7, and print the result with a label.

### Solution
```python
# Ask user to enter a number
number = int(input("Enter a number: "))

# Multiply the number by 7
result = number * 7

# Print the result with a descriptive label
print(f"Your number times 7 is: {result}")
```

### Expected Output
```
Enter a number: 5
Your number times 7 is: 35
```

### Common Mistakes
- Forgetting to use f-strings for a clear label
- Not converting input to int before multiplying

---

## Intermediate Problems

---

## Problem 11: Miles to Kilometers

Write a miles-to-kilometers converter. Ask for miles, display kilometers (1 mile = 1.609 km).

### Solution
```python
# Ask user for distance in miles
miles = float(input("Miles: "))

# Convert to kilometers using the conversion factor
kilometers = miles * 1.609

# Display the result with 2 decimal places
print(f"{miles} miles = {kilometers:.2f} km")
```

### Expected Output
```
Miles: 5
5.0 miles = 8.05 km
```

### Common Mistakes
- Forgetting to use `:.2f` to format the result to 2 decimal places
- Using the wrong conversion factor

---

## Problem 12: Price with Sales Tax

Create a program that asks for a price and calculates the total cost with 8% sales tax.

### Solution
```python
# Ask user for the price
price = float(input("Price: $"))

# Calculate 8% sales tax
tax = price * 0.08

# Calculate total
total = price + tax

# Display itemized breakdown
print(f"Price: ${price:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Total: ${total:.2f}")
```

### Expected Output
```
Price: $25.00
Price: $25.00
Tax: $2.00
Total: $27.00
```

### Common Mistakes
- Not using proper currency formatting (`.2f`)
- Forgetting to add the tax to the price

---

## Problem 13: Gross Pay, Tax, and Net Pay

Ask for hours worked and hourly rate, then calculate and display gross pay, tax (15%), and net pay.

### Solution
```python
# Ask user for hours and rate
hours = float(input("Hours worked: "))
rate = float(input("Hourly rate: $"))

# Calculate gross pay
gross = hours * rate

# Calculate 15% tax
tax = gross * 0.15

# Calculate net pay (after tax)
net = gross - tax

# Display breakdown
print(f"Gross: ${gross:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Net: ${net:.2f}")
```

### Expected Output
```
Hours worked: 40
Hourly rate: $15
Gross: $600.00
Tax: $90.00
Net: $510.00
```

### Common Mistakes
- Confusing the order: deducting tax from hours instead of from gross pay
- Not formatting currency values with 2 decimal places

---

## Problem 14: Calculate Birth Year

Write a program that asks for your name, age, and birth month, then calculates your approximate birth year.

### Solution
```python
# Get personal information from user
name = input("Name: ")
age = int(input("Age: "))
month = input("Birth month: ")

# Calculate approximate birth year (assuming current year is 2026)
birth_year = 2026 - age

# Display result
print(f"{name} was born around {birth_year} in {month}")
```

### Expected Output
```
Name: Emma
Age: 16
Birth month: March
Emma was born around 2010 in March
```

### Common Mistakes
- Using the wrong current year in the calculation
- Not converting age to int before subtracting

---

## Problem 15: Debug Input and Type Error

Debug this code and explain the error: `age = input("Age: "); total = age + 10; print(total)`

### Solution
```python
# Error: input() returns a string, can't directly add to an int
# Fix: Convert the input to an integer first

age = int(input("Age: "))
total = age + 10
print(total)
```

### Expected Output
```
Age: 25
35
```

### Common Mistakes
- Forgetting that input() always returns a string
- Trying to add a string to an integer (TypeError)

---

## Problem 16: Average of Three Test Scores

Create a program that asks for three test scores and calculates the average.

### Solution
```python
# Ask user for three test scores
score1 = float(input("Score 1: "))
score2 = float(input("Score 2: "))
score3 = float(input("Score 3: "))

# Calculate the average
average = (score1 + score2 + score3) / 3

# Display with 2 decimal places
print(f"Average: {average:.2f}")
```

### Expected Output
```
Score 1: 85
Score 2: 92
Score 3: 78
Average: 85.00
```

### Common Mistakes
- Dividing by 2 instead of 3
- Not formatting the average to 2 decimal places

---

## Problem 17: USD to EUR Currency Converter

Write a currency converter that converts USD to EUR (use 0.92 as the exchange rate).

### Solution
```python
# Ask user for USD amount
usd = float(input("USD amount: $"))

# Convert to EUR using the exchange rate
eur = usd * 0.92

# Display result with proper formatting
print(f"${usd:.2f} USD = €{eur:.2f} EUR")
```

### Expected Output
```
USD amount: $100
$100.00 USD = €92.00 EUR
```

### Common Mistakes
- Using the wrong exchange rate
- Not formatting both currencies consistently

---

## Problem 18: Rectangle Area and Perimeter

Ask for a rectangle's length and width, then calculate and display both the area and perimeter.

### Solution
```python
# Ask user for dimensions
length = float(input("Length: "))
width = float(input("Width: "))

# Calculate area and perimeter
area = length * width
perimeter = 2 * (length + width)

# Display results
print(f"Area: {area} square units")
print(f"Perimeter: {perimeter} units")
```

### Expected Output
```
Length: 10
Width: 5
Area: 50.0 square units
Perimeter: 30.0 units
```

### Common Mistakes
- Using wrong formulas (e.g., `length + width` for area)
- Forgetting to multiply by 2 in the perimeter formula

---

## Problem 19: String Concatenation

Create a program that demonstrates string concatenation by combining first name, space, and last name.

### Solution
```python
# Ask user for first and last name
first_name = input("First name: ")
last_name = input("Last name: ")

# Concatenate with a space in between
full_name = first_name + " " + last_name

# Display the full name
print(f"Full name: {full_name}")
```

### Expected Output
```
First name: John
Last name: Doe
Full name: John Doe
```

### Common Mistakes
- Forgetting to include the space in the concatenation
- Not using proper string concatenation syntax

---

## Problem 20: Annual Savings

Write a program that calculates how much money you'd have after saving a certain amount per month for a year.

### Solution
```python
# Ask user for monthly savings amount
monthly_savings = float(input("Monthly savings: $"))

# Calculate total after 12 months
total = monthly_savings * 12

# Display result formatted as currency
print(f"After one year: ${total:.2f}")
```

### Expected Output
```
Monthly savings: $250
After one year: $3000.00
```

### Common Mistakes
- Forgetting to multiply by 12 (months in a year)
- Not formatting the result as currency

---

## Challenge Problems

---

## Problem 21: Compound Interest Calculator

Create a compound interest calculator. Ask for principal, annual rate (%), and years. Calculate and display: A = P(1 + r/100)^n

### Solution
```python
# Ask user for investment details
principal = float(input("Principal: $"))
rate = float(input("Annual rate (%): "))
years = int(input("Years: "))

# Calculate compound interest using the formula
amount = principal * (1 + rate/100) ** years

# Display result with 2 decimal places
print(f"After {years} years: ${amount:.2f}")
```

### Expected Output
```
Principal: $1000
Annual rate (%): 5
Years: 10
After 10 years: $1628.89
```

### Common Mistakes
- Forgetting to divide the rate by 100
- Using the wrong exponent operator (^ instead of **)

---

## Problem 22: Age in Days

Write a program that calculates your age in days. Ask for birth month, day, and year. (Approximate is fine—assume 365 days/year)

### Solution
```python
# Ask user for birth date
birth_month = int(input("Birth month: "))
birth_day = int(input("Birth day: "))
birth_year = int(input("Birth year: "))

# Calculate age (current year is 2026)
age_years = 2026 - birth_year

# Convert to days (365 days per year, approximate)
age_days = age_years * 365

# Display result
print(f"You are approximately {age_days} days old")
```

### Expected Output
```
Birth month: 3
Birth day: 15
Birth year: 2010
You are approximately 5840 days old
```

### Common Mistakes
- Not accounting for leap years (though approximate is acceptable)
- Using the wrong current year

---

## Problem 23: Student Profile Card

Create a "student profile" program that collects name, grade, GPA, and whether student is on honor roll. Display everything in a formatted card with borders.

### Solution
```python
# Display top border
print("+" + "-"*30 + "+")
print("| STUDENT PROFILE             |")
print("|" + "-"*30 + "|")

# Ask for student information
name = input("Name: ")
grade = input("Grade: ")
gpa = float(input("GPA: "))
is_honors = input("Honor roll (yes/no): ")

# Display student information in a formatted card
print(f"| Name: {name:<24} |")
print(f"| Grade: {grade:<23} |")
print(f"| GPA: {gpa:<25.2f} |")
print(f"| Honors: {is_honors:<21} |")

# Display bottom border
print("+" + "-"*30 + "+")
```

### Expected Output
```
+------------------------------+
| STUDENT PROFILE             |
|------------------------------|
Name: Alice
Grade: 11
GPA: 3.85
Honor roll (yes/no): yes
| Name: Alice                  |
| Grade: 11                    |
| GPA: 3.85                    |
| Honors: yes                  |
+------------------------------+
```

### Common Mistakes
- Not aligning the output properly using f-string formatting specifiers
- Calculating border length incorrectly

---

## Problem 24: Fix Multiple Errors

Find and fix all THREE errors in this code:
```python
GPA = Float(input("GPA: "))
score = input("Score: ")
print("Your GPA is" GPA, "and score is", score)
```

### Solution
```python
# Error 1: Float should be lowercase float
# Error 2: Missing + between string and GPA in print
# Error 3: score should be converted to int

gpa = float(input("GPA: "))
score = int(input("Score: "))
print("Your GPA is " + str(gpa) + " and score is " + str(score))
```

### Expected Output
```
GPA: 3.85
Score: 95
Your GPA is 3.85 and score is 95
```

### Common Mistakes
- Not identifying all three errors
- Not understanding that function names are case-sensitive
- Forgetting to convert variables to strings when concatenating

---

## Problem 25: Tip Calculator

Write a tip calculator that asks for the bill amount, then calculates tip (18%), total with tip, and displays everything formatted with 2 decimal places.

### Solution
```python
# Ask user for the bill amount
bill = float(input("Bill amount: $"))

# Calculate 18% tip
tip = bill * 0.18

# Calculate total
total = bill + tip

# Display breakdown with 2 decimal places
print(f"Bill: ${bill:.2f}")
print(f"Tip (18%): ${tip:.2f}")
print(f"Total: ${total:.2f}")
```

### Expected Output
```
Bill amount: $45.00
Bill: $45.00
Tip (18%): $8.10
Total: $53.10
```

### Common Mistakes
- Not calculating the tip percentage correctly
- Forgetting to format with 2 decimal places

---

## Problem 26: Temperature Conversion (5-Step Process)

Create a program following the 5-step process (Define, Plan, Code, Test, Refine) that converts a temperature from Celsius to Fahrenheit.

### Solution
```python
# Define: Convert Celsius to Fahrenheit using F = C * 9/5 + 32
# Plan: 1) Ask user for Celsius, 2) Apply formula, 3) Display result
# Code:

celsius = float(input("Enter temperature in Celsius: "))
fahrenheit = celsius * 9/5 + 32
print(f"{celsius}°C = {fahrenheit:.1f}°F")

# Test: Try with 0°C (should be 32°F) and 100°C (should be 212°F)
# Refine: Code is clear and accurate
```

### Expected Output
```
Enter temperature in Celsius: 0
0.0°C = 32.0°F
```

### Common Mistakes
- Not following a structured approach
- Skipping the testing/refinement steps

---

## Problem 27: BMI Calculator

Write a simple BMI calculator. Ask for weight (lbs) and height (inches), calculate BMI using: BMI = weight / (height²) × 703

### Solution
```python
# Ask user for weight and height
weight = float(input("Weight (lbs): "))
height = float(input("Height (inches): "))

# Calculate BMI using the formula
bmi = (weight / (height ** 2)) * 703

# Display result
print(f"Your BMI: {bmi:.2f}")
```

### Expected Output
```
Weight (lbs): 150
Height (inches): 70
Your BMI: 21.52
```

### Common Mistakes
- Using height instead of height squared
- Using the wrong constant (should be 703 for imperial units)

---

## Problem 28: Invoice Program

Create an invoice program that asks for item name, quantity, and unit price. Calculate total and display a formatted receipt.

### Solution
```python
# Ask user for item details
item_name = input("Item name: ")
quantity = int(input("Quantity: "))
unit_price = float(input("Unit price: $"))

# Calculate total
total = quantity * unit_price

# Display formatted receipt
print("\n" + "="*30)
print("RECEIPT")
print("="*30)
print(f"Item: {item_name}")
print(f"Quantity: {quantity}")
print(f"Unit Price: ${unit_price:.2f}")
print(f"Total: ${total:.2f}")
print("="*30)
```

### Expected Output
```
Item name: Notebook
Quantity: 3
Unit price: $4.50

==============================
RECEIPT
==============================
Item: Notebook
Quantity: 3
Unit Price: $4.50
Total: $13.50
==============================
```

### Common Mistakes
- Not formatting the receipt clearly
- Not converting input to appropriate types

---

## Problem 29: Time Breakdown Percentages

Write a program that asks for the number of hours in a week you study, exercise, and sleep, then calculates what percentage of your week is spent on each.

### Solution
```python
# Ask user for hours spent on each activity
study_hours = float(input("Hours studying: "))
exercise_hours = float(input("Hours exercising: "))
sleep_hours = float(input("Hours sleeping: "))

# Total hours in a week
total_hours = 7 * 24

# Calculate percentages
study_pct = (study_hours / total_hours) * 100
exercise_pct = (exercise_hours / total_hours) * 100
sleep_pct = (sleep_hours / total_hours) * 100

# Display results
print(f"Study: {study_pct:.1f}%")
print(f"Exercise: {exercise_pct:.1f}%")
print(f"Sleep: {sleep_pct:.1f}%")
```

### Expected Output
```
Hours studying: 20
Hours exercising: 10
Hours sleeping: 56
Study: 11.9%
Exercise: 5.9%
Sleep: 33.3%
```

### Common Mistakes
- Forgetting that there are 168 hours in a week (7 × 24)
- Not multiplying by 100 when calculating percentage

---

## Problem 30: Time to Pay Off Debt

Create a "time to pay off debt" calculator. Ask for debt amount, monthly payment, and interest rate. Calculate approximate months to payoff (simplified version).

### Solution
```python
# Ask user for debt details
debt = float(input("Debt amount: $"))
monthly_payment = float(input("Monthly payment: $"))
interest_rate = float(input("Interest rate (%): "))

# Simplified calculation (ignoring compounding for simplicity)
# Months = Debt / (Monthly Payment - Monthly Interest)
monthly_interest = debt * (interest_rate / 100) / 12
monthly_principal = monthly_payment - monthly_interest

if monthly_principal > 0:
    months = debt / monthly_principal
    print(f"Approximate months to pay off: {months:.1f}")
else:
    print("Payment is too low to pay off the debt")
```

### Expected Output
```
Debt amount: $5000
Monthly payment: $150
Interest rate: 5
Approximate months to pay off: 35.6
```

### Common Mistakes
- Not accounting for interest in the calculation
- Using incorrect interest calculation (annual vs. monthly)
- Not checking if the payment is sufficient to pay off debt

---
