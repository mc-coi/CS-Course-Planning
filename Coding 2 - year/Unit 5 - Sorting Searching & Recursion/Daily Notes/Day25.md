# Day 25: Sorting Project Benchmarking & Data Generation

**Learning Target:** I can benchmark sorting algorithms on various data types and analyze performance scaling.

---

## Key Concepts

**Benchmarking Strategy:**
1. Generate multiple data types
2. Test on various sizes (100, 1000, 10000+)
3. Run each multiple times and average
4. Collect detailed timing data
5. Analyze scaling and patterns

**Data Types to Test:**
- Random: Completely unsorted
- Sorted: Already in order (best case for some)
- Reverse: Backwards order (worst case for some)
- Nearly Sorted: Mostly sorted with some swaps
- Few Unique: Many duplicate values

---

## Code Examples

```python
# Comprehensive benchmarking framework

import time
import random
from statistics import mean, stdev

class DataGenerator:
    """Generate various types of test data."""

    @staticmethod
    def random_data(size):
        """Completely random data."""
        return [random.randint(1, 10000) for _ in range(size)]

    @staticmethod
    def sorted_data(size):
        """Already sorted."""
        return list(range(size))

    @staticmethod
    def reverse_sorted_data(size):
        """Reverse sorted."""
        return list(range(size, 0, -1))

    @staticmethod
    def nearly_sorted_data(size, swap_percent=0.1):
        """Mostly sorted with some elements out of place."""
        arr = list(range(size))
        # Swap approximately swap_percent% of elements
        num_swaps = int(size * swap_percent)
        for _ in range(num_swaps):
            i = random.randint(0, size - 1)
            j = random.randint(0, size - 1)
            arr[i], arr[j] = arr[j], arr[i]
        return arr

    @staticmethod
    def few_unique_data(size, unique_count=10):
        """Many duplicates (few unique values)."""
        return [random.randint(1, unique_count) for _ in range(size)]

    @staticmethod
    def sawtooth_data(size):
        """Repeating pattern: [1,2,...,100,1,2,...,100,...]"""
        pattern_size = int(size ** 0.5)
        pattern = list(range(pattern_size))
        return (pattern * (size // pattern_size + 1))[:size]

class BenchmarkRunner:
    """Run and collect performance data."""

    def __init__(self):
        self.results = {}
        self.data_gen = DataGenerator()

    def benchmark_algorithm(self, algo_name, algo_func, arr, runs=3):
        """Time an algorithm on an array, run multiple times."""
        times = []

        for _ in range(runs):
            test_arr = arr.copy()

            try:
                start = time.perf_counter()
                algo_func(test_arr)
                elapsed = time.perf_counter() - start
                times.append(elapsed)
            except RecursionError:
                # Handle stack overflow for very deep recursion
                return None

        if not times:
            return None

        return {
            'min': min(times),
            'max': max(times),
            'mean': mean(times),
            'stdev': stdev(times) if len(times) > 1 else 0
        }

    def run_full_benchmark(self, algorithms, sizes, data_types):
        """
        Benchmark all algorithm/size/data_type combinations.

        Parameters:
            algorithms: list of (name, function) tuples
            sizes: list of array sizes to test
            data_types: list of ('name', generator_function) tuples
        """
        total_tests = len(algorithms) * len(sizes) * len(data_types)
        current = 0

        for size in sizes:
            for data_type_name, data_gen_func in data_types:
                print(f"\nGenerating {data_type_name} data ({size} elements)...", end="")
                arr = data_gen_func(size)
                print(" Done")

                for algo_name, algo_func in algorithms:
                    current += 1
                    progress = f"[{current}/{total_tests}]"

                    # Skip slow algorithms on large arrays
                    if size > 1000 and algo_name in ['Bubble Sort', 'Selection Sort']:
                        print(f"  {progress} {algo_name:20} on {data_type_name:15} (SKIPPED - too slow)")
                        continue

                    print(f"  {progress} {algo_name:20} on {data_type_name:15}...", end="", flush=True)

                    result = self.benchmark_algorithm(algo_name, algo_func, arr, runs=3)

                    if result is None:
                        print(" FAILED (error)")
                        continue

                    # Store result
                    key = f"{algo_name}_{size}_{data_type_name}"
                    self.results[key] = {
                        'algorithm': algo_name,
                        'size': size,
                        'data_type': data_type_name,
                        'time': result['mean'],
                        'stdev': result['stdev']
                    }

                    print(f" {result['mean']:.6f}s")

    def print_summary_table(self):
        """Print summary table of results."""
        if not self.results:
            print("No results to display")
            return

        print("\n" + "=" * 120)
        print("BENCHMARK RESULTS SUMMARY")
        print("=" * 120)

        # Group by size
        by_size = {}
        for result in self.results.values():
            size = result['size']
            if size not in by_size:
                by_size[size] = []
            by_size[size].append(result)

        for size in sorted(by_size.keys()):
            print(f"\nSize: {size:,} elements")
            print("-" * 120)

            # Group by data type
            by_data_type = {}
            for result in by_size[size]:
                dt = result['data_type']
                if dt not in by_data_type:
                    by_data_type[dt] = []
                by_data_type[dt].append(result)

            for data_type in sorted(by_data_type.keys()):
                print(f"  {data_type:20}")

                # Sort by time (fastest first)
                sorted_results = sorted(by_data_type[data_type],
                                       key=lambda r: r['time'])

                for i, result in enumerate(sorted_results):
                    rank = i + 1
                    algo = result['algorithm']
                    time_ms = result['time'] * 1000
                    print(f"    {rank}. {algo:20} {time_ms:10.3f}ms")

    def analyze_scaling(self):
        """Analyze how algorithms scale with size."""
        print("\n" + "=" * 120)
        print("SCALING ANALYSIS")
        print("=" * 120)

        # For each algorithm and data type, show scaling
        by_algo_type = {}

        for result in self.results.values():
            key = (result['algorithm'], result['data_type'])
            if key not in by_algo_type:
                by_algo_type[key] = []
            by_algo_type[key].append(result)

        for (algo, data_type) in sorted(by_algo_type.keys()):
            results = sorted(by_algo_type[(algo, data_type)],
                           key=lambda r: r['size'])

            if len(results) >= 2:
                print(f"\n{algo} on {data_type}:")

                # Calculate scaling factor
                smallest = results[0]
                largest = results[-1]
                size_ratio = largest['size'] / smallest['size']
                time_ratio = largest['time'] / smallest['time']

                print(f"  Size ratio: {size_ratio:.1f}x ({smallest['size']:,} → {largest['size']:,})")
                print(f"  Time ratio: {time_ratio:.1f}x")

                # Compare to expected scaling
                if algo in ['Bubble Sort', 'Selection Sort', 'Insertion Sort']:
                    expected = size_ratio ** 2  # O(n²)
                    expected_label = "O(n²)"
                else:
                    expected = size_ratio * (size_ratio ** 0.5).bit_length()  # Approximate O(n log n)
                    expected_label = "O(n log n)"

                print(f"  Expected scaling ({expected_label}): {expected:.1f}x")
                deviation = abs(time_ratio - expected) / expected * 100
                print(f"  Deviation from expected: {deviation:.1f}%")

    def get_fastest_algorithm(self, size, data_type=None):
        """Get the fastest algorithm for a specific size/data type."""
        matching = [r for r in self.results.values()
                   if r['size'] == size]

        if data_type:
            matching = [r for r in matching if r['data_type'] == data_type]

        if matching:
            return min(matching, key=lambda r: r['time'])
        return None

# Execute benchmarks
def run_comprehensive_benchmark():
    """Run complete benchmarking suite."""
    runner = BenchmarkRunner()
    data_gen = DataGenerator()

    # Algorithms to test
    algorithms = [
        ('Bubble Sort', bubble_sort),
        ('Selection Sort', selection_sort),
        ('Insertion Sort', insertion_sort),
        ('Merge Sort', merge_sort),
        ('Quick Sort', quick_sort),
        ('Built-in Sort', builtin_sort),
    ]

    # Data types
    data_types = [
        ('Random', data_gen.random_data),
        ('Sorted', data_gen.sorted_data),
        ('Reverse', data_gen.reverse_sorted_data),
        ('Nearly Sorted', data_gen.nearly_sorted_data),
        ('Few Unique', data_gen.few_unique_data),
    ]

    # Sizes
    sizes = [100, 500, 1000, 5000, 10000]

    print("=" * 120)
    print("COMPREHENSIVE SORTING ALGORITHM BENCHMARK")
    print("=" * 120)
    print(f"Testing {len(algorithms)} algorithms")
    print(f"On {len(sizes)} array sizes: {sizes}")
    print(f"With {len(data_types)} data types: {[d[0] for d in data_types]}")
    print()

    # Run benchmarks
    runner.run_full_benchmark(algorithms, sizes, data_types)

    # Display results
    runner.print_summary_table()
    runner.analyze_scaling()

    return runner
```

