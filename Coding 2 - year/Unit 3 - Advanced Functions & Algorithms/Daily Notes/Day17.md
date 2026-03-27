# Day 17: Fibonacci and Recursive Optimization

**Learning Target:** I can write Fibonacci using recursion and understand why optimization is necessary (memoization and tail recursion).

---

## Key Concepts

**Fibonacci Sequence** — Each number is the sum of the two before it: 0, 1, 1, 2, 3, 5, 8, 13, ...

**Inefficiency in Naive Recursion** — The simple recursive Fibonacci recalculates the same values many times (exponential time complexity).

**Memoization** — Caching results to avoid redundant calculations (reduces from exponential to linear).

**Tail Recursion** — A recursion where the last action is a recursive call. Some languages optimize this, but Python doesn't.

**Trade-offs:**
- Simple recursion: elegant but slow
- Memoized recursion: fast but uses memory
- Iterative: fast and memory-efficient (best for Fibonacci)

---

## Code Examples

```python
# Example 1: Simple recursive Fibonacci (slow!)
def fib_simple(n):
    if n <= 1:
        return n
    return fib_simple(n - 1) + fib_simple(n - 2)

# fib_simple(40) would take many seconds (don't try!)
print(fib_simple(10))  # Output: 55

# Example 2: Show redundant calls
def fib_trace(n, depth=0):
    print("  " * depth + f"fib({n})")
    if n <= 1:
        return n
    return fib_trace(n - 1, depth + 1) + fib_trace(n - 2, depth + 1)

fib_trace(5)  # Shows fib(2) is called 3 times, fib(1) is called 5 times!

# Example 3: Memoized Fibonacci (fast!)
def fib_memo(n, memo=None):
    if memo is None:
        memo = {}
    
    if n in memo:
        return memo[n]
    
    if n <= 1:
        return n
    
    memo[n] = fib_memo(n - 1, memo) + fib_memo(n - 2, memo)
    return memo[n]

print(fib_memo(40))  # Output: 102334155 (instant!)

# Example 4: Memoization as a decorator
def memoize(func):
    cache = {}
    def wrapper(n):
        if n not in cache:
            cache[n] = func(n)
        return cache[n]
    return wrapper

@memoize
def fib_decorated(n):
    if n <= 1:
        return n
    return fib_decorated(n - 1) + fib_decorated(n - 2)

print(fib_decorated(40))  # Very fast!

# Example 5: Iterative Fibonacci (most efficient)
def fib_iterative(n):
    if n <= 1:
        return n
    
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b

print(fib_iterative(40))  # Fast and O(1) space!

# Example 6: Generator for Fibonacci sequence
def fib_generator(limit):
    a, b = 0, 1
    while a < limit:
        yield a
        a, b = b, a + b

for fib in fib_generator(100):
    print(fib, end=" ")  # Output: 0 1 1 2 3 5 8 13 21 34 55 89

# Example 7: Comparison of approaches
import time

def time_it(func, n):
    start = time.time()
    result = func(n)
    elapsed = time.time() - start
    return result, elapsed

n = 35
result, time_simple = time_it(fib_simple, n)  # ~1 second
result, time_memo = time_it(fib_memo, n)      # ~0.0001 seconds
result, time_iter = time_it(fib_iterative, n) # ~0.00001 seconds

# Example 8: Tail-recursive Fibonacci (doesn't help in Python)
def fib_tail(n, a=0, b=1):
    if n == 0:
        return a
    return fib_tail(n - 1, b, a + b)

print(fib_tail(10))  # Output: 55

# Example 9: Counting Fibonacci calls (to understand inefficiency)
call_count = 0

def fib_count(n):
    global call_count
    call_count += 1
    if n <= 1:
        return n
    return fib_count(n - 1) + fib_count(n - 2)

call_count = 0
fib_count(10)
print(f"fib(10) called the function {call_count} times")  # 177 times!

call_count = 0
fib_count(20)
print(f"fib(20) called the function {call_count} times")  # 21891 times!

# Example 10: Using functools.lru_cache (built-in memoization)
from functools import lru_cache

@lru_cache(maxsize=None)
def fib_cache(n):
    if n <= 1:
        return n
    return fib_cache(n - 1) + fib_cache(n - 2)

print(fib_cache(40))  # Fast!
```

---

## Guided Practice

**Step 1:** Write a simple recursive Fibonacci function.
```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(6))  # Should print: 8
```

**Step 2:** Add memoization to make it fast.
```python
def fibonacci_memo(n, memo=None):
    if memo is None:
        memo = {}
    
    if n in memo:
        return memo[n]
    
    if n <= 1:
        return n
    
    memo[n] = fibonacci_memo(n - 1, memo) + fibonacci_memo(n - 2, memo)
    return memo[n]

print(fibonacci_memo(35))  # Should be instant
```

**Step 3:** Write an iterative version for comparison.
```python
def fibonacci_iterative(n):
    if n <= 1:
        return n
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b

print(fibonacci_iterative(35))  # Should print same result
```

---

## Practice Problems

**Beginner:** Write a recursive function to find the nth number in a simple sequence (like every other Fibonacci number).

**Intermediate:** Implement both simple and memoized versions of a recursive function and compare performance.

**Challenge:** Write a function that generates the Fibonacci sequence up to n terms (not up to a value, but n iterations).

<details>
<summary>💡 Hints</summary>
- For Beginner: Consider modifying the Fibonacci function
- For Intermediate: Use time.time() to measure
- For Challenge: Use a helper function or generator
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def fib_every_other(n):
    if n == 0:
        return 0
    if n == 1:
        return 1
    # Get fibonacci at position 2*n-1
    def fib(x):
        if x <= 1:
            return x
        return fib(x-1) + fib(x-2)
    return fib(2 * n - 1)

# Intermediate: see code above with time comparison

# Challenge
def fib_sequence(n):
    def fib(x):
        if x <= 1:
            return x
        return fib(x-1) + fib(x-2)
    return [fib(i) for i in range(n)]

print(fib_sequence(10))  # [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```
</details>
