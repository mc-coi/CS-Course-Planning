# Unit 5: Sorting, Searching & Recursion
> Master classic algorithms for sorting and searching. Understand their complexity and when to use each.

##  Unit Overview
- **Duration:** 9 days / 3 weeks
- **Key Concepts:** Linear/binary search, bubble/selection/insertion/merge sort, Python sorting, algorithm complexity, visualization
- **Big Idea:** Choose the right algorithm for your problem; performance matters at scale
- **TN Standard:** 9-12.CCI.3 — Implement and analyze algorithms

##  Learning Targets
- I can implement and understand linear and binary search
- I can implement and understand bubble, selection, insertion sorts
- I can implement and understand merge sort
- I can use Python's built-in sorting efficiently
- I can compare algorithms by complexity
- I can benchmark algorithms
- I can choose appropriate algorithms for problems

---

# Day 1: Linear Search
**Learning Target:** I can implement linear search and understand when it's appropriate.

### Key Concepts
Linear search checks each element sequentially until found.

Complexity: O(n)
Works on any list (sorted or unsorted)

### Code Examples
```python
def linear_search(lst, target):
    for i in range(len(lst)):
        if lst[i] == target:
            return i
    return -1

numbers = [10, 20, 30, 40, 50]
print(linear_search(numbers, 30))  # 2
print(linear_search(numbers, 100)) # -1

# With while loop
def linear_search_while(lst, target):
    i = 0
    while i < len(lst):
        if lst[i] == target:
            return i
        i += 1
    return -1
```

### Guided Practice
Implement linear search and count comparisons.

### Practice Problems
**Problem 1 — Beginner:** Linear search for a number.

**Problem 2 — Intermediate:** Linear search with count of comparisons.

**Problem 3 — Challenge:** Linear search in string for character.

<details>
<summary>✅ Sample Answers</summary>

```python
def linear_search_counting(lst, target):
    count = 0
    for item in lst:
        count += 1
        if item == target:
            return count
    return -1
```
</details>

---

# Day 2: Binary Search
**Learning Target:** I can implement binary search for sorted data and understand its O(log n) efficiency.

### Key Concepts
Binary search divides sorted data in half each iteration.

Complexity: O(log n) — much faster for large sorted lists
Data MUST be sorted

### Code Examples
```python
def binary_search(lst, target):
    low, high = 0, len(lst) - 1

    while low <= high:
        mid = (low + high) // 2
        if lst[mid] == target:
            return mid
        elif lst[mid] < target:
            low = mid + 1
        else:
            high = mid - 1

    return -1

numbers = [10, 20, 30, 40, 50, 60, 70, 80, 90]
print(binary_search(numbers, 50))  # 4
print(binary_search(numbers, 25))  # -1

# Recursive version
def binary_search_recursive(lst, target, low, high):
    if low > high:
        return -1

    mid = (low + high) // 2
    if lst[mid] == target:
        return mid
    elif lst[mid] < target:
        return binary_search_recursive(lst, target, mid + 1, high)
    else:
        return binary_search_recursive(lst, target, low, mid - 1)
```

### Guided Practice
Implement and compare linear vs binary search on large sorted list.

### Practice Problems
**Problem 1 — Beginner:** Binary search implementation.

**Problem 2 — Intermediate:** Compare linear vs binary performance.

**Problem 3 — Challenge:** Recursive binary search.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
import time

lst = list(range(1000000))
target = 999999

# Linear
start = time.time()
linear_search(lst, target)
print(f"Linear: {time.time() - start}")

# Binary
start = time.time()
binary_search(lst, target)
print(f"Binary: {time.time() - start}")
```
</details>

---

# Day 3: Bubble Sort
**Learning Target:** I can implement bubble sort and understand its O(n²) complexity.

### Key Concepts
Bubble sort repeatedly swaps adjacent elements if they're in wrong order.

Complexity: O(n²)
Simple but inefficient for large lists

### Code Examples
```python
def bubble_sort(lst):
    n = len(lst)
    for i in range(n):
        swapped = False
        for j in range(n - i - 1):
            if lst[j] > lst[j + 1]:
                lst[j], lst[j + 1] = lst[j + 1], lst[j]
                swapped = True
        if not swapped:  # Optimization: exit early if no swaps
            break
    return lst

numbers = [64, 34, 25, 12, 22, 11, 90]
print(bubble_sort(numbers))  # [11, 12, 22, 25, 34, 64, 90]
```

### Guided Practice
Visualize bubble sort step-by-step.

### Practice Problems
**Problem 1 — Beginner:** Implement basic bubble sort.

**Problem 2 — Intermediate:** Add optimization (swapped flag).

**Problem 3 — Challenge:** Count comparisons and swaps.

<details>
<summary>✅ Sample Answers</summary>

```python
def bubble_sort_counting(lst):
    n = len(lst)
    comparisons = swaps = 0
    for i in range(n):
        for j in range(n - i - 1):
            comparisons += 1
            if lst[j] > lst[j + 1]:
                lst[j], lst[j + 1] = lst[j + 1], lst[j]
                swaps += 1
    return lst, comparisons, swaps
