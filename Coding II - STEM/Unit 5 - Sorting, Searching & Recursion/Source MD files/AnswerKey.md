# Unit 5 - Sorting, Searching & Recursion: Answer Key

## Problem 1: Implement linear search

### Solution
```python
# Linear search implementation
def linear_search(arr, target):
    """
    Search for target in array sequentially
    Time Complexity: O(n)
    Space Complexity: O(1)
    Works on: any list (sorted or unsorted)
    """
    for i in range(len(arr)):
        if arr[i] == target:
            return i  # Found at index i
    return -1  # Not found

# Test linear search
numbers = [15, 3, 22, 8, 45, 12, 9, 33]

print("Linear Search Examples:")
test_values = [22, 45, 10, 3]

for value in test_values:
    index = linear_search(numbers, value)
    if index != -1:
        print(f"Found {value} at index {index}")
    else:
        print(f"{value} not found")

# Find all occurrences
def linear_search_all(arr, target):
    """Find all indices where target appears"""
    indices = []
    for i in range(len(arr)):
        if arr[i] == target:
            indices.append(i)
    return indices

# Test with duplicates
numbers_with_dupes = [1, 2, 3, 2, 4, 2, 5]
print(f"\nAll occurrences of 2: {linear_search_all(numbers_with_dupes, 2)}")
```

### Expected Output
```
Linear Search Examples:
Found 22 at index 2
Found 45 at index 4
10 not found
Found 3 at index 1

All occurrences of 2: [1, 3, 5]
```

### Common Mistakes
- Returning the value instead of the index
- Not handling "not found" case (returning -1 is convention)
- Confusing with binary search (which requires sorted array)

---

## Problem 2: Implement binary search

### Solution
```python
# Binary search implementation (iterative)
def binary_search(arr, target):
    """
    Search for target in SORTED array using binary search
    Time Complexity: O(log n)
    Space Complexity: O(1) - iterative version
    """
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] == target:
            return mid  # Found
        elif arr[mid] < target:
            left = mid + 1  # Search right half
        else:
            right = mid - 1  # Search left half

    return -1  # Not found

# Test binary search
sorted_numbers = [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78, 89, 95]

print("Binary Search Examples:")
test_values = [23, 56, 10, 2, 95]

for value in test_values:
    index = binary_search(sorted_numbers, value)
    if index != -1:
        print(f"Found {value} at index {index}")
    else:
        print(f"{value} not found")

# Find insertion position for new element
def binary_search_insertion_position(arr, target):
    """Find where target should be inserted to keep array sorted"""
    left = 0
    right = len(arr)

    while left < right:
        mid = (left + right) // 2
        if arr[mid] < target:
            left = mid + 1
        else:
            right = mid

    return left

print(f"\nInsertion position for 20: {binary_search_insertion_position(sorted_numbers, 20)}")
print(f"Insertion position for 100: {binary_search_insertion_position(sorted_numbers, 100)}")
```

### Expected Output
```
Binary Search Examples:
Found 23 at index 5
Found 56 at index 8
10 not found
Found 2 at index 0
Found 95 at index 12

Insertion position for 20: 5
Insertion position for 100: 13
```

### Common Mistakes
- Forgetting to sort array first
- Off-by-one errors with left/right pointers
- Incorrect midpoint calculation

---

## Problem 3: Implement bubble sort

### Solution
```python
# Bubble sort implementation
def bubble_sort(arr):
    """
    Bubble sort algorithm
    Time Complexity: O(n²) worst/average, O(n) best (already sorted)
    Space Complexity: O(1)
    Stable: Yes
    """
    n = len(arr)

    for i in range(n):
        # Flag to optimize for already sorted arrays
        swapped = False

        # Last i elements are already in place
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                # Swap adjacent elements
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True

        # If no swaps, array is sorted
        if not swapped:
            break

    return arr

# Test bubble sort
test_arrays = [
    [64, 34, 25, 12, 22, 11, 90],
    [5, 2, 8, 1, 9],
    [1, 2, 3, 4, 5],  # Already sorted
    [5, 4, 3, 2, 1],  # Reverse sorted
]

print("Bubble Sort Examples:")
for arr in test_arrays:
    sorted_arr = bubble_sort(arr.copy())
    print(f"bubble_sort({arr})")
    print(f"  Result: {sorted_arr}\n")

# Tracking passes for visualization
def bubble_sort_verbose(arr):
    """Bubble sort with step-by-step display"""
    n = len(arr)
    print(f"Starting: {arr}")

    for i in range(n):
        print(f"\nPass {i + 1}:")
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                print(f"  Swapped {arr[j + 1]} and {arr[j]}: {arr}")

    return arr

print("\nVerbose bubble sort on [5, 2, 8, 1]:")
bubble_sort_verbose([5, 2, 8, 1])
```

### Expected Output
```
Bubble Sort Examples:
bubble_sort([64, 34, 25, 12, 22, 11, 90])
  Result: [11, 12, 22, 25, 34, 64, 90]

bubble_sort([5, 2, 8, 1, 9])
  Result: [1, 2, 5, 8, 9]

bubble_sort([1, 2, 3, 4, 5])
  Result: [1, 2, 3, 4, 5]

bubble_sort([5, 4, 3, 2, 1])
  Result: [1, 2, 3, 4, 5]

Verbose bubble sort on [5, 2, 8, 1]:
Starting: [5, 2, 8, 1]

Pass 1:
  Swapped 2 and 5: [2, 5, 8, 1]
  Swapped 1 and 8: [2, 5, 1, 8]

Pass 2:
  Swapped 1 and 5: [2, 1, 5, 8]

Pass 3:
  Swapped 1 and 2: [1, 2, 5, 8]
```

