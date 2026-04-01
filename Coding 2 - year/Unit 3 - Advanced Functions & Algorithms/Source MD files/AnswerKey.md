# Unit 3: Advanced Functions & Algorithms — Complete Answer Key

---

## Beginner Problems

---

## Problem 1: Lambda Function for Absolute Difference

### Solution
```python
# Lambda function to find absolute difference
diff = lambda x, y: abs(x - y)

# Test cases
print(diff(5, 8))    # 3
print(diff(8, 5))    # 3
print(diff(-5, 3))   # 8
```

### Expected Output
```
3
3
8
```

### Common Mistakes
- Using `|x - y|` instead of `abs(x - y)` (vertical bars not valid in Python)
- Forgetting the `lambda` keyword: `def diff = ...`
- Using wrong syntax: `lambda x, y abs(x - y)` (missing colon)

---

## Problem 2: Map Celsius to Fahrenheit

### Solution
```python
celsius = [0, 10, 20, 30]

# Using map with lambda
fahrenheit = list(map(lambda c: (c * 9/5) + 32, celsius))

print(fahrenheit)  # [32.0, 50.0, 68.0, 86.0]
```

### Expected Output
```
[32.0, 50.0, 68.0, 86.0]
```

### Common Mistakes
- Formula wrong: `(c * 5/9) + 32` instead of `(c * 9/5) + 32` (converts wrong direction)
- Forgetting `list()` wrapper around map() (map returns iterator in Python 3)
- Using `map(celsius, lambda ...)` instead of `map(lambda ..., celsius)` (wrong order)

---

## Problem 3: Filter Strings Longer Than 4 Characters

### Solution
```python
words = ["cat", "elephant", "dog", "python"]

# Using filter with lambda
long_words = list(filter(lambda w: len(w) > 4, words))

print(long_words)  # ['elephant', 'python']
```

### Expected Output
```
['elephant', 'python']
```

### Common Mistakes
- Using `len(w) >= 4` instead of `> 4` (4-char words would be included)
- Forgetting `list()` wrapper around filter()
- Using `>= 5` instead of `> 4` (same logic but less clear)

---

## Problem 4: List Comprehension Squares

### Solution
```python
squares = [x**2 for x in range(1, 11)]

print(squares)  # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

### Expected Output
```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

### Common Mistakes
- Using `range(10)` instead of `range(1, 11)` (starts at 0, gives 0-81)
- Using `range(1, 10)` instead of `range(1, 11)` (missing 100)
- Using `x * 2` instead of `x**2` (multiplication instead of exponentiation)

---

## Problem 5: Zip Names with Ages

### Solution
```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 28]

# Using zip to pair them
people = dict(zip(names, ages))

print(people)  # {'Alice': 25, 'Bob': 30, 'Charlie': 28}
```

### Expected Output
```
{'Alice': 25, 'Bob': 30, 'Charlie': 28}
```

### Common Mistakes
- Forgetting `dict()` wrapper—`zip()` returns pairs but not a dictionary
- Swapping order: `dict(zip(ages, names))` (would have ages as keys)
- Not realizing zip stops at shortest list if lists differ in length

---

## Problem 6: Recursive Factorial

### Solution
```python
def factorial(n):
    """Calculate factorial recursively."""
    if n <= 1:
        return 1
    return n * factorial(n - 1)

# Test
print(factorial(5))   # 120
print(factorial(1))   # 1
print(factorial(0))   # 1
```

### Expected Output
```
120
1
1
```

### Common Mistakes
- No base case: `if n == 1: return 1` doesn't handle 0 (should use `<= 1`)
- Wrong base case: `if n == 0: return 0` (0! = 1, not 0)
- Missing recursive call: just returning n
- Infinite recursion: `factorial(n)` instead of `factorial(n - 1)`

---

## Problem 7: Set Comprehension for Unique First Letters

### Solution
```python
words = ["apple", "apricot", "banana", "blueberry"]

# Set comprehension to get unique first letters
first_letters = {word[0] for word in words}

print(first_letters)  # {'a', 'b'}
```

### Expected Output
```
{'a', 'b'}
```

### Common Mistakes
- Using list comprehension `[word[0] for ...]` instead of set comprehension `{...}`
- Using wrong index: `word[1]` instead of `word[0]` (second letter)
- Not realizing sets are unordered (order may differ but contents same)

---

## Problem 8: Generator for Numbers 1 to n

