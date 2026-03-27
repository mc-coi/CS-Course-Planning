# Day 16: NumPy Arrays – Advanced Operations

**Learning Target:** I can use NumPy for filtering, sorting, and advanced array operations.

---

## Key Concepts

**Array Filtering:** Use boolean indexing to select elements that meet conditions.

```python
arr = np.array([1, 2, 3, 4, 5])
filtered = arr[arr > 3]  # [4, 5]
```

**Sorting:** Arrange array elements in order.

**Reshaping:** Change array dimensions without changing data.

**Broadcasting:** Apply operations across different sized arrays.

---

## Code Examples

```python
import numpy as np

# FILTERING with boolean indexing
scores = np.array([85, 92, 78, 95, 88, 76])

# Get scores above 85
high_scores = scores[scores > 85]
print(high_scores)                     # [92 95 88]

# Count scores above 85
count = np.sum(scores > 85)
print(count)                           # 3

# Multiple conditions
mid_range = scores[(scores >= 80) & (scores <= 90)]
print(mid_range)                       # [85 88]

# SORTING
data = np.array([3, 1, 4, 1, 5, 9, 2])
sorted_data = np.sort(data)
print(sorted_data)                     # [1 1 2 3 4 5 9]

# RESHAPING
arr = np.arange(12)                    # [0 1 2 ... 11]
reshaped = arr.reshape(3, 4)          # 3x4 matrix
print(reshaped)

# UNIQUE values
data = np.array([1, 2, 2, 3, 3, 3, 4])
unique = np.unique(data)
print(unique)                          # [1 2 3 4]

# CONCATENATE arrays
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
combined = np.concatenate([arr1, arr2])
print(combined)                        # [1 2 3 4 5 6]

# WHERE - conditional replacement
scores = np.array([85, 92, 78, 95])
grades = np.where(scores >= 90, 'A', 'B')
print(grades)                          # ['B' 'A' 'B' 'A']
```

---

## Guided Practice

1. **Filter Data:** Create an array of test scores and find all scores above 80.

2. **Sort and Filter:** Sort temperature data and find the 3 highest temperatures.

3. **Reshape Data:** Convert a 1D array of 12 numbers into a 3x4 matrix.

4. **Conditional Assignment:** Create grades based on scores (A: 90+, B: 80-89, etc.).

---

## Practice Problems

**Beginner:** Create an array of numbers 1-20 and filter all even numbers.

**Intermediate:** Given a dataset of sales figures, find the highest 5 values and their average.

**Challenge:** Create a system that filters data by multiple conditions and displays statistics.

<details>
<summary>💡 Hints</summary>
- Use boolean indexing: `arr[arr > value]`
- Combine conditions with `&` (and) and `|` (or)
- Use `np.sort()` to sort in ascending order
- Use `np.reshape()` to change dimensions
- Use `np.where()` for conditional operations
- `np.unique()` gets unique values
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import numpy as np

arr = np.arange(1, 21)
even = arr[arr % 2 == 0]
print(even)  # [2 4 6 8 10 12 14 16 18 20]
```

**Intermediate:**
```python
import numpy as np

sales = np.array([1500, 2300, 1800, 2800, 1200, 3200, 2100])
top5 = np.sort(sales)[-5:]
print(f"Top 5: {top5}")
print(f"Average: {np.mean(top5)}")
```

**Challenge:**
```python
import numpy as np

data = np.array([45, 78, 92, 34, 56, 88, 76, 95, 42, 68])
filtered = data[(data >= 60) & (data <= 90)]
print(f"Filtered: {filtered}")
print(f"Mean: {np.mean(filtered)}")
print(f"Count: {len(filtered)}")
```
</details>
