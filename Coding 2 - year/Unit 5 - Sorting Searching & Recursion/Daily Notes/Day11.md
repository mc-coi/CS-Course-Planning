# Day 11: Insertion Sort Algorithm

**Learning Target:** I can implement insertion sort and understand when it's more efficient than bubble/selection sort.

---

## Key Concepts

**Insertion Sort**: Build the sorted list one element at a time. Take each element and insert it into the correct position in the already-sorted portion.

**Analogy:** Like sorting playing cards in your hand. You pick up one card at a time and insert it in the correct position.

**Time Complexity:**
- Best case: O(n) — if already sorted (just scan, no insertions)
- Average case: O(n²)
- Worst case: O(n²) — if reverse sorted

**Why Use It?**
- Very efficient for small arrays or nearly sorted data
- Stable (preserves relative order of equal elements)
- Adaptive (faster on partially sorted data)
- Used in real sorting libraries (like Python's Timsort) for small subarrays

---

## Code Examples

```python
# Basic Insertion Sort
def insertion_sort(arr):
    """
    Build sorted list one element at a time.
    For each element, find its correct position and insert it.
    """
    for i in range(1, len(arr)):
        key = arr[i]  # Element to insert
        j = i - 1  # Last element of sorted portion

        # Shift elements greater than key to the right
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1

        # Insert key into its correct position
        arr[j + 1] = key

    return arr

# Test
numbers = [64, 34, 25, 12, 22, 11, 90]
print(insertion_sort(numbers))  # Output: [11, 12, 22, 25, 34, 64, 90]

# With visualization
def insertion_sort_verbose(arr):
    """Show the sorted portion growing."""
    n = len(arr)
    print(f"Initial: {arr}")
    print(f"Sorted: [{arr[0]}]\n")

    for i in range(1, n):
        key = arr[i]
        j = i - 1

        print(f"Step {i}: Insert {key} into {arr[:i]}")

        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1

        arr[j + 1] = key
        print(f"  Result: {arr}")
        print(f"  Sorted: {arr[:i+1]}\n")

    return arr

# Performance comparison with counting
def insertion_sort_count(arr):
    """Count comparisons and shifts."""
    comparisons = 0
    shifts = 0

    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1

        while j >= 0 and arr[j] > key:
            comparisons += 1
            arr[j + 1] = arr[j]
            shifts += 1
            j -= 1

        if j >= 0:
            comparisons += 1  # Last comparison that failed
        arr[j + 1] = key

    return arr, comparisons, shifts

# Test
test = [5, 2, 8, 1, 9, 3, 7]
sorted_arr, comps, shfts = insertion_sort_count(test.copy())
print(f"Comparisons: {comps}, Shifts: {shfts}")
```

---

## Guided Practice

**Step 1: Manual Trace**

Sort `[5, 2, 8, 1]` using insertion sort:
```
Initial: [5, 2, 8, 1]
Sorted portion: [5]

Step 1: Insert 2
  Compare 2 with 5 (5 > 2) → shift 5 right
  Insert 2 at position 0 → [2, 5, 8, 1]
Sorted portion: [2, 5]

Step 2: Insert 8
  Compare 8 with 5 (5 < 8) → no shift needed
  Insert 8 at position 2 → [2, 5, 8, 1]
Sorted portion: [2, 5, 8]

Step 3: Insert 1
  Compare 1 with 8 (8 > 1) → shift 8 right → [2, 5, 1, 8]
  Compare 1 with 5 (5 > 1) → shift 5 right → [2, 1, 5, 8]
  Compare 1 with 2 (2 > 1) → shift 2 right → [1, 2, 5, 8]
  Insert 1 at position 0 → [1, 2, 5, 8]
Sorted portion: [1, 2, 5, 8]
```

**Step 2: Best vs. Worst Case**

Best case (already sorted): Each comparison succeeds (arr[j] < key), so we break immediately. O(n).

Worst case (reverse sorted): Each element must be shifted all the way. O(n²).

**Step 3: Compare All Three Sorts**

Trace the same array `[3, 1, 4, 2]` using bubble, selection, and insertion sort. Which makes the fewest swaps?

---

## Practice Problems

**Beginner:** Implement insertion sort and sort `[7, 3, 9, 2, 5]` by hand, showing each step.

**Intermediate:** Write a function that counts comparisons AND shifts (movements). For which type of input data is insertion sort most efficient?

**Challenge:** Modify insertion sort to use binary search to find the correct insertion position. This is called **binary insertion sort**. Does it reduce the overall complexity?

<details>
<summary>💡 Hints</summary>
- **Beginner:** Start with i=1. For each i, find where arr[i] should go by comparing backwards.
- **Intermediate:** A shift is when you move an element. Compare to bubble/selection sort on the same data.
- **Challenge:** Binary search finds the position in O(log n), but you still need to shift elements, which is O(n). So overall it's still O(n²), but with fewer comparisons.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner & Intermediate
def insertion_sort_trace(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        comparisons = 0

        while j >= 0 and arr[j] > key:
            comparisons += 1
            arr[j + 1] = arr[j]
            j -= 1

        arr[j + 1] = key
        print(f"Step {i}: Inserted {key}, {comparisons} comparisons → {arr}")

insertion_sort_trace([7, 3, 9, 2, 5])

# Challenge - Binary Insertion Sort
def binary_insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]

        # Use binary search to find insertion position
        left, right = 0, i - 1
        while left <= right:
            mid = (left + right) // 2
            if arr[mid] > key:
                right = mid - 1
            else:
                left = mid + 1

        # Shift elements and insert
        for j in range(i - 1, left - 1, -1):
            arr[j + 1] = arr[j]
        arr[left] = key

    return arr

# Still O(n²) due to shifting, but fewer comparisons (O(n log n) comparisons).
```
</details>
