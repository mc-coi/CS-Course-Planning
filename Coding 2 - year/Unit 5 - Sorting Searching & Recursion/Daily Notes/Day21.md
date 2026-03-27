# Day 21: Algorithm Comparison & Selection Guide

**Learning Target:** I can choose the right algorithm for any sorting/searching problem and justify my choice.

---

## Key Concepts

**Comprehensive Algorithm Comparison:**

```
Algorithm    | Best Case  | Average    | Worst Case | Space | Stable | In-Place | Use When
-------------|------------|------------|------------|-------|--------|----------|------------------
Linear Search| O(n)       | O(n)       | O(n)       | O(1)  | —      | Yes      | Unsorted, small
Binary Search| O(1)       | O(log n)   | O(log n)   | O(1)  | —      | Yes      | Sorted data
Bubble Sort  | O(n)       | O(n²)      | O(n²)      | O(1)  | Yes    | Yes      | Teaching, tiny
Selection    | O(n²)      | O(n²)      | O(n²)      | O(1)  | No     | Yes      | Memory tight
Insertion    | O(n)       | O(n²)      | O(n²)      | O(1)  | Yes    | Yes      | Nearly sorted
Merge Sort   | O(n log n) | O(n log n) | O(n log n) | O(n)  | Yes    | No       | Need stable, guaranteed
Quick Sort   | O(n log n) | O(n log n) | O(n²)*    | O(log n)| No    | Yes      | General purpose
Heap Sort    | O(n log n) | O(n log n) | O(n log n) | O(1)  | No     | Yes      | Guaranteed + in-place
Timsort      | O(n)       | O(n log n) | O(n log n) | O(n)  | Yes    | No       | Real-world data (Python)
```

*With random pivot selection

**Decision Tree for Sorting:**

```
Is array very small (< 50)?
  ├─ Yes → Insertion sort (simple, fast on small)
  └─ No → Continue...

Is array nearly sorted?
  ├─ Yes → Insertion sort (O(n) best case)
  └─ No → Continue...

Do you need stability?
  ├─ Yes → Merge sort or Timsort
  └─ No → Continue...

Is memory very limited?
  ├─ Yes → Quick sort or Selection sort
  └─ No → Continue...

Use: Quick sort (average O(n log n), in-place) or Timsort (very fast real-world)
```

---

## Code Examples

