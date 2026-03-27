# Unit 5 Assessment: Sorting, Searching & Recursion

**Total Points: 100**
**Time Limit: 90 minutes** (Part 1-3: 45 min, Part 4: 45 min)
**Resources Allowed:** ReferenceGuide.md, Python interpreter (for Part 4)

---

## Scoring Rubric

| Part | Points | Time | Content |
|------|--------|------|---------|
| Part 1 | 25 | 15 min | Algorithm Traces |
| Part 2 | 25 | 15 min | Multiple Choice |
| Part 3 | 20 | 15 min | Short Answer |
| Part 4 | 30 | 45 min | Coding Challenges |
| **Total** | **100** | **90 min** | |

---

## Part 1: Algorithm Traces (25 points)

Show your work clearly. Write array states after each step.

### Question 1.1: Bubble Sort Trace (10 points)

Trace bubble sort on the array `[5, 3, 8, 1, 9, 2]`. Show the array **after each pass**.

```
Initial: [5, 3, 8, 1, 9, 2]
Pass 1: _________________________
Pass 2: _________________________
Pass 3: _________________________
Pass 4: _________________________
Pass 5: _________________________
Final:  [1, 2, 3, 5, 8, 9]
```

**Points breakdown:**
- 2 points: Correct Pass 1
- 2 points: Correct Pass 2
- 2 points: Correct Pass 3
- 2 points: Correct Pass 4
- 2 points: Correct Pass 5

---

### Question 1.2: Binary Search Trace (8 points)

Trace binary search for **target = 7** on the sorted array `[1, 3, 5, 7, 9, 11, 13]`.

For each iteration, show:
- left index
- right index
- mid index
- value at arr[mid]
- next action (search left, search right, or found)

```
Iteration 1: left=___, right=___, mid=___, arr[mid]=___, [next: ___]
Iteration 2: left=___, right=___, mid=___, arr[mid]=___, [next: ___]
...
Result: Found at index ___
```

**Points breakdown:**
- 1 point per iteration (up to 2 iterations typical)
- 2 points: Correct final index

---

### Question 1.3: Selection Sort Trace (7 points)

Trace selection sort on the array `[4, 2, 7, 1, 5]`. Show the array **after each selection**.

```
Initial:     [4, 2, 7, 1, 5]
Selection 1: _________________________
Selection 2: _________________________
Selection 3: _________________________
Selection 4: _________________________
Final:       [1, 2, 4, 5, 7]
```

**Points breakdown:**
- 1.75 points per correct selection state

---

## Part 2: Multiple Choice (25 points)

**Each question: 2.5 points** (total 10 questions)

**Question 2.1:** What is the Big O time complexity of bubble sort in the **worst case**?

A) O(n)
B) O(n log n)
C) O(n²)
D) O(log n)

---

**Question 2.2:** Merge sort's O(n log n) performance comes from its divide-and-conquer approach. What is the main disadvantage of merge sort?

A) It's difficult to understand the algorithm
B) It requires O(n) extra space for temporary arrays during merging
C) It doesn't work on linked lists
D) It performs poorly on small arrays

---

**Question 2.3:** When is **binary search** the appropriate choice?

A) When the array is unsorted and you want to find a value
B) When you need to find all occurrences of a value
C) When the array is sorted AND you're searching for a single value
D) Never — linear search is always better

---

**Question 2.4:** Which sorting algorithm performs best when the data is **already nearly sorted**?

A) Bubble sort with the swapped optimization
B) Selection sort
C) Merge sort
D) Quick sort with random pivot

---

**Question 2.5:** What does `sorted(students, key=lambda s: s.age)` do?

A) Sorts students by their default order
B) Sorts students by age in ascending order
C) Sorts students by age in descending order
D) Deletes students under a certain age

---

**Question 2.6:** What is the **best case** time complexity of quick sort?

A) O(n)
B) O(n log n)
C) O(n²)
D) O(log n)

---

**Question 2.7:** A recursive function MUST contain which of the following?

A) A loop statement
B) A base case AND a recursive case
C) A global variable
D) Only a return statement

---

**Question 2.8:** What is the time complexity of linear search?

