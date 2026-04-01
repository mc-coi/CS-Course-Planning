# Unit 5: Practice Problems — 20 Problems with Solutions

---

## Beginner Problems (5 problems)

### Problem 1: Linear Search

Implement linear search to find a value in a list.

```python
def linear_search(arr, target):
    """
    Find target in array by checking each element.
    Return index if found, -1 if not found.
    """
    pass

# Test cases
assert linear_search([1, 3, 5, 7, 9], 5) == 2
assert linear_search([1, 3, 5, 7, 9], 1) == 0
assert linear_search([1, 3, 5, 7, 9], 9) == 4
assert linear_search([1, 3, 5, 7, 9], 4) == -1
assert linear_search([], 5) == -1
```

<details>
<summary>✅ Solution</summary>

```python
def linear_search(arr, target):
    """Linear search - check each element."""
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1
```

**Explanation:** Start at index 0 and check each element. If we find the target, return its index. If we reach the end without finding it, return -1. Time: O(n), Space: O(1).

</details>

---

### Problem 2: Trace Bubble Sort

Trace bubble sort on the array `[3, 1, 4, 1, 5]` and show the array **after each pass**.

```
Initial: [3, 1, 4, 1, 5]
Pass 1: ___________
Pass 2: ___________
Pass 3: ___________
Pass 4: ___________
Final: [1, 1, 3, 4, 5]
```

<details>
<summary>✅ Solution</summary>

```
Initial: [3, 1, 4, 1, 5]
Pass 1: [1, 3, 1, 4, 5]  (5 bubbles to end)
Pass 2: [1, 1, 3, 4, 5]  (4 bubbles to position)
Pass 3: [1, 1, 3, 4, 5]  (no swaps needed)
Pass 4: [1, 1, 3, 4, 5]  (no swaps needed)
Final: [1, 1, 3, 4, 5]
```

**Explanation:** Bubble sort compares adjacent elements and swaps them if they're in the wrong order. Each pass bubbles the largest unsorted element to its correct position at the end.

</details>

---

### Problem 3: Binary Search vs Linear Search

For an array of 1 million sorted numbers, which is faster: binary search or linear search?

How many comparisons does each do in the **worst case** (element not found)?

<details>
<summary>✅ Solution</summary>

**Binary search is much faster.**

- **Linear search:** 1 million comparisons in worst case
- **Binary search:** log₂(1,000,000) ≈ 20 comparisons in worst case

Binary search eliminates half the search space each iteration, while linear search must check every element.

**Time Complexity:**
- Linear search: O(n) = 1,000,000
- Binary search: O(log n) = 20

This is why binary search is preferred for large sorted datasets.

</details>

---

### Problem 4: Recursion Base Case

What is wrong with this recursive function? Fix it.

```python
def countdown(n):
    print(n)
    return countdown(n - 1)
```

<details>
<summary>✅ Solution</summary>

**Problem:** No base case — the function will call itself infinitely!

**Fixed version:**
```python
def countdown(n):
    if n < 0:  # BASE CASE: stop when n is negative
        return
    print(n)
    countdown(n - 1)  # RECURSIVE CASE: call with smaller value
```

**Key principle:** Every recursive function MUST have:
1. **Base case:** Condition to stop recursion
2. **Recursive case:** Call itself with a smaller/simpler problem

</details>

---

### Problem 5: Selection Sort Algorithm

Describe selection sort in one sentence, then implement it.

<details>
<summary>✅ Solution</summary>

**Description:** "Find the minimum element and place it at the beginning, then repeat for the remaining array."

**Implementation:**
```python
def selection_sort(arr):
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

**Key traits:**
- Time: O(n²) always (no best case)
- Space: O(1) (in-place)
- Good when memory is limited
- Not stable (may reorder equal elements)

</details>

---

## Intermediate Problems (8 problems)

### Problem 6: Implement Binary Search (Recursive)

Write a recursive binary search function.

```python
def binary_search_recursive(arr, target, left=0, right=None):
    """
    Recursive binary search.
    Return index if found, -1 if not found.
    """
    pass

