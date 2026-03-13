# Day 4: Selection Sort
**Learning Target:** I can implement selection sort and compare with bubble sort.

### Key Concepts
Selection sort finds minimum and moves to front.

Complexity: O(n²)
Similar to bubble but fewer swaps

### Code Examples
```python
def selection_sort(lst):
    n = len(lst)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if lst[j] < lst[min_idx]:
                min_idx = j
        lst[i], lst[min_idx] = lst[min_idx], lst[i]
    return lst

numbers = [64, 34, 25, 12, 22, 11, 90]
print(selection_sort(numbers))  # [11, 12, 22, 25, 34, 64, 90]
```

### Guided Practice
Compare selection sort to bubble sort.

### Practice Problems
**Problem 1 — Beginner:** Implement selection sort.

**Problem 2 — Intermediate:** Compare with bubble sort.

**Problem 3 — Challenge:** Optimize selection sort variants.

<details>
<summary>✅ Sample Answers</summary>

```python
# Comparison shows selection usually has fewer swaps than bubble
def count_swaps(sort_func, lst):
    swaps = 0
    lst_copy = lst.copy()
    # Modify sort_func to count swaps
    # ...
```
</details>

---

---
