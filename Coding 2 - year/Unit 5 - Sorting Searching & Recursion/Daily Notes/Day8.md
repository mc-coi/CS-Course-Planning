# Day 8: Bubble Sort Algorithm & Visualization

**Learning Target:** I can implement bubble sort, visualize how it works, and explain its O(n²) complexity.

---

## Key Concepts

**Bubble Sort**: Repeatedly steps through the list, compares adjacent elements, and swaps them if they're in the wrong order. The largest element "bubbles up" to the end after each pass.

**How it works:**
```
Pass 1: Compare pairs, swap if needed. Largest element ends up at the end.
Pass 2: Repeat for remaining elements (excluding last). Second largest now at position n-1.
Pass 3: Continue until the list is sorted.
```

**Time Complexity:**
- Best case: O(n) — if list is already sorted (with optimization)
- Average case: O(n²) — typical case
- Worst case: O(n²) — if list is sorted backwards

**Space Complexity:** O(1) — sorts in place, doesn't need extra space.

---

## Code Examples

```python
# Basic Bubble Sort
def bubble_sort(arr):
    """Sort array using bubble sort. Modifies in place."""
    n = len(arr)

    # Outer loop: number of passes
    for i in range(n):
        # Inner loop: compare adjacent pairs
        for j in range(0, n - i - 1):
            # Swap if the current element is greater than the next
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

    return arr

# Test
numbers = [64, 34, 25, 12, 22, 11, 90]
print(bubble_sort(numbers))  # Output: [11, 12, 22, 25, 34, 64, 90]

# Optimized Bubble Sort with early exit
def bubble_sort_optimized(arr):
    """Bubble sort that stops early if array becomes sorted."""
    n = len(arr)

    for i in range(n):
        swapped = False  # Track if any swaps happened
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True

        # If no swaps happened, array is already sorted
        if not swapped:
            break

    return arr

# Test
already_sorted = [1, 2, 3, 4, 5]
print(bubble_sort_optimized(already_sorted))  # Output: [1, 2, 3, 4, 5]

# Bubble Sort with step-by-step visualization
def bubble_sort_verbose(arr):
    """Show the state of the array after each pass."""
    n = len(arr)

    for i in range(n):
        print(f"Pass {i + 1}: {arr}")
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                print(f"  Swap {arr[j + 1]} and {arr[j]}: {arr}")

    print(f"Sorted: {arr}")
    return arr

# Test with visualization
print("Sorting [5, 2, 8, 1, 9]:")
bubble_sort_verbose([5, 2, 8, 1, 9])
```

---

## Guided Practice

**Step 1: Manual Trace**

Sort `[5, 2, 4, 1]` using bubble sort by hand.

```
Initial: [5, 2, 4, 1]

Pass 1:
  Compare 5 and 2 → swap → [2, 5, 4, 1]
  Compare 5 and 4 → swap → [2, 4, 5, 1]
  Compare 5 and 1 → swap → [2, 4, 1, 5]  ← 5 is in place

Pass 2:
  Compare 2 and 4 → no swap → [2, 4, 1, 5]
  Compare 4 and 1 → swap → [2, 1, 4, 5]  ← 4 is in place

Pass 3:
  Compare 2 and 1 → swap → [1, 2, 4, 5]  ← 2 is in place

Pass 4:
  No comparisons needed → [1, 2, 4, 5] sorted!
```

**Step 2: Count Comparisons**

For an array of size n:
- Pass 1: n-1 comparisons
- Pass 2: n-2 comparisons
- ...
- Total: (n-1) + (n-2) + ... + 1 = n(n-1)/2 ≈ n²/2

**Step 3: Why O(n²)?**

Even if you divide n² by 2, it's still O(n²) because constants don't matter in Big O.

---

## Practice Problems

**Beginner:** Implement basic bubble sort (non-optimized) and sort `[9, 3, 7, 1, 5]`.

**Intermediate:** Add a counter to track the number of comparisons and swaps. How many of each for a 10-element array?

**Challenge:** The optimized version uses `swapped` flag to stop early. Explain why this makes it O(n) in the best case. When does this optimization help the most?

<details>
<summary>💡 Hints</summary>
- **Beginner:** Follow the code structure above. Remember that `arr[j], arr[j+1] = arr[j+1], arr[j]` swaps two elements.
- **Intermediate:** Initialize `comparisons = 0` and `swaps = 0`. Increment in the appropriate places.
- **Challenge:** If the array is already sorted, `swapped` stays False and the loop breaks after the first pass, which is O(n) (just one iteration of the outer loop).
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

# Intermediate
def bubble_sort_count(arr):
    n = len(arr)
    comparisons = 0
    swaps = 0

    for i in range(n):
        for j in range(0, n - i - 1):
            comparisons += 1
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swaps += 1

    return arr, comparisons, swaps

result, comps, swps = bubble_sort_count([9, 3, 7, 1, 5])
print(f"Sorted: {result}, Comparisons: {comps}, Swaps: {swps}")
# Output: Sorted: [1, 3, 5, 7, 9], Comparisons: 10, Swaps: 7

# Challenge
# If array is already sorted, the swapped flag stays False.
# Outer loop runs once (i = 0), inner loop makes n-1 comparisons, no swaps.
# Then the if not swapped: break triggers, exiting immediately.
# This is O(n) because we only did n-1 comparisons total (one pass).
```
</details>