```
</details>

---

# Day 4: Selection Sort
**Learning Target:** I can implement selection sort and compare with bubble sort.

### Key Concepts
Selection sort finds minimum and moves to front.

Complexity: O(n²)
Similar to bubble but fewer swaps

### Code Examples
```python
def selection_sort(lst):
    n = len(lst)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if lst[j] < lst[min_idx]:
                min_idx = j
        lst[i], lst[min_idx] = lst[min_idx], lst[i]
    return lst

numbers = [64, 34, 25, 12, 22, 11, 90]
print(selection_sort(numbers))  # [11, 12, 22, 25, 34, 64, 90]
```

### Guided Practice
Compare selection sort to bubble sort.

### Practice Problems
**Problem 1 — Beginner:** Implement selection sort.

**Problem 2 — Intermediate:** Compare with bubble sort.

**Problem 3 — Challenge:** Optimize selection sort variants.

<details>
<summary>✅ Sample Answers</summary>

```python
# Comparison shows selection usually has fewer swaps than bubble
def count_swaps(sort_func, lst):
    swaps = 0
    lst_copy = lst.copy()
    # Modify sort_func to count swaps
    # ...
```
</details>

---

# Day 5: Insertion Sort
**Learning Target:** I can implement insertion sort and understand its advantage for nearly-sorted data.

### Key Concepts
Insertion sort builds sorted array one element at a time.

Complexity: O(n²) average, O(n) best case (already sorted)
Efficient for small/nearly-sorted lists

### Code Examples
```python
def insertion_sort(lst):
    for i in range(1, len(lst)):
        key = lst[i]
        j = i - 1
        while j >= 0 and lst[j] > key:
            lst[j + 1] = lst[j]
            j -= 1
        lst[j + 1] = key
    return lst

numbers = [64, 34, 25, 12, 22, 11, 90]
print(insertion_sort(numbers))  # [11, 12, 22, 25, 34, 64, 90]
```

### Guided Practice
Show efficiency on nearly-sorted data.

### Practice Problems
**Problem 1 — Beginner:** Implement insertion sort.

**Problem 2 — Intermediate:** Test on nearly-sorted data.

**Problem 3 — Challenge:** Optimize for specific use cases.

<details>
<summary>✅ Sample Answers</summary>

```python
# Nearly-sorted list
almost_sorted = [1, 2, 3, 4, 5, 6, 50, 7, 8]
# Insertion sort is very fast here
```
</details>

---

# Day 6: Merge Sort
**Learning Target:** I can implement merge sort using divide-and-conquer.

### Key Concepts
Merge sort: divide, conquer, combine
Complexity: O(n log n)
Uses more memory but much faster than bubble/selection/insertion

### Code Examples
```python
def merge_sort(lst):
    if len(lst) <= 1:
        return lst

    mid = len(lst) // 2
    left = merge_sort(lst[:mid])
    right = merge_sort(lst[mid:])

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

numbers = [64, 34, 25, 12, 22, 11, 90]
print(merge_sort(numbers))  # [11, 12, 22, 25, 34, 64, 90]
```

### Guided Practice
Trace merge sort execution.

### Practice Problems
**Problem 1 — Beginner:** Implement merge sort.

**Problem 2 — Intermediate:** Compare to bubble sort performance.

**Problem 3 — Challenge:** Count operations in merge sort.

<details>
<summary>✅ Sample Answers</summary>

```python
import time

lst_large = list(range(10000, 0, -1))  # Reversed

start = time.time()
bubble_sort(lst_large.copy())
print(f"Bubble: {time.time() - start}")

start = time.time()
merge_sort(lst_large.copy())
print(f"Merge: {time.time() - start}")
# Merge will be dramatically faster
```
</details>

---

# Day 7: Python Built-in Sorting
**Learning Target:** I can use Python's efficient sorted() and list.sort() with key parameters.

### Key Concepts
Python uses Timsort (hybrid of merge+insertion) — very efficient
Always use built-in unless learning algorithms

`sorted()` returns new list
`list.sort()` modifies in place
`key` parameter for custom sorting

### Code Examples
```python
numbers = [64, 34, 25, 12, 22, 11, 90]

# Basic sorting
sorted_nums = sorted(numbers)
numbers.sort()  # In-place

# Reverse sorting
sorted_desc = sorted(numbers, reverse=True)

# Sorting strings
names = ["zach", "alice", "bob"]
sorted_names = sorted(names)  # Alphabetical

# Custom key
students = [("Alice", 95), ("Bob", 87), ("Charlie", 92)]
by_grade = sorted(students, key=lambda s: s[1])

