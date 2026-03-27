# Day 34: Building Multi-Step Calculations — Tax Calculators, Grade Averagers

**Learning Target:** I can build complete programs that perform complex, multi-step calculations and display results professionally.

### Key Concepts

This lesson combines everything learned so far to build programs that:
1. Accept user input
2. Perform multiple calculation steps
3. Use type conversion and compound expressions
4. Format output professionally with f-strings
5. Apply real-world logic

**Key patterns:**
- Read input → convert to correct type → store in variables
- Perform calculations step by step
- Use intermediate variables to store results
- Display formatted output

### Code Examples

```python
# Example 1: Sales tax calculator
price = float(input("Item price: $"))
tax_rate = 0.08  # 8%
tax = price * tax_rate
total = price + tax
print(f"Price: ${price:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Total: ${total:.2f}")

# Example 2: Grade average calculator
score1 = float(input("Score 1: "))
score2 = float(input("Score 2: "))
score3 = float(input("Score 3: "))
average = (score1 + score2 + score3) / 3
print(f"Scores: {score1:.1f}, {score2:.1f}, {score3:.1f}")
print(f"Average: {average:.1f}")

# Example 3: Discount calculator
original_price = float(input("Original price: $"))
discount_percent = float(input("Discount percent: "))
discount_amount = original_price * (discount_percent / 100)
final_price = original_price - discount_amount
savings = discount_amount
print(f"Original: ${original_price:.2f}")
print(f"Discount ({discount_percent}%): ${discount_amount:.2f}")
print(f"You save: ${savings:.2f}")
print(f"Final price: ${final_price:.2f}")
```

### Guided Practice

Build a **Meal Cost Splitter**:
1. Ask for the meal subtotal
2. Ask for the tip percentage
3. Calculate the tip amount
4. Calculate the total (subtotal + tip)
5. Ask how many people to split between
6. Calculate cost per person
7. Display formatted breakdown

### Practice Problems

**Problem 1 — Beginner: Sales Tax Calculator**
Write a program that:
- Asks for item price
- Calculates 7% sales tax
- Displays price, tax, and total (formatted to 2 decimals)

```python
price = float(input("Price: $"))

tax =
total =

print(f"Price: ${price:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Total: ${total:.2f}")
```

**Problem 2 — Intermediate: Course Grade Calculator**
Write a program that:
- Asks for four test scores
- Calculates the average
- Asks for homework points (0-100)
- Calculates final grade: 80% of test average + 20% of homework
- Displays formatted results

**Problem 3 — Challenge: Commission Calculator**
Write a program that:
- Asks for annual sales amount
- Applies tiered commission:
  - Sales < $50,000: 2%
  - Sales $50,000-$100,000: 3%
  - Sales > $100,000: 4%
- Displays the sales amount, commission rate, commission earned, and income after commission
- Formats all currency to 2 decimals

<details>
<summary>💡 Hints</summary>

- Problem 1: tax = price * 0.07, total = price + tax.
- Problem 2: test_avg = (s1+s2+s3+s4)/4, final = test_avg*0.8 + homework*0.2.
- Problem 3: Use if/elif to check sales amounts and set commission rate, then commission = sales * rate.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
price = float(input("Price: $"))
tax = price * 0.07
total = price + tax
print(f"Price: ${price:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Total: ${total:.2f}")

# Problem 2 Example
s1 = float(input("Test 1: "))
s2 = float(input("Test 2: "))
s3 = float(input("Test 3: "))
s4 = float(input("Test 4: "))
homework = float(input("Homework (0-100): "))
test_avg = (s1 + s2 + s3 + s4) / 4
final = test_avg * 0.8 + homework * 0.2
print(f"Test average: {test_avg:.1f}")
print(f"Final grade: {final:.1f}")

# Problem 3 Example
sales = float(input("Annual sales: $"))
if sales < 50000:
    rate = 0.02
elif sales < 100000:
    rate = 0.03
else:
    rate = 0.04
commission = sales * rate
income = sales + commission
print(f"Sales: ${sales:,.2f}")
print(f"Commission rate: {rate:.0%}")
print(f"Commission: ${commission:,.2f}")
print(f"Income: ${income:,.2f}")
```

</details>

---
