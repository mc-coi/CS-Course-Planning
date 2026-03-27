# Day 31: Augmented Assignment Operators — +=, -=, *=, /=, //=

**Learning Target:** I can use compound assignment operators to modify variables efficiently.

### Key Concepts

**Augmented assignment operators** (also called compound assignment) combine an operator with assignment. They're shorthand for updating a variable based on its current value.

- `x += 5` means `x = x + 5` (add 5 to x)
- `x -= 3` means `x = x - 3` (subtract 3)
- `x *= 2` means `x = x * 2` (multiply by 2)
- `x /= 4` means `x = x / 4` (divide by 4, result is float)
- `x //= 2` means `x = x // 2` (integer divide)
- `x %= 3` means `x = x % 3` (remainder)
- `x **= 2` means `x = x ** 2` (exponentiation)

These operators are particularly useful in loops and when tracking scores, counts, or running totals. They're cleaner and faster than writing out the full assignment.

### Code Examples

```python
# Basic augmented assignment
score = 0
score += 10
print(score)  # 10

score += 5
print(score)  # 15

score -= 3
print(score)  # 12

score *= 2
print(score)  # 24

score //= 3
print(score)  # 8

# Using in sequences
count = 1
count += 1  # 2
count += 1  # 3
count += 1  # 4
print(count)  # 4

# Building a running total
total = 0
total += 100
total += 50
total += 75
print(f"Total: ${total}")  # Total: $225

# Game score tracker
player_score = 0
print("Starting score:", player_score)
player_score += 10
print("After first action:", player_score)
player_score += 25
print("After second action:", player_score)
player_score -= 5
print("After penalty:", player_score)

# Countdown
time_left = 60
time_left -= 15
time_left -= 15
time_left -= 15
print(f"Time remaining: {time_left}s")  # 15

# Doubling (exponential growth)
amount = 1
amount *= 2
amount *= 2
amount *= 2
print(amount)  # 8
```

### Guided Practice

1. Create a variable for a score starting at 0.
2. Use `+=` to add 10, 15, and 20 to the score (print after each).
3. Use `-=` to subtract 5 (print).
4. Use `*=` to double the score (print).
5. Use `//=` to divide the score by 3 (print).

### Practice Problems

**Problem 1 — Beginner:**
Create a score variable starting at 100. Use `+=` and `-=` to update it, printing after each operation.

```python
score = 100
score += 10
print(score)

score -= 5
print(score)

# Add 2 more operations
```

**Problem 2 — Intermediate:**
Simulate a savings account:
- Start with $500
- Add $100 (paycheck)
- Subtract $45 (bill)
- Add $50 (bonus)
- Multiply by 1.02 (interest accrual)
- Print the final amount

**Problem 3 — Challenge:**
Create a compound growth calculation:
- Start with 100 bacteria
- After hour 1, multiply by 2 (use `*=`)
- After hour 2, multiply by 2
- After hour 3, multiply by 2
- Calculate the same using exponentiation: `100 * (2 ** 3)`
- Verify both give the same result

<details>
<summary>💡 Hints</summary>

- Problem 1: Just use `+=` and `-=` operators; remember to print after each.
- Problem 2: Use `+=`, `-=`, then `*=` for the interest.
- Problem 3: Compare `*=` repeated three times vs. using `** 3` exponentiation.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
score = 100
score += 10
print(score)  # 110
score -= 5
print(score)  # 105
score += 20
print(score)  # 125
score -= 15
print(score)  # 110

# Problem 2 Example
balance = 500
balance += 100
balance -= 45
balance += 50
balance *= 1.02
print(f"Final balance: ${balance:.2f}")

# Problem 3 Example
bacteria = 100
bacteria *= 2
bacteria *= 2
bacteria *= 2
print(f"Method 1: {bacteria}")

bacteria2 = 100 * (2 ** 3)
print(f"Method 2: {bacteria2}")
print(f"Same? {bacteria == bacteria2}")
```

</details>

---
