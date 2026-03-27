# Day 11: Introduction to Decorators

**Learning Target:** I can write and use simple decorators to modify or extend function behavior without changing the original function.

---

## Key Concepts

**Decorator** — A function that takes another function as input and returns a modified version of that function. Built on closures!

**@decorator syntax** — Syntactic sugar for `function = decorator(function)`. The `@` symbol goes directly above the function definition.

**Wrapping** — A decorator creates a wrapper function that:
1. Accepts the same arguments as the original function
2. Calls the original function (or doesn't)
3. Can add code before, after, or around the original call
4. Returns a result

**Key Point:** Decorators are functions that modify other functions. They're one of Python's most powerful patterns!

---

## Code Examples

```python
# Example 1: Simple decorator that adds a greeting
def simple_decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

@simple_decorator
def say_hello():
    print("Hello!")

say_hello()
# Output:
# Before function call
# Hello!
# After function call

# Example 2: Decorator with arguments
def my_decorator(func):
    def wrapper(*args, **kwargs):  # Accept any arguments
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)  # Call original function
        print(f"{func.__name__} returned {result}")
        return result
    return wrapper

@my_decorator
def add(a, b):
    return a + b

print(add(5, 3))
# Output:
# Calling add
# add returned 8
# 8

# Example 3: Decorator for timing function execution
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.4f} seconds")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(0.5)
    return "Done!"

slow_function()
# Output: slow_function took 0.5001 seconds

# Example 4: Decorator that validates arguments
def validate_positive(func):
    def wrapper(x):
        if x < 0:
            print(f"Error: {x} is not positive")
            return None
        return func(x)
    return wrapper

@validate_positive
def square_root(x):
    return x ** 0.5

print(square_root(9))   # Output: 3.0
print(square_root(-4))  # Output: Error: -4 is not positive

# Example 5: Decorator that counts function calls
def count_calls(func):
    count = 0
    def wrapper(*args, **kwargs):
        nonlocal count
        count += 1
        print(f"{func.__name__} has been called {count} time(s)")
        return func(*args, **kwargs)
    return wrapper

@count_calls
def greet(name):
    return f"Hello, {name}!"

greet("Alice")   # greet has been called 1 time(s)
greet("Bob")     # greet has been called 2 time(s)
greet("Charlie") # greet has been called 3 time(s)

# Example 6: Multiple decorators (applied bottom-up)
def add_exclamation(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result + "!"
    return wrapper

def add_question(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result + "?"
    return wrapper

@add_exclamation
@add_question
def say_hi(name):
    return f"Hi {name}"

print(say_hi("Alice"))  # Output: Hi Alice?!

# Example 7: Decorator as a practical example - caching
def cache(func):
    cached_results = {}
    def wrapper(n):
        if n in cached_results:
            print(f"Using cached result for {n}")
            return cached_results[n]
        print(f"Computing result for {n}")
        result = func(n)
        cached_results[n] = result
        return result
    return wrapper

@cache
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(5))
# Output shows cached vs. computed calls
```

---

## Guided Practice

**Step 1:** Write a simple decorator that prints when a function starts and ends.
```python
def start_end(func):
    def wrapper(*args, **kwargs):
        print("Function starting...")
        result = func(*args, **kwargs)
        print("Function ending...")
        return result
    return wrapper

@start_end
def add(a, b):
    return a + b

print(add(5, 3))
# Should print:
# Function starting...
# Function ending...
# 8
```

**Step 2:** Write a decorator that converts the return value to uppercase (for string-returning functions).
```python
def uppercase_result(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result.upper()
    return wrapper

@uppercase_result
def get_greeting():
    return "hello world"

print(get_greeting())  # Should print: HELLO WORLD
```

**Step 3:** Write a decorator that counts how many times a function is called.
```python
def call_counter(func):
    calls = 0
    def wrapper(*args, **kwargs):
        nonlocal calls
        calls += 1
        print(f"Call #{calls}")
        return func(*args, **kwargs)
    return wrapper

@call_counter
def say_hi():
    return "Hi!"

say_hi()  # Call #1
say_hi()  # Call #2
```

---

## Practice Problems

**Beginner:** Write a decorator that prints "Function called" before a function executes.

**Intermediate:** Write a decorator that adds 10 to the return value of a function that returns a number.

**Challenge:** Write a decorator that repeats a function call a specified number of times and returns all results in a list.

<details>
<summary>💡 Hints</summary>
- For Beginner: Print a message, then call func(), then return result
- For Intermediate: Get the result, add 10, return it
- For Challenge: You'll need a parameterized decorator: `def repeat(times): def decorator(func): ...`
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def announce(func):
    def wrapper(*args, **kwargs):
        print("Function called")
        return func(*args, **kwargs)
    return wrapper

@announce
def test():
    return "Result"

test()

# Intermediate
def add_ten(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result + 10
    return wrapper

@add_ten
def get_number():
    return 5

print(get_number())  # Output: 15

# Challenge
def repeat(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            results = []
            for _ in range(times):
                results.append(func(*args, **kwargs))
            return results
        return wrapper
    return decorator

@repeat(3)
def say_hi():
    return "Hi!"

print(say_hi())  # Output: ['Hi!', 'Hi!', 'Hi!']
```
</details>