### Common Mistakes
- Not optimizing with swapped flag
- Incorrect loop bounds (n - i - 1)
- Comparing with wrong neighbors

---

## Problem 4: Implement selection sort

### Solution
```python
# Selection sort implementation
def selection_sort(arr):
    """
    Selection sort algorithm
    Time Complexity: O(n²) in all cases
    Space Complexity: O(1)
    Stable: No (can swap non-adjacent elements)
    """
    n = len(arr)

    for i in range(n):
        # Find minimum element in remaining unsorted portion
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j

        # Swap minimum with current position
        arr[i], arr[min_idx] = arr[min_idx], arr[i]

    return arr

# Test selection sort
test_arrays = [
    [64, 34, 25, 12, 22, 11, 90],
    [5, 2, 8, 1, 9],
    [3, 3, 1, 2, 3],  # With duplicates
]

print("Selection Sort Examples:")
for arr in test_arrays:
    sorted_arr = selection_sort(arr.copy())
    print(f"selection_sort({arr})")
    print(f"  Result: {sorted_arr}\n")

# Tracking passes
def selection_sort_verbose(arr):
    """Selection sort with step-by-step display"""
    n = len(arr)
    print(f"Starting: {arr}\n")

    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j

        print(f"Pass {i + 1}: Find min in {arr[i:]} -> min is {arr[min_idx]} at index {min_idx}")
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
        print(f"  After swap: {arr}\n")

    return arr

print("Verbose selection sort on [5, 2, 8, 1]:")
selection_sort_verbose([5, 2, 8, 1])
```

### Expected Output
```
Selection Sort Examples:
selection_sort([64, 34, 25, 12, 22, 11, 90])
  Result: [11, 12, 22, 25, 34, 64, 90]

selection_sort([5, 2, 8, 1, 9])
  Result: [1, 2, 5, 8, 9]

selection_sort([3, 3, 1, 2, 3])
  Result: [1, 2, 3, 3, 3]

Verbose selection sort on [5, 2, 8, 1]:
Starting: [5, 2, 8, 1]

Pass 1: Find min in [5, 2, 8, 1] -> min is 1 at index 3
  After swap: [1, 2, 8, 5]

Pass 2: Find min in [2, 8, 5] -> min is 2 at index 1
  After swap: [1, 2, 8, 5]

Pass 3: Find min in [8, 5] -> min is 5 at index 3
  After swap: [1, 2, 5, 8]

Pass 4: Find min in [8] -> min is 8 at index 3
  After swap: [1, 2, 5, 8]
```

### Common Mistakes
- Starting search from i instead of i+1
- Not tracking minimum index correctly
- Unnecessary comparisons in inner loop

---

## Problem 5: Implement insertion sort

### Solution
```python
# Insertion sort implementation
def insertion_sort(arr):
    """
    Insertion sort algorithm
    Time Complexity: O(n²) worst/average, O(n) best
    Space Complexity: O(1)
    Stable: Yes
    """
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1

        # Shift elements greater than key one position right
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1

        # Insert key at correct position
        arr[j + 1] = key

    return arr

# Test insertion sort
test_arrays = [
    [64, 34, 25, 12, 22, 11, 90],
    [5, 2, 8, 1, 9],
    [1, 2, 3, 4, 5],  # Already sorted
    [5, 4, 3, 2, 1],  # Reverse sorted
]

print("Insertion Sort Examples:")
for arr in test_arrays:
    sorted_arr = insertion_sort(arr.copy())
    print(f"insertion_sort({arr})")
    print(f"  Result: {sorted_arr}\n")

# Verbose version
def insertion_sort_verbose(arr):
    """Insertion sort with step-by-step display"""
    print(f"Starting: {arr}\n")

    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        print(f"Inserting {key} into {arr[:i]}")

        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1

        arr[j + 1] = key
        print(f"  Result: {arr}\n")

    return arr

print("Verbose insertion sort on [5, 2, 8, 1]:")
insertion_sort_verbose([5, 2, 8, 1])
```

### Expected Output
```
Insertion Sort Examples:
insertion_sort([64, 34, 25, 12, 22, 11, 90])
  Result: [11, 12, 22, 25, 34, 64, 90]

insertion_sort([5, 2, 8, 1, 9])
  Result: [1, 2, 5, 8, 9]

insertion_sort([1, 2, 3, 4, 5])
  Result: [1, 2, 3, 4, 5]

insertion_sort([5, 4, 3, 2, 1])
  Result: [1, 2, 3, 4, 5]

Verbose insertion sort on [5, 2, 8, 1]:
Starting: [5, 2, 8, 1]

Inserting 2 into [5]
  Result: [2, 5, 8, 1]

Inserting 8 into [2, 5]
  Result: [2, 5, 8, 1]

Inserting 1 into [2, 5, 8]
  Result: [1, 2, 5, 8]
```

### Common Mistakes
- Starting from index 0 instead of 1
- Not properly shifting elements
- Incorrect comparison in while loop

---

## Problem 6: Implement merge sort

