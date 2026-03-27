# Day 2: List Operations (List Comprehensions, Nested Lists, 2D Lists)
**Learning Target:** I can use list comprehensions and work with nested and 2D lists effectively.

### Key Concepts
**List comprehension** is a concise way to create lists. Instead of looping, you use bracket notation:
```
[expression for item in list if condition]
```

**Nested lists** are lists containing other lists. Use multiple indices to access: `matrix[row][col]`

**2D lists (matrices)** are lists of lists representing rows and columns—useful for grids, game boards, and tables.

### Code Examples
```python
# List comprehension—create squares of numbers 1-5
squares = [x**2 for x in range(1, 6)]      # [1, 4, 9, 16, 25]

# List comprehension with condition
evens = [x for x in range(1, 11) if x % 2 == 0]  # [2, 4, 6, 8, 10]

# List comprehension with transformation
names = ["alice", "bob", "charlie"]
capitalized = [name.upper() for name in names]   # ["ALICE", "BOB", "CHARLIE"]

# Nested lists
student_scores = [
    ["Alice", 95],
    ["Bob", 87],
    ["Charlie", 92]
]
print(student_scores[0])      # ["Alice", 95]
print(student_scores[0][1])   # 95

# 2D list (matrix)
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
print(matrix[0])              # [1, 2, 3]
print(matrix[1][2])           # 6

# Iterating through 2D list
for row in matrix:
    for element in row:
        print(element, end=" ")  # Prints: 1 2 3 4 5 6 7 8 9

# Creating a 2D list with list comprehension
board = [[0 for _ in range(3)] for _ in range(3)]  # 3x3 grid of zeros
```

### Guided Practice
Create a program that:
1. Uses list comprehension to create a list of cubes (1³, 2³, 3³, etc.) for 1-10
2. Creates a 3x3 matrix of numbers 1-9
3. Prints the element at position [1][2]
4. Prints the entire second row
5. Iterates through the matrix and prints each row

### Practice Problems
**Problem 1 — Beginner:** Use list comprehension to create a list of all numbers from 1-20 that are divisible by 3.

**Problem 2 — Intermediate:** Create a 2x3 matrix (2 rows, 3 columns) and access the element at position [1][2].

**Problem 3 — Challenge:** Create a program that generates a 4x4 multiplication table using nested list comprehension.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `if x % 3 == 0` condition
- Problem 2: Matrix[row][col] where rows/cols start at 0
- Problem 3: Use nested comprehension: `[[i*j for j in ...] for i in ...]`
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
divisible_by_3 = [x for x in range(1, 21) if x % 3 == 0]
print(divisible_by_3)  # [3, 6, 9, 12, 15, 18]

# Problem 2 Example
matrix = [[1, 2, 3], [4, 5, 6]]
print(matrix[1][2])    # 6

# Problem 3 Example
table = [[i*j for j in range(1, 5)] for i in range(1, 5)]
for row in table:
    print(row)
```
</details>

---