# Dictionary sorting
people = [{"name": "Alice", "age": 30}, {"name": "Bob", "age": 25}]
by_age = sorted(people, key=lambda p: p["age"])
```

### Guided Practice
Sort various data structures using key parameter.

### Practice Problems
**Problem 1 — Beginner:** Sort a list of numbers.

**Problem 2 — Intermediate:** Sort complex objects with key.

**Problem 3 — Challenge:** Multi-level sorting (multiple keys).

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 3
students = [("Alice", 95, 10), ("Bob", 87, 9)]
# Sort by grade (desc), then by ID
sorted(students, key=lambda s: (-s[1], s[2]))
```
</details>

---

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

# Day 9: Project Day — Sort & Search Visualizer
**Learning Target:** I can create an interactive program visualizing sorting/searching algorithms.

### Project Overview
Build a visualizer showing:
- Different sorting algorithms in action
- Search algorithm steps
- Comparison and analysis
- Interactive controls

### Requirements
- Visualize algorithm steps (print state after each comparison/swap)
- Show statistics (comparisons, swaps, time)
- Support multiple algorithms
- Display results clearly

### Scaffold & Starter Code
```python
class SortVisualizer:
    def __init__(self, data):
        self.data = data
        self.comparisons = 0
        self.swaps = 0

    def display(self):
        print(self.data)

    def bubble_sort_visual(self):
        n = len(self.data)
        for i in range(n):
            for j in range(n - i - 1):
                self.comparisons += 1
                if self.data[j] > self.data[j + 1]:
                    self.data[j], self.data[j + 1] = self.data[j + 1], self.data[j]
                    self.swaps += 1
                self.display()
        return self.data

    def report(self):
        print(f"Comparisons: {self.comparisons}")
        print(f"Swaps: {self.swaps}")

# Usage
data = [5, 2, 8, 1, 9]
visualizer = SortVisualizer(data)
visualizer.bubble_sort_visual()
visualizer.report()
```

### Enhancement Ideas
- Color-coded visualization (showing comparisons, swaps)
- Step-by-step control (next/back buttons)
- Algorithm comparison side-by-side
- Custom data input
- Real-time statistics

---

# Unit Practice Bank

1. **Beginner:** Implement linear search.
2. **Beginner:** Implement binary search.
3. **Beginner:** Implement bubble sort.
4. **Intermediate:** Implement selection sort.
5. **Intermediate:** Implement insertion sort.
6. **Intermediate:** Implement merge sort.
7. **Intermediate:** Use sorted() with key parameter.
8. **Challenge:** Compare sorting algorithms on large data.
9. **Challenge:** Implement recursive binary search.
10. **Challenge:** Create sorting visualizer.
11. **Challenge:** Benchmark and analyze algorithms.
12. **Challenge:** Implement quicksort or heapsort.
13. **Challenge:** Create multi-level sorting.
14. **Challenge:** Optimize search in specific data structure.
15. **Challenge:** Build comprehensive algorithm analyzer.

---

# Common Mistakes & How to Fix Them
| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Using binary search on unsorted list | Returns wrong result | Sort data first |
| Off-by-one errors in loops | Misses last element or crashes | Double-check indices |
| Not resetting comparisons counter | Wrong statistics | Initialize before each sort |
| Comparing very different algorithm sizes | Unfair benchmark | Use same data size |

---

# Unit Assessment Prep

**Review Questions:**

1. What's the complexity of linear search?
2. What's required for binary search?
3. Compare bubble and selection sort.
4. What makes merge sort fast?
5. When is insertion sort efficient?
6. How does Python's sorted() work?
7. Compare best and worst cases.
8. When would you use each algorithm?
9. How do you benchmark algorithms?
10. What is the `key` parameter in sorted()?

**Answers:**

1. O(n) — checks each element
2. Data must be sorted
3. Both O(n²), but selection has fewer swaps
4. Divide-and-conquer, O(n log n) complexity
5. For small or nearly-sorted data
6. Uses Timsort hybrid algorithm
7. Best: O(n) on sorted data; Worst: O(n log n)
8. Choose based on data size, pre-sortedness, memory
9. Time actual execution on various data sizes
10. Function returning comparison key for sorting

---

# Vocabulary & Quick Reference

**Key Terms:**
- **Linear search:** Sequential checking, O(n)
- **Binary search:** Divide-and-conquer search, O(log n)
- **Bubble sort:** Compare and swap adjacent, O(n²)
- **Merge sort:** Divide-and-conquer sort, O(n log n)
- **Comparison:** Two items checked against each other
- **Swap:** Exchange two elements' positions
- **In-place:** Sorting without extra memory

**Big O Complexity:**
- O(1): Constant
- O(log n): Logarithmic (binary search)
- O(n): Linear (linear search)
- O(n log n): Fast sorting (merge sort)
- O(n²): Slow sorting (bubble, selection, insertion)