# Test cases
assert binary_search_recursive([1, 3, 5, 7, 9, 11], 7) == 3
assert binary_search_recursive([1, 3, 5, 7, 9, 11], 1) == 0
assert binary_search_recursive([1, 3, 5, 7, 9, 11], 11) == 5
assert binary_search_recursive([1, 3, 5, 7, 9, 11], 4) == -1
```

<details>
<summary>✅ Solution</summary>

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
        return binary_search_recursive(arr, target, mid + 1, right)  # Recursive case: right half
    else:
        return binary_search_recursive(arr, target, left, mid - 1)  # Recursive case: left half
```

**Key points:**
- Base cases: not found (left > right), or found (arr[mid] == target)
- Recursive cases: search right half or left half
- Time: O(log n)
- Space: O(log n) due to call stack depth

</details>

---

### Problem 7: Insertion Sort Tracing

Trace insertion sort on `[5, 2, 4, 6, 1, 3]` showing the array **after each insertion**.

```
Initial: [5, 2, 4, 6, 1, 3]
Insert 2: ___________
Insert 4: ___________
Insert 6: ___________
Insert 1: ___________
Insert 3: ___________
Final: [1, 2, 3, 4, 5, 6]
```

<details>
<summary>✅ Solution</summary>

```
Initial: [5, 2, 4, 6, 1, 3]
Insert 2: [2, 5, 4, 6, 1, 3]  (2 moves left of 5)
Insert 4: [2, 4, 5, 6, 1, 3]  (4 moves left of 5)
Insert 6: [2, 4, 5, 6, 1, 3]  (6 already in place)
Insert 1: [1, 2, 4, 5, 6, 3]  (1 moves to front)
Insert 3: [1, 2, 3, 4, 5, 6]  (3 moves to correct position)
Final: [1, 2, 3, 4, 5, 6]
```

**How insertion sort works:**
- Consider first element as sorted
- For each remaining element, find its correct position in the sorted part
- Shift larger elements right
- Insert the element

**Best case:** O(n) when array is already sorted
**Worst case:** O(n²) when array is reverse-sorted

</details>

---

### Problem 8: Merge Sort Implementation

Implement merge sort.

```python
def merge_sort(arr):
    """
    Recursive merge sort.
    Return sorted array.
    """
    pass

def merge(left, right):
    """Merge two sorted arrays."""
    pass

# Test cases
assert merge_sort([5, 3, 8, 1, 9, 2]) == [1, 2, 3, 5, 8, 9]
assert merge_sort([1]) == [1]
assert merge_sort([]) == []
assert merge_sort([5, 4, 3, 2, 1]) == [1, 2, 3, 4, 5]
```

<details>
<summary>✅ Solution</summary>

```python
def merge_sort(arr):
    """Divide and conquer sorting."""
    if len(arr) <= 1:
        return arr  # BASE CASE: single element or empty

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
```

**Key points:**
- Time: O(n log n) always
- Space: O(n) for temporary arrays
- Stable sort (preserves order of equal elements)
- Uses divide-and-conquer strategy

</details>

---

### Problem 9: Analyze Algorithm Complexity

Given this code, what is the Big O time complexity?

```python
def find_pairs(arr):
    """Find all pairs of numbers that sum to 10."""
    result = []
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if arr[i] + arr[j] == 10:
                result.append((arr[i], arr[j]))
    return result
```

<details>
<summary>✅ Solution</summary>

**Time complexity: O(n²)**

**Explanation:**
- Outer loop: n iterations
- Inner loop: up to n-1 iterations for each outer iteration
- Total: n × n = n²

Even though inner loop starts at i+1, in Big O analysis we ignore constant factors and coefficients. It's still quadratic.

**Space complexity: O(k)** where k is the number of pairs found (excluding the output, O(1))