### Solution
```python
def count_to(n):
    """Generator that yields numbers from 1 to n."""
    i = 1
    while i <= n:
        yield i
        i += 1

# Test
print(list(count_to(5)))  # [1, 2, 3, 4, 5]
```

### Expected Output
```
[1, 2, 3, 4, 5]
```

### Common Mistakes
- Using `return` instead of `yield` (returns single value instead of generator)
- Starting at 0 instead of 1: `i = 0` and `i <= n` (gives 0-n)
- Not incrementing i: infinite loop
- Using `range()` directly (defeats the purpose of teaching generators)

---

## Intermediate Problems

---

## Problem 9: Map and Filter Together

### Solution
```python
numbers = range(1, 11)

# Get squares of only even numbers
result = list(map(lambda x: x**2, filter(lambda x: x % 2 == 0, numbers)))

print(result)  # [4, 16, 36, 64, 100]
```

### Expected Output
```
[4, 16, 36, 64, 100]
```

### Common Mistakes
- Wrong order: map then filter (should filter first for efficiency)
- Filter condition wrong: `x % 2 == 1` (odd) instead of `== 0` (even)
- Forgetting to square: `x` instead of `x**2`
- List comprehension cleaner: `[x**2 for x in range(1, 11) if x % 2 == 0]`

---

## Problem 10: Dictionary Comprehension

### Solution
```python
words = ["python", "code", "algorithm"]

# Map words to their lengths
lengths = {word: len(word) for word in words}

print(lengths)  # {'python': 6, 'code': 4, 'algorithm': 9}
```

### Expected Output
```
{'python': 6, 'code': 4, 'algorithm': 9}
```

### Common Mistakes
- Using list comprehension syntax `[word: len(word) for ...]` (wrong brackets)
- Not using colon: `{word len(word) for ...}` (missing separator)
- Using wrong order: `{len(word): word for ...}` (lengths as keys)

---

## Problem 11: Flatten Nested List Recursively

### Solution
```python
def flatten(lst):
    """Flatten nested list using recursion."""
    result = []
    for item in lst:
        if isinstance(item, list):
            result.extend(flatten(item))  # Recursive call
        else:
            result.append(item)
    return result

# Test
print(flatten([[1, 2], [3, [4, 5]]]))  # [1, 2, 3, 4, 5]
```

### Expected Output
```
[1, 2, 3, 4, 5]
```

### Common Mistakes
- Using `append()` instead of `extend()` for recursive results (creates nested list)
- Not checking `isinstance(item, list)` (treats lists as single items)
- Not returning result
- Using `flatten(item)` without assigning back to result

---

## Problem 12: Palindrome Checker (Recursive)

### Solution
```python
def is_palindrome(s):
    """Check if string is palindrome (case-insensitive, no spaces)."""
    s = s.lower().replace(" ", "")

    if len(s) <= 1:
        return True

    return s[0] == s[-1] and is_palindrome(s[1:-1])

# Test
print(is_palindrome("racecar"))        # True
print(is_palindrome("hello"))          # False
print(is_palindrome("A man, a plan, a canal, Panama"))  # True with cleanup
```

### Expected Output
```
True
False
True
```

### Common Mistakes
- Not normalizing case and spaces (punctuation matters)
- Base case wrong: `if len(s) == 0: return True` vs `<= 1` (both work, <= 1 cleaner)
- Not comparing first and last: `return is_palindrome(s[1:-1])`
- Using `return s[0] == s[-1]` without recursive call (only checks first/last)

---

## Problem 13: Enumerate with Indices

### Solution
```python
# Using enumerate to iterate with indices
for index, item in enumerate(["a", "b", "c"]):
    print(f"{index}: {item}")
```

### Expected Output
```
0: a
1: b
2: c
```

### Common Mistakes
- Using `range(len(list))` instead of `enumerate()` (more verbose)
- Unpacking wrong order: `item, index` instead of `index, item`
- Not realizing enumerate starts at 0 by default

---

## Problem 14: Fibonacci Generator

### Solution
```python
def fibonacci(limit):
    """Generator that yields Fibonacci numbers up to limit."""
    a, b = 0, 1
    while a < limit:
        yield a
        a, b = b, a + b

# Test
print(list(fibonacci(20)))  # [0, 1, 1, 2, 3, 5, 8, 13]
```

### Expected Output
```
[0, 1, 1, 2, 3, 5, 8, 13]
```

