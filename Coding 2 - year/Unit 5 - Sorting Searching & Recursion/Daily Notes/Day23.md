# Day 23: Sorting & Searching Project Planning

**Learning Target:** I can plan and execute a multi-algorithm sorting/searching project with benchmarking and analysis.

---

## Key Concepts

**Project Scope:**
- Implement multiple sorting algorithms
- Implement multiple searching algorithms
- Benchmark and compare performance
- Analyze results and draw conclusions
- Document findings and recommendations

**Project Phases:**
1. Implementation (code all algorithms)
2. Testing (verify correctness)
3. Benchmarking (measure performance)
4. Analysis (interpret results)
5. Presentation (document findings)

---

## Project Assignment: Sorting & Searching Benchmark

### Phase 1: Implementation

Implement the following algorithms:

**Searching:**
- Linear search
- Binary search (iterative)
- Binary search (recursive)

**Sorting:**
- Bubble sort
- Selection sort
- Insertion sort
- Merge sort
- Quick sort
- Built-in Python sort

### Phase 2: Testing

For each algorithm, test:
```python
# Test cases
test_cases = [
    [],                              # Empty
    [5],                             # Single element
    [1, 2, 3, 4, 5],                 # Already sorted
    [5, 4, 3, 2, 1],                 # Reverse sorted
    [3, 1, 4, 1, 5, 9, 2, 6],        # Random with duplicates
]
```

Create a test suite that verifies all algorithms produce correct results.

### Phase 3: Benchmarking Code Structure

```python
# Example project structure

class SortingProject:
    """Complete sorting/searching benchmark project."""

    def __init__(self):
        self.algorithms = {}
        self.results = {}

    def register_algorithm(self, name, func, category='sort'):
        """Register an algorithm for benchmarking."""
        self.algorithms[name] = {'func': func, 'category': category}

    def verify_correctness(self, test_array):
        """Verify all algorithms produce correct output."""
        results = {}
        for name, algo_info in self.algorithms.items():
            try:
                result = algo_info['func'](test_array.copy())
                results[name] = {'correct': result == sorted(test_array)}
            except Exception as e:
                results[name] = {'correct': False, 'error': str(e)}
        return results

    def benchmark_all(self, sizes, data_types, runs=3):
        """Run comprehensive benchmark."""
        for size in sizes:
            for data_type in data_types:
                # Generate test data
                arr = self.generate_data(size, data_type)

                # Time each algorithm
                for name, algo_info in self.algorithms.items():
                    if algo_info['category'] != 'sort':
                        continue

                    times = []
                    for _ in range(runs):
                        start = time.perf_counter()
                        algo_info['func'](arr.copy())
                        times.append(time.perf_counter() - start)

                    # Store results
                    key = f"{size}_{data_type}_{name}"
                    self.results[key] = {
                        'size': size,
                        'type': data_type,
                        'algorithm': name,
                        'times': times,
                        'mean': sum(times) / len(times)
                    }

    def generate_data(self, size, data_type):
        """Generate test data."""
        if data_type == 'random':
            return [random.randint(1, 10000) for _ in range(size)]
        elif data_type == 'sorted':
            return list(range(size))
        elif data_type == 'reverse':
            return list(range(size, 0, -1))
        elif data_type == 'nearly_sorted':
            arr = list(range(size))
            for _ in range(max(1, size // 20)):
                i = random.randint(0, size - 1)
                j = random.randint(0, size - 1)
                arr[i], arr[j] = arr[j], arr[i]
            return arr

    def generate_report(self):
        """Generate analysis report."""
        print("=" * 100)
        print("SORTING ALGORITHM BENCHMARK REPORT")
        print("=" * 100)

        # Group by size and data type
        by_scenario = {}
        for key, result in self.results.items():
            scenario = f"{result['size']}_{result['type']}"
            if scenario not in by_scenario:
                by_scenario[scenario] = []
            by_scenario[scenario].append(result)

        # Print results for each scenario
        for scenario in sorted(by_scenario.keys()):
            parts = scenario.split('_')
            size = parts[0]
            data_type = '_'.join(parts[1:])

            print(f"\nSize: {size} elements | Type: {data_type}")
            print("-" * 100)

            results_sorted = sorted(by_scenario[scenario],
                                   key=lambda r: r['mean'])

            for result in results_sorted:
                algo = result['algorithm']
                mean_time = result['mean']
                print(f"  {algo:20} {mean_time:.6f}s")

    def analyze_results(self):
        """Provide analysis and recommendations."""
        print("\n" + "=" * 100)
        print("ANALYSIS & RECOMMENDATIONS")
        print("=" * 100)

        # Find fastest for each category
        fastest_by_size = {}
        for result in self.results.values():
            size = result['size']
            if size not in fastest_by_size or \
               result['mean'] < fastest_by_size[size]['mean']:
                fastest_by_size[size] = result

        print("\nFastest Algorithm by Size:")
        for size in sorted(fastest_by_size.keys()):
            algo = fastest_by_size[size]['algorithm']
            print(f"  {size:6} elements: {algo}")

        # Analyze scaling
        print("\nScaling Analysis:")
        bubble_times = [r for r in self.results.values()
                       if r['algorithm'] == 'Bubble Sort'
                       and r['type'] == 'random']
        quick_times = [r for r in self.results.values()
                      if r['algorithm'] == 'Quick Sort'
                      and r['type'] == 'random']

        if bubble_times and quick_times:
            bubble_times.sort(key=lambda r: r['size'])
            quick_times.sort(key=lambda r: r['size'])

            if len(bubble_times) >= 2:
                ratio = bubble_times[-1]['mean'] / bubble_times[0]['mean']
                print(f"  Bubble sort scaling: {ratio:.1f}x (expected ~10x for 10x size)")

            if len(quick_times) >= 2:
                ratio = quick_times[-1]['mean'] / quick_times[0]['mean']
                print(f"  Quick sort scaling: {ratio:.1f}x (expected ~5-10x for 10x size)")

# Project execution template

def execute_project():
    """Run the complete project."""
    project = SortingProject()

    # Register all algorithms
    project.register_algorithm('Bubble Sort', bubble_sort)
    project.register_algorithm('Selection Sort', selection_sort)
    project.register_algorithm('Insertion Sort', insertion_sort)
    project.register_algorithm('Merge Sort', merge_sort)
    project.register_algorithm('Quick Sort', quick_sort)
    project.register_algorithm('Built-in Sort', builtin_sort)

    # Phase 1: Verify correctness
    print("PHASE 1: Verifying Algorithm Correctness")
    print("-" * 100)
    test_data = [3, 1, 4, 1, 5, 9, 2, 6]
    correct_results = project.verify_correctness(test_data)
    for algo, result in correct_results.items():
        status = "✓ PASS" if result['correct'] else "✗ FAIL"
        print(f"  {algo:20} {status}")

    # Phase 2: Benchmark
    print("\n\nPHASE 2: Benchmarking")
    print("-" * 100)
    print("Running benchmarks... (this may take a minute)")
    project.benchmark_all(
        sizes=[100, 1000, 5000],
        data_types=['random', 'sorted', 'reverse'],
        runs=3
    )

    # Phase 3: Report & Analysis
    print("\n\nPHASE 3: Report & Analysis")
    project.generate_report()
    project.analyze_results()

    # Phase 4: Conclusions
    print("\n" + "=" * 100)
    print("CONCLUSIONS")
    print("=" * 100)
    print("""
Based on the benchmarks, we conclude:

1. **For small arrays (< 100)**: Insertion sort is competitive or faster
2. **For large arrays (> 1000)**: Quick sort and Merge sort dominate
3. **Python's built-in sort**: Uses Timsort and is highly optimized
4. **Worst case**: Bubble sort should be avoided in production
5. **Trade-offs**: Quick sort is in-place but less stable; Merge sort is stable but uses more memory

Recommendation: Use Python's built-in sorted() or .sort() in production code.
For learning purposes, understand when each algorithm is appropriate.
    """)
```

