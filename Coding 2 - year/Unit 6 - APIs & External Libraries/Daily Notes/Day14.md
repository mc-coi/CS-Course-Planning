# Day 14: Introduction to NumPy – Arrays & Operations

**Learning Target:** I can create and manipulate NumPy arrays for efficient numerical computing.

---

## Key Concepts

**NumPy:** A library for numerical computing in Python. Much faster than lists for large datasets.

**NumPy Array:** Like a list, but optimized for math. Can be 1D (vector), 2D (matrix), or multi-dimensional.

**Why NumPy:**
- **Speed:** 10-100x faster than Python lists for math
- **Memory:** Uses less memory
- **Functionality:** Built-in math operations without loops

**Key Differences from Lists:**
- Arrays are fixed type (all int, all float, etc.)
- Operations apply element-wise without loops
- Better for mathematical operations

---

## Code Examples

```python
import numpy as np

# Create arrays
arr1 = np.array([1, 2, 3, 4, 5])
print(arr1)                          # [1 2 3 4 5]

arr2 = np.array([10, 20, 30, 40, 50])
print(arr2)                          # [10 20 30 40 50]

# Operations (no loops needed!)
print(arr1 + arr2)                   # [11 22 33 44 55]
print(arr1 * 2)                      # [2  4  6  8 10]
print(arr1 + 10)                     # [11 12 13 14 15]

# Common functions
print(np.sum(arr1))                  # 15 (sum of all)
print(np.mean(arr1))                 # 3.0 (average)
print(np.max(arr1))                  # 5 (maximum)
print(np.min(arr1))                  # 1 (minimum)
print(np.std(arr1))                  # Standard deviation

# Create arrays with patterns
zeros = np.zeros(5)                  # [0. 0. 0. 0. 0.]
ones = np.ones(5)                    # [1. 1. 1. 1. 1.]
sequence = np.arange(0, 10, 2)       # [0 2 4 6 8]
linspace = np.linspace(0, 1, 5)      # [0.   0.25 0.5  0.75 1.  ]

# 2D arrays (matrices)
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
print(matrix)
print(matrix.shape)                  # (3, 3)
print(matrix[0, 1])                  # 2 (row 0, column 1)

# Accessing elements
arr = np.array([10, 20, 30, 40, 50])
print(arr[0])                        # 10
print(arr[1:3])                      # [20 30]
print(arr[-1])                       # 50 (last element)
```

---

## Guided Practice

1. **Create Arrays:** Create arrays of numbers 1-10 and perform basic math operations.

2. **Statistics:** Create an array of test scores and calculate mean, median, max, and min.

3. **Arrays from Data:** Convert a list of temperatures into a NumPy array and perform calculations.

4. **2D Arrays:** Create a 3x3 matrix and access specific elements.

---

## Practice Problems

**Beginner:** Create a NumPy array of numbers 1-10 and calculate the sum, mean, and max.

**Intermediate:** Create an array of temperatures and find how many are above the average.

**Challenge:** Create a 3x3 matrix and calculate the sum of each row.

<details>
<summary>💡 Hints</summary>
- Use `np.array()` to create arrays from lists
- Operations like `+`, `*` work element-wise (no loops!)
- Use `np.sum()`, `np.mean()`, `np.max()` for statistics
- Use slicing like `arr[1:3]` to get subsets
- `arr[arr > 5]` gets all elements greater than 5
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import numpy as np

arr = np.arange(1, 11)
print(f"Sum: {np.sum(arr)}")        # 55
print(f"Mean: {np.mean(arr)}")      # 5.5
print(f"Max: {np.max(arr)}")        # 10
```

**Intermediate:**
```python
import numpy as np

temps = np.array([72, 68, 75, 81, 69, 76])
avg = np.mean(temps)
above_avg = np.sum(temps > avg)
print(f"Above average: {above_avg}")
```

**Challenge:**
```python
import numpy as np

matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

for row in matrix:
    print(f"Row sum: {np.sum(row)}")
```
</details>
