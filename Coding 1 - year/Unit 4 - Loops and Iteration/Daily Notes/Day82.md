# Day 82: Nested Loops — Loops Inside Loops

**Learning Target:** I can write nested loops (loops within loops) and understand how the inner loop executes for each iteration of the outer loop.

### Key Concepts

A **nested loop** has a loop inside another loop. The inner loop completes all its iterations for each single iteration of the outer loop.

**Structure:**
```python
for outer in range(n):         # Outer loop
    for inner in range(m):     # Inner loop
        # Body executes n × m times
```

**Key Point:** The inner loop runs completely for each outer iteration.

**Execution order:**
```
Outer iteration 1:
  Inner iteration 1
  Inner iteration 2
  Inner iteration 3
Outer iteration 2:
  Inner iteration 1
  Inner iteration 2
  Inner iteration 3
Outer iteration 3:
  ...
```

**Total iterations:** outer × inner (e.g., 3 outer × 4 inner = 12 total executions)

**Visualization:** Think of nested loops as rows and columns:
- Outer loop = rows
- Inner loop = columns

### Code Examples

```python
# Example 1: Simple 2D grid (3 rows, 3 columns)
print("3×3 grid:")
for row in range(3):
    for col in range(3):
        print("*", end=" ")
    print()  # Newline after each row
print()

# Example 2: Print coordinates
print("Coordinates:")
for x in range(1, 4):
    for y in range(1, 4):
        print(f"({x},{y})", end=" ")
    print()
print()

# Example 3: Multiplication table
print("Multiplication table:")
for i in range(1, 6):
    for j in range(1, 6):
        print(f"{i*j:3}", end=" ")  # 3-width for alignment
    print()
print()

# Example 4: Building up pattern
print("Pattern:")
for i in range(1, 5):
    for j in range(1, i+1):
        print("*", end="")
    print()
```

### Guided Practice

Trace this code and predict the output:
```python
for i in range(2):
    for j in range(3):
        print(f"{i},{j}", end=" ")
    print()
```

Then, write a nested loop that creates a 4×4 checkerboard pattern (alternating spaces and X's).

### Practice Problems

**Problem 1 — Beginner:** Write nested loops that print a 4×4 grid of numbers (1-16):
```
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 16
```

**Problem 2 — Intermediate:** Write nested loops that print a right triangle of stars:
```
*
* *
* * *
* * * *
* * * * *
```

**Problem 3 — Challenge:** Write nested loops that print a diamond pattern:
```
    *
   * *
  * * *
 * * * *
* * * * *
 * * * *
  * * *
   * *
    *
```
(Hint: Use a variable for spaces, and two different nested loop sections for top and bottom.)

<details>
<summary>💡 Hints</summary>

- Problem 1: Keep a counter starting at 1. For each outer/inner iteration, print counter and increment.
- Problem 2: Outer loop from 1 to n+1, inner loop from 1 to i+1 (i is outer variable)
- Problem 3: Top half: spaces decrease, stars increase. Bottom half: spaces increase, stars decrease.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
counter = 1
for row in range(4):
    for col in range(4):
        print(counter, end=" ")
        counter += 1
    print()

# Problem 2 Example
for i in range(1, 6):
    for j in range(i):
        print("*", end=" ")
    print()

# Problem 3 Example (simplified)
for i in range(1, 6):
    spaces = 5 - i
    for s in range(spaces):
        print(" ", end="")
    for st in range(i):
        print("*", end=" ")
    print()

for i in range(4, 0, -1):
    spaces = 5 - i
    for s in range(spaces):
        print(" ", end="")
    for st in range(i):
        print("*", end=" ")
    print()
```

</details>

---
