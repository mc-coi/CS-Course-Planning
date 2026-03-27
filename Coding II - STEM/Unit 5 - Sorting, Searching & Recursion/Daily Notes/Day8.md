# Day 8: Algorithm Comparison & Testing
**Learning Target:** I can benchmark and compare algorithms systematically.

### Key Concepts
Empirical testing vs theoretical complexity
Time vs space tradeoffs
Choosing algorithms for your constraints

### Code Examples
```python
import time
import random

def benchmark(func, data, name):
    start = time.time()
    func(data.copy())
    elapsed = time.time() - start
    print(f"{name}: {elapsed:.6f}s")

# Test different sizes
for size in [100, 1000, 10000]:
    data = [random.randint(1, 1000) for _ in range(size)]
    print(f"\nSize: {size}")
    benchmark(bubble_sort, data, "Bubble")
    benchmark(selection_sort, data, "Selection")
    benchmark(insertion_sort, data, "Insertion")
    benchmark(merge_sort, data, "Merge")
    benchmark(sorted, data, "Built-in")
```

### Guided Practice
Run benchmarks and create comparison table.

### Practice Problems
**Problem 1 — Beginner:** Time a sorting algorithm.

**Problem 2 — Intermediate:** Compare two algorithms.

**Problem 3 — Challenge:** Create comprehensive benchmark report.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 3
results = {}
for size in [100, 1000, 10000]:
    data = list(range(size, 0, -1))  # Reverse sorted
    results[size] = {}
    for name, func in algorithms.items():
        results[size][name] = benchmark(func, data.copy())

# Print results table
for size, times in results.items():
    print(f"Size {size}: {times}")
```
</details>

---

---