---

## Guided Practice

**Activity 1: Project Planning**

Create a checklist:
- [ ] Implement 5 sorting algorithms
- [ ] Implement 2 searching algorithms
- [ ] Create test suite
- [ ] Run benchmarks on 3+ sizes
- [ ] Test on 4+ data types
- [ ] Generate report
- [ ] Analyze results
- [ ] Document conclusions

**Activity 2: Expected Results Preview**

Predict which algorithm will be fastest for:
- Small arrays (50 elements)
- Large random (10,000 elements)
- Nearly sorted (10,000 elements)

Then verify your predictions by running benchmarks.

**Activity 3: Write the Report**

Draft a short report including:
- Methodology (which algorithms, what sizes, what data types)
- Results (tables of times)
- Analysis (why is X faster than Y?)
- Recommendations (what to use when)

---

## Practice Problems

**Beginner:** Implement and test one sorting and one searching algorithm. Verify correctness on 5 test cases.

**Intermediate:** Implement 3 sorting algorithms and benchmark them on arrays of size 100, 1000, and 10,000.

**Challenge:** Complete the full project as described above with all algorithms, comprehensive benchmarking, and detailed analysis.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Use the implementations from previous days; test manually
- **Intermediate:** Use simple timing with time.perf_counter(); run each 3+ times
- **Challenge:** Use the project structure above as a template
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# See example project structure and execute_project() above
# Key steps:
# 1. Implement all algorithms (done in previous days)
# 2. Create test suite for each
# 3. Time each on different data sizes/types
# 4. Collect and analyze results
# 5. Draw conclusions and make recommendations
```
</details>