A) O(1)
B) O(log n)
C) O(n)
D) O(n²)

---

**Question 2.9:** In the recursive function `factorial(n) = n * factorial(n-1)`, which of these is a valid base case?

A) `if n == 1: return 1`
B) `if n == 0: return 1`
C) Both A and B are valid
D) The function has no valid base case

---

**Question 2.10:** Which statement best describes Python's `sorted()` function?

A) It uses bubble sort internally
B) It uses Timsort, a hybrid algorithm combining merge sort and insertion sort
C) It's slower than merge sort for most datasets
D) It requires the array to be pre-sorted

---

## Part 3: Short Answer (20 points)

Answer in 2-5 sentences. Show your reasoning.

### Question 3.1 (4 points): Binary Search Requirements

Explain why binary search requires the data to be sorted, but linear search does not.

---

### Question 3.2 (4 points): Algorithm Selection

You need to sort 1 million numbers one time. Would you choose bubble sort or merge sort? Explain your choice with reasoning about time complexity.

---

### Question 3.3 (4 points): Divide and Conquer

Write one sentence explaining what "divide and conquer" means in the context of merge sort.

---

### Question 3.4 (4 points): Recursion and Call Stack

A recursive function has this call stack progression:
```
fib(5) → fib(4) → fib(3) → fib(2) → fib(1) → return 1
```

Explain what happens next on the call stack. Where does the value 1 go? What function calls next?

---

### Question 3.5 (4 points): Comparing Simple Sorts

Compare insertion sort and bubble sort. Under what conditions might insertion sort be faster than bubble sort, even though both are O(n²)?

---

## Part 4: Coding Challenges (30 points)

Write syntactically correct Python code. Test your code on the provided test cases.

### Challenge 4.1: Binary Search Implementation (10 points)

Implement an **iterative** binary search function that:
- Takes a sorted list and a target value
- Returns the index if found, or -1 if not found
- Works on all test cases below

```python
def binary_search(arr, target):
    """
    Iterative binary search.
    - arr: sorted list of integers
    - target: value to find
    - return: index of target, or -1 if not found

    Time complexity: O(log n)
    Space complexity: O(1)
    """
    pass

# Test your implementation (all must pass)
assert binary_search([1, 3, 5, 7, 9, 11], 7) == 3
assert binary_search([1, 3, 5, 7, 9, 11], 1) == 0
assert binary_search([1, 3, 5, 7, 9, 11], 11) == 5
assert binary_search([1, 3, 5, 7, 9, 11], 4) == -1
assert binary_search([1, 3, 5, 7, 9, 11], 0) == -1
assert binary_search([1, 3, 5, 7, 9, 11], 12) == -1
assert binary_search([], 5) == -1
assert binary_search([5], 5) == 0
assert binary_search([5], 3) == -1

print("All binary search tests passed!")
```

**Grading (10 points):**
- 2 points: Correct structure and variables
- 3 points: Correct midpoint calculation
- 3 points: Correct search logic (left/right adjustment)
- 2 points: All test cases pass

---

### Challenge 4.2: Merge Sort Implementation (10 points)

Implement a **recursive** merge sort function that:
- Sorts a list in ascending order
- Uses the divide-and-conquer approach
- Includes a separate merge function
- Works on all test cases below

```python
def merge_sort(arr):
    """
    Recursive merge sort using divide and conquer.
    - arr: list of integers
    - return: sorted list

    Time complexity: O(n log n)
    Space complexity: O(n)
    """
    pass

def merge(left, right):
    """
    Merge two sorted arrays into one sorted array.
    """
    pass

# Test your implementation (all must pass)
assert merge_sort([5, 3, 8, 1, 9, 2]) == [1, 2, 3, 5, 8, 9]
assert merge_sort([1]) == [1]
assert merge_sort([]) == []
assert merge_sort([3, 3, 3]) == [3, 3, 3]
assert merge_sort([5, 4, 3, 2, 1]) == [1, 2, 3, 4, 5]
assert merge_sort([1, 2, 3, 4, 5]) == [1, 2, 3, 4, 5]
assert merge_sort([64, 34, 25, 12, 22, 11, 90]) == [11, 12, 22, 25, 34, 64, 90]

print("All merge sort tests passed!")
```

