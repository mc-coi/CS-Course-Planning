# Unit 5: Sorting, Searching & Recursion

> Master the algorithms that power software: searching for data efficiently and sorting it in order.

---

## Unit Overview

**Duration:** 28 days / ~5.5 weeks

**Key Concepts:** Linear search, binary search, bubble sort, selection sort, insertion sort, merge sort, quick sort, recursion, Big O notation, algorithm benchmarking, divide-and-conquer

**Big Idea:** Efficient algorithms are the foundation of fast software — the difference between O(n) and O(n²) can be the difference between instant results and waiting hours.

**TN Standard:** 9-12.CCI.3 — Design and implement algorithms

---

## Learning Targets

By the end of this unit, students will be able to:

- I can implement and trace linear and binary search algorithms
- I can implement bubble sort, selection sort, and insertion sort
- I can implement merge sort and explain divide-and-conquer
- I can implement quick sort with pivot-based partitioning
- I can use Python's built-in sorting with custom key functions
- I can compare algorithms using Big O notation
- I can benchmark algorithms to measure real-world performance
- I can solve recursive problems by identifying base and recursive cases
- I can optimize algorithms based on performance analysis

---

## Daily Lesson Breakdown

### **Day 1: Review — Recursion Fundamentals**

**Learning Target:** I can identify base cases and recursive cases in recursive functions.

**Key Concepts:**
- Recursion: A function calling itself with a simpler version of the problem
- Base case: The stopping condition that prevents infinite recursion
- Recursive case: The part where the function calls itself with smaller input
- Call stack: How function calls are tracked in memory

**Code Examples:**

```python
# Factorial: n! = n × (n-1)!
def factorial(n):
    if n == 0 or n == 1:  # BASE CASE
        return 1
    else:  # RECURSIVE CASE
        return n * factorial(n - 1)

# Sum of a list
def sum_list(arr):
    if len(arr) == 0:  # BASE CASE
        return 0
    else:  # RECURSIVE CASE
        return arr[0] + sum_list(arr[1:])

# Power function: x^n
def power(x, n):
    if n == 0:  # BASE CASE
        return 1
    else:  # RECURSIVE CASE
        return x * power(x, n - 1)
```

**Practice:**
- Trace factorial(5) on the call stack
- Implement sum_list and test it
- Identify base and recursive cases in power function

---

### **Day 2: Recursion Deep Dive — Call Stack Visualization**

**Learning Target:** I can visualize the call stack and explain how recursion works in memory.

**Key Concepts:**
- Call stack: LIFO (Last In First Out) data structure
- Stack frame: Memory allocated for each function call
- Unwinding the stack: Returning values back up the call stack
- Stack overflow: When recursion depth exceeds system limit

**Code Examples:**

```python
# Fibonacci with call stack tracing
def fibonacci(n, indent=0):
    print("  " * indent + f"fib({n})")
    if n <= 1:
        return n
    return fibonacci(n - 1, indent + 1) + fibonacci(n - 2, indent + 1)

# Call: fibonacci(5)
# Prints the call tree showing all recursive calls

# Countdown with stack visualization
def countdown(n):
    print(f"Start countdown({n})")
    if n == 0:
        print("Blastoff!")
        return
    countdown(n - 1)
    print(f"End countdown({n})")

countdown(3)
# Shows how stack frames are created and destroyed
```

**Practice:**
- Trace fibonacci(4) and draw the call tree
- Use print statements to visualize call stack depth
- Understand stack frame creation and destruction

---

### **Day 3: Linear Search — Algorithm and Implementation**

**Learning Target:** I can implement linear search and understand its characteristics.

**Key Concepts:**
- Linear search: Check each element one by one
- Time complexity: O(n) — must check every element
- Works on sorted AND unsorted data
- Simple to implement and understand

**Code Examples:**

```python
def linear_search(arr, target):
    """Find target by checking each element."""
    for i in range(len(arr)):
        if arr[i] == target:
            return i  # Found it
    return -1  # Not found

# Example
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
result = linear_search(numbers, 5)
print(result)  # Output: 4

# Count occurrences
def count_occurrences(arr, target):
    count = 0
    for i in range(len(arr)):
        if arr[i] == target:
            count += 1
    return count

print(count_occurrences(numbers, 1))  # Output: 2
```

**Practice:**
- Implement linear_search
- Find the value at position that would be slowest (last or not found)
- Discuss when linear search is necessary (unsorted data)

---

### **Day 4: Linear Search Analysis and Practice**

**Learning Target:** I can analyze linear search and compare it to other algorithms.

**Key Concepts:**
- Best case: O(n) — element is first
- Average case: O(n) — must check about half the elements
- Worst case: O(n) — element is last or not in array
- Always O(n) because best case is still checking every element in worst case

**Code Examples:**

```python
# Compare to Python's 'in' operator
def manual_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return True
    return False

# Python built-in (also linear search for lists)
result = target in numbers

# With early return for finding position
def find_position(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return None

# Multiple criteria search
def find_student_by_grade(students, target_grade):
    for student in students:
        if student['grade'] == target_grade:
            return student
    return None
```

**Practice:**
- Time linear_search on arrays of different sizes
- Understand why best case doesn't change Big O analysis
- Implement variations (find all, count, etc.)

---

### **Day 5: Binary Search Prerequisites — Why Data Must Be Sorted**

**Learning Target:** I can explain why binary search requires sorted data.

**Key Concepts:**
- Binary search eliminates half the search space each iteration
- This only works if you know: smaller values are on one side, larger on the other
- Sorting enables this guarantee
- Tradeoff: Can sort once, then search many times quickly

**Code Examples:**

```python
# Why sorting helps
unsorted = [5, 2, 8, 1, 9, 3, 7]
sorted_arr = [1, 2, 3, 5, 7, 8, 9]

# With sorted data, searching for 5:
# Can split at middle: [1, 2, 3] [5] [7, 8, 9]
# Know to search left because 5 > 3 but < 7

# With unsorted data, you can't make this guarantee
# [5, 2, 8] -- is 5 likely to be on left or right of 8? Unknown!

# Sorting code
import random
numbers = [random.randint(1, 100) for _ in range(1000)]
sorted_numbers = sorted(numbers)  # Now can use binary search
```

