# Unit 5: Sorting, Searching & Recursion — Complete Answer Key

---

## Beginner Problems

---

## Problem 1: Linear Search

### Solution
```python
def linear_search(arr, target):
    """Linear search: check each element sequentially."""
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

# Test cases
assert linear_search([1, 3, 5, 7, 9], 5) == 2
assert linear_search([1, 3, 5, 7, 9], 1) == 0
assert linear_search([1, 3, 5, 7, 9], 9) == 4
assert linear_search([1, 3, 5, 7, 9], 4) == -1
assert linear_search([], 5) == -1
```

### Expected Output
```
(all assertions pass - no output)
```

### Common Mistakes
- Returning True/False instead of index/-1
- Starting index from 1 instead of 0
- Returning inside loop without checking all elements
- Not handling empty list (would return -1, which is correct)

---

## Problem 2: Trace Bubble Sort

### Solution
```
Initial: [3, 1, 4, 1, 5]
Pass 1: [1, 3, 1, 4, 5]  (5 bubbles to end)
Pass 2: [1, 1, 3, 4, 5]  (4 bubbles to position)
Pass 3: [1, 1, 3, 4, 5]  (3 in correct position)
Pass 4: [1, 1, 3, 4, 5]  (1 in correct position)
Final: [1, 1, 3, 4, 5]
```

### Expected Output
```
[1, 1, 3, 4, 5]
```

### Common Mistakes
- Getting the order wrong after each pass
- Comparing adjacent elements incorrectly
- Not bubbling the largest to the end each pass

---

## Problem 3: Binary Search vs Linear Search

### Solution
```
For 1 million sorted elements:

Linear Search (worst case): 1,000,000 comparisons
Binary Search (worst case): log₂(1,000,000) ≈ 20 comparisons

Binary search is 50,000 times faster!
```

### Expected Output
```
Binary search is much faster (O(log n) vs O(n))
```

### Common Mistakes
- Thinking binary search works on unsorted arrays (must be sorted!)
- Calculating log₂(1,000,000) as 1 million / 2 repeatedly
- Not realizing the exponential difference in large datasets

---

## Problem 4: Recursion Base Case

### Solution
```python
def countdown(n):
    """Countdown from n to 0."""
    if n < 0:  # BASE CASE: stop when n is negative
        return
    print(n)
    countdown(n - 1)  # RECURSIVE CASE: call with n-1

# Test
countdown(5)
# Output: 5 4 3 2 1 0
```

### Expected Output
```
5
4
3
2
1
0
```

### Common Mistakes
- No base case (infinite recursion)
- Base case wrong: `if n == 0` doesn't stop before printing negative
- Not decreasing n: `countdown(n)` instead of `countdown(n - 1)`
- Printing after recursive call (reverses order)

---

## Problem 5: Selection Sort Algorithm

### Solution
```python
def selection_sort(arr):
    """Selection sort: find min, place at beginning."""
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

# Test
assert selection_sort([5, 3, 8, 1, 9]) == [1, 3, 5, 8, 9]
```

### Expected Output
```
[1, 3, 5, 8, 9]
```

### Common Mistakes
- Starting inner loop at `i` instead of `i+1` (compares element with itself)
- Comparing with wrong element: `arr[j] > arr[min_idx]` (ascending vs descending)
- Not swapping, just updating index
- Returning None instead of array

---

## Intermediate Problems

---

## Problem 6: Recursive Binary Search

### Solution
```python
def binary_search_recursive(arr, target, left=0, right=None):
    """Recursive binary search."""
    if right is None:
        right = len(arr) - 1

    if left > right:
        return -1  # BASE CASE: not found

    mid = (left + right) // 2

    if arr[mid] == target:
        return mid  # BASE CASE: found
    elif arr[mid] < target:
        # Search right half
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        # Search left half
        return binary_search_recursive(arr, target, left, mid - 1)

# Test
assert binary_search_recursive([1, 3, 5, 7, 9, 11], 7) == 3
assert binary_search_recursive([1, 3, 5, 7, 9, 11], 1) == 0
assert binary_search_recursive([1, 3, 5, 7, 9, 11], 11) == 5
assert binary_search_recursive([1, 3, 5, 7, 9, 11], 4) == -1
```

### Expected Output
```
(all assertions pass)
```

### Common Mistakes
- Not setting right = len(arr) - 1 initially
- Using `mid` instead of `mid + 1` or `mid - 1` in recursive calls
- Returning -1 for mid instead of mid when found
- Wrong comparison operators: < vs >

---

## Problem 7: Insertion Sort Tracing

