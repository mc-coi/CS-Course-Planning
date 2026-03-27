# Day 28: Unit 5 Assessment — Sorting, Searching & Recursion

**Learning Target:** I can demonstrate mastery of sorting and searching algorithms and recursive problem-solving.

---

## Assessment Overview

This comprehensive assessment covers all major topics from Unit 5:
- **Part 1 (25 points):** Algorithm Traces — Show step-by-step execution
- **Part 2 (25 points):** Multiple Choice — Big O and algorithm selection
- **Part 3 (20 points):** Short Answer — Conceptual understanding
- **Part 4 (30 points):** Coding Challenges — Implementation and analysis

**Total: 100 points**

**Time Limit:** 90 minutes (Part 1-3: 45 min, Part 4: 45 min)

**Resources Allowed:** Reference Guide, Python interpreter, but NOT other students' work or online solutions

---

## Part 1: Algorithm Traces (25 points)

For each trace, show the array state **after each comparison/pass/selection**. Write clearly and show your work.

### Question 1a: Bubble Sort (10 points)
Trace bubble sort on the array `[5, 3, 8, 1, 9, 2]`. Show the array after each **pass**.

```
Initial: [5, 3, 8, 1, 9, 2]
Pass 1: [___, ___, ___, ___, ___, ___]
Pass 2: [___, ___, ___, ___, ___, ___]
Pass 3: [___, ___, ___, ___, ___, ___]
Pass 4: [___, ___, ___, ___, ___, ___]
Pass 5: [___, ___, ___, ___, ___, ___]
Final: [1, 2, 3, 5, 8, 9]
```

### Question 1b: Binary Search (8 points)
Trace binary search for **target = 7** on the sorted array `[1, 3, 5, 7, 9, 11, 13]`.

For each iteration, show:
- left index
- right index
- mid index
- element at mid
- which direction to search next (or found)

```
Iteration 1: left=___, right=___, mid=___, arr[mid]=___, [next: left/right/found]
Iteration 2: left=___, right=___, mid=___, arr[mid]=___, [next: left/right/found]
...
Result: Found at index ___
```

### Question 1c: Selection Sort (7 points)
Trace selection sort on the array `[4, 2, 7, 1, 5]`. Show the array after **each selection** (when an element finds its place).

```
Initial: [4, 2, 7, 1, 5]
Selection 1 (find min of all): [___, ___, ___, ___, ___]
Selection 2 (find min of rest): [___, ___, ___, ___, ___]
Selection 3: [___, ___, ___, ___, ___]
Selection 4: [___, ___, ___, ___, ___]
Final: [1, 2, 4, 5, 7]
```

---

## Part 2: Multiple Choice (25 points)

**Questions 2.1 - 2.10** (2.5 points each)

**2.1** What is the Big O time complexity of bubble sort in the **worst case**?
- A) O(n)
- B) O(n log n)
- C) O(n²)
- D) O(log n)

**2.2** Merge sort's divide-and-conquer approach makes it O(n log n). What is the main disadvantage?
- A) It's hard to understand
- B) It requires O(n) extra space for merging
- C) It doesn't work on linked lists
- D) It performs poorly on small arrays

**2.3** When is **binary search** the appropriate choice?
- A) When the array is unsorted
- B) When you need to find all occurrences
- C) When the array is sorted AND you're searching for a single value
- D) Never — linear search is always better

**2.4** Which sorting algorithm is most efficient when the data is **nearly sorted**?
- A) Bubble sort (with optimization)
- B) Selection sort
- C) Merge sort
- D) Quick sort

**2.5** What does `sorted(students, key=lambda s: s.age)` do?
- A) Sorts by the default order
- B) Sorts by age in ascending order
- C) Sorts by age in descending order
- D) Deletes students under a certain age

**2.6** What is the **best case** time complexity of quick sort?
- A) O(n)
- B) O(n log n)
- C) O(n²)
- D) O(log n)

**2.7** A recursive function MUST have:
- A) A loop
- B) A base case and a recursive case
- C) A global variable
- D) A return statement

**2.8** What is the time complexity of linear search?
- A) O(1)
- B) O(log n)
- C) O(n)
- D) O(n²)

**2.9** In the recursive function `factorial(n) = n * factorial(n-1)`, what is the base case?
- A) `factorial(n) = n * factorial(n-1)`
- B) `if n == 0: return 1`
- C) `if n == 1: return 1`
- D) Both B and C are valid base cases

**2.10** Which of these is true about Python's `sorted()` function?
- A) It uses bubble sort internally
- B) It uses Timsort, a hybrid algorithm combining merge sort and insertion sort
- C) It's slower than merge sort
- D) It requires the array to be pre-sorted

---

## Part 3: Short Answer (20 points)

Answer in 2-4 sentences. Show your reasoning.

**3.1 (4 points):** Explain why binary search requires the array to be sorted, but linear search does not.

**3.2 (4 points):** You have 1 million numbers to sort. Would you choose bubble sort or merge sort? Why?

