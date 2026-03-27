# Day 14: F-Strings — Professional Output Formatting
**Learning Target:** I can format output using f-strings for professional-looking results.

### Key Concepts
**F-strings** (formatted string literals) are a powerful way to embed variables and expressions inside strings. They start with `f"..."` or `f'...'`.

**Basic syntax:** `f"text {variable} more text"`

**Formatting options:**
- `:d` = integer (no decimals)
- `:f` = float with decimals (default is 6)
- `:.2f` = float with exactly 2 decimal places
- `:>10` = right-align in 10 characters
- `:<10` = left-align in 10 characters
- `:^10` = center in 10 characters

**Examples:**
```python
name = "Alex"
age = 17
gpa = 3.85

# Basic f-string
print(f"Name: {name}, Age: {age}")

# Formatting decimals
print(f"GPA: {gpa:.2f}")  # 3.85

# Expressions inside f-strings
print(f"Next year I'll be {age + 1}")

# Alignment
print(f"{name:>10}")  # Right-aligned in 10 spaces
```

**F-strings vs string concatenation:**
- Old way: `"Total: $" + str(total)`
- F-string way: `f"Total: ${total:.2f}"`

F-strings are more readable and flexible!

### Code Examples
```python
# Money formatting
price = 19.5
print(f"Price: ${price:.2f}")  # $19.50

# Table with alignment
print(f"{'Item':<15} {'Price':>10}")
print(f"{'Bread':<15} {'$3.50':>10}")
print(f"{'Milk':<15} {'$2.25':>10}")

# Mixing text and variables
name = "Jordan"
score = 95.7
print(f"{name} scored {score:.1f}%")

# Using expressions inside
hours = 8
rate = 15.50
total_pay = hours * rate
print(f"Pay: {hours} hours × ${rate:.2f}/hr = ${total_pay:.2f}")

# Multiple formats
gpa = 3.857
print(f"GPA: {gpa:.2f}")  # 3.86 (rounded)
```

### Guided Practice
Create a program that:
1. Asks for product name, quantity, and unit price
2. Calculates total
3. Displays a formatted receipt with aligned columns
4. Shows all prices with exactly 2 decimal places

Example output:
```
===== RECEIPT =====
Item              Qty    Unit Price    Total
Bread              2      $3.50       $7.00
Milk               1      $2.25       $2.25
===== TOTAL: $9.25 =====
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that displays student info formatted nicely using f-strings.

**Problem 2 — Intermediate:** Create a formatted table showing 3 products with prices. Use alignment and decimal formatting.

**Problem 3 — Challenge:** Create a program that calculates and displays a formatted invoice with items, quantities, prices, subtotal, tax, and total.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use {variable:.2f} for numbers with decimals
- Problem 2: Use {text:>15} to right-align in a column
- Problem 3: Include line breaks and borders for a professional look
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = "Alex Johnson"
gpa = 3.85
age = 16
print(f"Student: {name}")
print(f"GPA: {gpa:.2f}")
print(f"Age: {age}")

# Problem 2 Example
print(f"{'Item':<15} {'Price':>10}")
print("-" * 25)
print(f"{'Apples':<15} {'$2.99':>10}")
print(f"{'Bananas':<15} {'$1.50':>10}")
print(f"{'Oranges':<15} {'$3.25':>10}")

# Problem 3 Example (simplified)
item = "Notebook"
qty = 3
price_each = 5.99
total = qty * price_each
tax = total * 0.08
final = total + tax
print("=== INVOICE ===")
print(f"{item} × {qty} @ ${price_each:.2f} = ${total:.2f}")
print(f"Tax (8%): ${tax:.2f}")
print(f"Total: ${final:.2f}")
```

</details>

---
