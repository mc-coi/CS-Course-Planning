# Day 83: Nested Loop Applications — Multiplication Tables and Patterns

**Learning Target:** I can apply nested loops to real-world problems like multiplication tables, searching 2D grids, and complex pattern generation.

### Key Concepts

Nested loops are powerful for:
- **Tables & matrices:** Multiplication tables, seating charts, game boards
- **Searching:** Find an element in a grid or list of lists
- **Pattern generation:** Complex visual patterns
- **Data processing:** Analyze all pairs or combinations

**Common pattern:** Inner loop depends on outer loop variable (e.g., growing triangle where row 1 has 1 star, row 2 has 2 stars).

### Code Examples

```python
# Example 1: Multiplication table (5×5)
print("Multiplication Table:")
for i in range(1, 6):
    for j in range(1, 6):
        print(f"{i*j:3}", end=" ")  # 3-character width
    print()
print()

# Example 2: Search in grid (find a number)
grid = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
    [13, 14, 15, 16]
]
target = 10
for row in range(len(grid)):
    for col in range(len(grid[row])):
        if grid[row][col] == target:
            print(f"Found {target} at position [{row},{col}]")
print()

# Example 3: Pyramid of numbers
print("Number Pyramid:")
for row in range(1, 6):
    for col in range(1, row+1):
        print(col, end=" ")
    print()
print()

# Example 4: Checkerboard pattern
print("Checkerboard (8×8):")
for row in range(8):
    for col in range(8):
        if (row + col) % 2 == 0:
            print("█", end=" ")
        else:
            print(" ", end=" ")
    print()
```

### Guided Practice

Write a program that displays a multiplication table:
1. Ask the user for the size (e.g., 5 for 5×5, 10 for 10×10)
2. Print a formatted multiplication table with headers
3. Example output:
   ```
     ×  1  2  3  4  5
     1  1  2  3  4  5
     2  2  4  6  8 10
     3  3  6  9 12 15
     ...
   ```

### Practice Problems

**Problem 1 — Beginner:** Create and print a 3×4 addition table (instead of multiplication):
```
+  1  2  3  4
1  2  3  4  5
2  3  4  5  6
3  4  5  6  7
```

**Problem 2 — Intermediate:** Create a program that checks if a given number appears in a 3×3 grid. If found, print its position; if not, print "Not found."

**Problem 3 — Challenge:** Print a hollow square (outer frame only, inner is empty):
```
* * * * *
*       *
*       *
*       *
* * * * *
```
Where the size is user-defined.

<details>
<summary>💡 Hints</summary>

- Problem 1: Similar to multiplication table, but use `+` instead of `*`
- Problem 2: Define a 3×3 grid as a list of lists. Nested loop through rows and columns.
- Problem 3: Check if you're on the edge (first/last row or first/last column). If yes, print "*"; else print space.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
print("+  1  2  3  4")
for i in range(1, 4):
    print(f"{i}  ", end="")
    for j in range(1, 5):
        print(f"{i+j}  ", end="")
    print()

# Problem 2 Example
grid = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
target = int(input("Find: "))
found = False
for row in range(3):
    for col in range(3):
        if grid[row][col] == target:
            print(f"Found at [{row},{col}]")
            found = True
if not found:
    print("Not found")

# Problem 3 Example
size = 5
for row in range(size):
    for col in range(size):
        if row == 0 or row == size-1 or col == 0 or col == size-1:
            print("*", end=" ")
        else:
            print(" ", end=" ")
    print()
```

</details>

---
