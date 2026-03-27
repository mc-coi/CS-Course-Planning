# Day 13: Math with Variables — Building Calculator Programs
**Learning Target:** I can build calculator-style programs with variables and arithmetic.

### Key Concepts
Now you can combine what you've learned:
- User input collection with `input()`
- Type conversion using `int()` and `float()`
- Variables and reassignment
- All seven arithmetic operators
- Order of operations with proper parentheses
- Output formatting with f-strings

**Steps for building calculation programs:**
1. Ask the user for necessary values using `input()`
2. Convert to appropriate types (int or float)
3. Store in well-named variables
4. Perform calculations with proper order of operations
5. Display results clearly with labels and formatting

**Best practices:**
- Use descriptive variable names (not x, y, z)
- Add comments explaining complex calculations
- Format output with proper decimal places using f-strings
- Show calculation steps or intermediate results when helpful
- Include units (dollars, meters, seconds, etc.) in output

### Code Examples
```python
# Example 1: Tip Calculator
bill = float(input("Bill amount: $"))
tip_percent = float(input("Tip percentage: "))
tip = bill * (tip_percent / 100)
total = bill + tip
print(f"Tip: ${tip:.2f}")
print(f"Total: ${total:.2f}")

# Example 2: Area and Perimeter
length = float(input("Rectangle length: "))
width = float(input("Rectangle width: "))
area = length * width
perimeter = 2 * (length + width)
print(f"Area: {area:.2f} sq units")
print(f"Perimeter: {perimeter:.2f} units")

# Example 3: Average grade calculator
grade1 = int(input("Grade 1: "))
grade2 = int(input("Grade 2: "))
grade3 = int(input("Grade 3: "))
average = (grade1 + grade2 + grade3) / 3
print(f"Average: {average:.2f}")
```

### Guided Practice
Create a calculator program for one of these:
- **Loan Payment Calculator:** Ask for loan amount, interest rate, and years. Calculate monthly payment (formula: M = P[r(1+r)^n]/[(1+r)^n-1])
- **Gas Mileage Calculator:** Ask for miles driven and gallons used. Calculate MPG.
- **Age Calculator:** Ask for birth year. Calculate age and years until 100.

### Practice Problems

**Problem 1 — Beginner:** Create a program that converts US dollars to euros. Ask for dollar amount and exchange rate, then display euros.

**Problem 2 — Intermediate:** Create a program that calculates the total cost of items with tax. Ask for item price and tax rate, then calculate and display total.

**Problem 3 — Challenge:** Create a program that calculates paycheck details. Ask for hours worked, hourly rate, and tax percentage. Calculate gross pay, tax amount, and net pay.

<details>
<summary>💡 Hints</summary>

- Problem 1: Multiply dollars by exchange rate
- Problem 2: Remember order of operations; tax = price × tax_rate
- Problem 3: Show all three calculations (gross, tax, net)
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
dollars = float(input("Dollars: $"))
rate = float(input("Exchange rate (1 USD = ? EUR): "))
euros = dollars * rate
print(f"${dollars:.2f} USD = €{euros:.2f} EUR")

# Problem 2 Example
price = float(input("Item price: $"))
tax_rate = float(input("Tax rate (as decimal): "))
tax = price * tax_rate
total = price + tax
print(f"Price: ${price:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Total: ${total:.2f}")

# Problem 3 Example
hours = float(input("Hours worked: "))
rate = float(input("Hourly rate: $"))
tax_percent = float(input("Tax percentage: "))
gross = hours * rate
tax = gross * (tax_percent / 100)
net = gross - tax
print(f"Gross: ${gross:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Net: ${net:.2f}")
```

</details>

---
