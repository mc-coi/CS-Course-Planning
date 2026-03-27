# Day 15: Quick Sort - Pivot & Partition

**Learning Target:** I can implement quick sort and explain the pivot/partition strategy.

---

## Key Concepts

**Quick Sort Strategy:**
1. Choose a **pivot** element
2. **Partition** the array: put all elements < pivot on the left, all elements > pivot on the right
3. Recursively sort the left and right partitions

**Time Complexity:**
- Best case: O(n log n) — balanced partition each time
- Average case: O(n log n)
- Worst case: O(n²) — if pivot is always the smallest/largest
- Space: O(log n) — recursion depth (not counting the array)

**Pivot Selection:**
- First element: simple but bad on sorted data
- Last element: similar to first
- Middle element: slightly better
- Random element: good but adds complexity
- Median-of-three: balance of speed and partition quality

**Stability:** NOT stable (equal elements might swap)

---

## Code Examples

```python
# Quick Sort with last element as pivot
def quick_sort(arr):
    """Quick sort wrapper."""
    quick_sort_helper(arr, 0, len(arr) - 1)
    return arr

def quick_sort_helper(arr, low, high):
    """Recursively sort using quick sort."""
    if low < high:
        # Partition and get pivot index
        pivot_index = partition(arr, low, high)

        # Recursively sort left and right partitions
        quick_sort_helper(arr, low, pivot_index - 1)
        quick_sort_helper(arr, pivot_index + 1, high)

def partition(arr, low, high):
    """
    Partition array around pivot.
    Returns the final index of the pivot.
    """
    pivot = arr[high]  # Choose last element as pivot
    i = low - 1  # Index of smaller element

    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    # Place pivot in its correct position
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

# Test
numbers = [64, 34, 25, 12, 22, 11, 90]
print(quick_sort(numbers.copy()))  # Output: [11, 12, 22, 25, 34, 64, 90]

# With visualization
def partition_verbose(arr, low, high):
    """Show partitioning process."""
    pivot = arr[high]
    print(f"Partitioning {arr[low:high+1]} around pivot {pivot}")

    i = low - 1

    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
            print(f"  Swap {arr[j]} and {arr[i]}: {arr[low:high+1]}")

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    print(f"  Pivot {pivot} at index {i + 1}: {arr[low:high+1]}\n")

    return i + 1

def quick_sort_verbose(arr, low=None, high=None, depth=0):
    """Quick sort with visualization."""
    if low is None:
        low = 0
    if high is None:
        high = len(arr) - 1

    indent = "  " * depth

    if low < high:
        print(f"{indent}Sort: {arr[low:high+1]}")
        pivot_index = partition_verbose(arr, low, high)

        print(f"{indent}Left partition: {arr[low:pivot_index]}")
        quick_sort_verbose(arr, low, pivot_index - 1, depth + 1)

        print(f"{indent}Right partition: {arr[pivot_index+1:high+1]}")
        quick_sort_verbose(arr, pivot_index + 1, high, depth + 1)

    return arr

# Pivot selection strategies
def quick_sort_random_pivot(arr, low, high):
    """Quick sort with random pivot selection."""
    if low < high:
        # Randomly choose pivot
        import random
        random_index = random.randint(low, high)
        arr[random_index], arr[high] = arr[high], arr[random_index]

        pivot_index = partition(arr, low, high)
        quick_sort_random_pivot(arr, low, pivot_index - 1)
        quick_sort_random_pivot(arr, pivot_index + 1, high)

def median_of_three(arr, low, high):
    """Choose median of first, middle, last as pivot."""
    mid = (low + high) // 2

    # Sort three elements
    if arr[low] > arr[mid]:
        arr[low], arr[mid] = arr[mid], arr[low]
    if arr[mid] > arr[high]:
        arr[mid], arr[high] = arr[high], arr[mid]
    if arr[low] > arr[mid]:
        arr[low], arr[mid] = arr[mid], arr[low]

    # Place median at end
    arr[mid], arr[high] = arr[high], arr[mid]
    return partition(arr, low, high)
```

---

## Guided Practice

**Step 1: Understand Partitioning**

Array: `[5, 2, 8, 1, 9, 3]`, partition around pivot 3 (last element):

```
Initial: [5, 2, 8, 1, 9, 3]
         i=-1, j=0

j=0: arr[0]=5, 5 < 3? No
j=1: arr[1]=2, 2 < 3? Yes, i becomes 0, swap arr[0] with arr[1] → [2, 5, 8, 1, 9, 3]
j=2: arr[2]=8, 8 < 3? No
j=3: arr[3]=1, 1 < 3? Yes, i becomes 1, swap arr[1] with arr[3] → [2, 1, 8, 5, 9, 3]
j=4: arr[4]=9, 9 < 3? No

Place pivot: i=1, swap arr[2] with arr[5] → [2, 1, 3, 5, 9, 8]
Pivot (3) is now at index 2.
```

**Step 2: Identify Left and Right Partitions**

From above: pivot at index 2
- Left partition: [2, 1]
- Right partition: [5, 9, 8]

**Step 3: Trace First Two Recursive Calls**

What pivot will be used for [2, 1]? For [5, 9, 8]?

---

## Practice Problems

**Beginner:** Implement quick sort using the last element as pivot. Trace through `[5, 2, 4, 1, 3]`.

**Intermediate:** Modify partition to count how many swaps are made. For which array configuration (sorted, reversed, random) are the most swaps needed?

**Challenge:** Implement the "median-of-three" pivot selection. Does it improve performance on sorted data compared to last-element pivot?

<details>
<summary>💡 Hints</summary>
- **Beginner:** Use the code structure above. Remember: low and high are indices, not values.
- **Intermediate:** Count swaps in the partition function. Test on arrays of different sizes.
- **Challenge:** Median-of-three helps avoid worst case on sorted or reverse-sorted data.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner - Quick sort basic implementation works as shown above
# Trace of [5, 2, 4, 1, 3]:
# Partition around 3: [2, 1, 3, 5, 4] → pivot at index 2
# Left: [2, 1], Right: [5, 4]
# Recursively sort...
# Final: [1, 2, 3, 4, 5]

# Intermediate
def partition_count_swaps(arr, low, high):
    pivot = arr[high]
    i = low - 1
    swaps = 0

    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
            swaps += 1

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    swaps += 1

    return i + 1, swaps

# Challenge - Median of three helps worst case:
# Sorted array [1,2,3,4,5] with last pivot: all comparisons
# Sorted array [1,2,3,4,5] with median-of-three: better balance
```
</details>
