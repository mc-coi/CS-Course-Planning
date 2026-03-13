# Day 4: Nested Loops
**Learning Target:** I can write nested loops for complex iteration.

### Key Concepts
A **nested loop** is a loop inside another loop. The inner loop runs completely for each iteration of the outer loop.

**Total iterations** = outer × inner

### Code Examples
```python
# Multiplication table
for i in range(1, 6):
    for j in range(1, 6):
        print(f"{i*j:4}", end=" ")  # 4-char width
    print()  # newline after inner loop

# Star pattern
for row in range(1, 6):
    for col in range(row):
        print("*", end="")
    print()  # 1 star, 2 stars, 3 stars...

# Print coordinates
for x in range(1, 4):
    for y in range(1, 4):
        print(f"({x},{y})", end=" ")
    print()
```

### Guided Practice
Create a program that prints a 5×5 grid of numbers (1-25).

### Practice Problems
**Problem 1 — Beginner:** Print a rectangle of stars: 3 rows × 4 columns.

**Problem 2 — Intermediate:** Print a triangle: row 1 has 1 star, row 2 has 2 stars, etc. (up to 6).

**Problem 3 — Challenge:** Print a multiplication table formatted as a grid (1-10 × 1-10).

<details>
<summary>💡 Hints</summary>

- Problem 1: Outer loop for rows, inner for columns
- Problem 2: Outer loop for rows, inner loop `range(row + 1)`
- Problem 3: Format with colons for alignment
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
for row in range(3):
    for col in range(4):
        print("*", end="")
    print()

# Problem 2
for row in range(1, 7):
    for star in range(row):
        print("*", end="")
    print()

# Problem 3
for i in range(1, 11):
    for j in range(1, 11):
        print(f"{i*j:4}", end="")
    print()
```
</details>

---