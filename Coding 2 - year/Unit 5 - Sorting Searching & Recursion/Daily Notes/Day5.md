# Day 5: Binary Search Prerequisites & Iterative Implementation

**Learning Target:** I can implement iterative binary search and explain why data must be sorted.

---

## Key Concepts

**Binary Search**: Dividing the search space in half repeatedly. Much faster than linear search but requires **sorted data**.

**Prerequisite:** The list MUST be sorted in ascending order.

**Time Complexity:**
- Best case: O(1) — found on first try (middle element)
- Average/Worst case: O(log n) — each comparison eliminates half the remaining data

**Why O(log n)?** Each step divides the list in half: 1000 items → 500 → 250 → 125 → 62 → 31 → 15 → 7 → 3 → 1. That's only 10 steps!

### Binary Search Strategy
```
Target: 35 in [5, 10, 15, 20, 25, 30, 35, 40, 45, 50]
                                       ↑
Step 1: Check middle → 27.5 (between indices 4 and 5). 35 > middle? Look right.
Step 2: Right half: [30, 35, 40, 45, 50]. Check middle → 40. 35 < 40? Look left.
Step 3: Left half: [30, 35]. Check middle → 35. Found!
```

---

## Code Examples

```python
# Iterative Binary Search
def binary_search(arr, target):
    """
    Search for target in SORTED array using binary search.
    Returns index if found, -1 if not found.
    """
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = (left + right) // 2  # Find middle index

        if arr[mid] == target:
            return mid  # Found it!
        elif arr[mid] < target:
            left = mid + 1  # Target is in the right half
        else:
            right = mid - 1  # Target is in the left half

    return -1  # Never found it

# Test with sorted list
numbers = [5, 10, 15, 20, 25, 30, 35, 40, 45, 50]
print(binary_search(numbers, 35))   # Output: 6
print(binary_search(numbers, 15))   # Output: 2
print(binary_search(numbers, 100))  # Output: -1

# With step-by-step visualization
def binary_search_verbose(arr, target):
    left = 0
    right = len(arr) - 1
    step = 0

    while left <= right:
        step += 1
        mid = (left + right) // 2
        print(f"Step {step}: Check index {mid} (value: {arr[mid]})")

        if arr[mid] == target:
            print(f"Found {target} at index {mid}!")
            return mid
        elif arr[mid] < target:
            print(f"  {arr[mid]} < {target}, search right half")
            left = mid + 1
        else:
            print(f"  {arr[mid]} > {target}, search left half")
            right = mid - 1

    print(f"Target {target} not found")
    return -1

# Test
print("\nSearching for 35:")
binary_search_verbose(numbers, 35)
```

---

## Guided Practice

**Step 1:** Sort this list manually: `[38, 12, 45, 9, 23, 67, 3]`

**Step 2:** Using your sorted list, trace `binary_search(sorted_list, 23)`.
- What's the middle element?
- Is 23 greater than or less than the middle?
- What's the new middle?
- When is the target found?

**Step 3:** Now trace searching for a value NOT in the list (like 50). At what point does the search stop?

**Step 4:** Compare: How many steps does binary search take vs. linear search for a 1000-item list?
- Linear search worst case: 1000 comparisons
- Binary search worst case: ~10 comparisons (log₂(1000) ≈ 10)

---

## Practice Problems

**Beginner:** Implement binary search on a list of ages: `[18, 22, 25, 31, 35, 42, 48, 55]`. Search for age 31. Trace through step by step.

**Intermediate:** Write a function that returns True/False instead of an index. Also, handle the case where the input list might NOT be sorted (check first, or return an error).

**Challenge:** What happens if you call binary search on an UNSORTED list? Give an example where it fails.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Count how many times you recalculate `mid` and adjust left/right bounds.
- **Intermediate:** You could add a check: `if arr != sorted(arr): raise ValueError("List not sorted")`
- **Challenge:** Try searching in `[5, 2, 8, 1, 9]` for the value 2. Because it's not sorted, the algorithm will skip over it.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner - Trace of binary_search([18, 22, 25, 31, 35, 42, 48, 55], 31)
# Step 1: left=0, right=7, mid=3, arr[3]=31. Found immediately!

# Intermediate
def binary_search_safe(arr, target):
    # Check if sorted
    if arr != sorted(arr):
        raise ValueError("List must be sorted for binary search")

    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return True
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return False

# Challenge
unsorted = [5, 2, 8, 1, 9]
# Searching for 2:
# mid = index 2 (value 8), 2 < 8, so search left
# mid = index 0 (value 5), 2 < 5, so search left
# left > right, return -1 (not found!)
# But 2 is actually in the list! Binary search fails on unsorted data.
```
</details>
