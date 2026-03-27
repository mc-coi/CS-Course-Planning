# Day 13: Decorators in Practice and Timing Decorators

**Learning Target:** I can write practical decorators like timing functions, logging, and error handling.

---

## Key Concepts

**Decorator Patterns:**
- **Timing** — Measure how long a function takes to execute
- **Logging** — Track function calls and parameters
- **Retry** — Automatically retry failed function calls
- **Validation** — Check arguments before executing
- **Caching/Memoization** — Store results to avoid recalculation

**Preserving Metadata** — Using `functools.wraps` to preserve the original function's name and docstring.

**Error Handling** — Decorators can catch exceptions and handle them gracefully.

**Performance** — Decorators add a small overhead; use them wisely.

---

## Code Examples

```python
import time
from functools import wraps

# Example 1: Timer decorator
def timer(func):
    @wraps(func)  # Preserve func's name and docstring
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        elapsed = time.time() - start
        print(f"{func.__name__} took {elapsed:.4f} seconds")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(0.5)
    return "Complete"

slow_function()  # Output: slow_function took 0.5001 seconds

# Example 2: Logging decorator
def log_calls(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with args={args}, kwargs={kwargs}")
        result = func(*args, **kwargs)
        print(f"{func.__name__} returned {result}")
        return result
    return wrapper

@log_calls
def add(a, b):
    return a + b

add(5, 3)
# Output:
# Calling add with args=(5, 3), kwargs={}
# add returned 8

# Example 3: Retry decorator
def retry(times=3):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(1, times + 1):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == times:
                        raise
                    print(f"Attempt {attempt} failed: {e}. Retrying...")
        return wrapper
    return decorator

@retry(times=3)
def unreliable_function(x):
    import random
    if random.random() < 0.7:
        raise Exception("Random failure")
    return f"Success with {x}"

# Will retry up to 3 times

# Example 4: Validation decorator
def validate_positive(func):
    @wraps(func)
    def wrapper(x):
        if x < 0:
            raise ValueError(f"{func.__name__} requires positive input, got {x}")
        return func(x)
    return wrapper

@validate_positive
def square_root(x):
    return x ** 0.5

print(square_root(9))   # Output: 3.0
# square_root(-4)      # Raises ValueError

# Example 5: Caching decorator (memoization)
def memoize(func):
    cache = {}
    @wraps(func)
    def wrapper(n):
        if n not in cache:
            cache[n] = func(n)
        return cache[n]
    return wrapper

@memoize
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(10))  # Fast due to caching

# Example 6: Type checking decorator
def require_int(func):
    @wraps(func)
    def wrapper(x):
        if not isinstance(x, int):
            raise TypeError(f"{func.__name__} requires an integer")
        return func(x)
    return wrapper

@require_int
def double(x):
    return x * 2

print(double(5))     # Output: 10
# double(5.5)        # Raises TypeError

# Example 7: Timing with high precision
def precise_timer(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()  # More precise than time.time()
        result = func(*args, **kwargs)
        elapsed = time.perf_counter() - start
        print(f"{func.__name__}: {elapsed * 1000:.2f}ms")
        return result
    return wrapper

@precise_timer
def quick_function():
    total = 0
    for i in range(1000000):
        total += i
    return total

quick_function()

# Example 8: Decorator with configuration
def repeat(times):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            results = []
            for _ in range(times):
                results.append(func(*args, **kwargs))
            return results
        return wrapper
    return decorator

@repeat(times=3)
def say_hello(name):
    return f"Hello, {name}!"

print(say_hello("Alice"))  # Output: ['Hello, Alice!', 'Hello, Alice!', 'Hello, Alice!']

# Example 9: Combining multiple decorators
@precise_timer
@log_calls
def complex_operation(x):
    """Performs a complex operation"""
    time.sleep(0.1)
    return x * 2

complex_operation(5)
# Output shows both logging and timing

# Example 10: Debugging decorator
def debug(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f"DEBUG: Calling {func.__name__}")
        print(f"  Args: {args}")
        print(f"  Kwargs: {kwargs}")
        result = func(*args, **kwargs)
        print(f"  Returned: {result}")
        return result
    return wrapper

@debug
def greet(name, greeting="Hi"):
    return f"{greeting}, {name}!"

greet("Alice", greeting="Hello")
# Output shows all debug information
```

---

## Guided Practice

**Step 1:** Write a timer decorator and test it on a function.
```python
import time
from functools import wraps

def timer(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        elapsed = time.time() - start
        print(f"{func.__name__} took {elapsed:.4f} seconds")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(0.2)
    return "Done"

slow_function()  # Should show timing
```

**Step 2:** Write a logging decorator that prints function calls.
```python
from functools import wraps

def log_calls(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        print(f"{func.__name__} completed")
        return result
    return wrapper

@log_calls
def multiply(a, b):
    return a * b

print(multiply(3, 4))  # Should show logs and return 12
```

**Step 3:** Write a validation decorator.
```python
from functools import wraps

def validate_string(func):
    @wraps(func)
    def wrapper(text):
        if not isinstance(text, str):
            raise TypeError(f"Expected string, got {type(text)}")
        return func(text)
    return wrapper

@validate_string
def uppercase(text):
    return text.upper()

print(uppercase("hello"))  # Should print: HELLO
```

---

## Practice Problems

**Beginner:** Write a decorator that adds a prefix to a function's return value.

**Intermediate:** Write a decorator that prevents a function from being called more than a certain number of times.

**Challenge:** Write a decorator that caches results based on all arguments (not just one). (Hint: Use tuple of arguments as key)

<details>
<summary>💡 Hints</summary>
- For Beginner: Get the result, concatenate prefix + result
- For Intermediate: Track call count with nonlocal
- For Challenge: Convert args and kwargs to a hashable key (use str or repr)
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
from functools import wraps

def add_prefix(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return f"Result: {result}"
    return wrapper

@add_prefix
def get_value():
    return 42

print(get_value())  # Output: Result: 42

# Intermediate
from functools import wraps

def max_calls(limit):
    def decorator(func):
        calls = 0
        @wraps(func)
        def wrapper(*args, **kwargs):
            nonlocal calls
            if calls >= limit:
                raise Exception(f"Function called more than {limit} times")
            calls += 1
            return func(*args, **kwargs)
        return wrapper
    return decorator

@max_calls(3)
def limited_function():
    return "OK"

# Challenge
from functools import wraps

def cache_all(func):
    cache = {}
    @wraps(func)
    def wrapper(*args, **kwargs):
        key = (args, tuple(sorted(kwargs.items())))
        if key not in cache:
            cache[key] = func(*args, **kwargs)
        return cache[key]
    return wrapper

@cache_all
def add(a, b):
    print(f"Computing {a} + {b}")
    return a + b

print(add(2, 3))  # Computing 2 + 3
print(add(2, 3))  # Uses cache
```
</details>