**3.3 (4 points):** Write a one-sentence explanation of what "divide and conquer" means in the context of merge sort.

**3.4 (4 points):** A recursive function has the call stack: `fib(5) → fib(4) → fib(3) → fib(2) → fib(1) → return 1`. Explain what happens next on the call stack.

**3.5 (4 points):** Compare insertion sort and bubble sort. Under what conditions might you prefer insertion sort?

---

## Part 4: Coding Challenges (30 points)

Write syntactically correct Python code. Include comments and test your code before submitting.

### Challenge 4.1: Binary Search Implementation (10 points)

Write an **iterative** binary search function that:
- Takes a sorted list and a target value
- Returns the index if found, or -1 if not found
- Works correctly on the following test cases:

```python
def binary_search(arr, target):
    """
    Implement binary search here.
    - arr: sorted list of integers
    - target: value to find
    - return: index of target, or -1 if not found
    """
    pass

# Test cases (all should pass)
assert binary_search([1, 3, 5, 7, 9, 11], 7) == 3
assert binary_search([1, 3, 5, 7, 9, 11], 1) == 0
assert binary_search([1, 3, 5, 7, 9, 11], 11) == 5
assert binary_search([1, 3, 5, 7, 9, 11], 4) == -1
assert binary_search([1, 3, 5, 7, 9, 11], 0) == -1
assert binary_search([1, 3, 5, 7, 9, 11], 12) == -1
assert binary_search([], 5) == -1
assert binary_search([5], 5) == 0
print("All binary search tests passed!")
```

### Challenge 4.2: Merge Sort Implementation (10 points)

Write a **recursive** merge sort function that:
- Sorts a list in ascending order
- Uses the divide-and-conquer approach
- Works correctly on the following test cases:

```python
def merge_sort(arr):
    """
    Implement merge sort here.
    - arr: list of integers
    - return: sorted list
    """
    pass

# Test cases (all should pass)
assert merge_sort([5, 3, 8, 1, 9, 2]) == [1, 2, 3, 5, 8, 9]
assert merge_sort([1]) == [1]
assert merge_sort([]) == []
assert merge_sort([3, 3, 3]) == [3, 3, 3]
assert merge_sort([5, 4, 3, 2, 1]) == [1, 2, 3, 4, 5]
assert merge_sort([1, 2, 3, 4, 5]) == [1, 2, 3, 4, 5]
assert merge_sort([64, 34, 25, 12, 22, 11, 90]) == [11, 12, 22, 25, 34, 64, 90]
print("All merge sort tests passed!")
```

### Challenge 4.3: Algorithm Analysis (10 points)

Given this code, answer the questions:

```python
def mystery_sort(arr):
    for i in range(len(arr)):
        min_idx = i
        for j in range(i + 1, len(arr)):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr
```

**3a (3 points):** What is this algorithm? What is its Big O time complexity in the worst case?

**3b (3 points):** Trace this algorithm on `[4, 1, 3, 2]` showing the array after each iteration of the outer loop.

**3c (4 points):** Write code that benchmarks this algorithm against Python's `sorted()` on an array of 1000 random numbers. Show how much faster (or slower) each is.

```python
import time
import random

def mystery_sort(arr):
    # [code from above]
    pass

# Write benchmark code here
# Compare mystery_sort vs sorted() on 1000 random numbers
# Show time for each

print("Benchmark results:")
# [your results here]
```

---

## Answer Key

### Part 1: Algorithm Traces

**1a: Bubble Sort on [5, 3, 8, 1, 9, 2]**

```
Initial: [5, 3, 8, 1, 9, 2]
Pass 1: [3, 5, 1, 8, 2, 9]  (9 bubbles to end)
Pass 2: [3, 1, 5, 2, 8, 9]  (8 bubbles to position)
Pass 3: [1, 3, 2, 5, 8, 9]  (5 bubbles to position)
Pass 4: [1, 2, 3, 5, 8, 9]  (3 bubbles to position)
Pass 5: [1, 2, 3, 5, 8, 9]  (no swaps, but still counted)
Final: [1, 2, 3, 5, 8, 9]
```

**1b: Binary Search for 7 in [1, 3, 5, 7, 9, 11, 13]**

```
Iteration 1: left=0, right=6, mid=3, arr[3]=7, FOUND!
Result: Found at index 3
```

**1c: Selection Sort on [4, 2, 7, 1, 5]**

```
Initial: [4, 2, 7, 1, 5]
Selection 1 (min=1): [1, 2, 7, 4, 5]  (swap 4 and 1)
Selection 2 (min=2): [1, 2, 7, 4, 5]  (2 already in place)
Selection 3 (min=4): [1, 2, 4, 7, 5]  (swap 7 and 4)
Selection 4 (min=5): [1, 2, 4, 5, 7]  (swap 7 and 5)
Final: [1, 2, 4, 5, 7]
```

### Part 2: Multiple Choice Answer Key

