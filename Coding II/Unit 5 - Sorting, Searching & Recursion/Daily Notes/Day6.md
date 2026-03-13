# Day 6: Merge Sort
**Learning Target:** I can implement merge sort using divide-and-conquer.

### Key Concepts
Merge sort: divide, conquer, combine
Complexity: O(n log n)
Uses more memory but much faster than bubble/selection/insertion

### Code Examples
```python
def merge_sort(lst):
    if len(lst) <= 1:
        return lst

    mid = len(lst) // 2
    left = merge_sort(lst[:mid])
    right = merge_sort(lst[mid:])

    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result

numbers = [64, 34, 25, 12, 22, 11, 90]
print(merge_sort(numbers))  # [11, 12, 22, 25, 34, 64, 90]
```

### Guided Practice
Trace merge sort execution.

### Practice Problems
**Problem 1 — Beginner:** Implement merge sort.

**Problem 2 — Intermediate:** Compare to bubble sort performance.

**Problem 3 — Challenge:** Count operations in merge sort.

<details>
<summary>✅ Sample Answers</summary>

```python
import time

lst_large = list(range(10000, 0, -1))  # Reversed

start = time.time()
bubble_sort(lst_large.copy())
print(f"Bubble: {time.time() - start}")

start = time.time()
merge_sort(lst_large.copy())
print(f"Merge: {time.time() - start}")
# Merge will be dramatically faster
```
</details>

---

---
