# Unit 3 Assessment: Advanced Functions & Algorithms

**Total Points:** 100
**Time Limit:** 90 minutes
**Format:** Multiple Choice (25 pts), Short Answer (25 pts), Coding Problems (50 pts)

---

## Part 1: Multiple Choice (25 points, 2.5 pts each)

**1.** What is the output of this lambda function?
```python
f = lambda x: x * 2 if x > 5 else x
print(f(10))
```
A) 10
B) 20
C) True
D) Error

**2.** Which of the following best describes what `map()` does?
A) Applies a function to each element and returns a generator
B) Filters elements based on a condition
C) Combines two lists element-by-element
D) Creates a new data structure from existing elements

**3.** What will this code print?
```python
numbers = [1, 2, 3, 4, 5]
result = list(filter(lambda x: x % 2 == 0, numbers))
print(result)
```
A) [1, 3, 5]
B) [2, 4]
C) [1, 2, 3, 4, 5]
D) None

**4.** The time complexity of binary search on a sorted list is:
A) O(1)
B) O(log n)
C) O(n)
D) O(n²)

**5.** What will this list comprehension produce?
```python
[x**2 for x in range(5) if x % 2 == 1]
```
A) [0, 4, 16]
B) [1, 9]
C) [1, 9, 25]
D) [0, 1, 4, 9, 16]

**6.** In the LEGB rule, what does "E" stand for?
A) Error
B) Enclosing
C) Evaluated
D) External

**7.** What does `yield` do in a generator?
A) Returns and exits the function
B) Pauses and resumes execution
C) Creates a list of values
D) Filters out values

**8.** Which has better time complexity?
A) Bubble sort: O(n²)
B) Merge sort: O(n log n)
C) Both are equivalent
D) Depends on input size

**9.** What is a closure?
A) A function that ends execution
B) A function that remembers variables from its enclosing scope
C) A loop that closes over variables
D) An error in Python

**10.** What will this code output?
```python
names = ["A", "B", "C"]
ages = [20, 30]
result = list(zip(names, ages))
print(result)
```
A) [("A", 20), ("B", 30), ("C", None)]
B) [("A", 20), ("B", 30)]
C) Error
D) [("A", "B", "C"), (20, 30)]

---

## Part 2: Short Answer (25 points)

**1.** (5 pts) Explain the difference between a list and a generator. When would you use each?

**2.** (5 pts) Write pseudocode for the binary search algorithm.

**3.** (5 pts) What is Big O notation and why is it important in computer science?

**4.** (5 pts) Explain what a decorator does and provide a one-sentence example of when you'd use one.

**5.** (5 pts) Draw the call stack for `factorial(3)` showing each recursive call and return value.

---

## Part 3: Coding Problems (50 points)

**Problem 1: Recursion (15 points)**

Write a recursive function that counts the number of times a target value appears in a list.

Example:
```python
count_occurrences([1, 2, 2, 3, 2, 4], 2)  # Returns: 3
```

<details>
<summary>Sample Solution</summary>

```python
def count_occurrences(lst, target):
    # Base case: empty list
    if len(lst) == 0:
        return 0

    # Recursive case
    if lst[0] == target:
        return 1 + count_occurrences(lst[1:], target)
    else:
        return count_occurrences(lst[1:], target)

# Test
assert count_occurrences([1, 2, 2, 3, 2, 4], 2) == 3
assert count_occurrences([], 5) == 0
assert count_occurrences([5, 5, 5], 5) == 3
```

</details>

---

**Problem 2: Comprehensions & Functional Programming (15 points)**

Use list comprehension and functional programming tools to solve this:

Given a list of dictionaries representing students with names and grades, create:
- A list of names for students with grade >= 80
- A dictionary mapping grades to lists of student names

Example input:
```python
students = [
    {"name": "Alice", "grade": 85},
    {"name": "Bob", "grade": 72},
    {"name": "Charlie", "grade": 90},
    {"name": "Diana", "grade": 88}
]
```

<details>
<summary>Sample Solution</summary>

