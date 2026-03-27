# Day 5: numpy Basics
**Learning Target:** I can use numpy for efficient numerical operations.

### Key Concepts
**numpy:** Numerical Python library
**Arrays:** Similar to lists but optimized
**Vectorized operations:** Element-wise operations without loops

### Code Examples
```python
import numpy as np

# Create arrays
arr = np.array([1, 2, 3, 4, 5])
zeros = np.zeros((3, 3))
ones = np.ones((2, 4))
range_arr = np.arange(0, 10, 2)

# Array operations
arr + 10       # [11, 12, 13, 14, 15]
arr * 2        # [2, 4, 6, 8, 10]
arr ** 2       # [1, 4, 9, 16, 25]

# Statistics
np.mean([1, 2, 3, 4, 5])   # 3.0
np.median([1, 2, 3, 4, 5]) # 3.0
np.std([1, 2, 3, 4, 5])    # 1.414...

# 2D arrays
matrix = np.array([[1, 2, 3], [4, 5, 6]])
matrix[0]       # [1, 2, 3]
matrix[0, 1]    # 2

# Reshaping
arr = np.arange(12)
reshaped = arr.reshape(3, 4)

# Useful functions
np.sum([1, 2, 3, 4])
np.max([1, 2, 3, 4])
np.min([1, 2, 3, 4])
np.sort([3, 1, 4, 1, 5])
```

### Guided Practice
Perform numerical operations on arrays.

### Practice Problems
**Problem 1 — Beginner:** Create numpy arrays and perform operations.

**Problem 2 — Intermediate:** Calculate statistics with numpy.

**Problem 3 — Challenge:** Work with 2D arrays and reshaping.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
import numpy as np
grades = np.array([92, 88, 95, 87, 90])
print(f"Mean: {np.mean(grades)}")
print(f"Median: {np.median(grades)}")
print(f"Std Dev: {np.std(grades)}")

# Problem 3
data = np.arange(12)
matrix = data.reshape(3, 4)
print(matrix.sum(axis=1))  # Sum each row
```
</details>

---

---
