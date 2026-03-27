# Day 10: Selection Sort vs. Bubble Sort

**Learning Target:** I can implement selection sort and compare it to bubble sort in terms of swaps and performance.

---

## Key Concepts

**Selection Sort**: Find the smallest element and move it to the beginning. Repeat for the rest of the array.

**Key Difference from Bubble Sort:**
- **Bubble sort:** Many swaps, few passes
- **Selection sort:** Fewer swaps, same number of passes

**Comparison:**
```
               Bubble Sort      Selection Sort
Time Complexity    O(n²)            O(n²)
Swaps             O(n²)            O(n)
Best Case         O(n)             O(n²)
Stability         Stable           Not stable
```

**Stable?** If two elements are equal, does their relative order stay the same?
- Bubble sort (stable): Doesn't swap equal elements
- Selection sort (unstable): May change order of equal elements

---

## Code Examples

```python
# Selection Sort
def selection_sort(arr):
    """
    Find the smallest element and move it to the front.
    Repeat for remaining elements.
    """
    n = len(arr)

    for i in range(n):
        # Find the minimum element in the remaining array
        min_index = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j

        # Swap the found minimum with the first element
        arr[i], arr[min_index] = arr[min_index], arr[i]

    return arr

# Test
numbers = [64, 34, 25, 12, 22, 11, 90]
print(selection_sort(numbers))  # Output: [11, 12, 22, 25, 34, 64, 90]

# With visualization
def selection_sort_verbose(arr):
    """Show the state after each selection."""
    n = len(arr)
    print(f"Initial: {arr}")

    for i in range(n):
        min_index = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j

        arr[i], arr[min_index] = arr[min_index], arr[i]
        print(f"Step {i + 1}: {arr} (moved {arr[i]} to position {i})")

    return arr

# Comparison: Bubble vs. Selection with swap counting
def selection_sort_count(arr):
    n = len(arr)
    swaps = 0

    for i in range(n):
        min_index = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j

        if min_index != i:
            arr[i], arr[min_index] = arr[min_index], arr[i]
            swaps += 1

    return arr, swaps

# Test both
test_array_1 = [5, 2, 8, 1, 9, 3, 7]
test_array_2 = [5, 2, 8, 1, 9, 3, 7]

bubble_result, bubble_swaps = bubble_sort_count(test_array_1)
selection_result, selection_swaps = selection_sort_count(test_array_2)

print(f"Bubble sort: {bubble_swaps} swaps")
print(f"Selection sort: {selection_swaps} swaps")
# Output: Bubble sort: 10 swaps
#         Selection sort: 6 swaps

# Stability comparison
def demonstrate_stability():
    """Show that selection sort is NOT stable."""
    # List of tuples: (value, original_position)
    bubble_data = [(5, 'a'), (2, 'b'), (5, 'c'), (1, 'd')]
    selection_data = [(5, 'a'), (2, 'b'), (5, 'c'), (1, 'd')]

    # Bubble sort preserves relative order of equal elements
    n = len(bubble_data)
    for i in range(n):
        for j in range(0, n - i - 1):
            if bubble_data[j][0] > bubble_data[j + 1][0]:
                bubble_data[j], bubble_data[j + 1] = bubble_data[j + 1], bubble_data[j]

    # Selection sort might not
    n = len(selection_data)
    for i in range(n):
        min_index = i
        for j in range(i + 1, n):
            if selection_data[j][0] < selection_data[min_index][0]:
                min_index = j
        selection_data[i], selection_data[min_index] = selection_data[min_index], selection_data[i]

    print("Bubble sort (stable):", bubble_data)
    print("Selection sort (unstable):", selection_data)
```

---

## Guided Practice

**Step 1: Manual Trace Selection Sort**

Sort `[5, 2, 8, 1]`:
```
Initial: [5, 2, 8, 1]

Pass 1: Find min in [5, 2, 8, 1] → 1 at index 3
        Swap with index 0 → [1, 2, 8, 5]

Pass 2: Find min in [2, 8, 5] → 2 at index 1
        Already in place → [1, 2, 8, 5]

Pass 3: Find min in [8, 5] → 5 at index 3
        Swap with index 2 → [1, 2, 5, 8]

Pass 4: Done! [1, 2, 5, 8]
```

**Step 2: Count Comparisons**

Selection sort ALWAYS makes n(n-1)/2 comparisons (even for sorted data).
This is different from bubble sort, which can optimize for already-sorted data.

**Step 3: Compare Swaps**

For a reverse-sorted array of size n:
- Bubble sort: ~n²/2 swaps
- Selection sort: n-1 swaps (at most)

Why? Selection sort only swaps when placing the minimum in the correct position.

---

## Practice Problems

**Beginner:** Implement selection sort from scratch. Trace through `[7, 3, 9, 2]`.

**Intermediate:** Modify selection sort to also return the count of comparisons AND swaps. Compare to bubble sort on the same data.

**Challenge:** Explain why selection sort is NOT stable. Provide an example with equal elements where the order changes.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Outer loop from i=0 to n. Inner loop from i+1 to n to find minimum. Swap.
- **Intermediate:** Count comparisons in the inner loop. Count swaps when min_index != i.
- **Challenge:** Think about what happens when you swap an element with a minimum element that comes after an equal element.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_index = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j
        arr[i], arr[min_index] = arr[min_index], arr[i]
    return arr

# Trace: [7, 3, 9, 2]
# Pass 1: min=2 at index 3, swap with 7 → [2, 3, 9, 7]
# Pass 2: min=3 at index 1, already in place → [2, 3, 9, 7]
# Pass 3: min=7 at index 3, swap with 9 → [2, 3, 7, 9]
# Pass 4: Done → [2, 3, 7, 9]

# Intermediate
def selection_sort_count(arr):
    n = len(arr)
    comparisons = 0
    swaps = 0

    for i in range(n):
        min_index = i
        for j in range(i + 1, n):
            comparisons += 1
            if arr[j] < arr[min_index]:
                min_index = j

        if min_index != i:
            arr[i], arr[min_index] = arr[min_index], arr[i]
            swaps += 1

    return arr, comparisons, swaps

# Challenge - Stability example
data = [(5, 'first_5'), (2, 'two'), (5, 'second_5')]
# Bubble sort keeps them in order: [(2, 'two'), (5, 'first_5'), (5, 'second_5')]
# Selection sort might change order: [(2, 'two'), (5, 'second_5'), (5, 'first_5')]
# Because when we swap to find the minimum, we change relative positions.
```
</details>
