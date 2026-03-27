# Day 12: Insertion Sort & When to Use Each Algorithm

**Learning Target:** I can choose the right sorting algorithm based on data size, current order, and performance needs.

---

## Key Concepts

**Algorithm Selection Criteria:**
1. **Input size:** Small (< 100) vs. large (> 1000)
2. **Current order:** Sorted, reversed, or random
3. **Memory:** Can we use extra space?
4. **Stability:** Does order of equal elements matter?
5. **Speed:** Do we need O(n log n) or is O(n²) acceptable?

**Quick Decision Table:**
```
Size < 50              → Insertion sort or bubble sort
Size > 1000            → Merge sort or quick sort (O(n log n))
Nearly sorted          → Insertion sort (O(n) best case)
Need stability         → Merge sort or insertion sort
Memory is scarce       → Selection sort or quick sort (in-place)
```

---

## Code Examples

```python
# Performance comparison function
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
        min_index = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j
        arr[i], arr[min_index] = arr[min_index], arr[i]
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

def insertion_sort_optimized(arr):
    """Insertion sort with early exit for sorted data."""
    n = len(arr)
    is_sorted = True

    for i in range(1, n):
        key = arr[i]
        j = i - 1

        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
            is_sorted = False

        arr[j + 1] = key

        # If no out-of-order elements found, it's sorted
        if is_sorted and i == n - 1:
            return arr

    return arr

# Compare performance
def compare_algorithms():
    # Test 1: Small random array (50 elements)
    small_random = [random.randint(1, 100) for _ in range(50)]

    algorithms = {
        'Bubble': bubble_sort,
        'Selection': selection_sort,
        'Insertion': insertion_sort,
    }

    print("Test 1: 50 random elements")
    for name, algo in algorithms.items():
        start = time.time()
        algo(small_random.copy())
        elapsed = time.time() - start
        print(f"  {name}: {elapsed:.6f}s")

    # Test 2: Nearly sorted array (100 elements)
    nearly_sorted = list(range(1, 101))
    random.shuffle(nearly_sorted)
    # Shuffle only 10% of positions
    for _ in range(5):
        i = random.randint(0, len(nearly_sorted) - 1)
        j = random.randint(0, len(nearly_sorted) - 1)
        nearly_sorted[i], nearly_sorted[j] = nearly_sorted[j], nearly_sorted[i]

    print("\nTest 2: 100 nearly sorted elements")
    for name, algo in algorithms.items():
        start = time.time()
        algo(nearly_sorted.copy())
        elapsed = time.time() - start
        print(f"  {name}: {elapsed:.6f}s")

    # Test 3: Already sorted (insertion sort advantage)
    already_sorted = list(range(1, 101))

    print("\nTest 3: 100 already sorted elements")
    for name, algo in algorithms.items():
        start = time.time()
        algo(already_sorted.copy())
        elapsed = time.time() - start
        print(f"  {name}: {elapsed:.6f}s")

# Recommendation guide
def recommend_algorithm(arr):
    """Suggest best algorithm based on array properties."""
    n = len(arr)

    # Check if nearly sorted
    sorted_count = sum(1 for i in range(len(arr) - 1) if arr[i] <= arr[i + 1])
    is_nearly_sorted = sorted_count > 0.8 * len(arr)

    if n < 50:
        return "Insertion sort (small size, simple)"
    elif is_nearly_sorted:
        return "Insertion sort (nearly sorted, adaptive)"
    elif n < 1000:
        return "Selection sort (simple, no extra memory)"
    else:
        return "Merge sort or Quick sort (large size, O(n log n))"

# Test recommendation
test_arrays = [
    [5, 2, 8, 1, 9],
    [1, 2, 3, 4, 5],
    list(range(100, 0, -1))
]

for arr in test_arrays:
    print(f"Array size {len(arr)}: {recommend_algorithm(arr)}")
```

---

## Guided Practice

**Activity 1: Performance Testing**

Run the comparison code above (or time it manually). For a 50-element array:
- Which algorithm is fastest?
- By how much?

**Activity 2: Best Case Analysis**

For each algorithm, what's the input that gives the BEST performance?
- Bubble sort: Already sorted (with optimization)
- Selection sort: Any order (always O(n²))
- Insertion sort: Already sorted (O(n))

**Activity 3: Choose the Algorithm**

For each scenario, pick the best algorithm:
1. Sorting 10 student IDs for a homework assignment
2. Sorting 1 million customer records by zipcode
3. Sorting real-time sensor data that's mostly in order
4. Teaching beginners about sorting

---

## Practice Problems

**Beginner:** Implement all three algorithms (bubble, selection, insertion) and test them on `[9, 3, 7, 1, 5]`. Which makes the fewest swaps?

**Intermediate:** Write a function that detects if an array is nearly sorted (>90% sorted). Use this to recommend which algorithm to use.

**Challenge:** For an array of size n that is k% sorted, estimate the number of operations for each algorithm. When is insertion sort faster than selection sort?

<details>
<summary>💡 Hints</summary>
- **Beginner:** Count swaps by incrementing a counter each time two elements are exchanged.
- **Intermediate:** Count how many adjacent pairs are in correct order. If > 90%, call it nearly sorted.
- **Challenge:** Insertion sort improves when k is high (fewer elements out of place). Selection sort is constant O(n²) regardless of k.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner - Compare swaps
def test_all_three(arr):
    test_copies = [arr.copy() for _ in range(3)]

    # Bubble
    swaps = 0
    for i in range(len(test_copies[0])):
        for j in range(0, len(test_copies[0]) - i - 1):
            if test_copies[0][j] > test_copies[0][j + 1]:
                test_copies[0][j], test_copies[0][j + 1] = test_copies[0][j + 1], test_copies[0][j]
                swaps += 1
    print(f"Bubble: {swaps} swaps")

    # Selection (similar tracking)
    # Insertion (similar tracking)

# Intermediate
def is_nearly_sorted(arr, threshold=0.9):
    if len(arr) < 2:
        return True
    correct_pairs = sum(1 for i in range(len(arr) - 1) if arr[i] <= arr[i + 1])
    return correct_pairs / (len(arr) - 1) >= threshold

# Challenge
# For k% sorted array:
# Insertion sort: Operations ≈ k * (n-1) + (1-k) * n²/2
#                 → O(n) when k=100%, O(n²) when k=0%
# Selection sort: Always (n-1) + (n-2) + ... + 1 = n²/2
#                 → O(n²) always
# Insertion is faster when k is high (almost sorted)
```
</details>
