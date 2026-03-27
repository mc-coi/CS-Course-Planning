# Day 27: Algorithm Benchmarking Lab — Day 2

**Learning Target:** I can benchmark multiple sorting algorithms and analyze their real-world performance differences.

---

## Key Concepts

**Performance Benchmarking:** Measuring actual execution time of algorithms on your computer to see real-world speed differences.

**The Big O Gap:** Big O notation tells us *theoretical* growth rates, but benchmarking reveals *practical* differences:
- Bubble Sort O(n²) vs Merge Sort O(n log n) sounds similar, but on n=10,000:
  - Bubble sort: ~100 million comparisons
  - Merge sort: ~130,000 comparisons
  - In practice: Bubble sort might take 10+ seconds, merge sort takes milliseconds

**Time Module:** Python's `time.time()` returns seconds since epoch (Jan 1, 1970). Subtract start time from end time to get elapsed seconds.

**Important:** Always test on the *same* data to compare fairly. Use `.copy()` so sorting doesn't modify the original list.

**Statistical Reality:** One run isn't enough — times vary due to system load, caching, etc. Run multiple times and average the results.

---

## Code Examples

```python
import time
import random

def bubble_sort(arr):
    """Bubble sort - O(n²) time complexity."""
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr

def selection_sort(arr):
    """Selection sort - O(n²) time complexity."""
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr

def insertion_sort(arr):
    """Insertion sort - O(n²) worst case, O(n) best case."""
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

def merge_sort(arr):
    """Merge sort - O(n log n) time complexity."""
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    return merge(left, right)

def merge(left, right):
    """Merge two sorted arrays."""
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

def benchmark(sort_function, data, runs=3):
    """Benchmark a sorting function by running it multiple times."""
    times = []

    for _ in range(runs):
        test_data = data.copy()
        start = time.time()
        sort_function(test_data)
        end = time.time()
        times.append(end - start)

    avg_time = sum(times) / len(times)
    return avg_time

# Generate test data of different sizes
small_data = random.sample(range(1000), 100)
medium_data = random.sample(range(10000), 1000)
large_data = random.sample(range(100000), 5000)

# Benchmark on small data
print("=== Small Data (100 elements) ===")
print(f"Bubble Sort: {benchmark(bubble_sort, small_data):.6f} seconds")
print(f"Selection Sort: {benchmark(selection_sort, small_data):.6f} seconds")
print(f"Insertion Sort: {benchmark(insertion_sort, small_data):.6f} seconds")
print(f"Merge Sort: {benchmark(merge_sort, small_data):.6f} seconds")
print(f"Python sorted(): {benchmark(lambda x: sorted(x), small_data):.6f} seconds")

# Benchmark on medium data
print("\n=== Medium Data (1000 elements) ===")
print(f"Bubble Sort: {benchmark(bubble_sort, medium_data):.6f} seconds")
print(f"Selection Sort: {benchmark(selection_sort, medium_data):.6f} seconds")
print(f"Insertion Sort: {benchmark(insertion_sort, medium_data):.6f} seconds")
print(f"Merge Sort: {benchmark(merge_sort, medium_data):.6f} seconds")
print(f"Python sorted(): {benchmark(lambda x: sorted(x), medium_data):.6f} seconds")

# Benchmark on large data
print("\n=== Large Data (5000 elements) ===")
print(f"Bubble Sort: {benchmark(bubble_sort, large_data):.6f} seconds")
print(f"Selection Sort: {benchmark(selection_sort, large_data):.6f} seconds")
print(f"Insertion Sort: {benchmark(insertion_sort, large_data):.6f} seconds")
print(f"Merge Sort: {benchmark(merge_sort, large_data):.6f} seconds")
print(f"Python sorted(): {benchmark(lambda x: sorted(x), large_data):.6f} seconds")
```

---

## Guided Practice

**Activity: Create a Performance Comparison Table**

1. Copy the benchmark code above into a Python file
2. Run it and record the times in a table like this:

| Algorithm | 100 elements | 1000 elements | 5000 elements |
|-----------|------------|-------------|-------------|
| Bubble Sort | | | |
| Selection Sort | | | |
| Insertion Sort | | | |
| Merge Sort | | | |
| Python sorted() | | | |

3. Analyze: Which algorithms got slower faster as data size increased?
4. Create a line graph showing time vs data size for each algorithm

**Discussion Questions:**
- Why is Python's `sorted()` so fast? (It uses Timsort, a hybrid algorithm)
- Which algorithm would you use for 100 elements? For 100,000 elements?
- How much slower is bubble sort than merge sort on 5000 elements?

---

## Practice Problems

**Beginner:**
Run bubble sort and Python's `sorted()` on a list of 100 random numbers. Time both using the benchmark code above. What do you notice about the difference?

```python
import time
import random

data = random.sample(range(1000), 100)

# Bubble sort
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

start = time.time()
bubble_sort(data.copy())
bubble_time = time.time() - start

start = time.time()
sorted(data)
sorted_time = time.time() - start

print(f"Bubble sort: {bubble_time:.6f}s")
print(f"Python sorted(): {sorted_time:.6f}s")
```

