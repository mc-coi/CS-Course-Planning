# Day 16: The 5-Step Software Development Process
**Learning Target:** I can apply the 5-step software development process to plan and code programs.

### Key Concepts
Professional programmers don't just sit down and start typing. They follow a systematic process:

**Step 1: Define (Ask)**
- Understand the problem completely
- What are the inputs?
- What should the output be?
- Are there any constraints?
- Example: "Calculate the area of a rectangle. Input: length and width. Output: area."

**Step 2: Plan (Design)**
- Break down the solution into steps
- Write pseudocode (English-like instructions, not code)
- Draw flowcharts if helpful
- Think about edge cases
- Plan variable names and calculations

**Step 3: Code**
- Translate your plan into Python
- Write clean, readable code
- Use descriptive variable names
- Include helpful comments

**Step 4: Test**
- Run your program with different inputs
- Test normal cases, edge cases (very small, very large, zero, negative)
- Check that output is correct
- Look for any errors

**Step 5: Refine (Debug & Improve)**
- Fix any bugs found during testing
- Make code cleaner or more efficient
- Improve output formatting
- Add comments if needed

### Code Examples
```python
# Example: Temperature Converter following 5-step process

# Step 1: Define
# Input: temperature in Fahrenheit
# Output: temperature in Celsius
# Formula: C = (F - 32) × 5/9

# Step 2: Plan (pseudocode):
# a) Ask user for Fahrenheit temperature
# b) Convert using formula
# c) Round to 1 decimal place
# d) Display result with units

# Step 3: Code
fahrenheit = float(input("Enter temperature (°F): "))
celsius = (fahrenheit - 32) * 5 / 9
celsius_rounded = round(celsius, 1)
print(f"{fahrenheit}°F = {celsius_rounded}°C")

# Step 4: Test
# Test cases:
# - 32°F should be 0°C ✓
# - 212°F should be 100°C ✓
# - 68°F should be 20°C ✓

# Step 5: Refine
# Code looks good, clear variable names, good comments
```

### Guided Practice
Follow the 5-step process to create a BMI calculator:
1. **Define:** BMI = weight(lbs) / height(in)² × 703
2. **Plan:** Write pseudocode
3. **Code:** Write the Python program
4. **Test:** Try several inputs (healthy range, underweight, obese)
5. **Refine:** Make sure output is clear and helpful

### Practice Problems

**Problem 1 — Beginner:** Follow the 5-step process to create a celsius-to-fahrenheit converter. F = C × 9/5 + 32

**Problem 2 — Intermediate:** Follow the 5-step process to create a simple savings calculator. Ask for starting balance, monthly savings, and months. Calculate total.

**Problem 3 — Challenge:** Follow the 5-step process to create a percentage grade calculator. Ask for points earned and points possible. Calculate percentage and assign a letter grade (90+=A, 80+=B, 70+=C, etc.)

<details>
<summary>💡 Hints</summary>

- Problem 1: Write your define and plan steps first!
- Problem 2: Test with edge cases like 0 months
- Problem 3: Use if statements (you'll learn soon!) or note this for later
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
# Step 1 - Define: Convert C to F using F = C × 9/5 + 32
# Step 2 - Plan: Ask for C, apply formula, display F
# Step 3 - Code:
celsius = float(input("Celsius: "))
fahrenheit = celsius * 9/5 + 32
print(f"{celsius}°C = {fahrenheit:.1f}°F")
# Step 4 - Test: 0°C = 32°F ✓
# Step 5 - Refine: Code is clear and correct

# Problem 2 Example
# Step 1 - Define: Calculate total savings
# Step 2 - Plan: Get inputs, multiply monthly by count, add to principal
principal = float(input("Starting balance: $"))
monthly = float(input("Monthly savings: $"))
months = int(input("Months: "))
total = principal + (monthly * months)
print(f"Total after {months} months: ${total:.2f}")
```

</details>

---