**Could this be optimized?**
Yes! Use a set to track which numbers we've seen:

```python
def find_pairs_optimized(arr):
    seen = set()
    result = []
    target = 10

    for num in arr:
        complement = target - num
        if complement in seen:
            result.append((min(num, complement), max(num, complement)))
        seen.add(num)

    return list(set(result))  # Remove duplicates
```

**Optimized time complexity: O(n)**

</details>

---

### Problem 10: Sorting Custom Objects

Sort a list of dictionaries by age using Python's `sorted()` with a key function.

```python
students = [
    {'name': 'Alice', 'age': 20},
    {'name': 'Bob', 'age': 18},
    {'name': 'Charlie', 'age': 19},
]

# Your code here
result = sorted(...)

# Result should be sorted by age (18, 19, 20)
assert result[0]['age'] == 18
assert result[1]['age'] == 19
assert result[2]['age'] == 20
```

<details>
<summary>✅ Solution</summary>

```python
result = sorted(students, key=lambda s: s['age'])
```

**Explanation:**
- `sorted(students, ...)` takes the list of dictionaries
- `key=lambda s: s['age']` extracts the 'age' value from each dictionary
- Lambda function receives each dictionary and returns the age
- `sorted()` uses these ages to determine order

**Alternative with lambda and reverse:**
```python
# Sort by age descending
result = sorted(students, key=lambda s: s['age'], reverse=True)
```

**Or with multiple keys:**
```python
# Sort by name, then by age if names are equal
result = sorted(students, key=lambda s: (s['name'], s['age']))
```

**Key points:**
- The `key` function is applied to each element
- The function receives one element at a time
- It should return a value used for comparison
- Common: `lambda x: x[key]` for dictionaries, `lambda x: x.attribute` for objects

</details>

---

### Problem 11: Quick Sort Partition

Implement the partition function for quick sort.

```python
def partition(arr, low, high):
    """
    Partition array around a pivot.
    Return the partition index.
    """
    pass

# Test
arr = [3, 7, 1, 9, 2]
pivot_idx = partition(arr, 0, 4)
# After partition, elements < pivot are left, elements > pivot are right
```

<details>
<summary>✅ Solution</summary>

```python
def partition(arr, low, high):
    """
    Partition array using last element as pivot.
    Returns the partition index.
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

**How it works:**
1. Choose the last element as pivot
2. Use two pointers: i and j
3. j scans through elements
4. If element < pivot, swap with position i
5. Finally, swap pivot to its correct position

**Example trace on [3, 7, 1, 9, 2]:**
```
pivot = 2, i = -1
j=0: arr[0]=3 > 2, don't swap
j=1: arr[1]=7 > 2, don't swap
j=2: arr[2]=1 < 2, swap: [1, 7, 3, 9, 2], i=0
j=3: arr[3]=9 > 2, don't swap
Final swap pivot to position i+1: [1, 2, 3, 9, 7]
Return i+1 = 1
```

</details>

---

### Problem 12: Compare Two Algorithms

Which is faster for 10,000 elements: bubble sort or insertion sort? Explain why.

<details>
<summary>✅ Solution</summary>

**Insertion sort is faster** (usually 2-5x faster).

**Reason:**
Both are O(n²) in the worst case, but insertion sort has better:

1. **Cache locality:** Insertion sort accesses memory sequentially (better CPU cache usage)
2. **Fewer swaps:** Bubble sort always swaps adjacent elements, insertion sort shifts
3. **Early termination:** If data is partially sorted, insertion sort can be much faster

**Real benchmark (approximate):**
- Bubble sort on 10,000 random elements: ~1-2 seconds
- Insertion sort on 10,000 random elements: ~0.2-0.5 seconds
- Merge sort on 10,000 random elements: ~0.001-0.01 seconds

**Lesson:** Even with the same Big O complexity, actual performance varies based on:
- Constant factors
- Memory access patterns
- CPU cache behavior
- Specific data patterns

For large datasets, choose O(n log n) algorithms (merge sort, quick sort, Python's sorted()) instead.

</details>

---

## Challenge Problems (7 problems)

### Problem 13: Recursive Fibonacci with Memoization

Implement Fibonacci recursively, but with memoization to avoid recalculating values.

```python
def fibonacci(n, memo=None):
    """
    Calculate the nth Fibonacci number.
    Use memoization to cache results.
    """
    pass

