# Day 5: Insertion Sort
**Learning Target:** I can implement insertion sort and understand its advantage for nearly-sorted data.

### Key Concepts
Insertion sort builds sorted array one element at a time.

Complexity: O(n²) average, O(n) best case (already sorted)
Efficient for small/nearly-sorted lists

### Code Examples
```python
def insertion_sort(lst):
    for i in range(1, len(lst)):
        key = lst[i]
        j = i - 1
        while j >= 0 and lst[j] > key:
            lst[j + 1] = lst[j]
            j -= 1
        lst[j + 1] = key
    return lst

numbers = [64, 34, 25, 12, 22, 11, 90]
print(insertion_sort(numbers))  # [11, 12, 22, 25, 34, 64, 90]
```

### Guided Practice
Show efficiency on nearly-sorted data.

### Practice Problems
**Problem 1 — Beginner:** Implement insertion sort.

**Problem 2 — Intermediate:** Test on nearly-sorted data.

**Problem 3 — Challenge:** Optimize for specific use cases.

<details>
<summary>✅ Sample Answers</summary>

```python
# Nearly-sorted list
almost_sorted = [1, 2, 3, 4, 5, 6, 50, 7, 8]
# Insertion sort is very fast here
```
</details>

---

---
