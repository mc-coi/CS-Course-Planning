# Unit 1 Practice Bank — 20 Problems by Difficulty

## Beginner Problems (Straightforward, foundational concepts)

**Problem 1:** Write a program that prints your name, grade, and age on three separate lines.

**Problem 2:** Create variables for each data type (str, int, float, bool) and use `type()` to print each one.

**Problem 3:** Write a program that asks the user for their name and favorite color, then prints "Hello, [name]! I like [color] too!"

**Problem 4:** Convert 300 minutes into hours and remaining minutes using `//` and `%`.

**Problem 5:** Calculate 15 + 8 * 3 by hand, then write code to verify your answer demonstrates PEMDAS.

**Problem 6:** Write a program that asks for two numbers and prints their sum, difference, product, and quotient.

**Problem 7:** Ask the user for their height (in inches) and weight (in pounds), then store both in variables and print them.

**Problem 8:** Create a program that converts 32 Celsius to Fahrenheit using the formula F = C * 9/5 + 32.

**Problem 9:** Write a program with at least 3 comments explaining what it does.

**Problem 10:** Ask the user for a number, multiply it by 7, and print the result with a label.

---

## Intermediate Problems (Multiple steps, combining concepts)

**Problem 11:** Write a miles-to-kilometers converter. Ask for miles, display kilometers (1 mile = 1.609 km).

**Problem 12:** Create a program that asks for a price and calculates the total cost with 8% sales tax.

**Problem 13:** Ask for hours worked and hourly rate, then calculate and display gross pay, tax (15%), and net pay.

**Problem 14:** Write a program that asks for your name, age, and birth month, then calculates your approximate birth year.

**Problem 15:** Debug this code and explain the error: `age = input("Age: "); total = age + 10; print(total)`

**Problem 16:** Create a program that asks for three test scores and calculates the average.

**Problem 17:** Write a currency converter that converts USD to EUR (use 0.92 as the exchange rate).

**Problem 18:** Ask for a rectangle's length and width, then calculate and display both the area and perimeter.

**Problem 19:** Create a program that demonstrates string concatenation by combining first name, space, and last name.

**Problem 20:** Write a program that calculates how much money you'd have after saving a certain amount per month for a year.

---

## Challenge Problems (Complex, requires synthesis of multiple concepts)

**Problem 21:** Create a compound interest calculator. Ask for principal, annual rate (%), and years. Calculate and display: A = P(1 + r/100)^n

**Problem 22:** Write a program that calculates your age in days. Ask for birth month, day, and year. (Approximate is fine—assume 365 days/year)

**Problem 23:** Create a "student profile" program that collects name, grade, GPA, and whether student is on honor roll. Display everything in a formatted card with borders.

**Problem 24:** Find and fix all THREE errors in this code:
```python
GPA = Float(input("GPA: "))
score = input("Score: ")
print("Your GPA is" GPA, "and score is", score)
```

**Problem 25:** Write a tip calculator that asks for the bill amount, then calculates tip (18%), total with tip, and displays everything formatted with 2 decimal places.

**Problem 26:** Create a program following the 5-step process (Define, Plan, Code, Test, Refine) that converts a temperature from Celsius to Fahrenheit.

**Problem 27:** Write a simple BMI calculator. Ask for weight (lbs) and height (inches), calculate BMI using: BMI = weight / (height²) × 703

**Problem 28:** Create an invoice program that asks for item name, quantity, and unit price. Calculate total and display a formatted receipt.

**Problem 29:** Write a program that asks for the number of hours in a week you study, exercise, and sleep, then calculates what percentage of your week is spent on each.

**Problem 30:** Create a "time to pay off debt" calculator. Ask for debt amount, monthly payment, and interest rate. Calculate approximate months to payoff (simplified version).

---

## Problem Solutions

### Beginner Solutions

**Problem 1:**
```python
print("Alex")
print("10")
print("17")
```

**Problem 2:**
```python
name = "Jordan"
age = 16
height = 5.75
is_student = True

print(type(name))
print(type(age))
print(type(height))
print(type(is_student))
```

**Problem 3:**
```python
name = input("What is your name? ")
color = input("What is your favorite color? ")
print(f"Hello, {name}! I like {color} too!")
```

**Problem 4:**
```python
minutes = 300
hours = minutes // 60
remaining = minutes % 60
print(f"{minutes} minutes = {hours} hours and {remaining} minutes")
```

**Problem 5:**
```python
# By hand: 8 * 3 = 24, then 15 + 24 = 39
result = 15 + 8 * 3
print(result)  # Prints 39
```