# Test cases
assert fibonacci(0) == 0
assert fibonacci(1) == 1
assert fibonacci(5) == 5
assert fibonacci(10) == 55
assert fibonacci(20) == 6765
```

<details>
<summary>✅ Solution</summary>

```python
def fibonacci(n, memo=None):
    """Fibonacci with memoization."""
    if memo is None:
        memo = {}

    if n in memo:
        return memo[n]  # Return cached result

    if n <= 1:
        return n  # BASE CASE

    # RECURSIVE CASE: calculate and cache
    result = fibonacci(n - 1, memo) + fibonacci(n - 2, memo)
    memo[n] = result
    return result
```

**Why memoization helps:**
- Without it: fibonacci(5) recalculates fibonacci(3) many times
- With it: Each value calculated only once

**Time complexity:**
- Without memoization: O(2ⁿ) — exponential!
- With memoization: O(n) — linear!

**Alternative: Bottom-up approach**
```python
def fibonacci_iterative(n):
    if n <= 1:
        return n

    prev, curr = 0, 1
    for _ in range(2, n + 1):
        prev, curr = curr, prev + curr

    return curr
```

This is even more efficient: O(n) time, O(1) space.

</details>

---

### Problem 14: Three-Way Partition

Given an array with only 0s, 1s, and 2s, partition it so all 0s come first, then 1s, then 2s. Do it in one pass (O(n) time) without extra space.

```python
def partition_colors(arr):
    """
    Partition array of 0s, 1s, and 2s in one pass.
    Modify array in-place.
    """
    pass

# Test
arr = [2, 0, 1, 2, 1, 0]
partition_colors(arr)
assert arr == [0, 0, 1, 1, 2, 2]
```

<details>
<summary>✅ Solution</summary>

```python
def partition_colors(arr):
    """Three-way partition in one pass."""
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
```

**How it works:**
- Use three pointers: low, mid, high
- low: boundary between 0s and others
- high: boundary between 2s and others
- mid: current element being examined

**Trace on [2, 0, 1, 2, 1, 0]:**
```
Initial: [2, 0, 1, 2, 1, 0], low=0, mid=0, high=5
arr[0]=2: swap with high=5 → [0, 0, 1, 2, 1, 2], high=4
arr[0]=0: swap with low=0 → [0, 0, 1, 2, 1, 2], low=1, mid=1
arr[1]=0: swap with low=1 → [0, 0, 1, 2, 1, 2], low=2, mid=2
arr[2]=1: mid++ → mid=3
arr[3]=2: swap with high=4 → [0, 0, 1, 1, 2, 2], high=3
arr[3]=1: mid++ → mid=4
mid > high: done
```

**Time: O(n), Space: O(1)**

</details>

---

### Problem 15: Find Kth Smallest Element

Find the kth smallest element in an unsorted array without fully sorting it.

```python
def find_kth_smallest(arr, k):
    """
    Find the kth smallest element.
    For k=1, return the smallest.
    For k=len(arr), return the largest.
    """
    pass

# Test
arr = [3, 1, 4, 1, 5, 9, 2, 6]
assert find_kth_smallest(arr, 1) == 1
assert find_kth_smallest(arr, 2) == 1
assert find_kth_smallest(arr, 3) == 2
assert find_kth_smallest(arr, 8) == 9
```

<details>
<summary>✅ Solution</summary>

**Solution 1: Using sorted() (simple)**
```python
def find_kth_smallest(arr, k):
    sorted_arr = sorted(arr)
    return sorted_arr[k - 1]
