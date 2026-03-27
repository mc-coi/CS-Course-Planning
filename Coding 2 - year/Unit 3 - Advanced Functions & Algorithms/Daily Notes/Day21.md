# Day 21: Space Complexity and Algorithm Optimization

**Learning Target:** I can analyze space complexity and optimize algorithms for both time and space efficiency.

---

## Key Concepts

**Space Complexity** — How much extra memory (beyond input) an algorithm uses, described with Big O.

**Space vs. Time Trade-offs:**
- More space can reduce time (caching results)
- Less space often means more time (recomputing)
- Balance depends on the problem context

**Common Space Complexities:**
- **O(1)** — Constant space (a few variables)
- **O(n)** — Linear space (new array of size n)
- **O(log n)** — Logarithmic (recursion depth in binary search)
- **O(n²)** — Quadratic (2D array)

**Optimization Techniques:**
1. In-place algorithms (modify input, use O(1) extra space)
2. Iterative instead of recursive (reduce call stack)
3. Hash tables for fast lookups
4. Sorting to enable efficient algorithms

---

## Code Examples

```python
# Example 1: High space complexity - storing intermediate results
def pairs_product_bad(lst):
    """O(n²) space - stores all pairs"""
    result = []
    for i in range(len(lst)):
        for j in range(len(lst)):
            result.append(lst[i] * lst[j])
    return result
# Space: O(n²) output + O(1) extra

# Example 2: Optimized space - generator instead of list
def pairs_product_good(lst):
    """O(1) extra space - uses generator"""
    for i in range(len(lst)):
        for j in range(len(lst)):
            yield lst[i] * lst[j]
# Space: O(1) extra, returns one pair at a time

# Example 3: Recursion depth = O(n) space (call stack)
def factorial_recursive(n):
    if n <= 1:
        return 1
    return n * factorial_recursive(n - 1)
# Space: O(n) due to recursion depth

# Example 4: Iterative = O(1) space (no call stack)
def factorial_iterative(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result
# Space: O(1)

# Example 5: In-place sorting (O(1) or O(log n) extra space)
def bubble_sort_inplace(lst):
    """Modifies list in-place, O(1) extra space"""
    for i in range(len(lst)):
        for j in range(len(lst) - 1):
            if lst[j] > lst[j + 1]:
                lst[j], lst[j + 1] = lst[j + 1], lst[j]
    return lst

# Example 6: Merge sort (O(n) extra space)
def merge_sort(lst):
    if len(lst) <= 1:
        return lst
    mid = len(lst) // 2
    left = merge_sort(lst[:mid])   # O(n) space for copies
    right = merge_sort(lst[mid:])  # O(n) space for copies
    return merge(left, right)

def merge(left, right):
    result = []  # O(n) space
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

# Example 7: Caching for time optimization (space trade-off)
# Without cache: O(2ⁿ) time, O(n) space (recursion)
def fib_slow(n):
    if n <= 1:
        return n
    return fib_slow(n - 1) + fib_slow(n - 2)

# With cache: O(n) time, O(n) space
def fib_cached(n, cache=None):
    if cache is None:
        cache = {}
    if n in cache:
        return cache[n]
    if n <= 1:
        return n
    result = fib_cached(n - 1, cache) + fib_cached(n - 2, cache)
    cache[n] = result
    return result

# Example 8: Hash table for O(1) lookups (space for speed)
# Without hash: O(n) to find element
def has_element_linear(lst, target):
    for x in lst:
        if x == target:
            return True
    return False

# With hash table: O(1) to find element
def has_element_hash(lst, target):
    hash_set = set(lst)  # O(n) space
    return target in hash_set  # O(1) lookup

# Example 9: Finding two numbers that sum to target
# Bad: O(n²) time, O(1) space
def two_sum_slow(lst, target):
    for i in range(len(lst)):
        for j in range(i + 1, len(lst)):
            if lst[i] + lst[j] == target:
                return (lst[i], lst[j])
    return None

# Good: O(n) time, O(n) space
def two_sum_fast(lst, target):
    seen = set()
    for x in lst:
        needed = target - x
        if needed in seen:
            return (x, needed)
        seen.add(x)
    return None

# Example 10: String reversal - space implications
# O(n) space - creates new string
def reverse_string_new(s):
    return s[::-1]

# O(n) space (lists are mutable) - convert and reverse
def reverse_string_inplace(s):
    """In-place for mutable list of characters"""
    lst = list(s)
    left, right = 0, len(lst) - 1
    while left < right:
        lst[left], lst[right] = lst[right], lst[left]
        left += 1
        right -= 1
    return ''.join(lst)

# Example 11: Analyzing space of recursive algorithms
def sum_list_recursive(lst):
    """O(n) space due to call stack depth"""
    if not lst:
        return 0
    return lst[0] + sum_list_recursive(lst[1:])  # Also O(n) for slicing!

def sum_list_better(lst, index=0):
    """Still O(n) call stack, but O(1) extra beyond recursion"""
    if index == len(lst):
        return 0
    return lst[index] + sum_list_better(lst, index + 1)

# Example 12: Dynamic programming (space for memoization)
def fib_dp(n):
    """O(n) space for memoization array"""
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]
```

---

## Guided Practice

**Step 1:** Compare space complexity of recursive vs. iterative.
```python
# Recursive: O(n) space
def factorial_rec(n):
    if n <= 1:
        return 1
    return n * factorial_rec(n - 1)

# Iterative: O(1) space
def factorial_iter(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result
```

**Step 2:** Use a hash table to optimize from O(n²) to O(n).
```python
def find_duplicate_optimized(lst):
    seen = set()
    for x in lst:
        if x in seen:
            return x
        seen.add(x)
    return None
```

**Step 3:** Compare merge sort (O(n) space) to bubble sort (O(1) space).

---

## Practice Problems

**Beginner:** Write a function with O(1) space complexity and one with O(n) space, doing the same task.

**Intermediate:** Optimize an O(n²) algorithm using a hash table or set.

**Challenge:** Implement an algorithm that minimizes space while maintaining reasonable time complexity.

<details>
<summary>💡 Hints</summary>
- For Beginner: Think about whether you need extra storage
- For Intermediate: Use dictionaries or sets for O(1) lookups
- For Challenge: Consider in-place operations and careful iteration
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
# O(1) space
def check_even(n):
    return n % 2 == 0

# O(n) space
def create_list_evens(n):
    return [x for x in range(n) if x % 2 == 0]

# Intermediate
def find_pairs_sum(lst, target):
    seen = set()
    pairs = []
    for x in lst:
        if target - x in seen:
            pairs.append((x, target - x))
        seen.add(x)
    return pairs

# Challenge: Reverse array in-place with O(1) extra space
def reverse_array(lst):
    left, right = 0, len(lst) - 1
    while left < right:
        lst[left], lst[right] = lst[right], lst[left]
        left += 1
        right -= 1
    return lst
```
</details>
