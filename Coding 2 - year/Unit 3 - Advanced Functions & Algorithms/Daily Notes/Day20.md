# Day 20: Big O Notation and Time Complexity

**Learning Target:** I can analyze algorithms using Big O notation and understand how to classify time complexity.

---

## Key Concepts

**Big O Notation** — Describes how an algorithm's running time grows as input size increases. Focuses on worst-case scenario.

**Common Big O Classes (best to worst):**
- **O(1)** — Constant time (lookup in hash table)
- **O(log n)** — Logarithmic (binary search)
- **O(n)** — Linear (simple loop)
- **O(n log n)** — Linearithmic (efficient sorts like merge sort)
- **O(n²)** — Quadratic (nested loops, bubble sort)
- **O(n³)** — Cubic (triple nested loops)
- **O(2ⁿ)** — Exponential (recursive Fibonacci)
- **O(n!)** — Factorial (generating permutations)

**Rules for calculating Big O:**
1. Drop constant factors: O(2n) → O(n)
2. Drop lower-order terms: O(n² + n) → O(n²)
3. Focus on dominant term: what happens as n gets very large?

**Space Complexity** — How much memory an algorithm uses (follows same Big O notation).

---

## Code Examples

```python
# Example 1: O(1) - Constant time
def get_first_element(lst):
    return lst[0]  # Always takes same time, regardless of list size

# Example 2: O(log n) - Binary search
def binary_search(lst, target):
    left, right = 0, len(lst) - 1
    while left <= right:
        mid = (left + right) // 2
        if lst[mid] == target:
            return mid
        elif lst[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
# Roughly log₂(n) comparisons needed

# Example 3: O(n) - Linear search
def linear_search(lst, target):
    for i in range(len(lst)):  # Loop runs n times
        if lst[i] == target:
            return i
    return -1

# Example 4: O(n log n) - Merge sort
def merge_sort(lst):
    if len(lst) <= 1:
        return lst
    mid = len(lst) // 2
    # Split: O(log n) levels
    # Merge: O(n) work at each level
    # Total: O(n log n)
    left = merge_sort(lst[:mid])
    right = merge_sort(lst[mid:])
    return merge(left, right)

# Example 5: O(n²) - Bubble sort
def bubble_sort(lst):
    n = len(lst)
    for i in range(n):           # Outer loop: n times
        for j in range(n - 1):   # Inner loop: n times
            if lst[j] > lst[j + 1]:
                lst[j], lst[j + 1] = lst[j + 1], lst[j]
    return lst

# Example 6: O(n²) - Nested loops
def print_pairs(n):
    for i in range(n):           # n times
        for j in range(n):       # n times
            print(i, j)          # O(n²) prints

# Example 7: O(n³) - Triple nested loops
def print_triplets(n):
    for i in range(n):
        for j in range(n):
            for k in range(n):
                print(i, j, k)

# Example 8: O(2ⁿ) - Exponential (inefficient!)
def fibonacci_simple(n):
    if n <= 1:
        return n
    return fibonacci_simple(n - 1) + fibonacci_simple(n - 2)
# Each call makes 2 more calls, leading to exponential growth

# Example 9: Analyzing combined operations
def mixed_operations(lst):
    print(lst[0])              # O(1)
    for x in lst:              # O(n)
        print(x)
    for i in range(len(lst)):  # O(n²)
        for j in range(len(lst)):
            print(lst[i], lst[j])
    # Total: O(1) + O(n) + O(n²) = O(n²) (drop lower terms)

# Example 10: Comparing actual runtimes
import time

def compare_algorithms(n):
    # Linear: O(n)
    start = time.time()
    for i in range(n):
        x = i
    linear_time = time.time() - start
    
    # Quadratic: O(n²)
    start = time.time()
    for i in range(n):
        for j in range(n):
            x = i + j
    quadratic_time = time.time() - start
    
    print(f"n={n}: Linear={linear_time:.6f}s, Quadratic={quadratic_time:.6f}s")

# For n=1000, quadratic is roughly 1000x slower!
# For n=10000, quadratic is roughly 10000x slower!

# Example 11: Space complexity
def create_list_O_1(n):
    """O(1) space - doesn't depend on input"""
    total = 0
    for i in range(n):
        total += i
    return total

def create_list_O_n(n):
    """O(n) space - creates list of size n"""
    return list(range(n))

def create_list_O_n2(n):
    """O(n²) space - creates 2D list"""
    return [[i + j for j in range(n)] for i in range(n)]

# Example 12: Practical implications
# When n=1000:
# O(log n): ~10 operations
# O(n): ~1000 operations
# O(n log n): ~10,000 operations
# O(n²): ~1,000,000 operations
# O(2ⁿ): ~10³⁰ operations (impossible!)
```

---

## Guided Practice

**Step 1:** Classify these functions by Big O:
```python
# Function 1: O(1)
def first(lst):
    return lst[0]

# Function 2: O(n)
def count_elements(lst):
    count = 0
    for x in lst:
        count += 1
    return count

# Function 3: O(n²)
def check_duplicates(lst):
    for i in range(len(lst)):
        for j in range(i + 1, len(lst)):
            if lst[i] == lst[j]:
                return True
    return False
```

**Step 2:** Analyze the time complexity of a function.
```python
def sum_matrix(matrix):
    total = 0
    for row in matrix:        # Outer loop: n times
        for value in row:     # Inner loop: m times
            total += value
    return total
# Time complexity: O(n * m) or O(n²) if square
```

**Step 3:** Compare performance of O(n) vs O(n²) algorithms.
```python
# See compare_algorithms() above
```

---

## Practice Problems

**Beginner:** Classify the following by Big O: summing an array, printing all pairs, binary search.

**Intermediate:** Write a function and determine its time and space complexity.

**Challenge:** Optimize an O(n²) algorithm to O(n log n) or better if possible.

<details>
<summary>💡 Hints</summary>
- For Beginner: O(n), O(n²), O(log n)
- For Intermediate: Count loops and nested operations
- For Challenge: Consider sorting, hashing, or divide-and-conquer
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
# Sum array: O(n)
# Print pairs: O(n²)
# Binary search: O(log n)

# Intermediate: Your function depends on your choice

# Challenge example: Finding duplicates
# Bad: O(n²)
def has_duplicates_slow(lst):
    for i in range(len(lst)):
        for j in range(i + 1, len(lst)):
            if lst[i] == lst[j]:
                return True
    return False

# Better: O(n)
def has_duplicates_fast(lst):
    seen = set()
    for x in lst:
        if x in seen:
            return True
        seen.add(x)
    return False
```
</details>
