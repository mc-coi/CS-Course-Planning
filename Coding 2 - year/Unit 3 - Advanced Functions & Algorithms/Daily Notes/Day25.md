# Day 25: Review and Practice - Comprehensive Concepts

**Learning Target:** I can apply and synthesize all Unit 3 concepts to solve complex problems.

---

## Concept Review Map

### Functional Programming (Days 1-6)
- Lambda functions: `lambda x: x ** 2`
- map(), filter(), zip(), reduce()
- List comprehensions: `[x for x in range(10) if x % 2 == 0]`

### Advanced Functions (Days 7-10)
- Dictionary/set comprehensions
- Closures and scope (LEGB rule)
- Nested comprehensions

### Decorators & Generators (Days 11-15)
- Function decorators: `@decorator`, `@property`, `@staticmethod`
- Generators with `yield`
- Generator expressions: `(x ** 2 for x in range(10))`

### Recursion (Days 16-19)
- Base case + recursive case
- Fibonacci, factorials, tree traversal
- Memoization for optimization

### Algorithm Analysis (Days 20-22)
- Big O notation: O(1), O(n), O(n²), O(2ⁿ)
- Space complexity
- Pseudocode and design patterns

---

## Practice Problems (Mixed Concepts)

### Level 1: Basic Review

**Problem 1.1:** Write a lambda that filters a list of numbers to keep only multiples of 3.
```python
numbers = [1, 3, 5, 6, 9, 12, 15, 18]
multiples_of_3 = list(filter(lambda x: x % 3 == 0, numbers))
# Expected: [3, 6, 9, 12, 15, 18]
```

**Problem 1.2:** Use a comprehension to create a dictionary mapping words to their lengths.
```python
words = ["python", "code", "learn"]
word_lengths = {word: len(word) for word in words}
# Expected: {'python': 6, 'code': 4, 'learn': 5}
```

**Problem 1.3:** Write a closure that returns a function to multiply by a given number.
```python
def make_multiplier(n):
    return lambda x: x * n

times_3 = make_multiplier(3)
print(times_3(5))  # Expected: 15
```

---

### Level 2: Intermediate Synthesis

**Problem 2.1:** Combine multiple concepts - filter high-scoring students, extract names, sort alphabetically.
```python
students = [
    {"name": "Alice", "score": 95},
    {"name": "Bob", "score": 78},
    {"name": "Charlie", "score": 88},
    {"name": "Diana", "score": 92},
]

# Filter score >= 90, get names, sort
top_students = sorted(
    list(map(lambda s: s["name"], filter(lambda s: s["score"] >= 90, students)))
)
print(top_students)  # Expected: ['Alice', 'Diana']
```

**Problem 2.2:** Write a generator that yields Fibonacci numbers up to a limit.
```python
def fibonacci(limit):
    a, b = 0, 1
    while a < limit:
        yield a
        a, b = b, a + b

print(list(fibonacci(100)))
# Expected: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
```

**Problem 2.3:** Analyze the time complexity of this function:
```python
def analyze_me(lst):
    for i in range(len(lst)):
        for j in range(len(lst)):
            if lst[i] == lst[j] and i != j:
                return True
    return False
```
**Answer:** O(n²) - nested loops

---

### Level 3: Challenge Synthesis

**Problem 3.1:** Implement a recursive function with memoization that calculates the nth Catalan number efficiently.

```python
def catalan(n, memo=None):
    """Catalan number: useful in combinatorics"""
    if memo is None:
        memo = {}
    
    if n in memo:
        return memo[n]
    
    if n <= 1:
        return 1
    
    result = sum(catalan(i, memo) * catalan(n - 1 - i, memo) for i in range(n))
    memo[n] = result
    return result

print(catalan(5))  # Expected: 42
```

**Problem 3.2:** Write a function that uses a decorator to count execution time and a generator to process data.

```python
import time
from functools import wraps

def timer(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        elapsed = time.time() - start
        print(f"{func.__name__} took {elapsed:.4f}s")
        return result
    return wrapper

@timer
def process_large_dataset():
    # Use generator for memory efficiency
    data = (x ** 2 for x in range(1000000))
    return sum(data)

process_large_dataset()
```

**Problem 3.3:** Tree problem combining recursion and analysis.

```python
class TreeNode:
    def __init__(self, value, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right

def serialize_tree(node):
    """Convert tree to list (preorder + None markers)"""
    if node is None:
        return None
    result = [node.value]
    result.extend(serialize_tree(node.left) or [])
    result.extend(serialize_tree(node.right) or [])
    return result

# Build and test
root = TreeNode(1, TreeNode(2, TreeNode(4)), TreeNode(3))
print(serialize_tree(root))  # Expected: [1, 2, 4, None, None, 3, None, None]
```

---

## Study Strategy

1. **Review key patterns:** Keep a reference of common lambdas, comprehensions, and recursion patterns
2. **Practice variations:** Solve the same problem using different techniques (loops vs. comprehensions vs. reduce)
3. **Analyze complexity:** For every algorithm, ask: What's the Big O? Can I optimize?
4. **Connect concepts:** How do decorators relate to higher-order functions? How do closures enable memoization?

---

## Topics to Review Before Assessment

- [ ] Lambda syntax and when to use it
- [ ] map(), filter(), zip(), reduce() differences
- [ ] List/dict/set comprehensions
- [ ] Closure creation and nonlocal/global
- [ ] Decorators (@, @property, @staticmethod, @classmethod)
- [ ] Generator yield and generator expressions
- [ ] Recursion (base case, recursive case, call stack)
- [ ] Binary search and divide-and-conquer
- [ ] Big O notation and complexity analysis
- [ ] Tree traversal (preorder, inorder, postorder)

---

## Quick Reference

**Lambda Syntax:**
```python
lambda x: x ** 2
lambda x, y: x + y
lambda x: x ** 2 if x > 0 else 0
```

**Comprehensions:**
```python
[x ** 2 for x in range(10)]
{x: x ** 2 for x in range(10)}
{x for x in range(10) if x % 2 == 0}
```

**Recursion Template:**
```python
def recursive(n):
    if n == 0:  # Base case
        return something
    return combine(n, recursive(n - 1))  # Recursive case
```

**Complexity Recall:**
- Linear search: O(n)
- Binary search: O(log n)
- Bubble sort: O(n²)
- Merge sort: O(n log n)