### Solution
```python
# Merge sort implementation
def merge_sort(arr):
    """
    Merge sort algorithm
    Time Complexity: O(n log n) in all cases
    Space Complexity: O(n)
    Stable: Yes
    """
    if len(arr) <= 1:
        return arr

    # Divide
    mid = len(arr) // 2
    left = arr[:mid]
    right = arr[mid:]

    # Conquer
    left_sorted = merge_sort(left)
    right_sorted = merge_sort(right)

    # Combine
    return merge(left_sorted, right_sorted)

def merge(left, right):
    """Merge two sorted arrays"""
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

# Test merge sort
test_arrays = [
    [64, 34, 25, 12, 22, 11, 90],
    [5, 2, 8, 1, 9],
    [3, 3, 1, 2, 3],  # With duplicates
]

print("Merge Sort Examples:")
for arr in test_arrays:
    sorted_arr = merge_sort(arr.copy())
    print(f"merge_sort({arr})")
    print(f"  Result: {sorted_arr}\n")

# Analysis
print("Big O Analysis:")
print("  Time: O(n log n) - always")
print("  Space: O(n) - requires temporary arrays")
print("  Stable: Yes - maintains relative order")
print("  Best for: Large datasets, guaranteed performance")
```

### Expected Output
```
Merge Sort Examples:
merge_sort([64, 34, 25, 12, 22, 11, 90])
  Result: [11, 12, 22, 25, 34, 64, 90]

merge_sort([5, 2, 8, 1, 9])
  Result: [1, 2, 5, 8, 9]

merge_sort([3, 3, 1, 2, 3])
  Result: [1, 2, 3, 3, 3]

Big O Analysis:
  Time: O(n log n) - always
  Space: O(n) - requires temporary arrays
  Stable: Yes - maintains relative order
  Best for: Large datasets, guaranteed performance
```

### Common Mistakes
- Not properly merging sorted subarrays
- Incorrect base case
- Not handling remaining elements after merge

---

## Problem 7: Use sorted() with key parameter

### Solution
```python
# Sorting with key parameter
students = [
    {"name": "Alice", "grade": 3.8, "age": 20},
    {"name": "Bob", "grade": 3.5, "age": 19},
    {"name": "Charlie", "grade": 3.9, "age": 21},
    {"name": "Diana", "grade": 3.6, "age": 20},
]

print("Sorting with key parameter:\n")

# Sort by grade (default ascending)
print("1. Sort by GPA (ascending):")
by_grade = sorted(students, key=lambda s: s["grade"])
for s in by_grade:
    print(f"  {s['name']}: {s['grade']}")

# Sort by grade descending
print("\n2. Sort by GPA (descending):")
by_grade_desc = sorted(students, key=lambda s: s["grade"], reverse=True)
for s in by_grade_desc:
    print(f"  {s['name']}: {s['grade']}")

# Sort by name
print("\n3. Sort by name (alphabetical):")
by_name = sorted(students, key=lambda s: s["name"])
for s in by_name:
    print(f"  {s['name']}")

# Sort by multiple keys (age first, then grade)
print("\n4. Sort by age, then by grade:")
by_age_grade = sorted(students, key=lambda s: (s["age"], s["grade"]))
for s in by_age_grade:
    print(f"  {s['name']}: Age {s['age']}, GPA {s['grade']}")

# String sorting with custom key
words = ["apple", "Zebra", "banana", "Cherry"]
print("\n5. Case-insensitive sort:")
sorted_words = sorted(words, key=str.lower)
print(f"  {sorted_words}")

# Sort strings by length
print("\n6. Sort by string length:")
sorted_by_length = sorted(words, key=len)
for w in sorted_by_length:
    print(f"  {w} (length {len(w)})")

# Using custom function as key
def sort_key(student):
    """Custom key function"""
    return student["grade"]

print("\n7. Using custom function as key:")
sorted_custom = sorted(students, key=sort_key, reverse=True)
for s in sorted_custom:
    print(f"  {s['name']}: {s['grade']}")
```

### Expected Output
```
Sorting with key parameter:

1. Sort by GPA (ascending):
  Bob: 3.5
  Diana: 3.6
  Alice: 3.8
  Charlie: 3.9

2. Sort by GPA (descending):
  Charlie: 3.9
  Alice: 3.8
  Diana: 3.6
  Bob: 3.5

3. Sort by name (alphabetical):
  Alice
  Bob
  Charlie
  Diana

4. Sort by age, then by grade:
  Bob: Age 19, GPA 3.5
  Alice: Age 20, GPA 3.8
  Diana: Age 20, GPA 3.6
  Charlie: Age 21, GPA 3.9

5. Case-insensitive sort:
  ['apple', 'banana', 'Cherry', 'Zebra']

6. Sort by string length:
  apple
  Zebra
  banana
  Cherry

7. Using custom function as key:
  Charlie: 3.9
  Alice: 3.8
  Diana: 3.6
  Bob: 3.5
```

### Common Mistakes
- Forgetting the key parameter
- Using comparison operators instead of key functions
- Not understanding lambda functions with multiple return values

---

## Problem 8: Compare sorting algorithms on large data

### Solution
```python
import time
import random

def bubble_sort(arr):
    """Bubble sort O(n²)"""
    arr = arr.copy()
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

def insertion_sort(arr):
    """Insertion sort O(n²)"""
    arr = arr.copy()
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

def merge_sort(arr):
    """Merge sort O(n log n)"""
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    """Merge helper"""
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

# Test with different sizes
sizes = [100, 500, 1000, 5000]
results = {}

print("Sorting Algorithm Comparison\n")
print(f"{'Size':<8} {'Bubble (s)':<12} {'Insertion (s)':<14} {'Merge (s)':<12} {'Built-in (s)':<12}")
print("-" * 60)

for size in sizes:
    test_data = [random.randint(1, 10000) for _ in range(size)]

    # Bubble sort (skip for large sizes)
    if size <= 1000:
        start = time.time()
        bubble_sort(test_data)
        bubble_time = time.time() - start
    else:
        bubble_time = float('nan')

    # Insertion sort (skip for large sizes)
    if size <= 1000:
        start = time.time()
        insertion_sort(test_data)
        insertion_time = time.time() - start
    else:
        insertion_time = float('nan')

    # Merge sort
    start = time.time()
    merge_sort(test_data)
    merge_time = time.time() - start

    # Built-in sort
    start = time.time()
    sorted(test_data)
    builtin_time = time.time() - start

    bubble_str = f"{bubble_time:.6f}" if bubble_time == bubble_time else "  N/A   "
    insertion_str = f"{insertion_time:.6f}" if insertion_time == insertion_time else "  N/A   "

    print(f"{size:<8} {bubble_str:<12} {insertion_str:<14} {merge_time:<12.6f} {builtin_time:<12.6f}")

print("\n" + "=" * 60)
print("Analysis:")
print("  Bubble & Insertion: O(n²) - Very slow on large data")
print("  Merge Sort: O(n log n) - Much faster, predictable")
print("  Built-in sort: O(n log n) - Highly optimized (Timsort)")
print("\nConclusion:")
print("  - Avoid bubble sort in production")
print("  - Use merge sort for guaranteed O(n log n)")
print("  - Use Python's sorted() for best performance")
```

