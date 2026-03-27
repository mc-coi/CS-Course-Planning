# Day 7: 2D Lists & Nested Structures

**Learning Target:** I can create, access, and iterate through 2D lists (lists of lists).

---

## Key Concepts

**2D lists** (also called **nested lists** or **matrices**) are lists containing other lists. They are useful for representing tabular data like spreadsheets, game boards, or images.

**Accessing elements** requires two indices: the row index and the column index. For `matrix[i][j]`, i is the row and j is the column.

**Row-major order** (the standard in Python) means data is stored row-by-row.

**Why 2D structures matter:** Many real-world problems involve grid-like data. Think: student grade tables, game boards, pixel grids in images, etc.

---

## Code Examples

```python
# Creating a 2D list
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Accessing elements
print(matrix[0][0])  # 1 (row 0, col 0)
print(matrix[1][2])  # 6 (row 1, col 2)
print(matrix[2][1])  # 8 (row 2, col 1)

# Creating a 2D list of zeros (3x3)
zeros = [[0 for _ in range(3)] for _ in range(3)]
print(zeros)  # [[0, 0, 0], [0, 0, 0], [0, 0, 0]]

# Modifying elements
matrix[1][1] = 99
print(matrix[1][1])  # 99

# Iterating through rows
for row in matrix:
    print(row)

# Iterating with indices
for i in range(len(matrix)):
    for j in range(len(matrix[i])):
        print(f"matrix[{i}][{j}] = {matrix[i][j]}")

# Using enumerate
for i, row in enumerate(matrix):
    for j, val in enumerate(row):
        print(f"({i}, {j}) -> {val}")
```

---

## Guided Practice

**Activity: Build a Grade Table**

1. Create a 3x4 2D list representing 3 students and 4 test scores
2. Fill it with realistic grade data
3. Print the entire matrix
4. Access and print the first student's grades
5. Update the grade at row 1, column 2
6. Write a loop to calculate the average for each student
7. Write nested loops to find the highest score in the matrix

---

## Practice Problems

**Beginner:** Create a 2x3 matrix (2 rows, 3 columns) and print the element at row 1, column 2.

**Intermediate:** Write a function `print_matrix(matrix)` that prints a 2D list in a nicely formatted grid (each column aligned). Test it with a 3x3 matrix.

**Challenge:** Write a function `get_diagonal(matrix)` that returns the diagonal elements of a square 2D list. For a 3x3 matrix, it should return the top-left to bottom-right diagonal.

<details>
<summary>💡 Hints</summary>

- Beginner: Use square bracket notation twice: matrix[row][col]
- Intermediate: Use string formatting with width specifiers (e.g., f"{val:5d}")
- Challenge: The diagonal elements are at positions where row index equals column index

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Beginner
matrix = [[1, 2, 3], [4, 5, 6]]
print(matrix[1][2])  # 6

# Intermediate
def print_matrix(matrix):
    for row in matrix:
        print(" ".join(f"{val:5d}" for val in row))

# Challenge
def get_diagonal(matrix):
    return [matrix[i][i] for i in range(len(matrix))]
```

</details>
