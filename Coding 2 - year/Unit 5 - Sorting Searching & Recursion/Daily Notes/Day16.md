# Day 16: Quick Sort Implementation & Worst Case

**Learning Target:** I can implement quick sort efficiently and understand its worst-case behavior.

---

## Key Concepts

**Quick Sort Complexity Analysis:**
- **Best/Average: O(n log n)** — pivot splits array evenly
- **Worst: O(n²)** — pivot is always smallest or largest

**Worst Case Example:**
```
Sorted array: [1, 2, 3, 4, 5]
Using last element as pivot each time:
  Partition around 5 → [1, 2, 3, 4] | 5
  Partition around 4 → [1, 2, 3] | 4 | 5
  ...continues degrades to O(n²)
```

**Why It's Still Popular:**
- Average case is O(n log n)
- In-place (uses O(log n) space)
- Cache-friendly
- Easy to randomize for worst-case resistance

**Randomization:** Using random pivot selection makes worst case O(n²) probability negligible

---

## Code Examples

```python
# Complete quick sort implementation
def quick_sort(arr):
    quick_sort_helper(arr, 0, len(arr) - 1)
    return arr

def quick_sort_helper(arr, low, high):
    if low < high:
        pivot_index = partition(arr, low, high)
        quick_sort_helper(arr, low, pivot_index - 1)
        quick_sort_helper(arr, pivot_index + 1, high)

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

# Random pivot variant
import random

def quick_sort_random(arr):
    quick_sort_random_helper(arr, 0, len(arr) - 1)
    return arr

def quick_sort_random_helper(arr, low, high):
    if low < high:
        pivot_index = partition_random(arr, low, high)
        quick_sort_random_helper(arr, low, pivot_index - 1)
        quick_sort_random_helper(arr, pivot_index + 1, high)

def partition_random(arr, low, high):
    # Choose random pivot
    random_index = random.randint(low, high)
    arr[random_index], arr[high] = arr[high], arr[random_index]
    return partition(arr, low, high)

# Test performance on worst case
import time

def test_quick_sort():
    # Worst case: sorted array
    sorted_arr = list(range(1, 101))

    print("Performance on sorted array (worst case):")

    # Standard quick sort
    arr1 = sorted_arr.copy()
    start = time.time()
    quick_sort(arr1)
    std_time = time.time() - start
    print(f"  Standard: {std_time:.6f}s")

    # Random pivot quick sort
    arr2 = sorted_arr.copy()
    start = time.time()
    quick_sort_random(arr2)
    rand_time = time.time() - start
    print(f"  Random pivot: {rand_time:.6f}s")

# Comparison with merge sort
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
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

def compare_quick_and_merge():
    print("Quick Sort vs. Merge Sort:")
    print("Array Type      | Quick Sort | Merge Sort")
    print("----------------|------------|----------")

    test_cases = [
        ("Random", [random.randint(1, 100) for _ in range(100)]),
        ("Sorted", list(range(1, 101))),
        ("Reverse", list(range(100, 0, -1))),
    ]

    for name, arr in test_cases:
        # Quick sort (with random pivot to handle worst case)
        start = time.time()
        quick_sort_random(arr.copy())
        quick_time = time.time() - start

        # Merge sort
        start = time.time()
        merge_sort(arr.copy())
        merge_time = time.time() - start

        print(f"{name:15} | {quick_time:.6f}s | {merge_time:.6f}s")

# Count swaps and comparisons
def quick_sort_count_ops(arr, low=None, high=None):
    """Quick sort that counts operations."""
    if low is None:
        low = 0
    if high is None:
        high = len(arr) - 1

    comparisons = 0
    swaps = 0

    def partition_count(arr, low, high):
        nonlocal comparisons, swaps
        pivot = arr[high]
        i = low - 1
        for j in range(low, high):
            comparisons += 1
            if arr[j] < pivot:
                i += 1
                arr[i], arr[j] = arr[j], arr[i]
                swaps += 1
        arr[i + 1], arr[high] = arr[high], arr[i + 1]
        swaps += 1
        return i + 1

    def sort_helper(arr, low, high):
        nonlocal comparisons, swaps
        if low < high:
            pivot_index = partition_count(arr, low, high)
            sort_helper(arr, low, pivot_index - 1)
            sort_helper(arr, pivot_index + 1, high)

    sort_helper(arr, low, high)
    return arr, comparisons, swaps
```

---

## Guided Practice

**Activity 1: Worst Case Demonstration**

Sort `[1, 2, 3, 4, 5]` with standard quick sort (last element pivot).

Count the recursion levels. Compare to merge sort (should be much more shallow).

**Activity 2: Compare Pivot Strategies**

For a sorted array of 20 elements, trace the first two partition calls with:
1. Last element pivot
2. Random pivot
3. Middle element pivot

Which tends to give more balanced splits?

**Activity 3: Why Random Pivot Helps**

Probability analysis: if we choose pivots randomly, the chance of always getting terrible splits approaches zero as n grows.

---

## Practice Problems

**Beginner:** Implement quick sort from scratch. Test on `[9, 3, 7, 1, 5]`.

**Intermediate:** Add operation counting (comparisons and swaps). Compare to merge sort on same data.

**Challenge:** Implement the three-way partition (elements < pivot, == pivot, > pivot). Why does this help with duplicate values?

<details>
<summary>💡 Hints</summary>
- **Beginner:** Two nested loops: one recursively sorts left, one sorts right.
- **Intermediate:** Count inside partition function and recursively sum counts.
- **Challenge:** Three-way partition avoids redundantly sorting equal elements.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner - standard implementation as shown above

# Intermediate - shown above with quick_sort_count_ops

# Challenge - Three-way partition
def partition_three_way(arr, low, high):
    """Partition into <, ==, > pivot. Returns (lt, gt) indices."""
    pivot = arr[low]
    lt = low
    gt = high
    i = low + 1

    while i <= gt:
        if arr[i] < pivot:
            arr[lt], arr[i] = arr[i], arr[lt]
            lt += 1
            i += 1
        elif arr[i] > pivot:
            arr[i], arr[gt] = arr[gt], arr[i]
            gt -= 1
        else:
            i += 1

    return lt, gt

# Three-way quick sort
def quick_sort_three_way(arr, low=None, high=None):
    if low is None:
        low = 0
    if high is None:
        high = len(arr) - 1

    if low < high:
        lt, gt = partition_three_way(arr, low, high)
        quick_sort_three_way(arr, low, lt - 1)
        quick_sort_three_way(arr, gt + 1, high)

    return arr

# Benefits: Duplicates are grouped together, not sorted recursively
```
</details>