### Common Mistakes
- Using `return` instead of `yield`
- Starting with `a, b = 1, 1` (skips 0)
- Wrong update: `a = b; b = a + b` (loses value of a)
- Using `while a <= limit` (includes limit)

---

## Problem 15: Flatten 2D List with Nested Comprehension

### Solution
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Nested list comprehension to flatten
flattened = [x for row in matrix for x in row]

print(flattened)  # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Expected Output
```
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Common Mistakes
- Wrong order: `for x in row for row in matrix` (row not yet defined)
- Using `append()` instead of comprehension: `[...].append(x)` (invalid)
- Using `list.extend()` syntax instead of comprehension

---

## Problem 16: Multiply Corresponding Elements

### Solution
```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]

# Use zip with map to multiply corresponding elements
products = list(map(lambda x, y: x * y, list1, list2))

print(products)  # [4, 10, 18]
```

### Expected Output
```
[4, 10, 18]
```

### Common Mistakes
- Wrong lambda signature: `lambda x: x * x` (missing y parameter)
- Using addition instead of multiplication: `x + y`
- Forgetting `list()` wrapper

---

## Challenge Problems

---

## Problem 17: Maximum in Nested List

### Solution
```python
def max_in_nested(lst):
    """Find maximum value in nested list recursively."""
    max_val = float('-inf')
    for item in lst:
        if isinstance(item, list):
            max_val = max(max_val, max_in_nested(item))
        else:
            max_val = max(max_val, item)
    return max_val

# Test
print(max_in_nested([1, [2, [3, 4]]]))  # 4
print(max_in_nested([[1, 2], [3, [4, 5]]]))  # 5
```

### Expected Output
```
4
5
```

### Common Mistakes
- Not initializing `max_val` to `-inf` (could miss negative numbers or 0)
- Not checking `isinstance(item, list)` recursively
- Not using recursion properly
- Using `max(list)` directly (doesn't work on nested lists)

---

## Problem 18: Timer Decorator

### Solution
```python
import time

def timer(func):
    """Decorator that measures execution time."""
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"Execution time: {end - start:.4f}s")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(1)
    return "Done"

# Test
slow_function()  # Execution time: 1.0002s, then returns "Done"
```

### Expected Output
```
Execution time: 1.0002s
```

### Common Mistakes
- Not using `*args, **kwargs` (can't handle all argument types)
- Not returning result from wrapper
- Not returning wrapper function from decorator
- Forgetting to print/return anything

---

## Problem 19: Fibonacci Iterator Class

### Solution
```python
class FibonacciIterator:
    """Iterator class for Fibonacci sequence."""

    def __init__(self, limit):
        self.limit = limit
        self.a, self.b = 0, 1

    def __iter__(self):
        """Return iterator object."""
        return self

    def __next__(self):
        """Return next Fibonacci number."""
        if self.a > self.limit:
            raise StopIteration
        result = self.a
        self.a, self.b = self.b, self.a + self.b
        return result

# Test
for num in FibonacciIterator(20):
    print(num, end=' ')  # 0 1 1 2 3 5 8 13
```

### Expected Output
```
0 1 1 2 3 5 8 13
```

### Common Mistakes
- Not implementing `__iter__()` method
- Not raising `StopIteration` when done
- Wrong update formula: `self.a = self.b; self.b = self.a + self.b` (loses old a)
- Using `self.a >= limit` instead of `>` (includes limit)

---

## Problem 20: Big O Analysis and Optimization

### Solution
```python
# INEFFICIENT: O(n²)
def has_duplicates_slow(lst):
    """Brute force: check every pair."""
    for i in range(len(lst)):
        for j in range(i + 1, len(lst)):
            if lst[i] == lst[j]:
                return True
    return False

# EFFICIENT: O(n)
def has_duplicates_fast(lst):
    """Using set for O(1) lookup."""
    seen = set()
    for item in lst:
        if item in seen:
            return True
        seen.add(item)
    return False

# Test
test_list = [1, 2, 3, 4, 5, 3]
print(has_duplicates_slow(test_list))  # True
print(has_duplicates_fast(test_list))  # True

# Complexity comparison:
# slow: n² = 10000 comparisons for 100 elements
# fast: n = 100 comparisons for 100 elements
```

### Expected Output
```
True
True
```

### Common Mistakes
- Not understanding Big O complexity
- Not recognizing when to use sets for O(1) lookup
- Creating unnecessary nested loops
- Not recognizing that set membership test is O(1) vs list O(n)

---
