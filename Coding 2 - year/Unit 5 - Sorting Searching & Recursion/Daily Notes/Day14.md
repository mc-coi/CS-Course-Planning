# Day 14: Merge Sort Implementation & Recursion Practice

**Learning Target:** I can implement merge sort from scratch and verify its O(n log n) performance.

---

## Key Concepts

**Merge Sort Recap:**
- Divide array in half recursively
- Sort the halves
- Merge the sorted halves back together
- Always O(n log n) — very predictable

**Call Stack Depth:** For array of size n, recursion depth is O(log n)
- Size 8: depth 3
- Size 16: depth 4
- Size 1,000,000: depth ~20

**Trade-offs:**
```
Pros:
  - O(n log n) guaranteed
  - Stable
  - Parallelizable (sort halves independently)

Cons:
  - Requires O(n) extra space
  - Slower than quick sort on average (more overhead)
  - Not adaptive (no faster on nearly sorted data)
```

---

## Code Examples

```python
# Complete merge sort implementation
def merge_sort(arr):
    """Top-level merge sort function."""
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    return merge(left, right)

def merge(left, right):
    """Merge two sorted arrays."""
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

# Performance testing
import time

def test_merge_sort_performance():
    """Test merge sort on different sizes."""
    for size in [100, 1000, 10000]:
        arr = list(range(size, 0, -1))  # Worst case: reverse sorted

        start = time.time()
        merge_sort(arr)
        elapsed = time.time() - start

        print(f"Size {size:6d}: {elapsed:.6f}s")

# test_merge_sort_performance()

# Counting operations
def merge_with_count(left, right):
    """Merge with operation counting."""
    result = []
    i = j = 0
    comparisons = 0

    while i < len(left) and j < len(right):
        comparisons += 1
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])

    return result, comparisons

def merge_sort_with_count(arr):
    """Merge sort with comparison counting."""
    if len(arr) <= 1:
        return arr, 0

    mid = len(arr) // 2
    left, left_comps = merge_sort_with_count(arr[:mid])
    right, right_comps = merge_sort_with_count(arr[mid:])

    merged, merge_comps = merge_with_count(left, right)

    return merged, left_comps + right_comps + merge_comps

# Compare to other sorts
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

def compare_sorts():
    """Compare merge sort to bubble sort on various sizes."""
    print("Array Size | Merge Sort | Bubble Sort")
    print("-----------|------------|------------")

    for size in [50, 100, 500, 1000]:
        arr = list(range(size, 0, -1))

        # Merge sort
        start = time.time()
        merge_sort(arr.copy())
        merge_time = time.time() - start

        # Bubble sort (skip very large sizes)
        if size <= 500:
            start = time.time()
            bubble_sort(arr.copy())
            bubble_time = time.time() - start
        else:
            bubble_time = float('inf')

        print(f"{size:9d} | {merge_time:.6f}s | {bubble_time:.6f}s")

# Recursion visualization
def merge_sort_tree(arr, depth=0):
    """Visualize the recursion tree."""
    indent = "  " * depth

    if len(arr) <= 1:
        print(f"{indent}Leaf: {arr}")
        return arr

    print(f"{indent}Sort: {arr}")

    mid = len(arr) // 2
    left = merge_sort_tree(arr[:mid], depth + 1)
    right = merge_sort_tree(arr[mid:], depth + 1)

    result = merge(left, right)
    print(f"{indent}Done: {result}")

    return result

# Example: merge_sort_tree([5, 2, 8, 1])
```

---

## Guided Practice

**Activity 1: Trace the Recursion**

For `[6, 3, 8, 2]`, draw the complete call stack:
```
merge_sort([6, 3, 8, 2])
├── merge_sort([6, 3])
│   ├── merge_sort([6]) → [6]
│   ├── merge_sort([3]) → [3]
│   └── merge([6], [3]) → [3, 6]
├── merge_sort([8, 2])
│   ├── merge_sort([8]) → [8]
│   ├── merge_sort([2]) → [2]
│   └── merge([8], [2]) → [2, 8]
└── merge([3, 6], [2, 8]) → [2, 3, 6, 8]
```

**Activity 2: Count Operations**

Manually count the number of comparisons in merge sort for `[4, 2, 3, 1]`.
- Merge [4] and [2]: 1 comparison
- Merge [3] and [1]: 1 comparison
- Merge [2, 4] and [1, 3]: 2 comparisons
- Total: 4 comparisons

Compare this to bubble sort (many more!).

**Activity 3: Recursion Depth**

For arrays of size 8, 16, 32, 64, 128, calculate the recursion depth needed.
- Size 8: log₂(8) = 3
- Size 16: log₂(16) = 4
- ...

---

## Practice Problems

**Beginner:** Implement merge sort from scratch. Test it on `[9, 3, 7, 1, 5]`.

**Intermediate:** Add a parameter to track and print the recursion depth at each step. What's the maximum depth for a 16-element array?

**Challenge:** Implement merge sort iteratively (bottom-up) instead of recursively. Start by merging subarrays of size 1, then 2, then 4, etc.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Follow the code structure above. Remember the base case: if array size <= 1, return it.
- **Intermediate:** Add a `depth` parameter and increment it in recursive calls. Print at each level.
- **Challenge:** Use a loop to process each "level" of merging. Start with subarrays of size 1, merge to size 2, then 4, etc., until the whole array is sorted.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

# Intermediate
def merge_sort_depth(arr, depth=0):
    if len(arr) <= 1:
        return arr, depth

    mid = len(arr) // 2
    left, left_depth = merge_sort_depth(arr[:mid], depth + 1)
    right, right_depth = merge_sort_depth(arr[mid:], depth + 1)

    result = merge(left, right)
    max_depth = max(left_depth, right_depth)
    print(f"Depth {max_depth}: merged arrays of size {len(left)} and {len(right)}")
    return result, max_depth

# Challenge - Iterative merge sort (bottom-up)
def merge_sort_iterative(arr):
    n = len(arr)
    current_size = 1

    while current_size < n:
        # Pick starting index of left sub array to be merged
        start = 0

        while start < n:
            # Find ending point of left subarray
            mid = min(start + current_size, n)

            # Find ending point of right subarray
            end = min(start + current_size * 2, n)

            # Merge subarrays arr[start...mid-1] and arr[mid...end-1]
            if mid < end:
                left = arr[start:mid]
                right = arr[mid:end]
                merged = merge(left, right)
                arr[start:end] = merged

            start += current_size * 2

        current_size *= 2

    return arr
```
</details>
