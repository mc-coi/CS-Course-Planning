# Day 18: Binary Search and Recursive Algorithms

**Learning Target:** I can implement binary search recursively and understand how divide-and-conquer algorithms work.

---

## Key Concepts

**Binary Search** — Efficiently find a target in a sorted list by repeatedly dividing the search space in half. O(log n) time complexity.

**Divide and Conquer** — Break problem into smaller subproblems, solve recursively, combine results.

**Precondition** — Binary search requires the list to be sorted!

**Advantages of Binary Search:**
- Much faster than linear search for large sorted lists
- O(log n) vs O(n) time complexity
- Elegant recursive implementation

**Recursive Binary Search Structure:**
1. Base case: item found or search space empty
2. Recursive case: search left or right half

---

## Code Examples

```python
# Example 1: Simple linear search (for comparison)
def linear_search(lst, target):
    for i, value in enumerate(lst):
        if value == target:
            return i
    return -1

numbers = [2, 5, 7, 10, 15, 20, 25]
print(linear_search(numbers, 15))  # Output: 4

# Example 2: Binary search - iterative
def binary_search_iterative(lst, target):
    left, right = 0, len(lst) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if lst[mid] == target:
            return mid
        elif lst[mid] < target:
            left = mid + 1  # Search right half
        else:
            right = mid - 1  # Search left half
    
    return -1  # Not found

numbers = [2, 5, 7, 10, 15, 20, 25]
print(binary_search_iterative(numbers, 15))  # Output: 4

# Example 3: Binary search - recursive
def binary_search_recursive(lst, target, left=0, right=None):
    if right is None:
        right = len(lst) - 1
    
    if left > right:
        return -1  # Base case: not found
    
    mid = (left + right) // 2
    
    if lst[mid] == target:
        return mid  # Base case: found!
    elif lst[mid] < target:
        return binary_search_recursive(lst, target, mid + 1, right)  # Search right
    else:
        return binary_search_recursive(lst, target, left, mid - 1)   # Search left

numbers = [2, 5, 7, 10, 15, 20, 25]
print(binary_search_recursive(numbers, 15))  # Output: 4

# Example 4: Find first occurrence
def binary_search_first(lst, target, left=0, right=None):
    if right is None:
        right = len(lst) - 1
    
    if left > right:
        return -1
    
    mid = (left + right) // 2
    
    if lst[mid] == target:
        # Keep searching left for first occurrence
        if mid == 0 or lst[mid - 1] != target:
            return mid
        else:
            return binary_search_first(lst, target, left, mid - 1)
    elif lst[mid] < target:
        return binary_search_first(lst, target, mid + 1, right)
    else:
        return binary_search_first(lst, target, left, mid - 1)

numbers = [1, 2, 2, 2, 3, 4, 5]
print(binary_search_first(numbers, 2))  # Output: 1

# Example 5: Find insertion position
def binary_search_insert(lst, target):
    """Find where target should be inserted to keep list sorted"""
    left, right = 0, len(lst)
    
    while left < right:
        mid = (left + right) // 2
        if lst[mid] < target:
            left = mid + 1
        else:
            right = mid
    
    return left

numbers = [1, 3, 5, 7, 9]
print(binary_search_insert(numbers, 6))  # Output: 3 (insert at index 3)

# Example 6: Merge sort (divide and conquer)
def merge_sort(lst):
    if len(lst) <= 1:
        return lst  # Base case
    
    mid = len(lst) // 2
    left = merge_sort(lst[:mid])      # Divide left half
    right = merge_sort(lst[mid:])     # Divide right half
    
    return merge(left, right)          # Conquer: merge

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

numbers = [38, 27, 43, 3, 9, 82, 10]
print(merge_sort(numbers))  # Output: [3, 9, 10, 27, 38, 43, 82]

# Example 7: Time complexity comparison
import time

def time_search(func, lst, target):
    start = time.time()
    func(lst, target)
    return time.time() - start

import random
numbers = sorted([random.randint(1, 10000) for _ in range(10000)])

time_linear = time_search(linear_search, numbers, 5000)
time_binary = time_search(binary_search_iterative, numbers, 5000)

# Binary search is much faster for large sorted lists

# Example 8: Visualizing binary search
def binary_search_visual(lst, target):
    """Binary search that shows the process"""
    left, right = 0, len(lst) - 1
    
    while left <= right:
        mid = (left + right) // 2
        print(f"Searching between indices {left} and {right}: lst[{mid}] = {lst[mid]}")
        
        if lst[mid] == target:
            print(f"Found {target} at index {mid}!")
            return mid
        elif lst[mid] < target:
            print(f"  {target} > {lst[mid]}, search right half")
            left = mid + 1
        else:
            print(f"  {target} < {lst[mid]}, search left half")
            right = mid - 1
    
    print(f"{target} not found")
    return -1

numbers = [2, 5, 7, 10, 15, 20, 25, 30, 35]
binary_search_visual(numbers, 15)
```

---

## Guided Practice

**Step 1:** Implement binary search recursively.
```python
def binary_search(lst, target, left=0, right=None):
    if right is None:
        right = len(lst) - 1
    
    if left > right:
        return -1
    
    mid = (left + right) // 2
    if lst[mid] == target:
        return mid
    elif lst[mid] < target:
        return binary_search(lst, target, mid + 1, right)
    else:
        return binary_search(lst, target, left, mid - 1)

numbers = [1, 3, 5, 7, 9, 11, 13]
print(binary_search(numbers, 7))  # Should print: 3
```

**Step 2:** Trace through a binary search to understand the divisions.
```python
# On [1, 3, 5, 7, 9, 11, 13] searching for 7:
# mid = 3, lst[3] = 7, found!
```

**Step 3:** Implement merge sort.
```python
def merge_sort(lst):
    if len(lst) <= 1:
        return lst
    mid = len(lst) // 2
    return merge(merge_sort(lst[:mid]), merge_sort(lst[mid:]))

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
    return result + left[i:] + right[j:]

print(merge_sort([3, 1, 4, 1, 5]))  # Should print: [1, 1, 3, 4, 5]
```

---

## Practice Problems

**Beginner:** Write an iterative binary search function.

**Intermediate:** Implement binary search for finding the leftmost (first) occurrence of a value.

**Challenge:** Implement a complete merge sort and compare its performance to Python's built-in sort.

<details>
<summary>💡 Hints</summary>
- For Beginner: Use while loop with left/right pointers
- For Intermediate: When found, continue searching left
- For Challenge: Time both and note the difference
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def binary_search_iter(lst, target):
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

# Intermediate: (see Day 18 Example 4)

# Challenge: see merge_sort above
```
</details>
