# Day 17: Quick Sort Analysis & Algorithm Comparison

**Learning Target:** I can compare quick sort, merge sort, bubble, and selection sort in terms of performance and use cases.

---

## Key Concepts

**Quick Sort Strengths:**
- Fast average case: O(n log n)
- In-place: uses only O(log n) extra space
- Cache-friendly (good locality of reference)
- Most practical sorting algorithm

**Quick Sort Weaknesses:**
- Worst case O(n²) (though rare with random pivot)
- Not stable
- Needs random number generation for best performance
- More complex than merge sort

**When Each Sort Excels:**
```
Algorithm      | Time Best | Time Avg  | Time Worst | Space | Stable | Use Case
---------------|-----------|-----------|-----------|-------|--------|------------------
Bubble         | O(n)      | O(n²)     | O(n²)     | O(1)  | Yes    | Teaching, tiny
Selection      | O(n²)     | O(n²)     | O(n²)     | O(1)  | No     | Memory limited
Insertion      | O(n)      | O(n²)     | O(n²)     | O(1)  | Yes    | Nearly sorted
Merge          | O(n log n)| O(n log n)| O(n log n)| O(n)  | Yes    | External sort, stable needed
Quick          | O(n log n)| O(n log n)| O(n²)     | O(log n)| No   | General purpose, fast
```

---

## Code Examples

```python
# Comparison framework
import time
import random

def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
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

def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[random.randint(0, len(arr) - 1)]
    less = [x for x in arr if x < pivot]
    equal = [x for x in arr if x == pivot]
    greater = [x for x in arr if x > pivot]
    return quick_sort(less) + equal + quick_sort(greater)

# Comprehensive performance test
def benchmark_sorts():
    print("BENCHMARK: Various Array Sizes and Types\n")

    for size in [50, 200, 1000]:
        print(f"Array Size: {size}")
        print("-" * 70)

        # Generate test arrays
        random_arr = [random.randint(1, 1000) for _ in range(size)]
        sorted_arr = list(range(size))
        reverse_arr = list(range(size, 0, -1))

        algorithms = [
            ('Bubble', bubble_sort),
            ('Selection', selection_sort),
            ('Insertion', insertion_sort),
            ('Merge', merge_sort),
            ('Quick', quick_sort),
        ]

        for arr_type, arr in [('Random', random_arr), ('Sorted', sorted_arr), ('Reverse', reverse_arr)]:
            print(f"\n  {arr_type}:")

            for name, algo in algorithms:
                # Skip slow algorithms for large sizes
                if size > 200 and name in ['Bubble', 'Selection']:
                    print(f"    {name:10} : (skipped - too slow)")
                    continue

                try:
                    start = time.time()
                    result = algo(arr.copy())
                    elapsed = time.time() - start
                    print(f"    {name:10} : {elapsed:.6f}s")
                except Exception as e:
                    print(f"    {name:10} : Error - {e}")

# Analysis by data characteristics
def analyze_algorithm_choice(arr):
    """Recommend an algorithm based on array properties."""
    n = len(arr)

    # Check if sorted
    is_sorted = all(arr[i] <= arr[i + 1] for i in range(len(arr) - 1))

    # Check if reverse sorted
    is_reverse = all(arr[i] >= arr[i + 1] for i in range(len(arr) - 1))

    # Count duplicates
    unique = len(set(arr))
    dup_ratio = 1 - (unique / n)

    print(f"Array Analysis:")
    print(f"  Size: {n}")
    print(f"  Sorted: {is_sorted}, Reverse: {is_reverse}")
    print(f"  Duplicate ratio: {dup_ratio:.1%}")

    # Recommend
    if n < 50:
        return "Insertion sort (small)"
    elif is_sorted:
        return "Insertion sort (already sorted, O(n))"
    elif dup_ratio > 0.3:
        return "Three-way quick sort (many duplicates)"
    elif n > 10000:
        return "Merge sort (large, guaranteed O(n log n))"
    else:
        return "Quick sort (general purpose)"
```

---

## Guided Practice

**Activity 1: Fill in the Decision Table**

Create a table showing which algorithm is best for:
- Small arrays (< 50 elements)
- Large arrays (> 10,000)
- Nearly sorted arrays
- Arrays with many duplicates
- When memory is limited
- When stability is required

**Activity 2: Real-World Scenarios**

For each scenario, choose the best algorithm and justify:
1. Sorting 5 test scores
2. Sorting 1 million student records by ID
3. Sorting streaming data (elements arrive over time)
4. Sorting linked list nodes
5. External merge (data doesn't fit in RAM)

**Activity 3: Empirical Testing**

Run the benchmark code above and observe which algorithms dominate different scenarios. Do the results match your expectations?

---

## Practice Problems

**Beginner:** Write a function that tests all 5 algorithms on an array of size 100 and returns the fastest one's name.

**Intermediate:** Create a function that selects the "best" algorithm based on array size, sortedness, and duplicate count.

**Challenge:** Implement Timsort (Python's actual sort): use insertion sort for small chunks, then merge them with merge sort.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Time each algorithm and compare results.
- **Intermediate:** Use thresholds: if size < 50 use insertion, else if nearly sorted use insertion, else use quick.
- **Challenge:** Timsort: sort chunks of size ~64 with insertion, then merge chunks together.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def find_fastest(arr):
    algorithms = {
        'bubble': bubble_sort,
        'selection': selection_sort,
        'insertion': insertion_sort,
        'merge': merge_sort,
        'quick': quick_sort
    }

    fastest = None
    fastest_time = float('inf')

    for name, algo in algorithms.items():
        start = time.time()
        algo(arr.copy())
        elapsed = time.time() - start

        if elapsed < fastest_time:
            fastest = name
            fastest_time = elapsed

    return fastest

# Intermediate
def choose_best_sort(arr):
    n = len(arr)
    is_sorted = all(arr[i] <= arr[i+1] for i in range(n-1))

    if n < 50 or is_sorted:
        return insertion_sort
    else:
        return quick_sort
```
</details>
