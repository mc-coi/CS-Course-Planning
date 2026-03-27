# Day 8: Functional Programming Patterns (Decorators, Closures)
**Learning Target:** I can use decorators and closures for advanced function techniques.

### Key Concepts
**Closures:** Nested functions that capture variables from outer scope.
**Decorators:** Functions that modify other functions' behavior.

### Code Examples
```python
# Closure example
def outer(x):
    def inner(y):
        return x + y
    return inner

add_5 = outer(5)
print(add_5(3))  # 8

# Decorator example
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        print(f"Done!")
        return result
    return wrapper

@my_decorator
def greet(name):
    return f"Hello, {name}!"

greet("Zach")

# Decorator for timing
import time
def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        print(f"Took {time.time() - start:.4f} seconds")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(1)
    return "Done"

slow_function()
```

### Guided Practice
Create a decorator for logging, validation, or caching.

### Practice Problems
**Problem 1 — Beginner:** Write a simple decorator that prints "Starting" and "Finished".

**Problem 2 — Intermediate:** Write a decorator that counts how many times a function is called.

**Problem 3 — Challenge:** Write a memoization decorator that caches function results.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
def simple_decorator(func):
    def wrapper(*args, **kwargs):
        print("Starting")
        result = func(*args, **kwargs)
        print("Finished")
        return result
    return wrapper

# Problem 2
def call_counter(func):
    func.call_count = 0
    def wrapper(*args, **kwargs):
        func.call_count += 1
        return func(*args, **kwargs)
    return wrapper

# Problem 3
def memoize(func):
    cache = {}
    def wrapper(*args):
        if args in cache:
            return cache[args]
        result = func(*args)
        cache[args] = result
        return result
    return wrapper
```
</details>

---

---
