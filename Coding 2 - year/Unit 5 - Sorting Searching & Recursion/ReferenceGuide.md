# Unit 5: Sorting, Searching & Recursion — Reference Guide

Quick reference for all algorithms, Big O complexities, and code templates.

---

## Big O Complexity Comparison Table

| Algorithm | Best Case | Average Case | Worst Case | Space | Notes |
|-----------|-----------|--------------|-----------|-------|-------|
| **Linear Search** | O(n) | O(n) | O(n) | O(1) | Check every element |
| **Binary Search** | O(1) | O(log n) | O(log n) | O(1) | Requires sorted data |
| **Bubble Sort** | O(n) | O(n²) | O(n²) | O(1) | Simple, slow on large data |
| **Selection Sort** | O(n²) | O(n²) | O(n²) | O(1) | Always O(n²) regardless of input |
| **Insertion Sort** | O(n) | O(n²) | O(n²) | O(1) | Fast on nearly-sorted data |
| **Merge Sort** | O(n log n) | O(n log n) | O(n log n) | O(n) | Consistent, requires extra space |
| **Quick Sort** | O(n log n) | O(n log n) | O(n²) | O(log n) | Fast average case, bad if pivot is poor |
| **Python sorted()** | O(n log n) | O(n log n) | O(n log n) | O(n) | Uses Timsort (hybrid algorithm) |

---

## Binary Search

### Iterative Implementation

```python
def binary_search(arr, target):
    """
    Find target in sorted array.
    Returns: index if found, -1 if not found
    Time: O(log n)
    Space: O(1)
    """
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1  # Search right half
        else:
            right = mid - 1  # Search left half

    return -1  # Not found
```

### Recursive Implementation

```python
def binary_search_recursive(arr, target, left=0, right=None):
    """
    Recursive binary search.
    Time: O(log n)
    Space: O(log n) due to call stack
    """
    if right is None:
        right = len(arr) - 1

    if left > right:
        return -1  # Base case: not found

    mid = (left + right) // 2

    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        return binary_search_recursive(arr, target, left, mid - 1)
```

### Usage Example

```python
numbers = [1, 3, 5, 7, 9, 11, 13]
result = binary_search(numbers, 7)
print(result)  # Output: 3
```

---

## Bubble Sort

### Standard Implementation

```python
def bubble_sort(arr):
    """
    Bubble sort - repeatedly swap adjacent elements if in wrong order.
    Time: O(n²)
    Space: O(1)
    """
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr
```

### Optimized Implementation (stops if no swaps)

```python
def bubble_sort_optimized(arr):
    """
    Bubble sort with early termination.
    Best case: O(n) when array is already sorted
    """
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break  # Array is sorted
    return arr
```

### Usage Example

```python
numbers = [5, 3, 8, 1, 9]
result = bubble_sort(numbers)
print(result)  # Output: [1, 3, 5, 8, 9]
```

---

## Selection Sort

### Implementation

```python
def selection_sort(arr):
    """
    Selection sort - find minimum and place at beginning.
    Time: O(n²) always
    Space: O(1)
    """
    n = len(arr)
    for i in range(n):
        min_idx = i
        # Find minimum in remaining array
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        # Swap minimum with current position
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr
```

### Usage Example

```python
numbers = [5, 3, 8, 1, 9]
result = selection_sort(numbers)
print(result)  # Output: [1, 3, 5, 8, 9]
```

---

## Insertion Sort

### Implementation

```python
def insertion_sort(arr):
    """
    Insertion sort - build sorted array one element at a time.
    Time: O(n) best case (sorted), O(n²) worst case
    Space: O(1)
    """
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        # Shift larger elements right
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr
```

### Usage Example

```python
numbers = [5, 3, 8, 1, 9]
result = insertion_sort(numbers)
print(result)  # Output: [1, 3, 5, 8, 9]
```

---

## Merge Sort

### Implementation