```

**Time: O(n log n), Space: O(n)**

**Solution 2: Using quick select (efficient)**
```python
def find_kth_smallest(arr, k):
    """Quick select algorithm - average O(n)."""
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
```

**Time: O(n) average, O(n²) worst case, Space: O(log n)**

**Why quick select is better:**
- Sorting takes O(n log n) but we only need kth element
- Quick select eliminates half the search space, like binary search
- Average case is linear: O(n)

</details>

---

### Problem 16: Compare Two Sorted Arrays

Given two sorted arrays, find the median of the combined sorted array without actually merging them.

```python
def find_median(arr1, arr2):
    """
    Find median of two sorted arrays.
    arr1 and arr2 are sorted.
    Don't merge them into a new array.
    """
    pass

# Test
assert find_median([1, 3], [2]) == 2.0
assert find_median([1, 2], [3, 4]) == 2.5
assert find_median([1, 3, 5], [2, 4, 6]) == 3.5
```

<details>
<summary>✅ Solution</summary>

```python
def find_median(arr1, arr2):
    """Find median using two pointers (merge without extra space)."""
    # Ensure arr1 is the smaller array
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
```

**How it works:**
- Use two pointers to traverse both arrays
- Count elements until we reach the middle
- For odd length: median is the middle element
- For even length: median is average of two middle elements

**Time: O(m + n), Space: O(1)**

**More efficient solution (binary search approach):**
```python
def find_median_binary(arr1, arr2):
    """O(log(min(m, n))) solution using binary search."""
    if len(arr1) > len(arr2):
        arr1, arr2 = arr2, arr1

    total_length = len(arr1) + len(arr2)
    is_even = total_length % 2 == 0
    half_len = (total_length + 1) // 2

    left, right = 0, len(arr1)

    while left <= right:
        partition1 = (left + right) // 2
        partition2 = half_len - partition1

        left_val1 = float('-inf') if partition1 == 0 else arr1[partition1 - 1]
        right_val1 = float('inf') if partition1 == len(arr1) else arr1[partition1]

        left_val2 = float('-inf') if partition2 == 0 else arr2[partition2 - 1]
        right_val2 = float('inf') if partition2 == len(arr2) else arr2[partition2]

        if left_val1 <= right_val2 and left_val2 <= right_val1:
            if is_even:
                return (max(left_val1, left_val2) + min(right_val1, right_val2)) / 2.0
            else:
                return float(max(left_val1, left_val2))

        elif left_val1 > right_val2:
            right = partition1 - 1
        else:
            left = partition1 + 1

    return -1
```

**Time: O(log(min(m, n))), Space: O(1)**

This is the most optimal but also most complex.

</details>

---

### Problem 17: Inversion Count

Count the number of inversions in an array (pairs where i < j but arr[i] > arr[j]).

```python
def count_inversions(arr):
    """
    Count pairs (i, j) where i < j but arr[i] > arr[j].
    Example: [3, 1, 2] has 2 inversions: (3,1) and (3,2)
    """
    pass

# Test
assert count_inversions([3, 1, 2]) == 2
assert count_inversions([1, 2, 3]) == 0
assert count_inversions([3, 2, 1]) == 3
assert count_inversions([2, 1, 3, 1, 2]) == 3
```

<details>
<summary>✅ Solution</summary>

**Solution 1: Brute force O(n²)**
```python
def count_inversions(arr):
    count = 0
    n = len(arr)
    for i in range(n):
        for j in range(i + 1, n):
            if arr[i] > arr[j]:
                count += 1
    return count
```

**Solution 2: Merge sort approach O(n log n)**
```python
def count_inversions(arr):
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
            inversions += len(left) - i  # All remaining left elements form inversions
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])

    return result, inversions
