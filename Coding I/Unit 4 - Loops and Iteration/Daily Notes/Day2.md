# Day 2: for Loops & range()
**Learning Target:** I can use for loops with range() in various forms.

### Key Concepts
A **for loop** iterates a fixed number of times. **range()** generates a sequence of numbers.

range() forms:
- `range(stop)` → 0 to stop-1
- `range(start, stop)` → start to stop-1
- `range(start, stop, step)` → start to stop-1 by step

### Code Examples
```python
# range(stop) — 0 to 9
for i in range(10):
    print(i)  # 0 1 2 3 4 5 6 7 8 9

# range(start, stop) — 1 to 10
for i in range(1, 11):
    print(i)  # 1 2 3 4 5 6 7 8 9 10

# range(start, stop, step) — by 2s
for i in range(0, 11, 2):
    print(i)  # 0 2 4 6 8 10

# Counting down
for i in range(10, 0, -1):
    print(i)  # 10 9 8 ... 1

# Sum numbers
total = 0
for i in range(1, 101):
    total += i
print(f"Sum 1-100: {total}")  # 5050
```

### Guided Practice
Create a program that prints a multiplication table for a number the user enters (rows 1-10).

### Practice Problems
**Problem 1 — Beginner:** Print numbers 1-20 using for loop with range().

**Problem 2 — Intermediate:** Print every 3rd number from 0-30 (0, 3, 6, 9...).

**Problem 3 — Challenge:** Print numbers 100 down to 1.

<details>
<summary>💡 Hints</summary>

- Problem 1: `range(1, 21)`
- Problem 2: `range(0, 31, 3)`
- Problem 3: `range(100, 0, -1)`
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
for i in range(1, 21):
    print(i)

# Problem 2
for i in range(0, 31, 3):
    print(i)

# Problem 3
for i in range(100, 0, -1):
    print(i)
```
</details>

---