**Practice:**
- Understand the relationship between sorting and searching
- See why binary search on unsorted data gives wrong results
- Discuss the cost/benefit: sort once O(n log n), then search O(log n)

---

### **Day 6: Binary Search — Iterative Implementation**

**Learning Target:** I can implement binary search iteratively.

**Key Concepts:**
- Iterative approach: Use a loop with left and right pointers
- Each iteration, move left or right pointer based on comparison
- Time complexity: O(log n) — cut search space in half each time
- Space complexity: O(1) — no extra data structures

**Code Examples:**

```python
def binary_search(arr, target):
    """Iterative binary search."""
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] == target:
            return mid  # Found!
        elif arr[mid] < target:
            left = mid + 1  # Search right half
        else:
            right = mid - 1  # Search left half

    return -1  # Not found

# Example
numbers = [1, 3, 5, 7, 9, 11, 13, 15]
result = binary_search(numbers, 7)
print(result)  # Output: 3

# Find range of equal elements
def binary_search_range(arr, target):
    """Find first and last position of target."""
    left, right = 0, len(arr) - 1
    first = last = -1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            first = mid
            right = mid - 1  # Keep searching left
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    # Similar process for finding last position
    left = 0
    right = len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            last = mid
            left = mid + 1  # Keep searching right
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return first, last
```

**Practice:**
- Trace binary_search on paper
- Implement and test on various arrays
- Find first and last occurrence of target

---

### **Day 7: Binary Search — Recursive Implementation**

**Learning Target:** I can implement binary search recursively.

**Key Concepts:**
- Recursive approach: Function calls itself with new left/right bounds
- Base cases: target found, or search space exhausted
- Recursive case: search left or right half
- Space complexity: O(log n) due to call stack depth

**Code Examples:**

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
        # RECURSIVE CASE: search right
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        # RECURSIVE CASE: search left
        return binary_search_recursive(arr, target, left, mid - 1)

# Example
numbers = [1, 3, 5, 7, 9, 11, 13, 15]
result = binary_search_recursive(numbers, 7)
print(result)  # Output: 3

# Count occurrences recursively
def count_target(arr, target, left=0, right=None):
    if right is None:
        right = len(arr) - 1

    if left > right:
        return 0

    mid = (left + right) // 2

    if arr[mid] == target:
        # Found one, count left and right
        return 1 + count_target(arr, target, left, mid - 1) + \
               count_target(arr, target, mid + 1, right)
    elif arr[mid] < target:
        return count_target(arr, target, mid + 1, right)
    else:
        return count_target(arr, target, left, mid - 1)
```

**Practice:**
- Compare iterative vs recursive implementations
- Understand call stack depth with recursion
- Trace recursive calls for small examples

---

### **Day 8: Bubble Sort — Algorithm Walkthrough**

**Learning Target:** I can explain how bubble sort works and trace it.

**Key Concepts:**
- Bubble sort: Repeatedly swap adjacent elements if in wrong order
- Each pass bubbles the largest unsorted element to the end
- Needs n-1 passes for n elements
- Inefficient but easy to understand

**Code Examples:**

```python
def bubble_sort(arr):
    """Bubble sort - simplest version."""
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

# Example
numbers = [5, 3, 8, 1, 9, 2]
bubble_sort(numbers)
print(numbers)  # Output: [1, 2, 3, 5, 8, 9]

# Trace on [5, 3, 8, 1]
# Pass 1: [3, 5, 1, 8] (8 bubbled to end)
# Pass 2: [3, 1, 5, 8] (5 bubbled to position)
# Pass 3: [1, 3, 5, 8] (3 bubbled to position)

