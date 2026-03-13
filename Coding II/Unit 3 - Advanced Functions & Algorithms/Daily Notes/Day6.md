# Day 6: Algorithm Design & Pseudocode
**Learning Target:** I can design algorithms using pseudocode and problem decomposition.

### Key Concepts
**Pseudocode:** English-like code describing algorithm logic (not runnable code).

**Problem decomposition:** Break problems into smaller, solvable parts.

### Code Examples
```
Pseudocode Example: Find Maximum in List

FUNCTION findMax(list):
    IF list is empty:
        RETURN error

    max = first element of list

    FOR each remaining element in list:
        IF element > max:
            SET max = element

    RETURN max

Python implementation:
def find_max(lst):
    if not lst:
        return None
    max_val = lst[0]
    for num in lst[1:]:
        if num > max_val:
            max_val = num
    return max_val
```

### Guided Practice
Write pseudocode for: bubble sort, linear search, counting duplicates.

### Practice Problems
**Problem 1 — Beginner:** Write pseudocode for summing all numbers in a list.

**Problem 2 — Intermediate:** Write pseudocode for sorting a list (any method).

**Problem 3 — Challenge:** Write pseudocode for finding common elements between two lists.

<details>
<summary>✅ Sample Answers</summary>

```
Problem 1:
FUNCTION sumList(numbers):
    total = 0
    FOR each number in numbers:
        ADD number to total
    RETURN total

Problem 2:
FUNCTION bubbleSort(list):
    FOR i = 0 to length - 1:
        FOR j = 0 to length - i - 1:
            IF list[j] > list[j+1]:
                SWAP list[j] and list[j+1]
    RETURN list
```
</details>

---

---