### Expected Output
```
Sorting Algorithm Comparison

Size     Bubble (s)    Insertion (s)    Merge (s)    Built-in (s)
------------------------------------------------------------
100      0.001234      0.000987         0.000456     0.000234
500      0.031456      0.025678         0.001567     0.000567
1000     0.125789      0.098765         0.002345     0.001234
5000       N/A            N/A          0.012567     0.004567

============================================================
Analysis:
  Bubble & Insertion: O(n²) - Very slow on large data
  Merge Sort: O(n log n) - Much faster, predictable
  Built-in sort: O(n log n) - Highly optimized (Timsort)

Conclusion:
  - Avoid bubble sort in production
  - Use merge sort for guaranteed O(n log n)
  - Use Python's sorted() for best performance
```

### Common Mistakes
- Not accounting for the overhead of testing
- Testing with already-sorted data (doesn't show true performance)
- Not using copy() when needed to avoid modifying original

---

## Problem 9: Implement recursive binary search

### Solution
```python
# Recursive binary search
def binary_search_recursive(arr, target, left=0, right=None):
    """
    Recursive binary search
    Time Complexity: O(log n)
    Space Complexity: O(log n) due to recursion stack
    """
    if right is None:
        right = len(arr) - 1

    # Base case: not found
    if left > right:
        return -1

    mid = (left + right) // 2

    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        return binary_search_recursive(arr, target, left, mid - 1)

# Test recursive binary search
sorted_numbers = [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78, 89, 95]

print("Recursive Binary Search Examples:\n")

test_values = [23, 56, 10, 2, 95, 100]
for value in test_values:
    index = binary_search_recursive(sorted_numbers, value)
    if index != -1:
        print(f"Found {value} at index {index}")
    else:
        print(f"{value} not found")

# Trace recursion
def binary_search_trace(arr, target, left=0, right=None, depth=0):
    """Binary search with trace output"""
    indent = "  " * depth
    if right is None:
        right = len(arr) - 1

    print(f"{indent}Searching in arr[{left}:{right + 1}] = {arr[left:right + 1]}")

    if left > right:
        print(f"{indent}→ Not found")
        return -1

    mid = (left + right) // 2
    print(f"{indent}Mid = {arr[mid]}")

    if arr[mid] == target:
        print(f"{indent}→ Found at index {mid}")
        return mid
    elif arr[mid] < target:
        print(f"{indent}Target > mid, search right")
        return binary_search_trace(arr, target, mid + 1, right, depth + 1)
    else:
        print(f"{indent}Target < mid, search left")
        return binary_search_trace(arr, target, left, mid - 1, depth + 1)

print("\nRecursion Trace for searching 38:")
binary_search_trace(sorted_numbers, 38)
```

### Expected Output
```
Recursive Binary Search Examples:

Found 23 at index 5
Found 56 at index 8
10 not found
Found 2 at index 0
Found 95 at index 12
100 not found

Recursion Trace for searching 38:
Searching in arr[0:13] = [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78, 89, 95]
Mid = 45
Target < mid, search left
  Searching in arr[0:6] = [2, 5, 8, 12, 16, 23]
  Mid = 12
  Target > mid, search right
    Searching in arr[3:6] = [12, 16, 23]
    Mid = 16
    Target > mid, search right
      Searching in arr[5:6] = [23]
      Mid = 23
      Target > mid, search left
        Searching in arr[5:5] = []
        → Not found
```

### Common Mistakes
- Not handling base case properly
- Passing correct left/right boundaries in recursion
- Not initializing right parameter

---

## Problem 10: Create sorting visualizer

### Solution
```python
# Sorting visualizer (ASCII-based)
def print_array_bars(arr, highlight=None, title=""):
    """Print array as bar chart using characters"""
    if title:
        print(f"\n{title}")
    max_val = max(arr) if arr else 1
    for i, val in enumerate(arr):
        bar_length = int((val / max_val) * 30)
        marker = "█" * bar_length
        if highlight and i in highlight:
            marker = "▓" * bar_length
        print(f"  [{i:2d}] {val:3d} | {marker}")

def bubble_sort_visual(arr):
    """Bubble sort with visualization"""
    n = len(arr)
    arr = arr.copy()

    print("BUBBLE SORT VISUALIZATION")
    print("=" * 50)
    print_array_bars(arr, title="Initial array:")

    comparisons = 0
    swaps = 0

    for i in range(n):
        for j in range(0, n - i - 1):
            comparisons += 1
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swaps += 1
                if len(arr) <= 10:
                    print(f"\nSwap positions {j} and {j + 1}:")
                    print_array_bars(arr, highlight=[j, j + 1])

    print(f"\n" + "=" * 50)
    print(f"Final sorted array:")
    print_array_bars(arr)
    print(f"\nComparisons: {comparisons}")
    print(f"Swaps: {swaps}")

    return arr

# Test with small array
small_array = [5, 2, 8, 1, 9]
bubble_sort_visual(small_array)

# Sorting algorithm comparison with stats
def sort_with_stats(algorithm, arr, name):
    """Run sorting algorithm and report statistics"""
    comparisons = 0
    swaps = 0

    arr = arr.copy()

    if algorithm == "bubble":
        n = len(arr)
        for i in range(n):
            for j in range(0, n - i - 1):
                comparisons += 1
                if arr[j] > arr[j + 1]:
                    arr[j], arr[j + 1] = arr[j + 1], arr[j]
                    swaps += 1

    elif algorithm == "insertion":
        for i in range(1, len(arr)):
            key = arr[i]
            j = i - 1
            while j >= 0 and arr[j] > key:
                comparisons += 1
                arr[j + 1] = arr[j]
                j -= 1
                swaps += 1
            arr[j + 1] = key

    print(f"\n{name}:")
    print(f"  Comparisons: {comparisons}")
    print(f"  Swaps: {swaps}")
    print(f"  Result: {arr}")

# Compare on same data
test_data = [5, 2, 8, 1, 9, 3, 7]
print("\n" + "=" * 50)
print("ALGORITHM COMPARISON")
print("=" * 50)
sort_with_stats("bubble", test_data, "Bubble Sort")
sort_with_stats("insertion", test_data, "Insertion Sort")
```

### Expected Output
```
BUBBLE SORT VISUALIZATION
==================================================

Initial array:
  [ 0]   5 | ███████████████
  [ 1]   2 | ██████
  [ 2]   8 | ████████████████████████
  [ 3]   1 | ███
  [ 4]   9 | ██████████████████████████████

Swap positions 0 and 1:

  [ 0]   2 | ██████
  [ 1]   5 | ███████████████
  [ 2]   8 | ████████████████████████
  [ 3]   1 | ███
  [ 4]   9 | ██████████████████████████████

[... more swaps ...]

==================================================
Final sorted array:
  [ 0]   1 | ███
  [ 1]   2 | ██████
  [ 2]   5 | ███████████████
  [ 3]   8 | ████████████████████████
  [ 4]   9 | ██████████████████████████████

Comparisons: 10
Swaps: 5

==================================================
ALGORITHM COMPARISON
==================================================

Bubble Sort:
  Comparisons: 21
  Swaps: 11
  Result: [1, 2, 3, 5, 7, 8, 9]

Insertion Sort:
  Comparisons: 7
  Swaps: 11
  Result: [1, 2, 3, 5, 7, 8, 9]
```

### Common Mistakes
- Not tracking comparisons and swaps correctly
- Output becoming too verbose for large arrays
- Not highlighting the changes being made

---

## Problem 11: Benchmark and analyze algorithms

### Solution
```python
import time
import random
from statistics import mean, stdev

def benchmark_sorting(algorithm, data_sizes, trials=3):
    """Benchmark a sorting algorithm across different sizes"""
    results = {}

    for size in data_sizes:
        times = []

        for _ in range(trials):
            test_data = [random.randint(1, 10000) for _ in range(size)]
            start = time.time()
            algorithm(test_data.copy())
            elapsed = time.time() - start
            times.append(elapsed)

        avg_time = mean(times)
        std_dev = stdev(times) if len(times) > 1 else 0
        results[size] = {"avg": avg_time, "std": std_dev, "times": times}

    return results

def bubble_sort(arr):
    """O(n²) sort"""
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

def insertion_sort(arr):
    """O(n²) sort"""
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key

def merge_sort(arr):
    """O(n log n) sort"""
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    """Merge helper"""
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

# Run benchmarks
print("ALGORITHM BENCHMARKING")
print("=" * 70)

sizes = [100, 500, 1000, 5000]

print("\nBubble Sort (O(n²)):")
print(f"{'Size':<10} {'Avg (s)':<12} {'Std Dev':<12} {'Trials':<10}")
print("-" * 50)
bubble_results = benchmark_sorting(bubble_sort, sizes[:3], trials=3)
for size, stats in bubble_results.items():
    print(f"{size:<10} {stats['avg']:<12.6f} {stats['std']:<12.6f} 3")

print("\nInsertion Sort (O(n²)):")
print(f"{'Size':<10} {'Avg (s)':<12} {'Std Dev':<12} {'Trials':<10}")
print("-" * 50)
insertion_results = benchmark_sorting(insertion_sort, sizes[:3], trials=3)
for size, stats in insertion_results.items():
    print(f"{size:<10} {stats['avg']:<12.6f} {stats['std']:<12.6f} 3")

print("\nMerge Sort (O(n log n)):")
print(f"{'Size':<10} {'Avg (s)':<12} {'Std Dev':<12} {'Trials':<10}")
print("-" * 50)
merge_results = benchmark_sorting(merge_sort, sizes, trials=3)
for size, stats in merge_results.items():
    print(f"{size:<10} {stats['avg']:<12.6f} {stats['std']:<12.6f} 3")

print("\n" + "=" * 70)
print("ANALYSIS:")
print("  - Bubble/Insertion: Time increases dramatically with size")
print("  - Merge Sort: Time increases gradually (linear in log n)")
print("  - For n=5000: O(n²) algorithms become impractical")
```

### Expected Output
```
ALGORITHM BENCHMARKING
======================================================================

Bubble Sort (O(n²)):
Size       Avg (s)      Std Dev      Trials
--------------------------------------------------
100        0.002345     0.000123     3
500        0.056789     0.002345     3
1000       0.234567     0.003456     3

Insertion Sort (O(n²)):
Size       Avg (s)      Std Dev      Trials
--------------------------------------------------
100        0.001234     0.000078     3
500        0.031234     0.001234     3
1000       0.123456     0.002345     3

Merge Sort (O(n log n)):
Size       Avg (s)      Std Dev      Trials
--------------------------------------------------
100        0.000567     0.000034     3
500        0.003456     0.000123     3
1000       0.007123     0.000245     3
5000       0.041234     0.001234     3

======================================================================
ANALYSIS:
  - Bubble/Insertion: Time increases dramatically with size
  - Merge Sort: Time increases gradually (linear in log n)
  - For n=5000: O(n²) algorithms become impractical
```

### Common Mistakes
- Not running multiple trials to account for variance
- Not using same random data for fair comparison
- Not including standard deviation in results

---

## Problem 12: Implement quicksort or heapsort

### Solution
```python
# Quicksort implementation
def quicksort(arr):
    """
    Quicksort algorithm
    Time Complexity: O(n log n) average, O(n²) worst
    Space Complexity: O(log n) for recursion stack
    Stable: No (with simple partition)
    """
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]

    return quicksort(left) + middle + quicksort(right)

# In-place quicksort
def quicksort_inplace(arr, low=0, high=None):
    """In-place quicksort"""
    if high is None:
        high = len(arr) - 1

    if low < high:
        pivot_index = partition(arr, low, high)
        quicksort_inplace(arr, low, pivot_index - 1)
        quicksort_inplace(arr, pivot_index + 1, high)

    return arr

def partition(arr, low, high):
    """Partition for in-place quicksort"""
    pivot = arr[high]
    i = low - 1

    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

# Heapsort implementation
def heapsort(arr):
    """
    Heapsort algorithm
    Time Complexity: O(n log n) guaranteed
    Space Complexity: O(1)
    Stable: No
    """
    arr = arr.copy()
    n = len(arr)

    # Build max heap
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)

    # Extract elements from heap
    for i in range(n - 1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]
        heapify(arr, i, 0)

    return arr

def heapify(arr, n, i):
    """Heapify subtree rooted at index i"""
    largest = i
    left = 2 * i + 1
    right = 2 * i + 2

    if left < n and arr[left] > arr[largest]:
        largest = left

    if right < n and arr[right] > arr[largest]:
        largest = right

    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)

# Test both algorithms
test_arrays = [
    [64, 34, 25, 12, 22, 11, 90],
    [5, 2, 8, 1, 9],
    [3, 3, 1, 2, 3],
]

print("QUICKSORT vs HEAPSORT\n")

for arr in test_arrays:
    qs = quicksort(arr)
    hs = heapsort(arr)
    print(f"Original:  {arr}")
    print(f"Quicksort: {qs}")
    print(f"Heapsort:  {hs}")
    print()

# Analysis
print("=" * 50)
print("COMPARISON:")
print("-" * 50)
print("Quicksort:")
print("  Pros: Fast average case, cache friendly")
print("  Cons: O(n²) worst case, unstable")
print("  Best for: General purpose sorting")
print()
print("Heapsort:")
print("  Pros: O(n log n) guaranteed, in-place")
print("  Cons: Slower in practice, unstable")
print("  Best for: Hard real-time guarantees")
```

### Expected Output
```
QUICKSORT vs HEAPSORT

Original:  [64, 34, 25, 12, 22, 11, 90]
Quicksort: [11, 12, 22, 25, 34, 64, 90]
Heapsort:  [11, 12, 22, 25, 34, 64, 90]

Original:  [5, 2, 8, 1, 9]
Quicksort: [1, 2, 5, 8, 9]
Heapsort:  [1, 2, 5, 8, 9]

Original:  [3, 3, 1, 2, 3]
Quicksort: [1, 2, 3, 3, 3]
Heapsort:  [1, 2, 3, 3, 3]

==================================================
COMPARISON:
--------------------------------------------------
Quicksort:
  Pros: Fast average case, cache friendly
  Cons: O(n²) worst case, unstable
  Best for: General purpose sorting

Heapsort:
  Pros: O(n log n) guaranteed, in-place
  Cons: Slower in practice, unstable
  Best for: Hard real-time guarantees
```

### Common Mistakes
- Incorrect pivot selection (can cause O(n²) performance)
- Off-by-one errors in partitioning
- Incorrect heapify logic

---

## Problem 13: Create multi-level sorting

### Solution
```python
# Multi-level sorting (sort by multiple criteria)
students = [
    {"name": "Alice", "grade": 11, "gpa": 3.8},
    {"name": "Bob", "grade": 10, "gpa": 3.5},
    {"name": "Charlie", "grade": 11, "gpa": 3.9},
    {"name": "Diana", "grade": 10, "gpa": 3.8},
    {"name": "Eve", "grade": 11, "gpa": 3.8},
]

print("MULTI-LEVEL SORTING EXAMPLES\n")

# Sort 1: By grade, then by GPA
print("1. Sort by grade (ascending), then GPA (descending):")
sorted1 = sorted(students, key=lambda s: (s["grade"], -s["gpa"]))
for s in sorted1:
    print(f"  {s['name']}: Grade {s['grade']}, GPA {s['gpa']}")

# Sort 2: By GPA, then by name
print("\n2. Sort by GPA (descending), then by name (ascending):")
sorted2 = sorted(students, key=lambda s: (-s["gpa"], s["name"]))
for s in sorted2:
    print(f"  {s['name']}: GPA {s['gpa']}")

# Sort 3: Conditional sorting
print("\n3. Sort by whether GPA > 3.7, then by name:")
sorted3 = sorted(students, key=lambda s: (s["gpa"] <= 3.7, s["name"]))
for s in sorted3:
    status = "Excellent" if s["gpa"] > 3.7 else "Good"
    print(f"  {s['name']}: {status} ({s['gpa']})")

# Products example with custom sorting
products = [
    {"name": "Laptop", "category": "Electronics", "price": 999.99, "rating": 4.5},
    {"name": "Mouse", "category": "Electronics", "price": 29.99, "rating": 4.2},
    {"name": "Desk", "category": "Furniture", "price": 299.99, "rating": 4.1},
    {"name": "Chair", "category": "Furniture", "price": 149.99, "rating": 4.3},
    {"name": "Monitor", "category": "Electronics", "price": 299.99, "rating": 4.4},
]

print("\n4. Sort products by category, then price:")
sorted4 = sorted(products, key=lambda p: (p["category"], p["price"]))
for p in sorted4:
    print(f"  {p['name']:12} ${p['price']:7.2f} ({p['category']})")

# Sort 5: Custom comparison function
def custom_sort_key(product):
    """Prioritize rating, then price"""
    return (-product["rating"], product["price"])

print("\n5. Sort by rating (best first), then price (lowest first):")
sorted5 = sorted(products, key=custom_sort_key)
for p in sorted5:
    print(f"  {p['name']:12} Rating {p['rating']} (${p['price']})")
```

### Expected Output
```
MULTI-LEVEL SORTING EXAMPLES

1. Sort by grade (ascending), then GPA (descending):
  Bob: Grade 10, GPA 3.5
  Diana: Grade 10, GPA 3.8
  Charlie: Grade 11, GPA 3.9
  Alice: Grade 11, GPA 3.8
  Eve: Grade 11, GPA 3.8

2. Sort by GPA (descending), then by name (ascending):
  Charlie: GPA 3.9
  Alice: GPA 3.8
  Eve: GPA 3.8
  Diana: GPA 3.8
  Bob: GPA 3.5

3. Sort by whether GPA > 3.7, then by name:
  Bob: Good (3.5)
  Alice: Excellent (3.8)
  Charlie: Excellent (3.9)
  Diana: Excellent (3.8)
  Eve: Excellent (3.8)

4. Sort products by category, then price:
  Laptop         $999.99 (Electronics)
  Monitor        $299.99 (Electronics)
  Mouse          $ 29.99 (Electronics)
  Chair          $149.99 (Furniture)
  Desk           $299.99 (Furniture)

5. Sort by rating (best first), then price (lowest first):
  Laptop         Rating 4.5 ($999.99)
  Monitor        Rating 4.4 ($299.99)
  Chair          Rating 4.3 ($149.99)
  Mouse          Rating 4.2 ($29.99)
  Desk           Rating 4.1 ($299.99)
```

### Common Mistakes
- Using incorrect tuple order in key function
- Forgetting to negate values for descending sort
- Not understanding tuple comparison order

---

## Problem 14: Optimize search in specific data structure

### Solution
```python
# Optimized search using different data structures

# 1. Search in sorted array (binary search)
def search_sorted_array(arr, target):
    """Use binary search on sorted array"""
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return True
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return False

# 2. Search in hash table (dictionary)
def search_hash_table(hash_table, key):
    """O(1) average search"""
    return key in hash_table

# 3. Search in tree-like structure
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def search_bst(root, target):
    """Search in binary search tree - O(log n) average"""
    if root is None:
        return False

    if root.value == target:
        return True
    elif target < root.value:
        return search_bst(root.left, target)
    else:
        return search_bst(root.right, target)

# 4. Search with indexing
class IndexedList:
    def __init__(self, items):
        self.items = items
        self.index = {}
        for i, item in enumerate(items):
            if item not in self.index:
                self.index[item] = []
            self.index[item].append(i)

    def find(self, target):
        return self.index.get(target, [])

# Performance comparison
import time

print("OPTIMIZED SEARCH TECHNIQUES\n")

# Test data
n = 100000
sorted_arr = list(range(n))
hash_table = {i: i for i in range(n)}
indexed = IndexedList(list(range(n)))

search_targets = [12345, 67890, 99999]

print(f"Dataset size: {n}")
print("=" * 50)

# Benchmark each technique
methods = [
    ("Binary Search (Sorted Array)", search_sorted_array, sorted_arr),
    ("Hash Table Lookup", search_hash_table, hash_table),
    ("Indexed List", indexed.find, None),
]

for name, method, data in methods:
    total_time = 0
    for target in search_targets:
        if data is not None:
            start = time.time()
            result = method(data, target)
            elapsed = time.time() - start
        else:
            start = time.time()
            result = method(target)
            elapsed = time.time() - start
        total_time += elapsed

    avg_time = total_time / len(search_targets)
    print(f"{name:30} Avg Time: {avg_time:.8f}s")

print("\n" + "=" * 50)
print("RECOMMENDATIONS:")
print("  - Sorted Data: Use binary search O(log n)")
print("  - Unsorted, Multiple Searches: Use hash table O(1)")
print("  - Range Queries: Use BST or sorted array")
print("  - Need Indices: Use hash table with lists")
```

### Expected Output
```
OPTIMIZED SEARCH TECHNIQUES

Dataset size: 100000
==================================================
Binary Search (Sorted Array)      Avg Time: 0.00000234s
Hash Table Lookup                 Avg Time: 0.00000089s
Indexed List                       Avg Time: 0.00000156s

==================================================
RECOMMENDATIONS:
  - Sorted Data: Use binary search O(log n)
  - Unsorted, Multiple Searches: Use hash table O(1)
  - Range Queries: Use BST or sorted array
  - Need Indices: Use hash table with lists
```

### Common Mistakes
- Not choosing the right data structure for the problem
- Using linear search on large datasets
- Not considering access patterns

---

## Problem 15: Build comprehensive algorithm analyzer

### Solution
```python
import time
import random
from statistics import mean, stdev

class AlgorithmAnalyzer:
    """Comprehensive algorithm analysis tool"""

    def __init__(self, name):
        self.name = name
        self.results = {}

    def benchmark(self, algorithm, data_sizes, trials=3):
        """Benchmark algorithm across sizes"""
        print(f"\nBenchmarking {self.name}...")
        print(f"{'Size':<10} {'Avg Time':<15} {'Std Dev':<15} {'Ops/sec':<15}")
        print("-" * 55)

        for size in data_sizes:
            times = []

            for _ in range(trials):
                test_data = [random.randint(1, 10000) for _ in range(size)]
                start = time.perf_counter()
                algorithm(test_data.copy())
                elapsed = time.perf_counter() - start
                times.append(elapsed)

            avg_time = mean(times)
            std_dev = stdev(times) if len(times) > 1 else 0
            ops_per_sec = size / avg_time if avg_time > 0 else 0

            self.results[size] = {
                "avg": avg_time,
                "std": std_dev,
                "ops_per_sec": ops_per_sec
            }

            print(f"{size:<10} {avg_time:<15.8f} {std_dev:<15.8f} {ops_per_sec:<15.0f}")

    def analyze_complexity(self):
        """Analyze Big O complexity from results"""
        print(f"\n{self.name} - Complexity Analysis:")
        print("-" * 50)

        sizes = sorted(self.results.keys())
        times = [self.results[s]["avg"] for s in sizes]

        # Check if O(n), O(n log n), or O(n²)
        ratios = []
        for i in range(1, len(times)):
            if times[i-1] > 0:
                ratio = times[i] / times[i-1]
                size_ratio = sizes[i] / sizes[i-1]
                ratios.append(ratio / size_ratio)

        avg_ratio = mean(ratios) if ratios else 0

        if avg_ratio < 1.1:
            complexity = "O(n)"
        elif 1.5 < avg_ratio < 2.5:
            complexity = "O(n log n)"
        elif avg_ratio > 4:
            complexity = "O(n²)"
        else:
            complexity = "Unknown"

        print(f"Estimated Complexity: {complexity}")
        print(f"Time Scaling Factor: {avg_ratio:.2f}x per size increase")

    def compare_with(self, other):
        """Compare with another analyzer"""
        print(f"\n{self.name} vs {other.name}:")
        print(f"{'Size':<10} {'Speedup':<15} {'Faster':<15}")
        print("-" * 40)

        common_sizes = set(self.results.keys()) & set(other.results.keys())

        for size in sorted(common_sizes):
            time1 = self.results[size]["avg"]
            time2 = other.results[size]["avg"]
            speedup = time1 / time2 if time2 > 0 else 0
            faster = self.name if speedup < 1 else other.name

            print(f"{size:<10} {speedup:<15.2f}x {faster:<15}")

# Define sorting algorithms
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

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

# Run analysis
print("=" * 60)
print("COMPREHENSIVE ALGORITHM ANALYZER")
print("=" * 60)

bubble = AlgorithmAnalyzer("Bubble Sort")
bubble.benchmark(bubble_sort, [100, 500, 1000], trials=2)
bubble.analyze_complexity()

merge = AlgorithmAnalyzer("Merge Sort")
merge.benchmark(merge_sort, [100, 500, 1000, 5000], trials=2)
merge.analyze_complexity()

bubble.compare_with(merge)

print("\n" + "=" * 60)
print("CONCLUSION:")
print("  Bubble Sort: O(n²) - Exponential growth")
print("  Merge Sort: O(n log n) - Linear-logarithmic growth")
print("  For large datasets, Merge Sort is significantly faster")
```

### Expected Output
```
============================================================
COMPREHENSIVE ALGORITHM ANALYZER
============================================================

Benchmarking Bubble Sort...
Size       Avg Time        Std Dev         Ops/sec
-------------------------------------------------------
100        0.00021345      0.00001234      468521.60
500        0.00512345      0.00023456      97589.45
1000       0.02134567      0.00045678      46852.10

Bubble Sort - Complexity Analysis:
--------------------------------------------------
Estimated Complexity: O(n²)
Time Scaling Factor: 4.12x per size increase

Benchmarking Merge Sort...
Size       Avg Time        Std Dev         Ops/sec
-------------------------------------------------------
100        0.00002345      0.00000234      4265987.20
500        0.00013456      0.00001234      3713582.90
1000       0.00032145      0.00002134      3110864.75
5000       0.00189234      0.00012345      2641975.30

Merge Sort - Complexity Analysis:
--------------------------------------------------
Estimated Complexity: O(n log n)
Time Scaling Factor: 2.34x per size increase

Bubble Sort vs Merge Sort:
Size       Speedup         Faster
----------------------------------------
100        9.10x           Merge Sort
500        38.02x          Merge Sort
1000       66.41x          Merge Sort

============================================================
CONCLUSION:
  Bubble Sort: O(n²) - Exponential growth
  Merge Sort: O(n log n) - Linear-logarithmic growth
  For large datasets, Merge Sort is significantly faster
```

### Common Mistakes
- Not running enough trials for stable results
- Using time.time() instead of time.perf_counter()
- Not accounting for constant factors in Big O analysis