```python
# List of names with grade >= 80
passing = [s["name"] for s in students if s["grade"] >= 80]
# Result: ["Alice", "Charlie", "Diana"]

# Dictionary mapping grades to names
by_grade = {
    grade: [s["name"] for s in students if s["grade"] == grade]
    for grade in set(s["grade"] for s in students)
}
# Result: {85: ['Alice'], 72: ['Bob'], 90: ['Charlie'], 88: ['Diana']}

# Or using groupby:
from itertools import groupby
by_grade_alt = {
    grade: [s["name"] for s in group]
    for grade, group in groupby(sorted(students, key=lambda x: x["grade"]), key=lambda x: x["grade"])
}
```

</details>

---

**Problem 3: Algorithm Analysis & Optimization (20 points)**

**Part A (10 pts):** Analyze the time and space complexity of this function:

```python
def find_pairs_sum(arr, target):
    pairs = []
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if arr[i] + arr[j] == target:
                pairs.append((arr[i], arr[j]))
    return pairs
```

**Part B (10 pts):** Optimize it to have better time complexity and provide your optimized version.

<details>
<summary>Sample Solution</summary>

```python
# Part A Analysis:
# Time Complexity: O(n²) - two nested loops
# Space Complexity: O(k) where k is number of pairs found

# Part B Optimized solution - O(n):
def find_pairs_sum_optimized(arr, target):
    seen = set()
    pairs = set()

    for num in arr:
        complement = target - num
        if complement in seen:
            pair = tuple(sorted([num, complement]))
            pairs.add(pair)
        seen.add(num)

    return list(pairs)

# Optimized Analysis:
# Time Complexity: O(n) - single pass through array
# Space Complexity: O(n) - for the set

# Test cases
assert find_pairs_sum_optimized([1, 5, 7, -1, 5], 6) == {(1, 5), (-1, 7)}
assert find_pairs_sum_optimized([1, 2, 3, 4], 10) == set()
```

</details>

---

## Rubric

### Multiple Choice (25 points)
- 10 questions × 2.5 points = 25 points
- All or nothing per question

### Short Answer (25 points)
- Each question worth 5 points
- Partial credit possible
- Grading scale:
  - 5 pts: Complete, correct, well-explained
  - 4 pts: Mostly correct with minor issues
  - 3 pts: Correct general idea but missing details
  - 2 pts: Partially correct
  - 0-1 pts: Incorrect or blank

### Coding Problems (50 points)

**Problem 1 (15 pts):**
- Correct base case: 5 pts
- Correct recursive case: 7 pts
- Tested with examples: 3 pts

**Problem 2 (15 pts):**
- Correct comprehension syntax: 5 pts
- Solves both parts: 10 pts

**Problem 3 (20 pts):**
- Part A analysis: 10 pts (5 pts per complexity)
- Part B optimization: 10 pts (correct solution)

---

## Answer Key

### Multiple Choice Answers
1. B
2. A
3. B
4. B
5. B
6. B
7. B
8. B
9. B
10. B

### Short Answer Key

**1.** List: Eager evaluation (computes all values), mutable, more memory. Generator: Lazy evaluation (computes on demand), memory efficient. Use generators for large datasets, infinite sequences, or when you don't need all values. Use lists when you need random access or multiple iterations.

**2.** Binary Search Pseudocode:
```
function binarySearch(sortedArray, target, low, high):
    if low > high:
        return -1
    mid = (low + high) / 2
    if array[mid] == target:
        return mid
    else if array[mid] < target:
        return binarySearch(array, target, mid + 1, high)
    else:
        return binarySearch(array, target, low, mid - 1)
```

**3.** Big O notation describes how an algorithm's runtime or space grows as input size increases. It helps us compare algorithms and predict performance on large inputs.

**4.** A decorator is a function that wraps another function to modify its behavior. Example: A timing decorator that measures how long a function takes to run.

**5.** Call stack for factorial(3):
```
factorial(3)
  ├─ 3 * factorial(2)
  │  ├─ 2 * factorial(1)
  │  │  ├─ returns 1
  │  ├─ returns 2
  ├─ returns 6
```

---

## Success Criteria

- **90-100 (A):** Mastered all concepts, excellent problem-solving
- **80-89 (B):** Strong understanding, minor errors
- **70-79 (C):** Solid understanding, some gaps
- **60-69 (D):** Basic understanding, significant gaps
- **Below 60 (F):** Needs review and additional practice
