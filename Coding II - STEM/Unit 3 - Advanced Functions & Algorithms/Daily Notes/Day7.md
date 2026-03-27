# Day 7: Complexity Analysis (Big O Notation)
**Learning Target:** I can analyze algorithm complexity and choose appropriate algorithms.

### Key Concepts
**Big O notation** describes how algorithm performance scales with input size.

- O(1) — Constant time (instant)
- O(n) — Linear time (proportional to input)
- O(n²) — Quadratic time (exponential slowdown)
- O(log n) — Logarithmic time (very fast for large inputs)
- O(n log n) — Efficient sorting

### Code Examples
```python
# O(1) — Constant time
def get_first(lst):
    return lst[0]

# O(n) — Linear time
def sum_all(lst):
    total = 0
    for num in lst:
        total += num
    return total

# O(n²) — Quadratic time (nested loops)
def bubble_sort(lst):
    for i in range(len(lst)):
        for j in range(len(lst) - 1):
            if lst[j] > lst[j + 1]:
                lst[j], lst[j + 1] = lst[j + 1], lst[j]

# O(log n) — Binary search (must be sorted)
def binary_search(sorted_lst, target):
    low, high = 0, len(sorted_lst) - 1
    while low <= high:
        mid = (low + high) // 2
        if sorted_lst[mid] == target:
            return mid
        elif sorted_lst[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

# Comparing performance
import time

big_list = list(range(100000))

# Linear search: O(n)
start = time.time()
for item in big_list:
    if item == 50000:
        break
print(f"Linear: {time.time() - start}")

# Binary search: O(log n)
start = time.time()
binary_search(big_list, 50000)
print(f"Binary: {time.time() - start}")
```

### Guided Practice
Identify Big O for various code snippets. Compare algorithm efficiency.

### Practice Problems
**Problem 1 — Beginner:** What is the Big O of checking if a number is in a list?

**Problem 2 — Intermediate:** Compare bubble sort vs merge sort complexity.

**Problem 3 — Challenge:** Optimize an O(n²) algorithm to O(n log n) if possible.

<details>
<summary>✅ Sample Answers</summary>

```
Problem 1: O(n) — must check each element

Problem 2: Bubble sort O(n²), Merge sort O(n log n)

Problem 3: Use sorting + efficient algorithms instead of nested loops
```
</details>

---

---
