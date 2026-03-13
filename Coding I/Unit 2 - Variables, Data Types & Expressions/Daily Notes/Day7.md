# Day 7: String Formatting with f-strings
**Learning Target:** I can use f-strings to create clean formatted output.

### Key Concepts
**f-strings** (formatted string literals) let you embed variables and expressions directly in strings. Use an `f` before the quote and put variables in `{curly braces}`.

Formatting options:
- `{variable}` - plain value
- `{expression}` - math or function calls
- `{value:.2f}` - float with 2 decimals
- `{value:10}` - right-aligned in 10-character width
- `{value:<10}` - left-aligned in 10-character width
- `{value:>10}` - right-aligned (explicit)
- `{value:^10}` - centered in 10-character width

### Code Examples
```python
# Basic f-strings
name = "Alex"
age = 17
print(f"My name is {name}")        # "My name is Alex"
print(f"I am {age} years old")     # "I am 17 years old"

# Expressions in f-strings
print(f"Next year I'll be {age + 1}")  # "Next year I'll be 18"
print(f"3 + 4 = {3 + 4}")          # "3 + 4 = 7"

# Decimal formatting
price = 19.5
print(f"Price: ${price:.2f}")      # "Price: $19.50"
gpa = 3.9467
print(f"GPA: {gpa:.2f}")           # "GPA: 3.95"

# Width and alignment
name = "Bob"
print(f"Name: {name:10}")          # "Name: Bob       " (10 chars, right-aligned)
print(f"Name: {name:<10}")         # "Name: Bob       " (left-aligned)
print(f"Name: {name:>10}")         # "Name:        Bob" (right-aligned)
print(f"Name: {name:^10}")         # "Name:    Bob    " (centered)

# Report example
print(f"{'Item':<15} {'Price':>10} {'Qty':>5}")
print(f"{'Apple':<15} {'$1.50':>10} {'3':>5}")
print(f"{'Banana':<15} {'$0.75':>10} {'6':>5}")
```

### Guided Practice
Create a receipt formatter that:
1. Asks for item name, price, and quantity
2. Calculates subtotal
3. Calculates tax (8%)
4. Calculates total
5. Prints a nicely formatted receipt using f-strings

### Practice Problems
**Problem 1 — Beginner:** Use an f-string to print: "Hello [name], you are [age] years old" where name and age are variables.

```python
name =
age =

print()
```

**Problem 2 — Intermediate:** Create a simple invoice for a purchase. Use f-strings to format prices to 2 decimals and align items in columns.

**Problem 3 — Challenge:** Print a table of squares (1-10) using f-strings with proper alignment and formatting.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use f"Hello {name}, you are {age}" syntax
- Problem 2: Use :.2f for prices and :10 or :<15 for alignment
- Problem 3: Print a header row, then loop and format each number and its square
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2 Example
item = "Laptop"
price = 999.5
quantity = 1
subtotal = price * quantity
tax = subtotal * 0.08
total = subtotal + tax

print(f"{'Item':<20} {'Price':>10}")
print(f"{item:<20} ${price:>9.2f}")
print(f"{'Subtotal:':<20} ${subtotal:>9.2f}")
print(f"{'Tax (8%):':<20} ${tax:>9.2f}")
print(f"{'Total:':<20} ${total:>9.2f}")

# Problem 3 Example
print(f"{'Number':<10} {'Square':>10}")
for i in range(1, 11):
    print(f"{i:<10} {i**2:>10}")
```
</details>

---