```python
# Comprehensive algorithm selection system

class SortingAlgorithm:
    """Base class for sorting algorithms."""
    name = "Unknown"
    best_case = "?"
    avg_case = "?"
    worst_case = "?"
    space = "?"
    stable = False
    inplace = True

    def sort(self, arr):
        raise NotImplementedError

class SelectionSort(SortingAlgorithm):
    name = "Selection Sort"
    best_case = "O(n²)"
    avg_case = "O(n²)"
    worst_case = "O(n²)"
    space = "O(1)"
    stable = False
    inplace = True

    def sort(self, arr):
        n = len(arr)
        for i in range(n):
            min_idx = i
            for j in range(i + 1, n):
                if arr[j] < arr[min_idx]:
                    min_idx = j
            arr[i], arr[min_idx] = arr[min_idx], arr[i]
        return arr

class InsertionSort(SortingAlgorithm):
    name = "Insertion Sort"
    best_case = "O(n)"
    avg_case = "O(n²)"
    worst_case = "O(n²)"
    space = "O(1)"
    stable = True
    inplace = True

    def sort(self, arr):
        for i in range(1, len(arr)):
            key = arr[i]
            j = i - 1
            while j >= 0 and arr[j] > key:
                arr[j + 1] = arr[j]
                j -= 1
            arr[j + 1] = key
        return arr

class MergeSort(SortingAlgorithm):
    name = "Merge Sort"
    best_case = "O(n log n)"
    avg_case = "O(n log n)"
    worst_case = "O(n log n)"
    space = "O(n)"
    stable = True
    inplace = False

    def sort(self, arr):
        if len(arr) <= 1:
            return arr
        mid = len(arr) // 2
        left = self.sort(arr[:mid])
        right = self.sort(arr[mid:])
        return self.merge(left, right)

    def merge(self, left, right):
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

class QuickSort(SortingAlgorithm):
    name = "Quick Sort"
    best_case = "O(n log n)"
    avg_case = "O(n log n)"
    worst_case = "O(n²)"
    space = "O(log n)"
    stable = False
    inplace = True

    def sort(self, arr, low=None, high=None):
        if low is None:
            low = 0
        if high is None:
            high = len(arr) - 1

        if low < high:
            pivot_idx = self.partition(arr, low, high)
            self.sort(arr, low, pivot_idx - 1)
            self.sort(arr, pivot_idx + 1, high)
        return arr

    def partition(self, arr, low, high):
        pivot = arr[high]
        i = low - 1
        for j in range(low, high):
            if arr[j] < pivot:
                i += 1
                arr[i], arr[j] = arr[j], arr[i]
        arr[i + 1], arr[high] = arr[high], arr[i + 1]
        return i + 1

# Algorithm recommender system
def recommend_algorithm(arr, constraints=None):
    """Recommend best sorting algorithm based on array and constraints."""
    if constraints is None:
        constraints = {}

    n = len(arr)

    # Analyze array characteristics
    sorted_count = sum(1 for i in range(n - 1) if arr[i] <= arr[i + 1])
    sortedness = sorted_count / (n - 1) if n > 1 else 1.0

    unique = len(set(arr))
    dup_ratio = 1 - (unique / n)

    # Decision logic
    reasons = []

    if n < 50:
        reasons.append("Array is small")
        return InsertionSort(), reasons

    if sortedness > 0.8:
        reasons.append(f"Array is {sortedness:.0%} sorted")
        return InsertionSort(), reasons

    if constraints.get('memory_limited'):
        reasons.append("Memory is limited")
        return QuickSort(), reasons

    if constraints.get('need_stable'):
        reasons.append("Stability required")
        return MergeSort(), reasons

    reasons.append("General purpose")
    return QuickSort(), reasons

# Performance benchmark
import time

def benchmark_algorithms(arr, algorithms):
    """Benchmark multiple algorithms on the same array."""
    print(f"Array size: {len(arr)}")
    print("-" * 60)

    for algo in algorithms:
        test_arr = arr.copy()
        start = time.time()
        algo.sort(test_arr)
        elapsed = time.time() - start

        print(f"{algo.name:20} | {elapsed:.6f}s | {algo.best_case:10} | {algo.avg_case:10}")

# Usage examples
if __name__ == "__main__":
    # Example 1: Choose for random 100-element array
    arr1 = [int(__import__('random').random() * 100) for _ in range(100)]
    algo1, reasons1 = recommend_algorithm(arr1)
    print(f"Recommended: {algo1.name}")
    print(f"Reasons: {', '.join(reasons1)}\n")

    # Example 2: Choose for nearly sorted array
    arr2 = list(range(100))
    __import__('random').shuffle(arr2)
    # Shuffle only 10% to make it nearly sorted
    for _ in range(5):
        i = __import__('random').randint(0, 99)
        j = __import__('random').randint(0, 99)
        arr2[i], arr2[j] = arr2[j], arr2[i]

    algo2, reasons2 = recommend_algorithm(arr2)
    print(f"Recommended: {algo2.name}")
    print(f"Reasons: {', '.join(reasons2)}\n")

    # Benchmark
    test_arr = [__import__('random').randint(1, 1000) for _ in range(1000)]
    algorithms = [InsertionSort(), MergeSort(), QuickSort()]
    benchmark_algorithms(test_arr, algorithms)
```

---

## Guided Practice

**Activity 1: Decision Matrix**

For each scenario, fill in the recommended algorithm and justify:

| Scenario | Algorithm | Reason |
|----------|-----------|--------|
| 5 numbers | ? | ? |
| 1 million numbers, random | ? | ? |
| 10,000 nearly-sorted numbers | ? | ? |
| Need stable sort | ? | ? |
| Embedded system (low memory) | ? | ? |

**Activity 2: Trade-Off Analysis**

Compare quick sort vs. merge sort:
- Which is faster on average?
- Which uses less memory?
- Which is guaranteed O(n log n)?
- Which would you use for a production system?

**Activity 3: Real-World Choice**

For a library system sorting 1 million book records by ISBN:
- What algorithm would you use?
- Why?
- Would your answer change if sorting by author (with duplicates)?

---

## Practice Problems

**Beginner:** Given array characteristics, choose the best algorithm and explain why.

**Intermediate:** Implement a function that analyzes an array and recommends an algorithm.

**Challenge:** Design a hybrid sorting system that uses different algorithms based on subarray size and sortedness.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Consider size, sortedness, memory, stability requirements
- **Intermediate:** Check sortedness percentage, duplicate ratio, size thresholds
- **Challenge:** Similar to Timsort/Introsort: different algorithms for different conditions
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner decision table
# 5 numbers → Insertion sort (small, simple)
# 1M numbers → Quick sort (fast, in-place)
# 10K nearly-sorted → Insertion sort (O(n) best case)
# Need stable → Merge sort (guaranteed stable)
# Low memory → Quick sort or Selection (in-place)

# Intermediate - shown above in recommend_algorithm()

# Challenge - Adaptive sort (simplified Timsort-like)
def adaptive_sort(arr):
    if len(arr) < 50:
        insertion_sort(arr)
    else:
        merge_sort(arr)
```
</details>
