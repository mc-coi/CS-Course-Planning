# Day 2: Binary Search
**Learning Target:** I can implement binary search for sorted data and understand its O(log n) efficiency.

### Key Concepts
Binary search divides sorted data in half each iteration.

Complexity: O(log n) — much faster for large sorted lists
Data MUST be sorted

### Code Examples
```python
def binary_search(lst, target):
    low, high = 0, len(lst) - 1

    while low <= high:
        mid = (low + high) // 2
        if lst[mid] == target:
            return mid
        elif lst[mid] < target:
            low = mid + 1
        else:
            high = mid - 1

    return -1

numbers = [10, 20, 30, 40, 50, 60, 70, 80, 90]
print(binary_search(numbers, 50))  # 4
print(binary_search(numbers, 25))  # -1

# Recursive version
def binary_search_recursive(lst, target, low, high):
    if low > high:
        return -1

    mid = (low + high) // 2
    if lst[mid] == target:
        return mid
    elif lst[mid] < target:
        return binary_search_recursive(lst, target, mid + 1, high)
    else:
        return binary_search_recursive(lst, target, low, mid - 1)
```

### Guided Practice
Implement and compare linear vs binary search on large sorted list.

### Practice Problems
**Problem 1 — Beginner:** Binary search implementation.

**Problem 2 — Intermediate:** Compare linear vs binary performance.

**Problem 3 — Challenge:** Recursive binary search.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
import time

lst = list(range(1000000))
target = 999999

# Linear
start = time.time()
linear_search(lst, target)
print(f"Linear: {time.time() - start}")

# Binary
start = time.time()
binary_search(lst, target)
print(f"Binary: {time.time() - start}")
```
</details>

---

---
