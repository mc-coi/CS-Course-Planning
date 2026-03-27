# Day 22: Performance Testing & Benchmarking Sorting Algorithms

**Learning Target:** I can benchmark sorting algorithms and interpret performance results.

---

## Key Concepts

**Benchmarking Considerations:**
- **Warm-up runs:** JIT compilation (if applicable) needs time to optimize
- **Multiple runs:** Average results over many runs to reduce noise
- **Different data:** Test on random, sorted, reverse, and partially sorted
- **Various sizes:** From 10 to 100,000+ elements
- **Measurement:** Wall-clock time, operations counted, or profiler data

**Common Pitfalls:**
- Testing on tiny arrays (Python overhead dominates)
- Not averaging multiple runs
- Not testing different data patterns
- Ignoring system load during testing

---

## Code Examples

```python
# Comprehensive benchmarking suite

import time
import random
from statistics import mean, stdev

class BenchmarkSuite:
    """Run and analyze algorithm performance."""

    def __init__(self):
        self.results = {}

    def generate_test_data(self, size, data_type='random'):
        """Generate different types of test data."""
        if data_type == 'random':
            return [random.randint(1, 10000) for _ in range(size)]
        elif data_type == 'sorted':
            return list(range(size))
        elif data_type == 'reverse':
            return list(range(size, 0, -1))
        elif data_type == 'nearly_sorted':
            arr = list(range(size))
            # Shuffle ~10% of elements
            for _ in range(size // 10):
                i, j = random.randint(0, size - 1), random.randint(0, size - 1)
                arr[i], arr[j] = arr[j], arr[i]
            return arr
        else:
            raise ValueError(f"Unknown data type: {data_type}")

    def time_algorithm(self, algo_func, arr, runs=3):
        """Time an algorithm over multiple runs."""
        times = []

        for _ in range(runs):
            test_arr = arr.copy()
            start = time.perf_counter()
            algo_func(test_arr)
            elapsed = time.perf_counter() - start
            times.append(elapsed)

        return {
            'min': min(times),
            'max': max(times),
            'mean': mean(times),
            'stdev': stdev(times) if len(times) > 1 else 0
        }

    def benchmark(self, algorithms, sizes, data_types):
        """Run full benchmark suite."""
        print("=" * 100)
        print("COMPREHENSIVE SORTING ALGORITHM BENCHMARK")
        print("=" * 100)

        for size in sizes:
            print(f"\nArray Size: {size:,} elements")
            print("-" * 100)

            for data_type in data_types:
                print(f"\n  {data_type.upper()} DATA:")

                arr = self.generate_test_data(size, data_type)

                for name, algo_func in algorithms:
                    try:
                        result = self.time_algorithm(algo_func, arr)
                        print(f"    {name:20} | {result['mean']:.6f}s "
                              f"(±{result['stdev']:.6f}s)")
                    except Exception as e:
                        print(f"    {name:20} | ERROR: {e}")

# Example algorithms for testing

def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key

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
    return quick_sort([x for x in arr if x < pivot]) + \
           [x for x in arr if x == pivot] + \
           quick_sort([x for x in arr if x > pivot])

def builtin_sort(arr):
    return sorted(arr)

# Counting operations
def count_operations(arr, algo_func):
    """Count comparisons and assignments."""
    comparisons = [0]
    assignments = [0]

    original_lt = int.__lt__
    original_setitem = list.__setitem__

    def counting_lt(self, other):
        comparisons[0] += 1
        return original_lt(self, other)

    # This is simplified; real counting is complex
    algo_func(arr)
    return comparisons[0]

# Memory usage tracking
def estimate_memory(algo_func, arr):
    """Estimate extra memory used by algorithm."""
    import sys
    arr_size = sys.getsizeof(arr)
    # Note: This is simplified; real memory profiling requires tools
    return arr_size

# Main benchmark execution
def run_benchmarks():
    """Execute full benchmark suite."""
    suite = BenchmarkSuite()

    algorithms = [
        ('Insertion Sort', insertion_sort),
        ('Merge Sort', merge_sort),
        ('Quick Sort', quick_sort),
        ('Built-in Sort', builtin_sort),
    ]

    # Limit bubble sort to small sizes (it's slow!)
    small_algorithms = [
        ('Bubble Sort', bubble_sort),
        ('Insertion Sort', insertion_sort),
        ('Built-in Sort', builtin_sort),
    ]

    # Benchmark small arrays
    print("\nSMALL ARRAYS (Bubble sort included):")
    suite.benchmark(small_algorithms, [50, 100, 200], ['random'])

    # Benchmark large arrays
    print("\n" + "=" * 100)
    print("LARGE ARRAYS (Bubble sort skipped):")
    suite.benchmark(algorithms, [1000, 5000, 10000],
                   ['random', 'sorted', 'reverse', 'nearly_sorted'])

# Visualization helper
def create_performance_summary(results):
    """Create a summary table of results."""
    print("\n" + "=" * 100)
    print("PERFORMANCE SUMMARY")
    print("=" * 100)
    print(f"{'Algorithm':<20} {'1000 Elements':<20} {'10000 Elements':<20}")
    print("-" * 100)

    # Summary would be printed here based on results
```

---

## Guided Practice

**Activity 1: Run a Benchmark**

Execute the benchmarking code above and observe:
1. Which algorithm is fastest for each size?
2. How does performance scale with size?
3. Does data type (random vs. sorted) affect results?

**Activity 2: Compare Bubble vs. Quick**

For a 10,000-element random array:
- How much slower is bubble sort than quick sort?
- Can you estimate based on O(n²) vs. O(n log n)?

**Activity 3: Memory vs. Speed Trade-off**

Compare merge sort (uses extra memory) vs. quick sort (in-place):
- Which is faster?
- Is the extra memory worth it?

---

## Practice Problems

**Beginner:** Write a simple benchmarking function that times three algorithms on a 1000-element array.

**Intermediate:** Create a function that benchmarks an algorithm on different data types (random, sorted, reversed) and reports which is fastest/slowest.

**Challenge:** Implement operation counting (comparisons and assignments) for two algorithms and compare.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Use time.perf_counter() before and after, subtract to get elapsed time
- **Intermediate:** Generate different arrays with generate_test_data and time each
- **Challenge:** Count comparisons inside the algorithm (increment a counter variable)
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
import time

def simple_benchmark(algo, arr, runs=3):
    times = []
    for _ in range(runs):
        start = time.perf_counter()
        algo(arr.copy())
        times.append(time.perf_counter() - start)
    return sum(times) / len(times)

# Intermediate - shown in BenchmarkSuite.benchmark()

# Challenge
def insertion_sort_count_ops(arr):
    comparisons = 0
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0:
            comparisons += 1
            if arr[j] > key:
                arr[j + 1] = arr[j]
                j -= 1
            else:
                break
        arr[j + 1] = key
    return comparisons
```
</details>
