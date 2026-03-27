# Day 38: Working with Money — Rounding, Formatting Currency

**Learning Target:** I can handle monetary calculations accurately with proper rounding and professional formatting.

### Key Concepts

**Money and floating-point precision:** Computers can't represent decimals perfectly. This can cause issues when working with money. For example, `0.1 + 0.2` doesn't equal exactly `0.3` in a computer.

**Rounding for money:** Always round monetary amounts to 2 decimal places using `round(value, 2)`.

**Professional currency formatting:** Use f-strings to display currency with:
- A dollar sign: `$`
- Exactly 2 decimal places: `:.2f`
- Thousands separator (optional but professional): `,`

**Currency calculations pattern:**
1. Do all calculations with full precision
2. Round final results to 2 decimals
3. Display with professional formatting

**Sales tax and discounts:**
- Sales tax: `new_total = original + (original * tax_rate)`
- Discount: `new_total = original - (original * discount_rate)`
- Both: `new_total = original * (1 + tax_rate) - discount`

### Code Examples

```python
# Rounding for currency
price = 9.567
rounded = round(price, 2)  # 9.57
print(f"${rounded:.2f}")  # $9.57

# Basic formatting
amount = 1234.5
print(f"${amount:.2f}")  # $1234.50

# With thousands separator
amount = 123456.78
print(f"${amount:,.2f}")  # $123,456.78

# Sales tax calculation
price = 99.99
tax_rate = 0.08
tax = price * tax_rate
total = price + tax
total = round(total, 2)
print(f"Price: ${price:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Total: ${total:.2f}")

# Discount calculation
original = 50.00
discount_rate = 0.20
discount_amount = original * discount_rate
final_price = original - discount_amount
final_price = round(final_price, 2)
print(f"Original: ${original:.2f}")
print(f"Discount (20%): ${discount_amount:.2f}")
print(f"Final: ${final_price:.2f}")

# Receipt with multiple items
item1_price = 9.99
item2_price = 24.50
item3_price = 5.01

subtotal = item1_price + item2_price + item3_price
tax = subtotal * 0.07
total = subtotal + tax
total = round(total, 2)

print(f"Subtotal: ${subtotal:.2f}")
print(f"Tax (7%): ${tax:.2f}")
print(f"Total: ${total:.2f}")

# Tip calculation
bill = 45.32
tip_percent = 18
tip = bill * (tip_percent / 100)
tip = round(tip, 2)
total_with_tip = bill + tip
total_with_tip = round(total_with_tip, 2)
print(f"Bill: ${bill:.2f}")
print(f"Tip ({tip_percent}%): ${tip:.2f}")
print(f"Total: ${total_with_tip:.2f}")
```

### Guided Practice

1. Create a receipt for 3 items with prices
2. Calculate subtotal
3. Calculate 8% sales tax
4. Display formatted with proper currency formatting
5. Calculate a tip (18%) and display total with tip

### Practice Problems

**Problem 1 — Beginner:**
Format these amounts as currency with 2 decimals and thousands separator:
- 9.5
- 100.1
- 1234.56
- 0.99

```python
amounts = [9.5, 100.1, 1234.56, 0.99]

for amount in amounts:
    print(f"${amount:,.2f}")
```

**Problem 2 — Intermediate:**
Create a shopping cart:
- Ask for 3 item prices
- Calculate subtotal
- Ask for tax rate percentage
- Calculate total with tax
- Round properly
- Display formatted receipt

**Problem 3 — Challenge:**
Create a **restaurant bill calculator**:
- Ask for meal subtotal
- Ask for tax rate (often shown as % like 7%)
- Calculate tax
- Ask for tip percentage
- Calculate tip on subtotal (not including tax)
- Display itemized: subtotal, tax, tip, total
- Calculate cost per person (ask how many people)
- All formatted with $ and 2 decimals

<details>
<summary>💡 Hints</summary>

- Problem 1: Use f-string formatting: `f"${amount:,.2f}"`.
- Problem 2: tax = subtotal * (tax_rate/100), total = subtotal + tax, then round final total.
- Problem 3: Tip is calculated on subtotal only. Use multiple variables for clarity.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
amounts = [9.5, 100.1, 1234.56, 0.99]
for amount in amounts:
    print(f"${amount:,.2f}")

# Problem 2 Example
price1 = float(input("Item 1: $"))
price2 = float(input("Item 2: $"))
price3 = float(input("Item 3: $"))

subtotal = price1 + price2 + price3
tax_rate = float(input("Tax rate (%): "))
tax = subtotal * (tax_rate / 100)
total = subtotal + tax
total = round(total, 2)

print(f"\nSubtotal: ${subtotal:.2f}")
print(f"Tax ({tax_rate}%): ${tax:.2f}")
print(f"Total: ${total:.2f}")

# Problem 3 Example
subtotal = float(input("Meal subtotal: $"))
tax_rate = float(input("Tax rate (%): "))
tax = subtotal * (tax_rate / 100)

tip_rate = float(input("Tip (%): "))
tip = subtotal * (tip_rate / 100)

total = subtotal + tax + tip
total = round(total, 2)

num_people = int(input("Number of people: "))
per_person = total / num_people

print(f"\nSubtotal: ${subtotal:.2f}")
print(f"Tax ({tax_rate}%): ${tax:.2f}")
print(f"Tip ({tip_rate}%): ${tip:.2f}")
print(f"Total: ${total:.2f}")
print(f"Per person: ${per_person:.2f}")
```

</details>

---
