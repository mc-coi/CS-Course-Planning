# Day 30: Practice Lab — Geometry Calculator & Unit Converter

**Learning Target:** I can apply type conversion, the math module, and compound expressions to build practical calculator programs.

### Key Concepts

This lab integrates everything from Days 26–29:
- Type conversion with `int()`, `float()`, `str()`
- Boolean comparisons for validation
- Compound expressions with correct operator precedence
- Math module functions and constants
- F-string formatting with decimal places
- Building complete, user-friendly programs

### Code Examples

```python
# Example 1: Circle Calculator
import math

radius = float(input("Enter radius: "))
area = math.pi * radius ** 2
circumference = 2 * math.pi * radius
print(f"Area: {area:.2f} sq units")
print(f"Circumference: {circumference:.2f} units")

# Example 2: Simple Unit Converter (miles to kilometers)
miles = float(input("Miles: "))
kilometers = miles * 1.60934
print(f"{miles} miles = {kilometers:.2f} km")

# Example 3: Temperature Converter
celsius = float(input("Celsius: "))
fahrenheit = (celsius * 9/5) + 32
print(f"{celsius}°C = {fahrenheit:.2f}°F")
```

### Guided Practice: Build a Geometry Calculator

Create a program that:
1. Asks the user what shape they want to calculate (circle, rectangle, triangle)
2. For each shape:
   - **Circle:** Ask for radius, calculate area and circumference
   - **Rectangle:** Ask for length and width, calculate area and perimeter
   - **Triangle:** Ask for base and height, calculate area
3. Display all results with 2 decimal places using f-strings

### Practice Problems

**Problem 1 — Beginner: Circle Calculator**
Write a program that:
- Asks for a circle's radius
- Calculates area and circumference
- Displays with 2 decimal places

```python
import math

radius = float(input("Radius: "))

# Your calculations here

print(f"Area: {area:.2f}")
print(f"Circumference: {circumference:.2f}")
```

**Problem 2 — Intermediate: Unit Converter**
Write a program that:
- Asks the user for a temperature in Celsius
- Converts to Fahrenheit: F = (C × 9/5) + 32
- Asks the user for a distance in meters
- Converts to feet: feet = meters × 3.28084
- Displays both conversions with appropriate precision

**Problem 3 — Challenge: BMI & Body Type Calculator**
Write a program that:
- Asks for weight (in pounds) and height (in inches)
- Converts weight to kilograms: kg = lbs ÷ 2.20462
- Converts height to meters: m = inches ÷ 39.3701
- Calculates BMI: BMI = kg ÷ (m²)
- Prints the BMI with 1 decimal place
- Categorizes based on BMI:
  - BMI < 18.5: "Underweight"
  - 18.5 ≤ BMI < 25: "Normal weight"
  - 25 ≤ BMI < 30: "Overweight"
  - BMI ≥ 30: "Obese"

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `math.pi`, formulas are area = π*r², circumference = 2*π*r.
- Problem 2: Celsius to Fahrenheit is F = (C*9/5)+32. Meters to feet is feet = m*3.28084.
- Problem 3: Convert units first, then use comparisons (>, <, >=, etc.) to categorize BMI.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
import math
radius = float(input("Radius: "))
area = math.pi * radius ** 2
circumference = 2 * math.pi * radius
print(f"Area: {area:.2f}")
print(f"Circumference: {circumference:.2f}")

# Problem 2 Example
celsius = float(input("Temperature (°C): "))
fahrenheit = (celsius * 9/5) + 32

meters = float(input("Distance (m): "))
feet = meters * 3.28084

print(f"{celsius}°C = {fahrenheit:.1f}°F")
print(f"{meters}m = {feet:.2f} ft")

# Problem 3 Example
import math

weight_lbs = float(input("Weight (lbs): "))
height_in = float(input("Height (in): "))

weight_kg = weight_lbs / 2.20462
height_m = height_in / 39.3701

bmi = weight_kg / (height_m ** 2)
print(f"BMI: {bmi:.1f}")

if bmi < 18.5:
    category = "Underweight"
elif bmi < 25:
    category = "Normal weight"
elif bmi < 30:
    category = "Overweight"
else:
    category = "Obese"

print(f"Category: {category}")
```

</details>

---

## Lab Reflection

Take 5 minutes to answer:
1. Which math function was most useful in your calculator?
2. What was the most difficult part of the conversion formula?
3. How could you extend this program to handle more shapes or units?
4. Why is it important to display money and measurements with the right decimal places?
