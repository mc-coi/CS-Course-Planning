# Day 32: String Formatting — F-Strings in Depth, Alignment, Decimal Places

**Learning Target:** I can use f-strings to format strings professionally with alignment, padding, and decimal precision.

### Key Concepts

**F-strings** (formatted string literals) allow you to embed variables and expressions directly into strings using `f"..."` syntax. They were introduced in Python 3.6 and are the modern way to format strings.

**Basic f-string:** `f"Hello, {name}"` embeds the variable `name` into the string.

**Decimal places:** `f"{value:.2f}"` formats a float with exactly 2 decimal places.
- `.1f` → 1 decimal place
- `.2f` → 2 decimal places
- `.3f` → 3 decimal places

**Alignment and width:**
- `f"{value:10}"` → Right-align in 10 characters
- `f"{value:<10}"` → Left-align in 10 characters
- `f"{value:^10}"` → Center in 10 characters
- `f"{value:>10}"` → Right-align explicitly

**Common formatting patterns:**
- Currency: `f"${amount:.2f}"` → `$9.99`
- Percentage: `f"{percent:.1%}"` → `95.5%`
- Expressions: `f"Total: {5 + 3}"` → `"Total: 8"`
- Expressions with formatting: `f"Average: {(a+b)/2:.1f}"`

### Code Examples

```python
# Basic f-strings
name = "Alice"
age = 25
print(f"Name: {name}, Age: {age}")  # Name: Alice, Age: 25

# Decimal places
price = 9.5
print(f"Price: ${price:.2f}")  # Price: $9.50

discount = 0.156
print(f"Discount: {discount:.1%}")  # Discount: 15.6%

# Expressions in f-strings
a = 10
b = 3
print(f"{a} + {b} = {a + b}")  # 10 + 3 = 13
print(f"{a} * {b} = {a * b}")  # 10 * 3 = 30

# Alignment
word = "Python"
print(f"{word:>10}")  # "    Python" (right-align)
print(f"{word:<10}")  # "Python    " (left-align)
print(f"{word:^10}")  # "  Python  " (center)

# Formatting numbers
num = 3.14159
print(f"{num:.2f}")  # 3.14
print(f"{num:.4f}")  # 3.1416

# Currency
price = 12.5
print(f"Total: ${price:.2f}")  # Total: $12.50

# Creating tables
print(f"{'Item':<15} {'Price':>10} {'Quantity':>10}")
print(f"{'Apple':<15} {'$1.50':>10} {'5':>10}")
print(f"{'Banana':<15} {'$0.75':>10} {'3':>10}")

# Multiple values
score1 = 85.4
score2 = 92.6
score3 = 78.2
average = (score1 + score2 + score3) / 3
print(f"Scores: {score1:.1f}, {score2:.1f}, {score3:.1f}")
print(f"Average: {average:.1f}")

# Padding with zeros
id_number = 42
print(f"ID: {id_number:05d}")  # ID: 00042
```

### Guided Practice

1. Create variables for name, age, and salary.
2. Use f-strings to print them in a formatted sentence.
3. Format a price to show exactly 2 decimal places.
4. Create a simple receipt showing item, price, and quantity in aligned columns.
5. Calculate an average and display it with 1 decimal place.

### Practice Problems

**Problem 1 — Beginner:**
Format a price with 2 decimal places and a product name:

```python
product = "Laptop"
price = 999.5

print(f"{product}: ${price:.2f}")
```

**Problem 2 — Intermediate:**
Create a receipt showing:
- Item names (left-aligned in 20 characters)
- Prices (right-aligned in 10 characters)
- Quantities (right-aligned in 8 characters)

**Problem 3 — Challenge:**
Create a grade report that:
- Shows three test scores formatted to 1 decimal
- Calculates and displays the average formatted to 1 decimal
- Shows a percentage score (use `.1%` formatting)
- Uses proper alignment for readability

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `f"{product}: ${price:.2f}"`.
- Problem 2: Use `f"{name:<20} ${price:>10.2f} {qty:>8}"`.
- Problem 3: Calculate average as `(s1+s2+s3)/3`, format with `:.1f`, and use percentage format.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
product = "Laptop"
price = 999.5
print(f"{product}: ${price:.2f}")

# Problem 2 Example
print(f"{'Item':<20} {'Price':>10} {'Quantity':>8}")
print(f"{'Keyboard':<20} {'$49.99':>10} {'2':>8}")
print(f"{'Mouse':<20} {'$19.99':>10} {'1':>8}")
print(f"{'Monitor':<20} {'$199.99':>10} {'1':>8}")

# Problem 3 Example
score1 = 87.5
score2 = 92.3
score3 = 81.6
average = (score1 + score2 + score3) / 3
print(f"Scores: {score1:.1f}, {score2:.1f}, {score3:.1f}")
print(f"Average: {average:.1f}")
print(f"Percentage: {average/100:.1%}")
```

</details>

---