### Solution
```
Initial: [5, 2, 4, 6, 1, 3]
Insert 2: [2, 5, 4, 6, 1, 3]  (2 shifts left of 5)
Insert 4: [2, 4, 5, 6, 1, 3]  (4 shifts left of 5)
Insert 6: [2, 4, 5, 6, 1, 3]  (6 already in place)
Insert 1: [1, 2, 4, 5, 6, 3]  (1 moves to front)
Insert 3: [1, 2, 3, 4, 5, 6]  (3 moves to correct position)
Final: [1, 2, 3, 4, 5, 6]
```

### Expected Output
```
[1, 2, 3, 4, 5, 6]
```

### Common Mistakes
- Getting the order of insertions wrong
- Not shifting elements properly
- Comparing with wrong elements
- Starting from wrong index

---

## Problem 8: Merge Sort Implementation

### Solution
```python
def merge_sort(arr):
    """Divide and conquer sorting."""
    if len(arr) <= 1:
        return arr  # BASE CASE

    # DIVIDE
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    # CONQUER
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

# Test
assert merge_sort([5, 3, 8, 1, 9, 2]) == [1, 2, 3, 5, 8, 9]
assert merge_sort([1]) == [1]
assert merge_sort([]) == []
assert merge_sort([5, 4, 3, 2, 1]) == [1, 2, 3, 4, 5]
```

### Expected Output
```
[1, 2, 3, 5, 8, 9]
[1]
[]
[1, 2, 3, 4, 5]
```

### Common Mistakes
- Not having base case: `if len(arr) <= 1`
- Wrong merge logic: comparing in wrong direction
- Not extending remaining elements
- Using `<` instead of `<=` in merge (affects stability)

---

## Problem 9: Algorithm Complexity Analysis

### Solution
```python
def find_pairs(arr):
    """Find all pairs that sum to 10 — O(n²)."""
    result = []
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if arr[i] + arr[j] == 10:
                result.append((arr[i], arr[j]))
    return result

# Time: O(n²) - nested loops, each up to n iterations
# Space: O(k) - k pairs found

# OPTIMIZED - O(n)
def find_pairs_optimized(arr):
    """Find pairs using set — O(n)."""
    seen = set()
    result = []
    target = 10

    for num in arr:
        complement = target - num
        if complement in seen:
            result.append((min(num, complement), max(num, complement)))
        seen.add(num)

    return list(set(result))  # Remove duplicates

# Test
arr = [3, 7, 2, 8, 1, 9]
print(find_pairs(arr))           # [(3, 7), (2, 8), (1, 9)]
print(find_pairs_optimized(arr)) # [(1, 9), (2, 8), (3, 7)]
```

### Expected Output
```
[(3, 7), (2, 8), (1, 9)]
[(1, 9), (2, 8), (3, 7)]
```

### Common Mistakes
- Thinking inner loop optimization matters for Big O (both still O(n²))
- Not recognizing set lookup is O(1)
- Not removing duplicate pairs in optimized version
- Using wrong target value

---

## Problem 10: Sorting Custom Objects

### Solution
```python
students = [
    {'name': 'Alice', 'age': 20},
    {'name': 'Bob', 'age': 18},
    {'name': 'Charlie', 'age': 19},
]

# Sort by age ascending
result = sorted(students, key=lambda s: s['age'])

assert result[0]['age'] == 18
assert result[1]['age'] == 19
assert result[2]['age'] == 20
```

### Expected Output
```
(assertions pass)
```