**Problem 6:**
```python
num1 = float(input("First number: "))
num2 = float(input("Second number: "))
print(f"Sum: {num1 + num2}")
print(f"Difference: {num1 - num2}")
print(f"Product: {num1 * num2}")
print(f"Quotient: {num1 / num2}")
```

**Problem 7:**
```python
height = int(input("Height (inches): "))
weight = int(input("Weight (pounds): "))
print(f"Height: {height} inches")
print(f"Weight: {weight} pounds")
```

**Problem 8:**
```python
celsius = 32
fahrenheit = celsius * 9/5 + 32
print(f"{celsius}°C = {fahrenheit}°F")
```

**Problem 9:**
```python
# This program asks for a student's name
name = input("What is your name? ")
# Calculate next year
next_year_age = 17 + 1
# Print a greeting
print(f"Hello {name}! Next year you'll be {next_year_age}!")
```

**Problem 10:**
```python
number = int(input("Enter a number: "))
result = number * 7
print(f"Your number times 7 is: {result}")
```

### Intermediate Solutions

**Problem 11:**
```python
miles = float(input("Miles: "))
kilometers = miles * 1.609
print(f"{miles} miles = {kilometers:.2f} km")
```

**Problem 12:**
```python
price = float(input("Price: $"))
tax = price * 0.08
total = price + tax
print(f"Price: ${price:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Total: ${total:.2f}")
```

**Problem 13:**
```python
hours = float(input("Hours worked: "))
rate = float(input("Hourly rate: $"))
gross = hours * rate
tax = gross * 0.15
net = gross - tax
print(f"Gross: ${gross:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Net: ${net:.2f}")
```

**Problem 14:**
```python
name = input("Name: ")
age = int(input("Age: "))
month = input("Birth month: ")
birth_year = 2026 - age
print(f"{name} was born around {birth_year} in {month}")
```

**Problem 15:**
```python
# Error: input() returns a string, can't add to int
# Fix:
age = int(input("Age: "))
total = age + 10
print(total)
```

**Problem 16:**
```python
score1 = float(input("Score 1: "))
score2 = float(input("Score 2: "))
score3 = float(input("Score 3: "))
average = (score1 + score2 + score3) / 3
print(f"Average: {average:.2f}")
```

**Problem 17:**
```python
usd = float(input("USD amount: $"))
eur = usd * 0.92
print(f"${usd:.2f} USD = €{eur:.2f} EUR")
```

**Problem 18:**
```python
length = float(input("Length: "))
width = float(input("Width: "))
area = length * width
perimeter = 2 * (length + width)
print(f"Area: {area} square units")
print(f"Perimeter: {perimeter} units")
```

**Problem 19:**
```python
first_name = input("First name: ")
last_name = input("Last name: ")
full_name = first_name + " " + last_name
print(f"Full name: {full_name}")
```

**Problem 20:**
```python
monthly_savings = float(input("Monthly savings: $"))
total = monthly_savings * 12
print(f"After one year: ${total:.2f}")
```

### Challenge Solutions

**Problem 21:**
```python
principal = float(input("Principal: $"))
rate = float(input("Annual rate (%): "))
years = int(input("Years: "))
amount = principal * (1 + rate/100) ** years
print(f"After {years} years: ${amount:.2f}")
```

**Problem 23:**
```python
print("+" + "-"*30 + "+")
print("| STUDENT PROFILE             |")
print("|" + "-"*30 + "|")
name = input("Name: ")
grade = input("Grade: ")
gpa = float(input("GPA: "))
is_honors = input("Honor roll (yes/no): ")
print(f"| Name: {name:<24} |")
print(f"| Grade: {grade:<23} |")
print(f"| GPA: {gpa:<25.2f} |")
print(f"| Honors: {is_honors:<21} |")
print("+" + "-"*30 + "+")
```

**Problem 24:**
Errors:
1. `Float` should be `float`
2. Missing `+` between "is" and GPA
3. score should be converted to int before using

Fixed:
```python
gpa = float(input("GPA: "))
score = int(input("Score: "))
print("Your GPA is " + str(gpa) + " and score is " + str(score))
```

**Problem 25:**
```python
bill = float(input("Bill amount: $"))
tip = bill * 0.18
total = bill + tip
print(f"Bill: ${bill:.2f}")
print(f"Tip (18%): ${tip:.2f}")
print(f"Total: ${total:.2f}")
```

**Problem 27:**
```python
weight = float(input("Weight (lbs): "))
height = float(input("Height (inches): "))
bmi = (weight / (height ** 2)) * 703
print(f"Your BMI: {bmi:.2f}")
```

---
