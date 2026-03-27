# Day 5: Problem Solving with Python
**Learning Target:** I can apply the 5-step software development process.

### Key Concepts
The **5-Step Software Development Process** helps you solve problems systematically:

1. **Define:** Understand what the problem is asking. What are inputs? What should the output be?
2. **Plan:** Break down the solution into steps. Write pseudocode (instructions in English, not Python).
3. **Code:** Translate your plan into Python. Write the code.
4. **Test:** Run your program with different inputs, including edge cases (very small, very large, zero, negative).
5. **Refine:** Fix any bugs or improve the code. Make it cleaner, more efficient, or easier to read.

Use the `round()` function to format decimal output: `round(3.14159, 2)` returns `3.14`.

### Code Examples
```python
# Temperature converter — Fahrenheit to Celsius
# Step 1 - Define: Input temp in °F, output in °C using formula C = (F - 32) × 5/9
# Step 2 - Plan:
#   a) Ask user for temperature in Fahrenheit
#   b) Apply conversion formula
#   c) Round to 2 decimal places
#   d) Print result in nice format

fahrenheit = float(input("Enter temperature (°F): "))
celsius = (fahrenheit - 32) * 5 / 9
celsius_rounded = round(celsius, 2)
print(f"{fahrenheit}°F = {celsius_rounded}°C")

# BMI Calculator
# BMI = weight (lbs) / (height (in))² × 703

weight = float(input("Enter weight in pounds: "))
height = float(input("Enter height in inches: "))
bmi = (weight / (height ** 2)) * 703
print(f"Your BMI is {round(bmi, 1)}")

# Paycheck calculator with tax
hours = float(input("Hours worked: "))
hourly_rate = float(input("Hourly rate: $"))
gross_pay = hours * hourly_rate
tax = gross_pay * 0.15  # 15% tax
net_pay = gross_pay - tax
print(f"Gross: ${gross_pay:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Net: ${net_pay:.2f}")
```

### Guided Practice
Follow the 5-step process to create a simple BMI calculator:
1. Define: What are inputs? What's the output?
2. Plan: Write the steps in English
3. Code: Write the Python program
4. Test: Try it with different heights and weights
5. Refine: Make the output cleaner or add a message about the BMI

### Practice Problems
**Problem 1 — Beginner:** Write a program using the 5-step process that converts a temperature from Celsius to Fahrenheit. (Formula: F = C × 9/5 + 32)

```python
# Step 1 - Define: ...
# Step 2 - Plan: ...
# Step 3 - Code:
celsius = float(input("Enter Celsius: "))

# Step 4 - Test: (write comments about test cases)
# Step 5 - Refine: (improve output)
```

**Problem 2 — Intermediate:** Create a savings calculator that asks for principal amount, monthly savings, and number of months, then prints total savings.

**Problem 3 — Challenge:** Create a currency converter. Ask for USD, then convert to EUR, JPY, and GBP using current approximate rates (you choose rates). Use proper formatting.

<details>
<summary>💡 Hints</summary>

- Problem 1: Work through the formula step-by-step with a calculator first
- Problem 2: Total = principal + (monthly_savings × months)
- Problem 3: Store exchange rates in variables for easy updating
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
celsius = float(input("Enter temperature (°C): "))
fahrenheit = celsius * 9/5 + 32
print(f"{celsius}°C = {round(fahrenheit, 2)}°F")

# Problem 2 Example
principal = float(input("Principal: $"))
monthly = float(input("Monthly savings: $"))
months = int(input("Number of months: "))
total = principal + (monthly * months)
print(f"Total savings: ${total:.2f}")
```
</details>

---