---

## Guided Practice

**Activity 1: Predict Scaling**

Before running benchmarks, predict:
- Bubble sort on 10x larger array: 100x slower? ✓
- Quick sort on 10x larger array: ~50x slower? ✓
- Insertion sort on sorted data: No slowdown? ✓

Then run benchmarks and compare to predictions.

**Activity 2: Data Type Impact**

Observe how each algorithm performs differently on:
- Random data (worst case for insertion sort)
- Sorted data (best case for insertion sort)
- Nearly sorted (insertion still good)

**Activity 3: Find Inflection Point**

At what array size does quick sort become faster than insertion sort?

---

## Practice Problems

**Beginner:** Run benchmarks on 3 sizes (100, 1000, 10000) and 2 data types (random, sorted).

**Intermediate:** Generate all 6 data types and benchmark all algorithms on sizes 100-10000.

**Challenge:** Implement a "smart" algorithm selector that chooses the best algorithm based on array size and data type.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Use the code above; start with small set
- **Intermediate:** Use full code above; may take a few minutes to run
- **Challenge:** Based on benchmark results, create decision rules
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# See BenchmarkRunner class above
# Execute: run_comprehensive_benchmark()
# Results will show which algorithm is best for each scenario

# Challenge - Smart selector
def choose_algorithm(size, data_type):
    if size < 100:
        return insertion_sort
    elif data_type == 'sorted':
        return insertion_sort
    elif data_type == 'few_unique':
        return quick_sort  # or three-way quicksort
    else:
        return quick_sort
```
</details>