**Grading (10 points):**
- 2 points: Base case handling
- 3 points: Divide step (splitting array)
- 2 points: Merge function logic
- 3 points: All test cases pass

---

### Challenge 4.3: Algorithm Analysis (10 points)

Given this code:

```python
def mystery_algorithm(arr):
    for i in range(len(arr)):
        min_idx = i
        for j in range(i + 1, len(arr)):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr
```

**Part A (2 points):** What is the name of this algorithm?

**Part B (2 points):** What is the Big O time complexity in the worst case?

**Part C (3 points):** Trace this algorithm on `[4, 1, 3, 2]` showing the array **after each iteration of the outer loop**.

```
Initial:     [4, 1, 3, 2]
Iteration 0: _________________________
Iteration 1: _________________________
Iteration 2: _________________________
Iteration 3: _________________________
```

**Part D (3 points):** Write code that benchmarks this algorithm against Python's `sorted()` on an array of 1000 random numbers. Show both execution times and calculate how much faster one is than the other.

```python
import time
import random

def mystery_algorithm(arr):
    # [code from above]
    pass

# Your benchmark code here:
# 1. Create an array of 1000 random numbers
# 2. Benchmark mystery_algorithm
# 3. Benchmark sorted()
# 4. Calculate ratio
# 5. Print results

# Expected output should show sorted() is 50-200x faster
```

---

# ANSWER KEY

## Part 1: Algorithm Traces

### Answer 1.1: Bubble Sort on [5, 3, 8, 1, 9, 2]

```
Initial: [5, 3, 8, 1, 9, 2]
Pass 1: [3, 5, 1, 8, 2, 9]
Pass 2: [3, 1, 5, 2, 8, 9]
Pass 3: [1, 3, 2, 5, 8, 9]
Pass 4: [1, 2, 3, 5, 8, 9]
Pass 5: [1, 2, 3, 5, 8, 9]
```

**Explanation:** Each pass bubbles the largest unsorted element to its correct position at the end.

---

### Answer 1.2: Binary Search for 7 in [1, 3, 5, 7, 9, 11, 13]

```
Iteration 1: left=0, right=6, mid=3, arr[3]=7, FOUND!
Result: Found at index 3
```

**Explanation:** The middle element is 7, so we immediately find it.

---

### Answer 1.3: Selection Sort on [4, 2, 7, 1, 5]

```
Initial:     [4, 2, 7, 1, 5]
Selection 1: [1, 2, 7, 4, 5]  (min=1, swap with position 0)
Selection 2: [1, 2, 7, 4, 5]  (min=2, already in position)
Selection 3: [1, 2, 4, 7, 5]  (min=4, swap with position 2)
Selection 4: [1, 2, 4, 5, 7]  (min=5, swap with position 3)
Final:       [1, 2, 4, 5, 7]
```

---

## Part 2: Multiple Choice Answer Key

| Q | Answer | Explanation |
|---|--------|-------------|
| 2.1 | **C** | O(n²) — bubble sort compares each element with every other in nested loops |
| 2.2 | **B** | Merge sort requires O(n) temporary space for combining sorted subarrays |
| 2.3 | **C** | Binary search only works on sorted data and is efficient for single value searches |
| 2.4 | **A** | Bubble sort with early termination is O(n) on nearly-sorted data |
| 2.5 | **B** | The lambda extracts the age and sorted() sorts in ascending order by default |
| 2.6 | **B** | Quick sort is O(n log n) when pivot divides the array evenly |
| 2.7 | **B** | Recursion requires BOTH a base case (to stop) and recursive case (to call itself) |
| 2.8 | **C** | Linear search must check each element: O(n) in worst case |
| 2.9 | **C** | Both factorial(0)=1 and factorial(1)=1 work as valid base cases |
| 2.10 | **B** | Python uses Timsort, a hybrid of merge sort and insertion sort |

---

## Part 3: Short Answer Answer Key

### Answer 3.1: Binary Search Requirements

Binary search works by eliminating half of the remaining search space with each comparison, jumping to the middle element. This only works correctly if data is sorted, because we can assume all smaller values are to the left and all larger values are to the right. Linear search just checks each element sequentially, so the order doesn't affect its correctness.

