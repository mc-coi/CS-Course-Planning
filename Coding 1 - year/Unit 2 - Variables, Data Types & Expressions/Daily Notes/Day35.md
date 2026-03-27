# Day 35: Practice Lab — Payroll Calculator & BMI Calculator

**Learning Target:** I can build complete, professional programs combining all Unit 2 concepts to solve real-world problems.

### Key Concepts

This lab integrates Days 31–34 and represents the pinnacle of Week 7 work:
- Complex multi-step calculations
- Professional output formatting
- Type conversion and error handling (basic)
- Augmented assignment operators
- F-string formatting with alignment and decimals
- Building programs that real people could use

### Code Examples

```python
# Example 1: Simple payroll
hours = float(input("Hours worked: "))
hourly_rate = float(input("Hourly rate: $"))
gross = hours * hourly_rate
taxes = gross * 0.15
net = gross - taxes
print(f"Gross: ${gross:.2f}")
print(f"Taxes (15%): ${taxes:.2f}")
print(f"Net pay: ${net:.2f}")

# Example 2: BMI calculation
import math
weight_lbs = float(input("Weight (lbs): "))
height_in = float(input("Height (in): "))
weight_kg = weight_lbs / 2.20462
height_m = height_in / 39.3701
bmi = weight_kg / (height_m ** 2)
print(f"BMI: {bmi:.1f}")
```

### Guided Practice: Build a Payroll System

Create a program that:
1. Asks for employee name, hourly rate, and hours worked
2. Calculates gross pay (rate × hours)
3. Calculates federal tax (15% of gross)
4. Calculates state tax (5% of gross)
5. Calculates net pay (gross - all taxes)
6. Displays a formatted paycheck

### Practice Problems

**Problem 1 — Beginner: Hourly Paycheck**
Write a program that:
- Asks for hourly rate and hours worked
- Calculates gross pay
- Calculates 12% tax
- Calculates net pay
- Displays formatted results

```python
hourly_rate = float(input("Hourly rate: $"))
hours = float(input("Hours worked: "))

gross =
tax =
net =

print(f"Gross: ${gross:.2f}")
print(f"Tax (12%): ${tax:.2f}")
print(f"Net: ${net:.2f}")
```

**Problem 2 — Intermediate: Complete Payroll**
Write a program that:
- Asks for name, hourly rate, hours worked
- Calculates gross pay (with overtime: 1.5× rate for hours > 40)
- Calculates federal tax (15%) and state tax (5%)
- Calculates social security (6.2%)
- Displays a detailed paycheck with:
  - Employee name
  - Hours and rate
  - Gross pay
  - Each deduction
  - Net pay

**Problem 3 — Challenge: BMI Health Assessment**
Write a program that:
- Asks for name, weight (lbs), height (inches)
- Converts to metric
- Calculates BMI
- Categorizes based on BMI:
  - < 18.5: "Underweight"
  - 18.5-24.9: "Normal weight"
  - 25-29.9: "Overweight"
  - ≥ 30: "Obese"
- Displays a health report with measurements and category

<details>
<summary>💡 Hints</summary>

- Problem 1: gross = rate * hours, tax = gross * 0.12, net = gross - tax.
- Problem 2: Check if hours > 40, then use time-and-a-half for overtime. Multiple deductions: fed = gross*0.15, etc.
- Problem 3: Convert with rate factors (1 lb ≈ 0.453592 kg, 1 in ≈ 0.0254 m). Use if/elif for BMI categories.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
hourly_rate = float(input("Hourly rate: $"))
hours = float(input("Hours worked: "))
gross = hourly_rate * hours
tax = gross * 0.12
net = gross - tax
print(f"Gross: ${gross:.2f}")
print(f"Tax (12%): ${tax:.2f}")
print(f"Net: ${net:.2f}")

# Problem 2 Example
name = input("Employee name: ")
hourly_rate = float(input("Hourly rate: $"))
hours = float(input("Hours worked: "))

if hours > 40:
    regular = 40 * hourly_rate
    overtime = (hours - 40) * hourly_rate * 1.5
    gross = regular + overtime
else:
    gross = hours * hourly_rate

fed_tax = gross * 0.15
state_tax = gross * 0.05
social_sec = gross * 0.062

net = gross - fed_tax - state_tax - social_sec

print(f"\n--- PAYCHECK ---")
print(f"Name: {name}")
print(f"Hours: {hours:.1f} @ ${hourly_rate:.2f}/hr")
print(f"Gross: ${gross:.2f}")
print(f"Federal Tax: ${fed_tax:.2f}")
print(f"State Tax: ${state_tax:.2f}")
print(f"Social Security: ${social_sec:.2f}")
print(f"Net Pay: ${net:.2f}")

# Problem 3 Example
import math
name = input("Name: ")
weight_lbs = float(input("Weight (lbs): "))
height_in = float(input("Height (in): "))

weight_kg = weight_lbs * 0.453592
height_m = height_in * 0.0254

bmi = weight_kg / (height_m ** 2)

if bmi < 18.5:
    category = "Underweight"
elif bmi < 25:
    category = "Normal weight"
elif bmi < 30:
    category = "Overweight"
else:
    category = "Obese"

print(f"\n--- HEALTH REPORT ---")
print(f"Name: {name}")
print(f"Weight: {weight_kg:.1f} kg")
print(f"Height: {height_m:.2f} m")
print(f"BMI: {bmi:.1f}")
print(f"Category: {category}")
```

</details>

---

## Lab Reflection

Take 5 minutes to answer:
1. What was the most challenging calculation in your program?
2. How did you verify your calculations were correct?
3. What would you add to make these programs more useful?
4. How could you improve the formatting of the output?
