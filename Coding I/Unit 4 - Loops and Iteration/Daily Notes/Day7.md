# Day 7: Accumulator Pattern
**Learning Target:** I can recognize and use the accumulator pattern in various situations.

### Key Concepts
**Accumulator pattern:** Initialize before loop, update inside loop with compound operator (+=, -=, etc.), use result after loop.

Works for: sum, product, count, min, max, string building, list building.

### Code Examples
```python
# Sum accumulator
total = 0
for i in range(1, 101):
    total += i
print(f"Sum: {total}")  # 5050

# Product accumulator
product = 1
for i in range(1, 6):
    product *= i
print(f"5! = {product}")  # 120

# Count accumulator
text = "hello world"
count = 0
for ch in text:
    if ch == "l":
        count += 1
print(f"L count: {count}")  # 3

# Min/max accumulators
numbers = [34, 12, 78, 5, 90, 23]
min_val = numbers[0]
max_val = numbers[0]
for num in numbers:
    if num < min_val:
        min_val = num
    if num > max_val:
        max_val = num
print(f"Min: {min_val}, Max: {max_val}")  # Min: 5, Max: 90

# String accumulator
text = "Python"
result = ""
for ch in text:
    if ch != "o":
        result += ch
print(result)  # "Pythn"
```

### Guided Practice
Write a program that:
1. Sums numbers 1-50
2. Finds product 1-5 (factorial)
3. Counts vowels in a sentence
4. Finds min and max in a list

### Practice Problems
**Problem 1 — Beginner:** Calculate factorial using accumulator: 5! = 1×2×3×4×5.

**Problem 2 — Intermediate:** Count how many times each vowel appears in a sentence.

**Problem 3 — Challenge:** Find the average of numbers input by user (until -1).

<details>
<summary>💡 Hints</summary>

- Problem 1: Initialize product = 1, then *=
- Problem 2: Five accumulators (one per vowel) or one loop counting each
- Problem 3: Accumulate total and count, divide at end
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
product = 1
for i in range(1, 6):
    product *= i
print(f"5! = {product}")

# Problem 3
total = 0
count = 0
while True:
    num = int(input("Number (-1 to quit): "))
    if num == -1:
        break
    total += num
    count += 1
average = total / count if count > 0 else 0
print(f"Average: {average:.2f}")
```
</details>

---