```

**Why merge sort works:**
- When merging, if we pick from right array before left, those are inversions
- If left[i] > right[j], then left[i], left[i+1], ... all > right[j]
- So we have (len(left) - i) inversions

**Time: O(n log n) vs O(n²) for brute force**

</details>

---

### Problem 18: Stable Sort Requirement

Sort an array of objects while preserving relative order of equal elements.

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

# Sort by priority, but Item(1, 3) should come before Item(3, 3)
# because Item(1) appeared first
result = sorted(...)  # Your solution

# Result should be: [Item(2,1), Item(4,2), Item(1,3), Item(3,3)]
```

<details>
<summary>✅ Solution</summary>

```python
result = sorted(items, key=lambda item: item.priority)
```

**Key insight:** Python's `sorted()` is **stable** — it preserves the relative order of elements with equal keys.

**Verification:**
```python
items = [Item(1, 3), Item(2, 1), Item(3, 3), Item(4, 2)]
result = sorted(items, key=lambda item: item.priority)

# Result:
# Item(2, 1) — priority 1
# Item(4, 2) — priority 2
# Item(1, 3) — priority 3 (came before Item(3, 3) originally)
# Item(3, 3) — priority 3 (came after Item(1, 3) originally)
```

**Why this matters:**
- Some sorting algorithms (like quick sort) are not stable
- Merge sort and insertion sort are stable
- When you need to preserve original order of equal elements, use a stable sort
- Python's `sorted()` uses Timsort, which is stable

**Checking if a sort is stable:**
```python
# If this is true, the sort is stable
data = [('a', 1), ('b', 1), ('c', 2)]
result = sorted(data, key=lambda x: x[1])
assert result == [('a', 1), ('b', 1), ('c', 2)]  # 'a' before 'b' preserved
```

</details>

---

### Problem 19: Benchmark Sorting Algorithms

Write code to benchmark bubble sort, insertion sort, and merge sort on arrays of size 100, 1000, and 10000.

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
    # Implementation from earlier problems
    pass

# Your benchmark code here
```

<details>
<summary>✅ Solution</summary>

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

**Expected output (approximate):**
```
Size       Bubble Sort          Insertion Sort       Merge Sort
----------------------------------------------------------------------
100        0.000010             0.000005             0.000002
1000       0.001000             0.000400             0.000015
10000      0.100000             0.040000             0.000150
```

**Observations:**
- Bubble sort gets progressively slower
- Insertion sort is 2-3x faster than bubble
- Merge sort is 100-1000x faster
- Gap widens as size increases (due to O(n²) vs O(n log n))

</details>

---

### Problem 20: Custom Comparator for Complex Sorting

Sort students by GPA (descending), and if GPAs are equal, by name (ascending).

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

# Sort by: GPA descending, then name ascending
# Expected: [Student(Alice, 3.8), Student(Bob, 3.8), Student(Diana, 3.8), Student(Charlie, 3.5)]
result = sorted(...)
```

<details>
<summary>✅ Solution</summary>

```python
result = sorted(students, key=lambda s: (-s.gpa, s.name))
```

**Explanation:**
- `-s.gpa` sorts by GPA descending (negative reverses order)
- `s.name` sorts by name ascending
- Tuple comparison: Python compares first element, then second if first is equal

**Result:**
```
[
    Student(Alice, 3.8),
    Student(Bob, 3.8),
    Student(Diana, 3.8),
    Student(Charlie, 3.5)
]
```

**Alternative with reverse parameter:**
```python
# Can't directly use reverse for partial sorting
# But can explicitly negate numeric values
result = sorted(students, key=lambda s: (-s.gpa, s.name))

# Or with a custom comparison function (older Python style):
from functools import cmp_to_key

def compare(s1, s2):
    if s1.gpa != s2.gpa:
        return s2.gpa - s1.gpa  # Descending GPA
    return s1.name < s2.name    # Ascending name

result = sorted(students, key=cmp_to_key(compare))
```

**Key patterns for complex sorts:**
- Use tuples in key function
- Negate numeric values to reverse order
- Multiple conditions in tuple are applied left-to-right
- For objects, use lambda with attribute access

</details>

