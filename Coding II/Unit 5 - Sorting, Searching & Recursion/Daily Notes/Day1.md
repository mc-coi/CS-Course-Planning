# Day 1: Linear Search
**Learning Target:** I can implement linear search and understand when it's appropriate.

### Key Concepts
Linear search checks each element sequentially until found.

Complexity: O(n)
Works on any list (sorted or unsorted)

### Code Examples
```python
def linear_search(lst, target):
    for i in range(len(lst)):
        if lst[i] == target:
            return i
    return -1

numbers = [10, 20, 30, 40, 50]
print(linear_search(numbers, 30))  # 2
print(linear_search(numbers, 100)) # -1

# With while loop
def linear_search_while(lst, target):
    i = 0
    while i < len(lst):
        if lst[i] == target:
            return i
        i += 1
    return -1
```

### Guided Practice
Implement linear search and count comparisons.

### Practice Problems
**Problem 1 — Beginner:** Linear search for a number.

**Problem 2 — Intermediate:** Linear search with count of comparisons.

**Problem 3 — Challenge:** Linear search in string for character.

<details>
<summary>✅ Sample Answers</summary>

```python
def linear_search_counting(lst, target):
    count = 0
    for item in lst:
        count += 1
        if item == target:
            return count
    return -1
```
</details>

---

---
