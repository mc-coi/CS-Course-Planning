# Day 3: Bubble Sort
**Learning Target:** I can implement bubble sort and understand its O(n²) complexity.

### Key Concepts
Bubble sort repeatedly swaps adjacent elements if they're in wrong order.

Complexity: O(n²)
Simple but inefficient for large lists

### Code Examples
```python
def bubble_sort(lst):
    n = len(lst)
    for i in range(n):
        swapped = False
        for j in range(n - i - 1):
            if lst[j] > lst[j + 1]:
                lst[j], lst[j + 1] = lst[j + 1], lst[j]
                swapped = True
        if not swapped:  # Optimization: exit early if no swaps
            break
    return lst

numbers = [64, 34, 25, 12, 22, 11, 90]
print(bubble_sort(numbers))  # [11, 12, 22, 25, 34, 64, 90]
```

### Guided Practice
Visualize bubble sort step-by-step.

### Practice Problems
**Problem 1 — Beginner:** Implement basic bubble sort.

**Problem 2 — Intermediate:** Add optimization (swapped flag).

**Problem 3 — Challenge:** Count comparisons and swaps.

<details>
<summary>✅ Sample Answers</summary>

```python
def bubble_sort_counting(lst):
    n = len(lst)
    comparisons = swaps = 0
    for i in range(n):
        for j in range(n - i - 1):
            comparisons += 1
            if lst[j] > lst[j + 1]:
                lst[j], lst[j + 1] = lst[j + 1], lst[j]
                swaps += 1
    return lst, comparisons, swaps
```
</details>

---

---
