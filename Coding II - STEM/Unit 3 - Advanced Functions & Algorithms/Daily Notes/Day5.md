# Day 5: Recursion Applied (Fibonacci, Traversal)
**Learning Target:** I can apply recursion to solve complex problems.

### Key Concepts
Recursion is powerful for: tree traversal, graph search, divide-and-conquer algorithms, and dynamic problems.

### Code Examples
```python
# Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8...
def fib(n):
    if n <= 1:
        return n
    return fib(n - 1) + fib(n - 2)

print(fib(6))  # 8

# Better: memoization (cache results)
def fib_memo(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib_memo(n - 1, memo) + fib_memo(n - 2, memo)
    return memo[n]

# Traverse nested structure
def flatten(nested):
    result = []
    for item in nested:
        if isinstance(item, list):
            result.extend(flatten(item))
        else:
            result.append(item)
    return result

print(flatten([1, [2, [3, 4]], 5]))  # [1, 2, 3, 4, 5]

# Binary search (divide and conquer)
def binary_search(sorted_list, target, low, high):
    if low > high:
        return -1
    mid = (low + high) // 2
    if sorted_list[mid] == target:
        return mid
    elif sorted_list[mid] < target:
        return binary_search(sorted_list, target, mid + 1, high)
    else:
        return binary_search(sorted_list, target, low, mid - 1)
```

### Guided Practice
Implement: sum of digits, tree traversal, permutations.

### Practice Problems
**Problem 1 — Beginner:** Write a recursive function to reverse a string.

**Problem 2 — Intermediate:** Write recursive binary search.

**Problem 3 — Challenge:** Write a function to generate all permutations of a string recursively.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
def reverse_string(s):
    if len(s) == 0:
        return s
    return reverse_string(s[1:]) + s[0]

# Problem 2 (shown above)

# Problem 3
def permutations(s):
    if len(s) <= 1:
        return [s]
    result = []
    for i, char in enumerate(s):
        for perm in permutations(s[:i] + s[i+1:]):
            result.append(char + perm)
    return result
```
</details>

---

---