```python
def merge_sort(arr):
    """
    Merge sort - divide and conquer recursive sort.
    Time: O(n log n) always
    Space: O(n) for temporary arrays
    """
    if len(arr) <= 1:
        return arr

    # Divide
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    # Conquer (merge)
    return merge(left, right)

def merge(left, right):
    """
    Merge two sorted arrays into one sorted array.
    """
    result = []
    i = j = 0

    # Compare elements from left and right
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    # Add remaining elements
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

### Usage Example

```python
numbers = [5, 3, 8, 1, 9]
result = merge_sort(numbers)
print(result)  # Output: [1, 3, 5, 8, 9]
```

---

## Quick Sort

### Implementation

```python
def quick_sort(arr):
    """
    Quick sort - divide and conquer with pivot.
    Time: O(n log n) average, O(n²) worst case
    Space: O(log n) for recursion
    """
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]

    return quick_sort(left) + middle + quick_sort(right)

def quick_sort_inplace(arr, low=0, high=None):
    """
    Quick sort in-place version (doesn't create new lists).
    """
    if high is None:
        high = len(arr) - 1

    if low < high:
        partition_idx = partition(arr, low, high)
        quick_sort_inplace(arr, low, partition_idx - 1)
        quick_sort_inplace(arr, partition_idx + 1, high)

    return arr

def partition(arr, low, high):
    """
    Partition array around pivot.
    """
    pivot = arr[high]
    i = low - 1

    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1
```

### Usage Example

```python
numbers = [5, 3, 8, 1, 9]
result = quick_sort(numbers)
print(result)  # Output: [1, 3, 5, 8, 9]
```

---

## Python's Built-in Sorting

### sorted() Function

```python
# Basic sorting
numbers = [5, 3, 8, 1, 9]
result = sorted(numbers)
print(result)  # [1, 3, 5, 8, 9]

# Reverse order
result = sorted(numbers, reverse=True)
print(result)  # [9, 8, 5, 3, 1]
```

### Sorting with key= Parameter

```python
# Sort by string length
words = ["apple", "pie", "zoo", "a"]
result = sorted(words, key=len)
print(result)  # ['a', 'pie', 'zoo', 'apple']

# Sort by absolute value
numbers = [-5, 3, -8, 1, -2]
result = sorted(numbers, key=abs)
print(result)  # [1, -2, 3, -5, -8]

# Sort dictionaries by value
students = [
    {'name': 'Alice', 'age': 20},
    {'name': 'Bob', 'age': 18},
    {'name': 'Charlie', 'age': 19}
]
result = sorted(students, key=lambda s: s['age'])
# [{'name': 'Bob', 'age': 18}, {'name': 'Charlie', 'age': 19}, {'name': 'Alice', 'age': 20}]

# Sort custom objects by attribute
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade

students = [Student('Alice', 85), Student('Bob', 92), Student('Charlie', 88)]
result = sorted(students, key=lambda s: s.grade)
# Sorted by grade

# Case-insensitive string sort
words = ["Apple", "banana", "Cherry"]
result = sorted(words, key=str.lower)
print(result)  # ['Apple', 'banana', 'Cherry']

# Multiple sort keys (tuple)
data = [('b', 2), ('a', 3), ('a', 1)]
result = sorted(data, key=lambda x: (x[0], x[1]))
# First sorts by first element, then by second if first is equal
print(result)  # [('a', 1), ('a', 3), ('b', 2)]
```

---

## Recursion Template

### Basic Pattern

```python
def recursive_function(n):
    # BASE CASE: when to stop
    if n == 0:  # or some stopping condition
        return 1  # or some base value

    # RECURSIVE CASE: call itself with smaller problem
    return n * recursive_function(n - 1)
```

### Common Patterns

**Factorial**
```python
def factorial(n):
    if n == 0 or n == 1:
        return 1
    return n * factorial(n - 1)
```

**Fibonacci**
```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```

**Sum of Array**
```python
def sum_array(arr):
    if len(arr) == 0:
        return 0
    return arr[0] + sum_array(arr[1:])
```

**Reverse String**
```python
def reverse_string(s):
    if len(s) == 0:
        return ""
    return reverse_string(s[1:]) + s[0]
```

**Binary Search Recursive**
```python
def binary_search(arr, target, left=0, right=None):
    if right is None:
        right = len(arr) - 1

    if left > right:
        return -1

    mid = (left + right) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search(arr, target, mid + 1, right)
    else:
        return binary_search(arr, target, left, mid - 1)
