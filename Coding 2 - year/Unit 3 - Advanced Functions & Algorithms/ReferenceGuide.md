# Unit 3 Reference Guide: Advanced Functions & Algorithms

## Lambda Functions
```python
# Syntax: lambda arguments: expression
add = lambda x, y: x + y
square = lambda x: x ** 2

# Use with map()
doubled = list(map(lambda x: x * 2, [1, 2, 3]))  # [2, 4, 6]
```

## Higher-Order Functions

### map(function, iterable)
```python
# Transform each element
numbers = [1, 2, 3]
squared = list(map(lambda x: x**2, numbers))  # [1, 4, 9]
```

### filter(function, iterable)
```python
# Keep only matching elements
numbers = [1, 2, 3, 4, 5]
evens = list(filter(lambda x: x % 2 == 0, numbers))  # [2, 4]
```

### zip(*iterables)
```python
names = ["A", "B", "C"]
ages = [20, 30, 40]
paired = list(zip(names, ages))  # [("A", 20), ("B", 30), ("C", 40)]
```

### enumerate(iterable, start=0)
```python
for i, item in enumerate(["a", "b", "c"]):
    print(f"{i}: {item}")  # 0: a, 1: b, 2: c
```

## Comprehensions

### List Comprehension
```python
# [expression for item in iterable if condition]
squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]
evens = [x for x in range(10) if x % 2 == 0]  # [0, 2, 4, 6, 8]
```

### Dictionary Comprehension
```python
# {key: value for item in iterable if condition}
squares = {x: x**2 for x in range(5)}  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

### Set Comprehension
```python
# {expression for item in iterable if condition}
unique = {x for x in [1, 2, 2, 3, 3]}  # {1, 2, 3}
```

### Generator Expression
```python
# (expression for item in iterable) - lazy evaluation
gen = (x**2 for x in range(1000))  # computes on demand
next(gen)  # 0
```

## Recursion Template

```python
def recursive_function(n):
    # Base case: when to stop
    if n <= 1:
        return base_value

    # Recursive case: call itself with smaller problem
    return combine(n, recursive_function(n - 1))
```

## Big O Complexity Chart

| Notation | Name | Example | Speed |
|----------|------|---------|-------|
| O(1) | Constant | Array access by index | Fastest |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Linear search |
| O(n log n) | Linearithmic | Merge sort |
| O(n²) | Quadratic | Bubble sort |
| O(n³) | Cubic | Triple nested loop |
| O(2^n) | Exponential | Recursive fib |
| O(n!) | Factorial | Permutations | Slowest |

## Closures

```python
def make_function():
    x = 10  # Enclosing scope
    def inner():
        return x  # Remembers x
    return inner

func = make_function()
print(func())  # 10
```

## Decorators

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        # Do something before
        result = func(*args, **kwargs)
        # Do something after
        return result
    return wrapper

@my_decorator
def my_function():
    pass
```

## Generators

```python
def my_generator():
    yield 1
    yield 2
    yield 3

for value in my_generator():
    print(value)  # 1, then 2, then 3
```

## Iterator Protocol

```python
class MyIterator:
    def __init__(self, max):
        self.max = max
        self.current = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.current >= self.max:
            raise StopIteration
        self.current += 1
        return self.current
```

## Common Algorithm Patterns

### Linear Search - O(n)
```python
def linear_search(arr, target):
    for i, num in enumerate(arr):
        if num == target:
            return i
    return -1
```

### Binary Search - O(log n)
```python
def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1
```

### Bubble Sort - O(n²)
```python
def bubble_sort(arr):
    for i in range(len(arr)):
        for j in range(len(arr) - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr
```

### Merge Sort - O(n log n)
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)
```

## LEGB Rule (Variable Scope)
1. **Local** - Inside current function
2. **Enclosing** - In outer function scope
3. **Global** - Top-level scope
4. **Built-in** - Python built-ins (len, print, etc.)

## Functional Programming Checklist

- [ ] Use pure functions (no side effects)
- [ ] Prefer immutability
- [ ] Use map/filter/reduce for transformations
- [ ] Leverage lambda for simple operations
- [ ] Consider comprehensions over map/filter
- [ ] Use recursion for tree/graph problems
- [ ] Cache results with memoization
- [ ] Compose functions effectively