**Intermediate:**
Create a function that benchmarks all four algorithms (bubble, selection, insertion, merge) on the same data and prints a comparison table showing time for each.

```python
import time
import random

def compare_sorts(data_size, runs=3):
    data = random.sample(range(data_size * 10), data_size)

    algorithms = {
        'Bubble Sort': bubble_sort,
        'Selection Sort': selection_sort,
        'Insertion Sort': insertion_sort,
        'Merge Sort': merge_sort,
    }

    print(f"\n=== Comparing {len(data)} elements ({runs} runs each) ===")
    print(f"{'Algorithm':<20} {'Time (seconds)':<15} {'Relative Speed':<15}")
    print("-" * 50)

    times = {}
    for name, func in algorithms.items():
        total_time = 0
        for _ in range(runs):
            start = time.time()
            func(data.copy())
            total_time += time.time() - start
        avg_time = total_time / runs
        times[name] = avg_time
        print(f"{name:<20} {avg_time:.6f}          ", end="")

    # Find fastest
    fastest = min(times.values())
    for name, t in times.items():
        print(f"{name:<20} {t/fastest:.1f}x")

compare_sorts(1000)
```

**Challenge:**
Test your algorithms on three different types of data:
1. **Random data:** `random.shuffle(list_copy)`
2. **Already sorted data:** `sorted(data)`
3. **Reverse sorted data:** `sorted(data, reverse=True)`

See which algorithms perform better or worse based on input order. Bubble sort with optimization should be much faster on nearly-sorted data!

```python
import time
import random

def test_different_inputs(size=1000):
    # Create test data
    base_data = list(range(size))

    # Three versions: random, sorted, reverse-sorted
    random_data = base_data.copy()
    random.shuffle(random_data)

    sorted_data = sorted(base_data)

    reverse_data = sorted(base_data, reverse=True)

    test_cases = [
        ("Random", random_data),
        ("Sorted", sorted_data),
        ("Reverse-sorted", reverse_data),
    ]

    for case_name, data in test_cases:
        print(f"\n=== {case_name} Data ===")
        # Test your algorithms and record times

test_different_inputs()
```

<details>
<summary>💡 Hints</summary>

- Use `time.time()` before and after calling the sort function
- Use `data.copy()` to ensure each algorithm gets the same original data
- Run multiple times (3-5) and average the results for more reliable data
- For challenge: use `random.shuffle()`, `sorted()`, and `sorted(..., reverse=True)` to create test cases
- Be patient with bubble sort on large data — it might take several seconds!
- If a test is taking too long, use smaller data sizes (500 elements instead of 5000)

</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner Answer:**
```python
import time
import random

def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr

data = random.sample(range(1000), 100)

start = time.time()
bubble_sort(data.copy())
bubble_time = time.time() - start

start = time.time()
sorted(data)
sorted_time = time.time() - start

print(f"Bubble sort: {bubble_time:.6f}s")
print(f"Python sorted(): {sorted_time:.6f}s")
print(f"Sorted is {bubble_time/sorted_time:.1f}x faster")
```

Expected output: Sorted is usually 2-10x faster on 100 elements.

**Intermediate Answer:**
```python
import time
import random

def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
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

def benchmark_all(size=1000):
    data = random.sample(range(size * 10), size)

    algorithms = {
        'Bubble Sort': bubble_sort,
        'Selection Sort': selection_sort,
        'Insertion Sort': insertion_sort,
        'Merge Sort': merge_sort,
    }

    print(f"\n=== Benchmarking {size} elements ===")
    print(f"{'Algorithm':<20} {'Time (seconds)':<20}")
    print("-" * 40)

    for name, func in algorithms.items():
        start = time.time()
        func(data.copy())
        elapsed = time.time() - start
        print(f"{name:<20} {elapsed:.6f}")

benchmark_all(1000)
```

**Challenge Answer:**
```python
import time
import random

def bubble_sort_optimized(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
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

def test_input_types(size=1000):
    base = list(range(size))

    test_cases = {
        'Random': random.sample(base, size),
        'Sorted': base.copy(),
        'Reverse': sorted(base, reverse=True),
    }

    print(f"{'Input Type':<20} {'Bubble Sort':<20} {'Merge Sort':<20}")
    print("-" * 60)

    for case_name, data in test_cases.items():
        bubble_time = 0
        merge_time = 0

        for _ in range(3):
            start = time.time()
            bubble_sort_optimized(data.copy())
            bubble_time += time.time() - start

            start = time.time()
            merge_sort(data.copy())
            merge_time += time.time() - start

        print(f"{case_name:<20} {bubble_time/3:.6f}s       {merge_time/3:.6f}s")

test_input_types(1000)
```

Expected results:
- Bubble sort is fastest on already-sorted data (optimization kicks in)
- Merge sort is consistent across all input types
- Random data is hardest for bubble sort

</details>