```

**Merge Sort Recursive**
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    return merge(left, right)
```

---

## Benchmarking with time Module

### Basic Timing

```python
import time

def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

# Time a single run
data = list(range(1000, 0, -1))  # Reverse sorted

start = time.time()
bubble_sort(data.copy())
end = time.time()

elapsed = end - start
print(f"Time: {elapsed:.6f} seconds")
```

### Averaging Multiple Runs

```python
import time
import random

def benchmark(sort_function, data, runs=3):
    """Benchmark a function by running it multiple times."""
    times = []

    for _ in range(runs):
        test_data = data.copy()
        start = time.time()
        sort_function(test_data)
        end = time.time()
        times.append(end - start)

    avg_time = sum(times) / len(times)
    return avg_time

# Test on different data sizes
data_100 = random.sample(range(1000), 100)
data_1000 = random.sample(range(10000), 1000)
data_5000 = random.sample(range(50000), 5000)

print("Bubble Sort Benchmarks:")
print(f"100 items: {benchmark(bubble_sort, data_100):.6f}s")
print(f"1000 items: {benchmark(bubble_sort, data_1000):.6f}s")
print(f"5000 items: {benchmark(bubble_sort, data_5000):.6f}s")
```

### Comparing Multiple Algorithms

```python
import time
import random

def compare_algorithms(data_size=1000):
    data = random.sample(range(data_size * 10), data_size)

    algorithms = {
        'Bubble Sort': bubble_sort,
        'Selection Sort': selection_sort,
        'Insertion Sort': insertion_sort,
        'Merge Sort': merge_sort,
        'Python sorted()': lambda x: sorted(x),
    }

    print(f"{'Algorithm':<20} {'Time (seconds)':<20}")
    print("-" * 40)

    for name, func in algorithms.items():
        start = time.time()
        func(data.copy())
        elapsed = time.time() - start
        print(f"{name:<20} {elapsed:.6f}")

compare_algorithms(1000)
```

---

## Algorithm Selection Quick Guide

**Use Linear Search when:**
- Data is unsorted
- Dataset is small
- You need simplicity

**Use Binary Search when:**
- Data is sorted
- Dataset is large
- Speed matters

**Use Bubble Sort when:**
- Data is nearly sorted (with optimization)
- Teaching/learning the concept
- Array is very small (<50 elements)

**Use Selection Sort when:**
- Memory is critical (O(1) space)
- Data is small
- Simplicity is more important than speed

**Use Insertion Sort when:**
- Data is nearly sorted
- Array is small to medium
- Stable sort is needed and online capability is useful

**Use Merge Sort when:**
- Consistent O(n log n) speed is needed
- Data is large
- Stability is important
- Extra space is available

**Use Quick Sort when:**
- Average-case speed is important
- Extra space is limited
- Good for general-purpose sorting

**Use Python's sorted() when:**
- In production code
- Writing real applications
- You need the best performance

---

## Common Mistakes to Avoid

1. **Binary Search:** Don't use on unsorted data
2. **Recursion:** Always include a base case to prevent infinite recursion
3. **Benchmarking:** Don't test with only one run — use multiple iterations
4. **Merge Sort:** Remember to create temporary arrays for merging
5. **Quick Sort:** Poor pivot selection can lead to O(n²) performance
6. **Bubble Sort:** Don't use on large datasets — it's quadratic
7. **Time Module:** Remember `time.time()` returns seconds since epoch, not elapsed time
8. **sorted() Key:** The key function receives each element individually

---

## Vocabulary

- **Algorithm:** Step-by-step procedure to solve a problem
- **Benchmark:** Measure actual execution time of code
- **Big O Notation:** Describes how algorithm performance scales with input size
- **Divide and Conquer:** Strategy that breaks problem into smaller subproblems
- **Pivot:** Element chosen to partition array in quick sort
- **Recursion:** Function calling itself with smaller input
- **Base Case:** Stopping condition in recursion
- **Recursive Case:** Part of recursion that calls itself
- **Stable Sort:** Maintains relative order of equal elements
- **In-place Sort:** Sorts without needing extra space
- **Timsort:** Python's hybrid sorting algorithm combining merge sort and insertion sort
- **Call Stack:** Memory structure that tracks function calls