# Visualization
def bubble_sort_verbose(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                print(f"Swapped {arr[j+1]} and {arr[j]}: {arr}")
```

**Practice:**
- Manually trace bubble sort on small arrays
- Count number of comparisons and swaps
- Understand why it's called "bubble" sort

---

### **Day 9: Bubble Sort — Code and Optimizations**

**Learning Target:** I can implement bubble sort with optimizations.

**Key Concepts:**
- Optimization: Stop early if no swaps occur (array is sorted)
- Best case: O(n) with optimization on sorted data
- Worst case: Still O(n²) on reverse-sorted data
- Swap optimization reduces operations but not Big O

**Code Examples:**

```python
def bubble_sort_optimized(arr):
    """Bubble sort with early termination."""
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break  # Array is sorted, exit early
    return arr

# Example
numbers = [1, 2, 3, 4, 5]  # Already sorted
bubble_sort_optimized(numbers)  # Exits after first pass with no swaps

# Cocktail sort variant (bubble from both ends)
def cocktail_sort(arr):
    n = len(arr)
    for i in range(n // 2):
        # Forward pass
        for j in range(i, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
        # Backward pass
        for j in range(n - i - 2, i, -1):
            if arr[j - 1] > arr[j]:
                arr[j - 1], arr[j] = arr[j], arr[j - 1]
    return arr
```

**Practice:**
- Test optimized version on different input types
- Measure improvement on nearly-sorted data
- Understand when optimization helps

---

### **Day 10: Bubble Sort — Big O Analysis**

**Learning Target:** I can analyze bubble sort's time and space complexity.

**Key Concepts:**
- Best case: O(n) with optimization (nearly sorted data)
- Average case: O(n²) — about n²/2 comparisons
- Worst case: O(n²) — about n²/2 comparisons
- Space: O(1) — sorts in place, no extra data structures

**Code Examples:**

```python
import time
import random

def bubble_sort(arr):
    n = len(arr)
    comparisons = 0
    swaps = 0
    for i in range(n):
        for j in range(0, n - i - 1):
            comparisons += 1
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swaps += 1
    return arr, comparisons, swaps

# Test on different sizes
for n in [10, 100, 1000]:
    data = random.sample(range(n * 10), n)
    _, comps, swaps = bubble_sort(data.copy())
    print(f"n={n}: {comps} comparisons, {swaps} swaps")
    # Results show n²/2 pattern

# Timing analysis
sizes = [100, 200, 400]
times = []
for size in sizes:
    data = random.sample(range(size * 10), size)
    start = time.time()
    bubble_sort(data)
    times.append(time.time() - start)

# If O(n²), doubling n quadruples time
for i in range(1, len(times)):
    ratio = times[i] / times[i-1]
    print(f"Doubling size: {ratio:.1f}x slower (expect ~4x for O(n²))")
```

**Practice:**
- Count comparisons and swaps manually
- Time on different array sizes
- Verify O(n²) relationship
- Compare to other O(n²) algorithms

---

### **Day 11: Selection Sort — Algorithm and Code**

**Learning Target:** I can implement and understand selection sort.

**Key Concepts:**
- Selection sort: Find minimum and place it at the beginning
- Repeat for remaining unsorted portion
- Always O(n²) regardless of input (no best case)
- Few swaps: O(n) swaps, O(n²) comparisons

**Code Examples:**

```python
def selection_sort(arr):
    """Selection sort - find min and place at front."""
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

# Example
numbers = [5, 3, 8, 1, 9, 2]
selection_sort(numbers)
print(numbers)  # Output: [1, 2, 3, 5, 8, 9]

# Trace on [5, 3, 8, 1]
# i=0: min=1 at j=3, swap: [1, 3, 8, 5]
# i=1: min=3 at j=1 (current), no swap: [1, 3, 8, 5]
# i=2: min=5 at j=3, swap: [1, 3, 5, 8]
# i=3: only [8] remains

# With selection_sort details
def selection_sort_verbose(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        if i != min_idx:
            arr[i], arr[min_idx] = arr[min_idx], arr[i]
            print(f"Selection {i}: {arr}")
```

**Practice:**
- Trace selection sort step by step
- Count comparisons (always n(n-1)/2)
- Count swaps (always n-1)
- Compare efficiency to bubble sort

---

### **Day 12: Selection Sort vs Bubble Sort Comparison**

**Learning Target:** I can compare selection sort and bubble sort.

**Key Concepts:**
- Both are O(n²), but different constant factors
- Bubble: Many swaps (~n²/2), but simple logic
- Selection: Fewer swaps (n), better in practice
- Neither should be used on large datasets

**Code Examples:**

```python
import time
import random

def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]

# Compare on same data
sizes = [100, 500, 1000]
print(f"{'Size':<10} {'Bubble':<15} {'Selection':<15} {'Ratio':<10}")
for size in sizes:
    data = random.sample(range(size * 10), size)

    start = time.time()
    bubble_sort(data.copy())
    bubble_time = time.time() - start

    start = time.time()
    selection_sort(data.copy())
    selection_time = time.time() - start

    ratio = bubble_time / selection_time
    print(f"{size:<10} {bubble_time:<15.6f} {selection_time:<15.6f} {ratio:<10.1f}x")

# Selection sort typically 2-5x faster despite same Big O
```

**Practice:**
- Benchmark both on different sizes
- Understand why constants matter in Big O
- Know when to use each (rarely, unless very small arrays)

---

### **Day 13: Insertion Sort — Algorithm and Code**

**Learning Target:** I can implement insertion sort.

**Key Concepts:**
- Insertion sort: Build sorted array one element at a time
- Take next unsorted element, find its place, insert it
- Best case: O(n) on nearly-sorted data
- Similar to sorting playing cards in your hand

**Code Examples:**

```python
def insertion_sort(arr):
    """Insertion sort - insert elements into sorted portion."""
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        # Shift elements larger than key to the right
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

# Example
numbers = [5, 3, 8, 1, 9, 2]
insertion_sort(numbers)
print(numbers)  # Output: [1, 2, 3, 5, 8, 9]

# Trace on [5, 3, 8, 1]
# i=1: key=3, shift 5 right, insert 3: [3, 5, 8, 1]
# i=2: key=8, already > 5, insert: [3, 5, 8, 1]
# i=3: key=1, shift all right, insert: [1, 3, 5, 8]

# Verbose version
def insertion_sort_verbose(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
        print(f"Insert {key}: {arr}")
```

**Practice:**
- Trace insertion sort on small arrays
- Understand best case O(n) on sorted data
- Compare to other simple sorts

---

### **Day 14: Insertion Sort — When It's Efficient**

**Learning Target:** I can explain when insertion sort is faster than other algorithms.

**Key Concepts:**
- Best case: O(n) on nearly-sorted data
- Better cache locality than bubble sort
- Stable sort (preserves order of equal elements)
- Used in Timsort (Python's sort) for small arrays

**Code Examples:**

```python
import time
import random

def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key

def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

# Test on nearly-sorted data
def create_nearly_sorted(size, disorder=0.1):
    """Create mostly sorted array with some disorder."""
    arr = list(range(size))
    num_swaps = int(size * disorder)
    for _ in range(num_swaps):
        i, j = random.sample(range(size), 2)
        arr[i], arr[j] = arr[j], arr[i]
    return arr

# Benchmark on different data types
print(f"{'Data Type':<20} {'Insertion':<15} {'Bubble':<15} {'Ratio':<10}")
size = 1000

# Random data
data = random.sample(range(size * 10), size)
start = time.time()
insertion_sort(data.copy())
ins_time = time.time() - start

start = time.time()
bubble_sort(data.copy())
bubble_time = time.time() - start

print(f"{'Random':<20} {ins_time:<15.6f} {bubble_time:<15.6f} {bubble_time/ins_time:<10.1f}x")

# Nearly sorted data
data = create_nearly_sorted(size, 0.05)
start = time.time()
insertion_sort(data.copy())
ins_time = time.time() - start

start = time.time()
bubble_sort(data.copy())
bubble_time = time.time() - start

print(f"{'Nearly Sorted':<20} {ins_time:<15.6f} {bubble_time:<15.6f} {bubble_time/ins_time:<10.1f}x")
```

**Practice:**
- Create nearly-sorted data and test
- Compare to bubble sort on different inputs
- Understand practical vs theoretical performance

---

### **Day 15: Divide and Conquer — Merge Sort Concept**

**Learning Target:** I can explain divide-and-conquer and its benefits.

**Key Concepts:**
- Divide and conquer: Break problem into subproblems, solve, combine
- Reduces complexity from O(n²) to O(n log n)
- Trade space O(n) for better time complexity
- Foundation for merge sort, quick sort, binary search

**Code Examples:**

```python
# Simple example: Max element using divide and conquer
def find_max_dc(arr, left=0, right=None):
    if right is None:
        right = len(arr) - 1

    # BASE CASE: single element
    if left == right:
        return arr[left]

    # DIVIDE: split into two halves
    mid = (left + right) // 2

    # CONQUER: find max in each half
    max_left = find_max_dc(arr, left, mid)
    max_right = find_max_dc(arr, mid + 1, right)

    # COMBINE: return larger of the two
    return max(max_left, max_right)

# Example
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
result = find_max_dc(numbers)
print(result)  # Output: 9

# Why divide and conquer helps
# Linear approach: compare each element O(n)
# Divide and conquer: still O(n) for max, but framework for faster sorts

# Count inversions example
def count_inversions_dc(arr):
    """Divide and conquer to count inversions."""
    if len(arr) <= 1:
        return arr, 0

    mid = len(arr) // 2
    left, left_inv = count_inversions_dc(arr[:mid])
    right, right_inv = count_inversions_dc(arr[mid:])

    merged = []
    inv_count = left_inv + right_inv
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            merged.append(left[i])
            i += 1
        else:
            merged.append(right[j])
            inv_count += len(left) - i  # All remaining left > right[j]
            j += 1

    merged.extend(left[i:])
    merged.extend(right[j:])
    return merged, inv_count
```

**Practice:**
- Understand divide step (split problem)
- Understand conquer step (solve subproblems)
- Understand combine step (merge results)
- See why this is faster than naive approach

---

### **Day 16: Merge Sort — Recursive Implementation Part 1**

**Learning Target:** I can implement the merge sort divide step.

**Key Concepts:**
- Base case: Single element arrays are sorted
- Divide: Split array into two halves recursively
- Time: O(n log n) because we divide n times, O(n) work per level
- Space: O(n) for temporary arrays

**Code Examples:**

```python
def merge_sort(arr):
    """Merge sort using divide and conquer."""
    # BASE CASE: single element or empty
    if len(arr) <= 1:
        return arr

    # DIVIDE
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    # CONQUER (merge)
    return merge(left, right)

def merge(left, right):
    """Merge two sorted arrays into one."""
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

# Example
numbers = [5, 3, 8, 1, 9, 2]
result = merge_sort(numbers)
print(result)  # Output: [1, 2, 3, 5, 8, 9]

# Trace on [5, 3, 8, 1]
# Split: [5, 3] and [8, 1]
# Split: [5], [3], [8], [1]
# Merge: [3, 5] and [1, 8]
# Merge: [1, 3, 5, 8]
```

**Practice:**
- Trace merge sort on small arrays
- Draw the recursion tree
- Understand the divide phase

---

### **Day 17: Merge Sort — Recursive Implementation Part 2**

**Learning Target:** I can implement the merge step and analyze merge sort.

**Key Concepts:**
- Merge step: Combine two sorted arrays
- Comparison logic: Always pick smaller from left or right
- Handle remaining elements from either side
- Stable sort: Preserves order of equal elements

**Code Examples:**

```python
def merge_sort_with_trace(arr, level=0):
    """Merge sort with detailed trace."""
    indent = "  " * level
    print(f"{indent}merge_sort({arr})")

    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort_with_trace(arr[:mid], level + 1)
    right = merge_sort_with_trace(arr[mid:], level + 1)

    result = merge_with_trace(left, right, level)
    return result

def merge_with_trace(left, right, level=0):
    """Merge with trace showing comparisons."""
    indent = "  " * level
    result = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            print(f"{indent}merge: take {left[i]} from left")
            i += 1
        else:
            result.append(right[j])
            print(f"{indent}merge: take {right[j]} from right")
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    print(f"{indent}merge result: {result}")
    return result

# Run with trace
numbers = [5, 3, 8, 1]
merge_sort_with_trace(numbers)
```

**Practice:**
- Understand merge logic in detail
- Count comparisons in merge (always less than total elements)
- See why merge is O(n) stable

---

### **Day 18: Merge Sort — Analysis and Tracing**

**Learning Target:** I can analyze merge sort's complexity and trace execution.

**Key Concepts:**
- Time: O(n log n) always (best, average, worst)
- Log n levels of recursion
- Each level does O(n) work merging
- Space: O(n) for temporary arrays
- Stable: Preserves order of equal elements

**Code Examples:**

```python
def merge_sort_analysis(arr):
    """Analyze merge sort with comparison counting."""
    def merge_sort_count(arr, level=0):
        comparisons = 0
        if len(arr) <= 1:
            return arr, comparisons

        mid = len(arr) // 2
        left, left_comps = merge_sort_count(arr[:mid], level + 1)
        right, right_comps = merge_sort_count(arr[mid:], level + 1)

        result, merge_comps = merge_count(left, right)
        comparisons = left_comps + right_comps + merge_comps

        return result, comparisons

    def merge_count(left, right):
        result = []
        comparisons = 0
        i = j = 0

        while i < len(left) and j < len(right):
            comparisons += 1
            if left[i] <= right[j]:
                result.append(left[i])
                i += 1
            else:
                result.append(right[j])
                j += 1

        result.extend(left[i:])
        result.extend(right[j:])
        return result, comparisons

    sorted_arr, comps = merge_sort_count(arr)
    return sorted_arr, comps

# Analyze complexity growth
import random
print(f"{'Size':<10} {'Comparisons':<15} {'n log n':<15} {'Ratio':<10}")
for n in [10, 100, 1000]:
    data = random.sample(range(n * 10), n)
    _, comps = merge_sort_analysis(data)
    n_log_n = n * (n.bit_length() - 1)
    ratio = comps / n_log_n if n_log_n > 0 else 0
    print(f"{n:<10} {comps:<15} {n_log_n:<15} {ratio:<10.2f}")

# Verify O(n log n) — ratio should be close to constant
```

**Practice:**
- Count comparisons in merge sort
- Verify O(n log n) relationship
- Compare to O(n²) algorithms
- Understand tradeoff of O(n) extra space

---

### **Day 19: Quick Sort — Pivot Selection Strategies**

**Learning Target:** I can explain pivot selection in quick sort.

**Key Concepts:**
- Pivot: Element chosen to partition array
- Good pivot: Divides array roughly in half
- Bad pivot: Divides into 1 and n-1 (degrades to O(n²))
- Strategies: First, last, middle, random, median-of-three

**Code Examples:**

```python
# Different pivot selection strategies

def partition_first(arr, low, high):
    """Use first element as pivot."""
    pivot = arr[low]
    i = low + 1
    for j in range(low + 1, high + 1):
        if arr[j] < pivot:
            arr[i], arr[j] = arr[j], arr[i]
            i += 1
    arr[low], arr[i - 1] = arr[i - 1], arr[low]
    return i - 1

def partition_last(arr, low, high):
    """Use last element as pivot."""
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

def partition_middle(arr, low, high):
    """Use middle element as pivot."""
    mid = (low + high) // 2
    arr[mid], arr[high] = arr[high], arr[mid]  # Move to end
    return partition_last(arr, low, high)

def partition_median_of_three(arr, low, high):
    """Use median of first, middle, last as pivot."""
    mid = (low + high) // 2
    # Find median of three
    if arr[low] > arr[mid]:
        arr[low], arr[mid] = arr[mid], arr[low]
    if arr[low] > arr[high]:
        arr[low], arr[high] = arr[high], arr[low]
    if arr[mid] > arr[high]:
        arr[mid], arr[high] = arr[high], arr[mid]
    # Middle is now median
    arr[mid], arr[high] = arr[high], arr[mid]
    return partition_last(arr, low, high)

import random

def analyze_pivot_strategies():
    """Compare pivot selection strategies."""
    # Worst case for first: already sorted array
    worst_case = list(range(1000))

    print("Pivot strategy performance on nearly-sorted array:")
    print(f"First pivot partitions at: {partition_first(worst_case.copy(), 0, 999)}")
    print(f"Last pivot partitions at: {partition_last(worst_case.copy(), 0, 999)}")
    print(f"Middle pivot partitions at: {partition_middle(worst_case.copy(), 0, 999)}")
    print(f"Median-of-3 partitions at: {partition_median_of_three(worst_case.copy(), 0, 999)}")
```

**Practice:**
- Understand impact of pivot choice
- See how bad pivot leads to O(n²)
- Understand why random pivot is safe
- Know about median-of-three optimization

---

### **Day 20: Quick Sort — Partition Function**

**Learning Target:** I can implement and understand the partition function.

**Key Concepts:**
- Partition: Arrange elements so pivot is in correct position
- Elements less than pivot on left, greater on right
- Returns partition index
- O(n) partition operation
- Determines quality of the sort

**Code Examples:**

```python
def partition(arr, low, high):
    """
    Partition array around last element as pivot.
    Elements < pivot go left, elements >= go right.
    Returns the partition index.
    """
    pivot = arr[high]
    i = low - 1

    # Scan through array
    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    # Place pivot in correct position
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

# Example
arr = [3, 7, 1, 9, 2]
pivot_idx = partition(arr, 0, 4)
print(f"Partitioned array: {arr}")
print(f"Pivot index: {pivot_idx}")
# Result: [2, 1, 3, 9, 7] with pivot 3 at index 2

# Trace partition on [3, 7, 1, 9, 2]
# pivot = 2, i = -1
# j=0: 3 > 2, don't swap
# j=1: 7 > 2, don't swap
# j=2: 1 < 2, swap arr[0] and arr[2]: [1, 7, 3, 9, 2], i=0
# j=3: 9 > 2, don't swap
# Final: swap pivot arr[1] and arr[4]: [1, 2, 3, 9, 7]

def partition_verbose(arr, low, high):
    """Partition with detailed output."""
    pivot = arr[high]
    print(f"Partitioning {arr[low:high+1]} with pivot {pivot}")
    i = low - 1

    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
            print(f"  Swapped {arr[j]} and {arr[i]}: {arr[low:high+1]}")

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    print(f"  Final pivot position: {i + 1}")
    return i + 1
```

**Practice:**
- Trace partition step by step
- Understand the two-pointer approach
- See how elements are moved
- Verify elements end up on correct sides of pivot

---

### **Day 21: Quick Sort — Full Recursive Implementation**

**Learning Target:** I can implement quick sort completely.

**Key Concepts:**
- Recursive quick sort using partition
- Time: O(n log n) average, O(n²) worst case
- Space: O(log n) for recursion (no extra arrays like merge sort)
- In-place: Sorts within the array
- Not stable: May reorder equal elements

**Code Examples:**

```python
def quick_sort(arr, low=0, high=None):
    """
    In-place quick sort using Lomuto partition.
    """
    if high is None:
        high = len(arr) - 1

    if low < high:
        # Partition and get pivot index
        pivot_idx = partition(arr, low, high)
        # Recursively sort left and right
        quick_sort(arr, low, pivot_idx - 1)
        quick_sort(arr, pivot_idx + 1, high)

    return arr

def partition(arr, low, high):
    """Partition around last element."""
    pivot = arr[high]
    i = low - 1

    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

# Example
numbers = [5, 3, 8, 1, 9, 2]
quick_sort(numbers)
print(numbers)  # Output: [1, 2, 3, 5, 8, 9]

# Trace on [5, 3, 8, 1]
# Partition: [1, 3, 5, 8] pivot=5 at index 2
# Quick sort [1, 3] left of 5
#   Partition: [1, 3] pivot=3 at index 1
#   Quick sort [1] (done)
# Quick sort [8] right of 5 (done)

def quick_sort_random_pivot(arr, low=0, high=None):
    """Quick sort with random pivot selection."""
    import random

    if high is None:
        high = len(arr) - 1

    if low < high:
        # Random pivot selection
        random_idx = random.randint(low, high)
        arr[random_idx], arr[high] = arr[high], arr[random_idx]

        pivot_idx = partition(arr, low, high)
        quick_sort_random_pivot(arr, low, pivot_idx - 1)
        quick_sort_random_pivot(arr, pivot_idx + 1, high)

    return arr

# Better performance on nearly-sorted data
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
quick_sort_random_pivot(numbers)
```

**Practice:**
- Implement and test quick sort
- Trace on different array types
- Understand recursion with partitioning
- Compare random pivot vs fixed pivot

---

### **Day 22: Python's Built-in Sorting — sorted() and Timsort**

**Learning Target:** I can use Python's sorted() function and understand Timsort.

**Key Concepts:**
- Python uses Timsort: hybrid of merge sort and insertion sort
- Time: O(n log n) always
- Space: O(n) for temporary arrays
- Stable: Preserves order of equal elements
- Optimized for real-world data

**Code Examples:**

```python
# Basic sorted() usage
numbers = [5, 3, 8, 1, 9, 2]
result = sorted(numbers)
print(result)  # [1, 2, 3, 5, 8, 9]

# Sorted maintains type
strings = ["banana", "apple", "cherry"]
result = sorted(strings)
print(result)  # ['apple', 'banana', 'cherry']

# Reverse order
result = sorted(numbers, reverse=True)
print(result)  # [9, 8, 5, 3, 2, 1]

# What Timsort does
# 1. Divide into small runs (min_run ≈ 32 elements)
# 2. Sort each run with insertion sort (fast on small arrays)
# 3. Merge sorted runs with merge sort (like merge sort)
# 4. Detect and use natural runs (already-sorted sequences)

# Example: sorted data benefits from Timsort's run detection
almost_sorted = [1, 2, 3, 4, 5, 100, 6, 7, 8, 9]
# Timsort detects [1-5] is sorted, [100], [6-9] is sorted
# Merges these runs efficiently

# In-place sort
numbers = [5, 3, 8, 1, 9, 2]
numbers.sort()  # Modifies numbers in place
print(numbers)  # [1, 2, 3, 5, 8, 9]

# sorted() vs .sort()
# - sorted() returns new list
# - .sort() modifies in place
# - sorted() works on any iterable
# - .sort() only works on lists
```

**Practice:**
- Use sorted() on various data types
- Understand difference between sorted() and .sort()
- Know when Timsort shines (nearly-sorted data)
- Appreciate Timsort's optimizations

---

### **Day 23: Python Sorting — Custom key= and Lambda Keys**

**Learning Target:** I can sort with custom key functions using lambda.

**Key Concepts:**
- key parameter: Function that extracts sort value from each element
- Lambda: Anonymous function for simple transformations
- Multiple keys: Use tuples in key function
- Negation: Reverse numeric sorting without reverse=True

**Code Examples:**

```python
# Sort by length
words = ["apple", "pie", "zoo", "a"]
result = sorted(words, key=len)
print(result)  # ['a', 'pie', 'zoo', 'apple']

# Sort by absolute value
numbers = [-5, 3, -8, 1, -2]
result = sorted(numbers, key=abs)
print(result)  # [1, -2, 3, -5, -8]

# Sort dictionaries
students = [
    {'name': 'Alice', 'grade': 85},
    {'name': 'Bob', 'grade': 92},
    {'name': 'Charlie', 'grade': 88}
]
result = sorted(students, key=lambda s: s['grade'])
# [{'name': 'Alice', 'grade': 85}, {'name': 'Charlie', 'grade': 88}, ...]

# Sort by multiple keys (name ascending, grade descending)
result = sorted(students, key=lambda s: (s['name'], -s['grade']))

# Case-insensitive string sort
words = ["Apple", "banana", "Cherry"]
result = sorted(words, key=str.lower)
print(result)  # ['Apple', 'banana', 'Cherry']

# Custom class sorting
class Student:
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa

    def __repr__(self):
        return f"{self.name}({self.gpa})"

students = [
    Student("Alice", 3.8),
    Student("Bob", 3.5),
    Student("Charlie", 3.9)
]

# Sort by GPA descending
result = sorted(students, key=lambda s: -s.gpa)
print(result)  # [Charlie(3.9), Alice(3.8), Bob(3.5)]

# Sort by GPA descending, then name ascending
result = sorted(students, key=lambda s: (-s.gpa, s.name))

# Sort complex objects
data = [
    {'id': 3, 'value': 10},
    {'id': 1, 'value': 30},
    {'id': 2, 'value': 20}
]
result = sorted(data, key=lambda x: (x['id'], -x['value']))
```

**Practice:**
- Create custom key functions
- Sort by multiple attributes
- Use lambda for complex sorting
- Understand how key parameter works

---

### **Day 24: Algorithm Comparison and Selection Guide**

**Learning Target:** I can choose the right algorithm for different situations.

**Key Concepts:**
- Each algorithm has tradeoffs in time, space, stability
- Context matters: small arrays, nearly-sorted, memory constraints
- Big O alone doesn't determine best choice
- Real-world factors: cache, constants, data patterns

**Code Examples:**

```python
# Algorithm comparison table
algorithms = {
    'Linear Search': {'time': 'O(n)', 'space': 'O(1)', 'sorted': False},
    'Binary Search': {'time': 'O(log n)', 'space': 'O(1)', 'sorted': True},
    'Bubble Sort': {'time': 'O(n²)', 'space': 'O(1)', 'stable': True},
    'Selection Sort': {'time': 'O(n²)', 'space': 'O(1)', 'stable': False},
    'Insertion Sort': {'time': 'O(n²)', 'space': 'O(1)', 'stable': True},
    'Merge Sort': {'time': 'O(n log n)', 'space': 'O(n)', 'stable': True},
    'Quick Sort': {'time': 'O(n²)', 'space': 'O(log n)', 'stable': False},
    'Python sorted()': {'time': 'O(n log n)', 'space': 'O(n)', 'stable': True},
}

# Decision tree examples
def choose_sort(size, constraints=None):
    """Choose sort based on problem constraints."""
    if size < 100:
        return "Bubble, Selection, or Insertion"
    elif 100 <= size < 10000:
        if constraints and 'stable' in constraints:
            return "Merge Sort"
        else:
            return "Quick Sort"
    else:  # Large datasets
        return "Python sorted() (Timsort)"

def choose_search(data, sorted_status=None):
    """Choose search based on data status."""
    if sorted_status:
        return "Binary Search O(log n)"
    else:
        return "Linear Search O(n)"

# Benchmark comparison
import time
import random

def benchmark_sorts(size=1000):
    """Benchmark all sorts on same data."""
    data = random.sample(range(size * 10), size)

    sorts = {
        'Bubble': bubble_sort,
        'Selection': selection_sort,
        'Insertion': insertion_sort,
        'Merge': merge_sort,
        'Built-in': sorted,
    }

    print(f"{'Algorithm':<15} {'Time (ms)':<15} {'Relative':<15}")
    print("-" * 45)

    times = {}
    for name, func in sorts.items():
        start = time.time()
        func(data.copy())
        elapsed = (time.time() - start) * 1000
        times[name] = elapsed
        print(f"{name:<15} {elapsed:<15.2f} {'...':<15}")

    # Calculate relative speeds
    fastest = min(times.values())
    print("\nRelative to fastest:")
    for name, t in times.items():
        ratio = t / fastest
        print(f"{name:<15} {ratio:<15.1f}x")

# Which algorithm to use when
print("""
USE LINEAR SEARCH WHEN:
- Data is unsorted
- Dataset is small (< 1000 elements)
- Need simplicity over speed

USE BINARY SEARCH WHEN:
- Data is sorted
- Large dataset (> 1000 elements)
- Need speed (O(log n) vs O(n))

USE BUBBLE SORT WHEN:
- Learning/teaching algorithms
- Data is nearly sorted (with optimization)
- Very small arrays (< 50 elements)

USE SELECTION SORT WHEN:
- Memory is critical (O(1) space)
- Simplicity is important
- Never on large datasets

USE INSERTION SORT WHEN:
- Data is small (< 100 elements)
- Data is nearly sorted (best case O(n))
- Stability is required
- Online algorithm needed

USE MERGE SORT WHEN:
- Stability is required
- Consistent O(n log n) needed
- Extra space is available
- Parallel processing desired

USE QUICK SORT WHEN:
- Average-case speed matters
- Space is limited (no extra arrays)
- Data doesn't have patterns quick sort struggles with

USE PYTHON'S sorted() WHEN:
- In production code
- Writing real applications
- Performance matters
- You want the best algorithm for the job
""")
```

**Practice:**
- Compare algorithms on different data sizes
- Understand tradeoffs beyond Big O
- Make informed algorithm choices
- Know when to use built-in functions

---

### **Day 25: Algorithm Complexity — Comparing Performance**

**Learning Target:** I can measure and analyze real algorithm performance.

**Key Concepts:**
- Big O is theoretical; benchmarking shows practice
- Constants matter: O(n²) can be faster than O(n log n) for small n
- Data patterns affect performance
- Cache effects, system load, implementation details matter

**Code Examples:**

```python
import time
import random

def measure_algorithm_growth():
    """Measure how algorithms scale with size."""
    sizes = [100, 500, 1000, 5000, 10000]

    print(f"{'Size':<10} {'Bubble':<15} {'Insertion':<15} {'Merge':<15} {'sorted()':<15}")
    print("-" * 60)

    for size in sizes:
        data = random.sample(range(size * 10), size)

        # Bubble sort
        start = time.time()
        bubble_sort(data.copy())
        bubble_time = (time.time() - start) * 1000

        # Insertion sort
        start = time.time()
        insertion_sort(data.copy())
        insert_time = (time.time() - start) * 1000

        # Merge sort
        start = time.time()
        merge_sort(data.copy())
        merge_time = (time.time() - start) * 1000

        # Python's sorted
        start = time.time()
        sorted(data)
        sorted_time = (time.time() - start) * 1000

        print(f"{size:<10} {bubble_time:<15.2f} {insert_time:<15.2f} {merge_time:<15.2f} {sorted_time:<15.2f}")

def verify_big_o():
    """Verify Big O relationships empirically."""
    print("\nVerifying O(n²) algorithms scale with 4x when size doubles:")

    sizes = [100, 200]
    bubble_times = []

    for size in sizes:
        data = random.sample(range(size * 10), size)
        start = time.time()
        bubble_sort(data)
        bubble_times.append(time.time() - start)

    ratio = bubble_times[1] / bubble_times[0]
    print(f"Time ratio when size doubled: {ratio:.1f}x (expect ~4x for O(n²))")

def compare_search_algorithms():
    """Compare linear vs binary search."""
    print("\nSearching in sorted array of 1 million elements:")

    data = list(range(1000000))

    # Linear search (slow!)
    start = time.time()
    for _ in range(100):
        linear_search(data, -1)  # Worst case: not found
    linear_time = time.time() - start

    # Binary search (fast!)
    start = time.time()
    for _ in range(100):
        binary_search(data, -1)
    binary_time = time.time() - start

    print(f"Linear search (100 iterations): {linear_time:.2f}s")
    print(f"Binary search (100 iterations): {binary_time:.4f}s")
    print(f"Binary search is {linear_time/binary_time:.0f}x faster!")

# Helper functions needed for examples
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

def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

**Practice:**
- Run benchmark comparisons
- Measure scaling relationships
- Verify Big O empirically
- Understand performance reality vs theory

---

### **Day 26: Sorting/Searching Project — Day 1 Setup**

**Learning Target:** I can set up and plan a sorting/searching algorithm comparison project.

**Project Overview:**
- Write implementations of multiple algorithms
- Create test data sets
- Set up benchmarking framework
- Plan Day 2 testing and analysis

**Setup Code:**

```python
"""
Sorting & Searching Algorithm Benchmarking Project
Day 1: Setup and Implementation
"""

import time
import random
from typing import Callable, List

class AlgorithmBenchmark:
    """Framework for benchmarking sorting and searching algorithms."""

    def __init__(self, data_size: int = 1000):
        self.data_size = data_size
        self.data = None
        self.generate_data()

    def generate_data(self):
        """Generate random test data."""
        self.data = random.sample(range(self.data_size * 10), self.data_size)

    def benchmark(self, func: Callable, runs: int = 3) -> float:
        """Run function multiple times and return average time."""
        times = []
        for _ in range(runs):
            test_data = self.data.copy()
            start = time.time()
            func(test_data)
            times.append(time.time() - start)
        return sum(times) / len(times)

# Sorting algorithms
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]

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

# Project planning
print("""
PROJECT PLAN:
=============

Day 1 (Today): Setup
- Implement all algorithms ✓
- Create benchmarking framework ✓
- Generate test data ✓
- Plan data collection

Day 2: Benchmarking
- Run comprehensive tests on different data sizes
- Create performance comparison tables
- Analyze results and draw conclusions
- Create visualizations
""")
```

**Practice:**
- Set up algorithm implementations
- Create benchmarking framework
- Plan test strategy
- Prepare for Day 2 testing

---

### **Day 27: Sorting/Searching Project — Day 2 Benchmarking**

[See Day27.md for complete detailed content]

---

### **Day 28: Unit Assessment — Sorting, Searching & Recursion**

[See Day28.md for complete assessment]

---

## Practice Bank

See `UnitPractice.md` for 20 comprehensive practice problems with solutions.

---

## Common Mistakes

**Recursion:**
- Forgetting the base case — causes infinite recursion
- Base case too general — stops too early
- Not making progress toward base case — infinite recursion

**Binary Search:**
- Using on unsorted data — gives wrong results
- Off-by-one errors in mid calculation
- Forgetting to check if left > right

**Sorting:**
- Using O(n²) sort on large dataset — wait hours for results
- Forgetting to handle edge cases (empty arrays, single elements)
- Modifying array incorrectly during in-place sorts

**Big O Analysis:**
- Thinking best case is irrelevant
- Not accounting for hidden constants
- Forgetting space complexity
- Missing that O(n) and O(n log n) look similar at small n

**Benchmarking:**
- Only running once — system load varies
- Not using same data for all algorithms
- Using too-small datasets — times too fast to measure
- Forgetting to copy data — modifications affect timing

---

## Assessment Prep

**Before the assessment:**
1. Complete UnitPractice.md (20 problems)
2. Review ReferenceGuide.md (all algorithms and templates)
3. Practice algorithm traces by hand
4. Run benchmark code to understand relative performance
5. Be able to explain Big O for each algorithm

**During the assessment:**
1. Read questions carefully
2. Show all work in traces
3. Test code before submitting
4. Manage your time: traces first, then multiple choice, short answers, coding

**Key things to know:**
- Every algorithm's Big O (best, average, worst)
- How to trace each algorithm step-by-step
- When to use each algorithm
- How to write efficient code
- How to analyze code complexity

---

## Vocabulary

- **Algorithm:** Step-by-step procedure to solve a problem
- **Benchmark:** Measure actual execution time of code
- **Big O Notation:** Describes how algorithm performance scales with input size
- **Binary Search:** Divide search space in half each iteration O(log n)
- **Bubble Sort:** Swap adjacent elements repeatedly O(n²)
- **Call Stack:** Memory structure tracking function calls
- **Base Case:** Stopping condition in recursion
- **Divide and Conquer:** Break problem into subproblems, solve, combine
- **In-place Sort:** Sort without needing extra space
- **Insertion Sort:** Build sorted array one element at a time
- **Linear Search:** Check each element one by one O(n)
- **Merge Sort:** Divide and conquer sort O(n log n) always
- **Partition:** Divide array around pivot element (quick sort)
- **Pivot:** Element chosen to partition array (quick sort)
- **Quick Sort:** Partition and recursively sort O(n log n) average
- **Recursion:** Function calling itself with simpler problem
- **Selection Sort:** Find minimum and place at front O(n²)
- **Stable Sort:** Preserves relative order of equal elements
- **Timsort:** Python's sorting algorithm (hybrid merge + insertion)

---

## Resources

- **ReferenceGuide.md:** Code templates for all algorithms
- **UnitPractice.md:** 20 practice problems with complete solutions
- **UnitAssessment.md:** Full formal assessment with answer key
- **Daily Notes (Days 1-28):** Detailed lesson content with examples

---

## Standards Alignment

**TN Standard 9-12.CCI.3:** Design and implement algorithms
- Students can implement searching algorithms (linear, binary)
- Students can implement sorting algorithms (multiple varieties)
- Students can analyze algorithm efficiency (Big O notation)
- Students can choose appropriate algorithms for situations

**Computing Practices:**
- Algorithm design and analysis
- Implementation of computational solutions
- Testing and verification
- Performance optimization