### Common Mistakes
- Not using `key` parameter
- Wrong lambda: `lambda s: s` (doesn't sort by age)
- Using `s.age` instead of `s['age']` (dictionaries use bracket notation)
- Not using reverse=True for descending

---

## Problem 11: Quick Sort Partition

### Solution
```python
def partition(arr, low, high):
    """Partition array using last element as pivot."""
    pivot = arr[high]
    i = low - 1

    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

# Test
arr = [3, 7, 1, 9, 2]
pivot_idx = partition(arr, 0, 4)
# After partition: [1, 2, 3, 9, 7]
```

### Expected Output
```
[1, 2, 3, 9, 7]
```

### Common Mistakes
- Starting i at 0 instead of -1 (index confusion)
- Not swapping correctly
- Comparing with wrong pivot value
- Not returning correct partition index

---

## Problem 12: Compare Two Algorithms

### Solution
```
For 10,000 random elements:

Bubble Sort:  O(n²) = 100,000,000 operations ≈ 1-2 seconds
Insertion Sort: O(n²) = 100,000,000 operations ≈ 0.2-0.5 seconds
Merge Sort: O(n log n) = 130,000 operations ≈ 0.001-0.01 seconds

Insertion sort is 2-5x faster than bubble sort (better constants)
Merge sort is 100-1000x faster than insertion sort
```

### Expected Output
```
Insertion sort is faster than bubble sort for same Big O
```

### Common Mistakes
- Thinking Big O is all that matters (constant factors count!)
- Not measuring actual time with timer
- Not understanding why insertion sort is faster
- Using too small dataset (modern computers may not show difference)

---

## Challenge Problems

---

## Problem 13: Fibonacci with Memoization

### Solution
```python
def fibonacci(n, memo=None):
    """Fibonacci with memoization."""
    if memo is None:
        memo = {}

    if n in memo:
        return memo[n]

    if n <= 1:
        return n

    result = fibonacci(n - 1, memo) + fibonacci(n - 2, memo)
    memo[n] = result
    return result

# Test
assert fibonacci(0) == 0
assert fibonacci(1) == 1
assert fibonacci(5) == 5
assert fibonacci(10) == 55
assert fibonacci(20) == 6765
```

### Expected Output
```
(all assertions pass)
```

### Common Mistakes
- Not initializing memo as {}
- Not checking if n in memo before calculating
- Not storing result in memo
- Not having base case: if n <= 1

---

## Problem 14: Three-Way Partition

### Solution
```python
def partition_colors(arr):
    """Partition 0s, 1s, 2s in one pass."""
    low = 0
    mid = 0
    high = len(arr) - 1

    while mid <= high:
        if arr[mid] == 0:
            arr[low], arr[mid] = arr[mid], arr[low]
            low += 1
            mid += 1
        elif arr[mid] == 1:
            mid += 1
        else:  # arr[mid] == 2
            arr[mid], arr[high] = arr[high], arr[mid]
            high -= 1

    return arr

# Test
arr = [2, 0, 1, 2, 1, 0]
partition_colors(arr)
assert arr == [0, 0, 1, 1, 2, 2]
```

### Expected Output
```
[0, 0, 1, 1, 2, 2]
```

### Common Mistakes
- Using wrong number of pointers (need 3: low, mid, high)
- Not incrementing mid after moving 0
- Incrementing mid after swapping 2 (should not increment)
- Not swapping when moving 2

---

## Problem 15: Find Kth Smallest Element

### Solution
```python
def find_kth_smallest(arr, k):
    """Find kth smallest using sorted."""
    sorted_arr = sorted(arr)
    return sorted_arr[k - 1]

# Alternative: Quick Select (average O(n))
def find_kth_smallest_fast(arr, k):
    """Quick select algorithm."""
    return quick_select(arr, 0, len(arr) - 1, k - 1)

def quick_select(arr, low, high, k_index):
    if low == high:
        return arr[low]

    pivot_idx = partition(arr, low, high)

    if k_index == pivot_idx:
        return arr[k_index]
    elif k_index < pivot_idx:
        return quick_select(arr, low, pivot_idx - 1, k_index)
    else:
        return quick_select(arr, pivot_idx + 1, high, k_index)

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

# Test
arr = [3, 1, 4, 1, 5, 9, 2, 6]
assert find_kth_smallest(arr, 1) == 1
assert find_kth_smallest(arr, 2) == 1
assert find_kth_smallest(arr, 3) == 2
assert find_kth_smallest(arr, 8) == 9
```

### Expected Output
```
(all assertions pass)
```

### Common Mistakes
- Using 0-based indexing: `sorted_arr[k]` instead of `[k-1]`
- Quick select pivot logic confused
- Not handling ties (duplicate values)

---

## Problem 16: Median of Two Sorted Arrays

### Solution
```python
def find_median(arr1, arr2):
    """Find median using two pointers."""
    if len(arr1) > len(arr2):
        arr1, arr2 = arr2, arr1

    total_length = len(arr1) + len(arr2)
    mid = (total_length + 1) // 2

    i = j = 0
    prev = curr = 0

    for _ in range(mid):
        prev = curr
        if i < len(arr1) and (j >= len(arr2) or arr1[i] <= arr2[j]):
            curr = arr1[i]
            i += 1
        else:
            curr = arr2[j]
            j += 1

    if total_length % 2 == 1:
        return float(curr)
    else:
        return (prev + curr) / 2.0

# Test
assert find_median([1, 3], [2]) == 2.0
assert find_median([1, 2], [3, 4]) == 2.5
assert find_median([1, 3, 5], [2, 4, 6]) == 3.5
```

### Expected Output
```
(all assertions pass)
```

### Common Mistakes
- Wrong median calculation for even-length arrays
- Not handling empty array case
- Using wrong pointer advancement logic
- Median calculation for odd vs even different

---

## Problem 17: Inversion Count

### Solution
```python
def count_inversions(arr):
    """Count inversions using merge sort."""
    _, count = merge_sort_count(arr)
    return count

def merge_sort_count(arr):
    if len(arr) <= 1:
        return arr, 0

    mid = len(arr) // 2
    left, left_inv = merge_sort_count(arr[:mid])
    right, right_inv = merge_sort_count(arr[mid:])
    merged, split_inv = merge_count(left, right)

    return merged, left_inv + right_inv + split_inv

def merge_count(left, right):
    result = []
    inversions = 0
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            inversions += len(left) - i  # All remaining left > right[j]
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result, inversions

# Test
assert count_inversions([3, 1, 2]) == 2
assert count_inversions([1, 2, 3]) == 0
assert count_inversions([3, 2, 1]) == 3
```

### Expected Output
```
(all assertions pass)
```

### Common Mistakes
- Using brute force O(n²) instead of merge sort O(n log n)
- Not counting inversions during merge
- Wrong count: `len(left) - i - 1` instead of `len(left) - i`

---

## Problem 18: Stable Sort Requirement

### Solution
```python
class Item:
    def __init__(self, id, priority):
        self.id = id
        self.priority = priority

    def __repr__(self):
        return f"Item({self.id}, {self.priority})"

items = [
    Item(1, 3),
    Item(2, 1),
    Item(3, 3),
    Item(4, 2),
]

# Python's sorted() is stable
result = sorted(items, key=lambda item: item.priority)

# Verify: items with priority 3 should be in original order
assert result[0].id == 2  # priority 1
assert result[1].id == 4  # priority 2
assert result[2].id == 1  # priority 3 (came before Item 3)
assert result[3].id == 3  # priority 3 (came after Item 1)
```

### Expected Output
```
(assertions pass)
```

### Common Mistakes
- Using unstable sort (quick sort)
- Assuming order doesn't matter
- Not testing with equal keys
- Not using stable sort in library

---

## Problem 19: Benchmark Sorting Algorithms

### Solution
```python
import time
import random

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

def benchmark(sort_func, data, runs=3):
    times = []
    for _ in range(runs):
        test_data = data.copy()
        start = time.time()
        if sort_func == merge_sort:
            sort_func(test_data)
        else:
            sort_func(test_data)
        times.append(time.time() - start)
    return sum(times) / len(times)

# Test on different sizes
sizes = [100, 1000, 10000]
print(f"{'Size':<10} {'Bubble Sort':<20} {'Insertion Sort':<20} {'Merge Sort':<20}")
print("-" * 70)

for size in sizes:
    data = random.sample(range(size * 10), size)
    bubble_time = benchmark(bubble_sort, data)
    insertion_time = benchmark(insertion_sort, data)
    merge_time = benchmark(merge_sort, data)
    print(f"{size:<10} {bubble_time:<20.6f} {insertion_time:<20.6f} {merge_time:<20.6f}")
```

### Expected Output
```
Size       Bubble Sort          Insertion Sort       Merge Sort
---------------------------------------------------------------
100        0.000050             0.000020             0.000005
1000       0.005000             0.002000             0.000080
10000      1.000000             0.400000             0.001500
```

### Common Mistakes
- Not averaging multiple runs
- Timing includes I/O or other overhead
- Using same list (already sorted from first test)
- Not using random data

---

## Problem 20: Custom Comparator for Complex Sorting

### Solution
```python
class Student:
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa

    def __repr__(self):
        return f"Student({self.name}, {self.gpa})"

students = [
    Student("Alice", 3.8),
    Student("Bob", 3.8),
    Student("Charlie", 3.5),
    Student("Diana", 3.8),
]

# Sort by: GPA descending (-gpa), then name ascending (name)
result = sorted(students, key=lambda s: (-s.gpa, s.name))

# Verify order
assert result[0].name == "Alice"      # 3.8, alphabetically first
assert result[1].name == "Bob"        # 3.8, alphabetically second
assert result[2].name == "Diana"      # 3.8, alphabetically third
assert result[3].name == "Charlie"    # 3.5, lowest GPA
```

### Expected Output
```
[Student(Alice, 3.8), Student(Bob, 3.8), Student(Diana, 3.8), Student(Charlie, 3.5)]
```

### Common Mistakes
- Using tuple without parentheses: `lambda s: -s.gpa, s.name` (syntax error)
- Not negating GPA: `s.gpa` (ascending instead of descending)
- Wrong order in tuple: `(s.name, -s.gpa)` (name first, then GPA)
- Using `reverse=True` (applies to all fields, not just first)

---