### Answer 3.2: Algorithm Selection

**Choose merge sort.** Bubble sort is O(n²), which on 1 million elements means up to 1 trillion comparisons. Merge sort is O(n log n), which is only about 20 million comparisons. In practice, this means bubble sort could take hours while merge sort completes in seconds or less.

### Answer 3.3: Divide and Conquer

Divide and conquer means breaking the problem into smaller subproblems (dividing the array in half), solving each independently (recursively sorting each half), and combining the solutions (merging the sorted halves back together).

### Answer 3.4: Recursion and Call Stack

After fib(1) returns 1, the call stack goes back to fib(2), which now has both arguments (fib(1)=1 and fib(0)=0, if calculated). So fib(2) can compute 1 + 0 = 1 and return. Then fib(3) can complete with fib(2)=1 and fib(1)=1, continuing back up the stack until fib(5) finally computes and returns.

### Answer 3.5: Insertion vs Bubble Sort

Insertion sort is often faster in practice because:
1. It works better on nearly-sorted data (best case O(n) vs bubble's O(n²))
2. It accesses memory sequentially (better CPU cache usage)
3. It performs fewer swaps (shift operations are faster than swaps)
4. It can be faster on small datasets

---

## Part 4: Coding Solutions

### Solution 4.1: Binary Search

```python
def binary_search(arr, target):
    """Iterative binary search."""
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

---

### Solution 4.2: Merge Sort

```python
def merge_sort(arr):
    """Recursive merge sort."""
    if len(arr) <= 1:
        return arr

    # Divide
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    # Conquer (merge)
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
```

---

### Solution 4.3: Algorithm Analysis

**Part A:** This is **Selection Sort**

**Part B:** **O(n²)** in the worst case (also best and average case)

**Part C:** Trace on [4, 1, 3, 2]

```
Initial:     [4, 1, 3, 2]
Iteration 0: [1, 4, 3, 2]  (min=1 at index 1, swap with index 0)
Iteration 1: [1, 2, 3, 4]  (min=2 at index 3, swap with index 1)
Iteration 2: [1, 2, 3, 4]  (min=3 at index 2, already in place)
Iteration 3: [1, 2, 3, 4]  (only element 4 remains, in correct position)
```

**Part D:** Benchmark code

```python
import time
import random

def mystery_algorithm(arr):
    for i in range(len(arr)):
        min_idx = i
        for j in range(i + 1, len(arr)):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr

# Create test data
test_data = random.sample(range(10000), 1000)

# Benchmark mystery_algorithm (selection sort)
start = time.time()
mystery_algorithm(test_data.copy())
mystery_time = time.time() - start

# Benchmark Python's sorted()
start = time.time()
sorted(test_data)
sorted_time = time.time() - start

print("Benchmark Results (1000 random numbers):")
print(f"Selection Sort:  {mystery_time:.6f} seconds")
print(f"Python sorted(): {sorted_time:.6f} seconds")
print(f"Ratio: sorted() is {mystery_time/sorted_time:.1f}x faster")

# Expected output: sorted() is 50-200x faster
```

**Expected results:**
- Selection sort: ~0.01-0.05 seconds
- Python sorted(): ~0.0001-0.001 seconds
- Ratio: 50-200x faster (because sorted() uses Timsort O(n log n) vs selection sort O(n²))

---

## Grading Rubric Summary

**Part 1 (25 points):** Detailed algorithm traces with correct state after each step
**Part 2 (25 points):** 2.5 points each × 10 questions
**Part 3 (20 points):** 4 points each for well-explained short answers
**Part 4 (30 points):** 10 points per coding challenge (correctness, efficiency, tests passing)

**Total: 100 points**

---

## Interpretation Guide

| Score | Grade | Mastery Level |
|-------|-------|----------------|
| 90-100 | A | Excellent — demonstrates full mastery |
| 80-89 | B | Good — understands core concepts with minor gaps |
| 70-79 | C | Satisfactory — understands basic concepts |
| 60-69 | D | Minimal — significant gaps in understanding |
| <60 | F | Insufficient — major misunderstandings |

