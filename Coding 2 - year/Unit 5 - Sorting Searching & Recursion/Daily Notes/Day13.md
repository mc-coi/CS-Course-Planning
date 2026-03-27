# Day 13: Merge Sort - Divide and Conquer

**Learning Target:** I can implement merge sort and explain the divide-and-conquer strategy and O(n log n) complexity.

---

## Key Concepts

**Divide and Conquer:**
1. **Divide:** Split the array in half repeatedly until you have subarrays of size 1
2. **Conquer:** Sort the small subarrays (trivial: 1 element is already sorted)
3. **Combine:** Merge the sorted subarrays back together

**Merge Sort Complexity:**
- **Time:** O(n log n) always (best, average, worst)
- **Space:** O(n) — needs extra space for merging
- **Stable:** Yes — equal elements maintain relative order

**Why O(n log n)?**
```
Levels of recursion: log₂(n)
Work at each level: n (comparing and merging)
Total: n * log₂(n)
```

**Why not always use it?** It uses extra memory (not in-place).

---

## Code Examples

```python
# Merge Sort
def merge_sort(arr):
    """
    Divide array in half recursively until single elements.
    Then merge sorted halves back together.
    """
    if len(arr) <= 1:
        return arr

    # Divide
    mid = len(arr) // 2
    left = arr[:mid]
    right = arr[mid:]

    # Conquer (recursively sort)
    left = merge_sort(left)
    right = merge_sort(right)

    # Combine (merge)
    return merge(left, right)

def merge(left, right):
    """Merge two sorted arrays into one sorted array."""
    result = []
    i = j = 0

    # Compare elements from left and right, add smaller one
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    # Add remaining elements
    result.extend(left[i:])
    result.extend(right[j:])

    return result

# Test
numbers = [64, 34, 25, 12, 22, 11, 90]
print(merge_sort(numbers))  # Output: [11, 12, 22, 25, 34, 64, 90]

# With visualization
def merge_sort_verbose(arr, depth=0):
    """Show the divide and merge process."""
    indent = "  " * depth

    if len(arr) <= 1:
        print(f"{indent}Base case: {arr}")
        return arr

    print(f"{indent}Dividing: {arr}")

    mid = len(arr) // 2
    left = arr[:mid]
    right = arr[mid:]

    print(f"{indent}  Left: {left}, Right: {right}")

    left = merge_sort_verbose(left, depth + 1)
    right = merge_sort_verbose(right, depth + 1)

    result = merge(left, right)
    print(f"{indent}Merged: {result}")

    return result

# In-place merge sort (more complex, but saves space)
def merge_sort_inplace(arr, left=0, right=None):
    """Merge sort that modifies array in place."""
    if right is None:
        right = len(arr) - 1

    if left < right:
        mid = (left + right) // 2

        # Recursively sort left and right halves
        merge_sort_inplace(arr, left, mid)
        merge_sort_inplace(arr, mid + 1, right)

        # Merge the sorted halves
        merge_inplace(arr, left, mid, right)

    return arr

def merge_inplace(arr, left, mid, right):
    """Merge two sorted portions of an array in place."""
    # Create copies of left and right portions
    left_copy = arr[left:mid + 1]
    right_copy = arr[mid + 1:right + 1]

    i = j = 0
    k = left

    # Merge back into arr
    while i < len(left_copy) and j < len(right_copy):
        if left_copy[i] <= right_copy[j]:
            arr[k] = left_copy[i]
            i += 1
        else:
            arr[k] = right_copy[j]
            j += 1
        k += 1

    # Copy remaining elements
    while i < len(left_copy):
        arr[k] = left_copy[i]
        i += 1
        k += 1

    while j < len(right_copy):
        arr[k] = right_copy[j]
        j += 1
        k += 1
```

---

## Guided Practice

**Step 1: Visualize Divide Phase**

Array: `[5, 2, 8, 1, 9, 3, 7, 4]`

```
[5, 2, 8, 1, 9, 3, 7, 4]
       ↓ divide
[5, 2, 8, 1]  |  [9, 3, 7, 4]
    ↓ divide        ↓ divide
[5, 2] | [8, 1]  [9, 3] | [7, 4]
  ↓ div   ↓ div    ↓ div   ↓ div
[5] [2] [8] [1]  [9] [3] [7] [4]
```

**Step 2: Visualize Merge Phase**

```
[5] [2]  →  [2, 5]
[8] [1]  →  [1, 8]
[2, 5] + [1, 8]  →  [1, 2, 5, 8]
```

**Step 3: Count Operations**

Merge sort at each level:
- Level 0: 8 elements, 1 array (divide only)
- Level 1: 4 elements × 2 arrays (some merging)
- Level 2: 2 elements × 4 arrays (more merging)
- Level 3: 1 element × 8 arrays (all merged)

Total comparisons: ~24 (compared to ~56 for bubble sort on same data)

---

## Practice Problems

**Beginner:** Trace merge sort on `[5, 2, 4, 1]`. Show both the divide and merge phases.

**Intermediate:** Implement merge sort and test it on a 100-element random array. Compare execution time to bubble sort.

**Challenge:** Explain why merge sort is stable. Can you break the stability by modifying the merge function?

<details>
<summary>💡 Hints</summary>
- **Beginner:** Draw the recursion tree. Each level divides the array further down until size 1.
- **Intermediate:** Use the time module to measure. Merge sort should be much faster.
- **Challenge:** Stability is preserved in the merge function because we check `left[i] <= right[j]`, so equal elements from left are placed before equal elements from right.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner - Trace of merge_sort([5, 2, 4, 1])
# Divide phase:
#   [5, 2, 4, 1] → [5, 2] | [4, 1]
#   [5, 2] → [5] | [2]
#   [4, 1] → [4] | [1]
#
# Merge phase:
#   [5] + [2] → [2, 5]
#   [4] + [1] → [1, 4]
#   [2, 5] + [1, 4] → [1, 2, 4, 5]

# Intermediate
import time

random_arr = list(range(100, 0, -1))

start = time.time()
merge_sort(random_arr)
merge_time = time.time() - start

start = time.time()
bubble_sort(random_arr)
bubble_time = time.time() - start

print(f"Merge sort: {merge_time:.6f}s")
print(f"Bubble sort: {bubble_time:.6f}s")
# Merge sort will be significantly faster

# Challenge
# Stability: When merging, we use `<=` (left comes first if equal).
# This preserves the original relative order of equal elements.
# To break stability, change to `<` (right comes first if equal).
```
</details>
