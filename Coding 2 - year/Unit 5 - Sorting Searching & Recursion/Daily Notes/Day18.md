# Day 18: Quick Sort Applications & Hybrid Approaches

**Learning Target:** I can optimize sorting for specific use cases and combine algorithms strategically.

---

## Key Concepts

**Adaptive Sorting:**
- Choose algorithm based on input characteristics
- Example: Check if array is small (use insertion), nearly sorted (use insertion), or large random (use quick/merge)

**Hybrid Approaches:**
- **Introsort:** Start with quick sort, switch to heap sort if recursion gets too deep (prevents O(n²) worst case)
- **Timsort:** Use insertion sort for small chunks, merge chunks with merge sort
- **3-way Quick Sort:** Optimize for arrays with many duplicates

**Practical Considerations:**
- Memory bandwidth is slow (cache matters)
- Stability requirements (financial data, stable sorts preferred)
- Partially sorted data (insertion sort dominates)
- Distribution of data (quick sort with good pivot selection)

---

## Code Examples

```python
# Introsort: Quick sort with heap sort fallback
import heapq

def introsort(arr):
    """Hybrid: quick sort with heap sort fallback."""
    introsort_helper(arr, 0, len(arr) - 1, 2 * len(arr).bit_length())
    return arr

def introsort_helper(arr, low, high, depth_limit):
    while low < high:
        if depth_limit == 0:
            # Depth limit exceeded, switch to heap sort
            heapsort(arr, low, high)
            return

        # Use quick sort
        pivot_index = partition(arr, low, high)

        # Recursively sort the smaller partition
        # to limit recursion depth
        if pivot_index - low < high - pivot_index:
            introsort_helper(arr, low, pivot_index - 1, depth_limit - 1)
            low = pivot_index + 1
        else:
            introsort_helper(arr, pivot_index + 1, high, depth_limit - 1)
            high = pivot_index - 1

        depth_limit -= 1

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

def heapsort(arr, low, high):
    """Heap sort for introsort fallback."""
    # Convert subarray to heap and extract
    def heapify(arr, n, i, low):
        smallest = i
        left = 2 * i + 1
        right = 2 * i + 2

        if left < n and arr[low + left] < arr[low + smallest]:
            smallest = left
        if right < n and arr[low + right] < arr[low + smallest]:
            smallest = right

        if smallest != i:
            arr[low + i], arr[low + smallest] = arr[low + smallest], arr[low + i]
            heapify(arr, n, smallest, low)

    n = high - low + 1
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i, low)

    for i in range(n - 1, 0, -1):
        arr[low], arr[low + i] = arr[low + i], arr[low]
        heapify(arr, i, 0, low)

# Timsort-inspired approach
MIN_RUN = 32

def timsort_simple(arr):
    """Simplified Timsort: insertion sort chunks, merge them."""
    # Step 1: Sort small runs with insertion sort
    for start in range(0, len(arr), MIN_RUN):
        end = min(start + MIN_RUN, len(arr))
        insertion_sort_range(arr, start, end)

    # Step 2: Merge runs
    current_size = MIN_RUN
    while current_size < len(arr):
        for start in range(0, len(arr), current_size * 2):
            mid = start + current_size
            end = min(start + current_size * 2, len(arr))

            if mid < end:
                merge_range(arr, start, mid, end)

        current_size *= 2

    return arr

def insertion_sort_range(arr, start, end):
    """Insertion sort on arr[start:end]."""
    for i in range(start + 1, end):
        key = arr[i]
        j = i - 1
        while j >= start and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key

def merge_range(arr, start, mid, end):
    """Merge arr[start:mid] with arr[mid:end]."""
    left = arr[start:mid]
    right = arr[mid:end]

    i = j = 0
    k = start

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            arr[k] = left[i]
            i += 1
        else:
            arr[k] = right[j]
            j += 1
        k += 1

    arr[k:end] = left[i:] + right[j:]

# Adaptive sort selector
def adaptive_sort(arr):
    """Choose algorithm based on array characteristics."""
    n = len(arr)

    # Check sortedness
    sorted_count = sum(1 for i in range(n - 1) if arr[i] <= arr[i + 1])
    sortedness = sorted_count / (n - 1) if n > 1 else 1

    # Check duplicates
    unique = len(set(arr))
    dup_ratio = 1 - (unique / n)

    # Decision
    if n < 50:
        insertion_sort(arr)
    elif sortedness > 0.9:
        insertion_sort(arr)
    elif dup_ratio > 0.4:
        three_way_quick_sort(arr, 0, n - 1)
    elif n > 100000:
        merge_sort(arr)
    else:
        introsort(arr)

    return arr

def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
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

def three_way_quick_sort(arr, low, high):
    """Quick sort optimized for duplicates."""
    if low < high:
        lt, gt = partition_three_way(arr, low, high)
        three_way_quick_sort(arr, low, lt - 1)
        three_way_quick_sort(arr, gt + 1, high)

def partition_three_way(arr, low, high):
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
```

---

## Guided Practice

**Activity 1: Understand Introsort**

Why does introsort switch to heap sort? When would this matter?
- On a random array, quick sort almost always gives O(n log n)
- On a pathological input, quick sort degrades to O(n²)
- Introsort guarantees O(n log n) always

**Activity 2: Timsort Advantage**

Why does Timsort (insertion + merge) work well for real data?
- Real data is often partially sorted or in chunks
- Insertion sort is very fast on small, nearly-sorted arrays
- Merging is predictable and cache-friendly

**Activity 3: Choose Algorithm for Scenario**

```
Array characteristics: 1 million integers, 60% already sorted
Choice: Insertion sort? Quick sort? Merge sort? Adaptive?
```

---

## Practice Problems

**Beginner:** Implement timsort_simple and test it on a 1000-element array. Compare to quick sort.

**Intermediate:** Add a depth counter to quick sort. At what depth does it typically exceed the limit before introsort switches?

**Challenge:** Implement adaptive_sort that analyzes the array and chooses the best algorithm. Log which algorithm is chosen for various inputs.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Timsort code above works; just time it vs. quick sort.
- **Intermediate:** In introsort_helper, count how many times depth_limit decreases.
- **Challenge:** Analyze sortedness and duplicate ratio, then make a decision.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner - timsort_simple code above

# Intermediate
def introsort_with_depth(arr):
    max_depth = [0]
    def helper(arr, low, high, depth_limit, current_depth=0):
        max_depth[0] = max(max_depth[0], current_depth)
        if depth_limit == 0:
            return heapsort(arr, low, high)
        # ... rest of logic

    helper(arr, 0, len(arr)-1, 2*len(arr).bit_length())
    return arr, max_depth[0]

# Challenge
def adaptive_sort_verbose(arr):
    n = len(arr)
    sorted_count = sum(1 for i in range(n-1) if arr[i] <= arr[i+1])
    sortedness = sorted_count / (n-1) if n > 1 else 1
    unique = len(set(arr))
    dup_ratio = 1 - (unique/n)

    if n < 50:
        print(f"Chose: Insertion (small array)")
        insertion_sort(arr)
    elif sortedness > 0.9:
        print(f"Chose: Insertion (already {sortedness:.0%} sorted)")
        insertion_sort(arr)
    # ... etc
```
</details>