| Question | Answer | Explanation |
|----------|--------|-------------|
| 2.1 | C | Bubble sort is O(n²) in worst case when array is reverse-sorted |
| 2.2 | B | Merge sort requires temporary arrays for merging, using O(n) extra space |
| 2.3 | C | Binary search only works on sorted data and finds single values efficiently |
| 2.4 | A | Bubble sort with early termination is O(n) on nearly-sorted data |
| 2.5 | B | Lambda sorts by age in ascending order |
| 2.6 | B | Quick sort best case is O(n log n) when pivot divides evenly |
| 2.7 | B | Recursion requires base case (to stop) and recursive case (to call itself) |
| 2.8 | C | Linear search must check each element: O(n) |
| 2.9 | D | Both `factorial(0)=1` and `factorial(1)=1` work as base cases |
| 2.10 | B | Python's sorted() uses Timsort, not simple bubble sort |

### Part 3: Short Answer Answer Key

**3.1:** Binary search works by eliminating half the search space each iteration, jumping to the middle. This only works if data is sorted because we know values to the left are smaller and values to the right are larger. Linear search just checks each element in order, so order doesn't matter.

**3.2:** Merge sort. With 1 million numbers, bubble sort would make up to 1 trillion comparisons (n²), while merge sort makes ~20 million (n log n). In practice, this is the difference between hours and seconds.

**3.3:** Divide and conquer means split the problem into smaller subproblems (divide the array in half), solve each independently (recursively sort each half), and combine the solutions (merge the sorted halves).

**3.4:** The function returns `1` to the call stack, so `fib(2)` completes with value `1`. The call stack now shows `fib(3)` waiting for `fib(2)`'s result, which it now has. The result propagates back up the stack.

**3.5:** Insertion sort is better on small arrays or nearly-sorted data. It's simpler to understand and has O(n) best case (when data is mostly sorted), while bubble sort is always O(n²) except on already-sorted data. Insertion sort also sorts "in-place" without extra memory like merge sort needs.

### Part 4: Coding Challenges Answer Key

**Challenge 4.1: Binary Search (Iterative)**

```python
def binary_search(arr, target):
    """
    Iterative binary search implementation.
    """
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1

# Test cases
assert binary_search([1, 3, 5, 7, 9, 11], 7) == 3
assert binary_search([1, 3, 5, 7, 9, 11], 1) == 0
assert binary_search([1, 3, 5, 7, 9, 11], 11) == 5
assert binary_search([1, 3, 5, 7, 9, 11], 4) == -1
assert binary_search([1, 3, 5, 7, 9, 11], 0) == -1
assert binary_search([1, 3, 5, 7, 9, 11], 12) == -1
assert binary_search([], 5) == -1
assert binary_search([5], 5) == 0
print("All binary search tests passed!")
```

**Challenge 4.2: Merge Sort (Recursive)**

```python
def merge_sort(arr):
    """
    Recursive merge sort implementation.
    """
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    return merge(left, right)

def merge(left, right):
    """
    Merge two sorted arrays into one sorted array.
    """
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

# Test cases
assert merge_sort([5, 3, 8, 1, 9, 2]) == [1, 2, 3, 5, 8, 9]
assert merge_sort([1]) == [1]
assert merge_sort([]) == []
assert merge_sort([3, 3, 3]) == [3, 3, 3]
assert merge_sort([5, 4, 3, 2, 1]) == [1, 2, 3, 4, 5]
assert merge_sort([1, 2, 3, 4, 5]) == [1, 2, 3, 4, 5]
assert merge_sort([64, 34, 25, 12, 22, 11, 90]) == [11, 12, 22, 25, 34, 64, 90]
print("All merge sort tests passed!")
```

**Challenge 4.3: Algorithm Analysis**

**3a:** This is **selection sort**. Time complexity is **O(n²)** in the worst case because we have nested loops that iterate through the entire remaining array for each position.

**3b:** Trace on [4, 1, 3, 2]:
```
Initial: [4, 1, 3, 2]
Iteration 0 (min=1): [1, 4, 3, 2]
Iteration 1 (min=2): [1, 2, 3, 4]
Iteration 2 (min=3): [1, 2, 3, 4]
Iteration 3: [1, 2, 3, 4]
Final: [1, 2, 3, 4]
```

**3c:** Benchmark code:
```python
import time
import random

def mystery_sort(arr):
    """Selection sort"""
    for i in range(len(arr)):
        min_idx = i
        for j in range(i + 1, len(arr)):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr

# Create test data
test_data = random.sample(range(10000), 1000)

# Benchmark mystery_sort
start = time.time()
mystery_sort(test_data.copy())
mystery_time = time.time() - start

# Benchmark Python sorted()
start = time.time()
sorted(test_data)
sorted_time = time.time() - start

print("Benchmark results (1000 random numbers):")
print(f"mystery_sort (selection): {mystery_time:.6f} seconds")
print(f"Python sorted(): {sorted_time:.6f} seconds")
print(f"Ratio: sorted() is {mystery_time/sorted_time:.1f}x faster")
```

Expected results: `sorted()` should be 50-200x faster depending on system, because it uses Timsort (O(n log n)) vs selection sort (O(n²)).

</details>
