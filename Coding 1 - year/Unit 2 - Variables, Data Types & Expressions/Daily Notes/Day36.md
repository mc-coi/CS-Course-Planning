# Day 36: Constants and Naming Conventions — UPPER_CASE, snake_case

**Learning Target:** I can follow Python naming conventions and use constants to write clean, maintainable code.

### Key Concepts

**Naming conventions** make code more readable and help other programmers (and your future self) understand your code quickly.

**Variables and functions** use **snake_case**: `first_name`, `calculate_total`, `user_age`. Letters are lowercase, words separated by underscores. Never use spaces or hyphens.

**Constants** use **UPPER_CASE**: `PI = 3.14159`, `MAX_ATTEMPTS = 5`, `TAX_RATE = 0.08`. Constants are values that don't change during program execution. By convention, we write them in all capitals.

**Why constants matter:**
1. They make numbers meaningful: `SALES_TAX = 0.07` is clearer than just using `0.07`
2. You only change them in one place if the value updates
3. They improve code readability
4. They're easier to find and understand

**Best practices for naming:**
- Use descriptive names: `score` not `s`, `employee_salary` not `es`
- Use lowercase for variables: `temperature`, `user_input`
- Use UPPER_CASE for constants: `FREEZING_POINT = 32`, `SPEED_OF_LIGHT = 299792458`
- Avoid single-letter variables except in loops (even then, descriptive is better)
- Don't use reserved words: `for`, `if`, `while`, `print` (these are keywords)

### Code Examples

```python
# Bad naming
a = 10
b = 5
c = a + b  # What do a, b, c represent?

# Good naming
width = 10
height = 5
area = width * height  # Clear what we're calculating

# Using constants
SALES_TAX_RATE = 0.08
DISCOUNT_PERCENT = 0.15

item_price = float(input("Item price: $"))
tax = item_price * SALES_TAX_RATE
discount = item_price * DISCOUNT_PERCENT
final_price = item_price - discount + tax

# Multiple constants for calculation
CELSIUS_TO_FAHRENHEIT_FACTOR = 9/5
CELSIUS_TO_FAHRENHEIT_OFFSET = 32

celsius = float(input("Temperature (°C): "))
fahrenheit = celsius * CELSIUS_TO_FAHRENHEIT_FACTOR + CELSIUS_TO_FAHRENHEIT_OFFSET
print(f"{celsius}°C = {fahrenheit:.1f}°F")

# Constants in practical use
MAX_LOGIN_ATTEMPTS = 3
MINIMUM_PASSWORD_LENGTH = 8
AVERAGE_NAME_LENGTH = 10

user_name = input("Enter username: ")
if len(user_name) < MINIMUM_PASSWORD_LENGTH:
    print("Name too short!")

# Good variable naming in calculations
employee_first_name = "Alice"
employee_last_name = "Johnson"
employee_hourly_rate = 25.50
hours_worked_this_week = 40

gross_pay = employee_hourly_rate * hours_worked_this_week
print(f"{employee_first_name} {employee_last_name}: ${gross_pay:.2f}")
```

### Guided Practice

1. Rewrite a previous program using proper naming conventions.
2. Identify any unclear variable names and improve them.
3. Add constants for any "magic numbers" (like tax rates, discount rates).
4. Compare the readability before and after.

### Practice Problems

**Problem 1 — Beginner:**
Rewrite this program with proper naming and constants:

```python
# Before
a = 100
b = 1.07
c = a * b
print(c)

# Starter code - rewrite this:
SALES_TAX_RATE =

```

**Problem 2 — Intermediate:**
Write a program for calculating tip with good naming:
- Ask for bill amount, tip percentage, and party size
- Use constants for tip percentages if relevant
- Calculate per-person tip
- Display with descriptive variable names

**Problem 3 — Challenge:**
Write a program that uses at least 5 constants and 10 variables with clear, descriptive names. Calculate something complex (grade calculation, payroll with deductions, etc.)

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `original_price`, `tax_rate`, and `total_price` instead of `a`, `b`, `c`.
- Problem 2: Use `bill_total`, `tip_percentage`, `party_size`, `tip_per_person`.
- Problem 3: Define constants at the top, use descriptive snake_case for variables.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
SALES_TAX_RATE = 0.07
original_price = 100
total_with_tax = original_price * (1 + SALES_TAX_RATE)
print(f"${original_with_tax:.2f}")

# Problem 2 Example
bill_total = float(input("Bill amount: $"))
tip_percentage = float(input("Tip percentage: "))
party_size = int(input("Number of people: "))

tip_amount = bill_total * (tip_percentage / 100)
tip_per_person = tip_amount / party_size

print(f"Total tip: ${tip_amount:.2f}")
print(f"Tip per person: ${tip_per_person:.2f}")

# Problem 3 Example
FEDERAL_TAX_RATE = 0.15
STATE_TAX_RATE = 0.05
SOCIAL_SECURITY_RATE = 0.062
OVERTIME_MULTIPLIER = 1.5
STANDARD_WORK_HOURS = 40

employee_name = "John"
hourly_wage = 25.50
hours_worked = 45

if hours_worked > STANDARD_WORK_HOURS:
    regular_hours_pay = STANDARD_WORK_HOURS * hourly_wage
    overtime_hours = hours_worked - STANDARD_WORK_HOURS
    overtime_pay = overtime_hours * hourly_wage * OVERTIME_MULTIPLIER
    gross_pay = regular_hours_pay + overtime_pay
else:
    gross_pay = hours_worked * hourly_wage

federal_taxes = gross_pay * FEDERAL_TAX_RATE
state_taxes = gross_pay * STATE_TAX_RATE
social_security = gross_pay * SOCIAL_SECURITY_RATE
net_pay = gross_pay - federal_taxes - state_taxes - social_security

print(f"Employee: {employee_name}")
print(f"Gross: ${gross_pay:.2f}")
print(f"Net: ${net_pay:.2f}")
```

</details>

---
