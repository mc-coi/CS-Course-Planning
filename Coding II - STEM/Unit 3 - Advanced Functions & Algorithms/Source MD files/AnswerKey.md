# Unit 3 - Advanced Functions & Algorithms: Answer Key

## Problem 1: Write a lambda that adds two numbers

### Solution
```python
# Lambda function that adds two numbers
add = lambda x, y: x + y

# Test the lambda
result = add(5, 3)
print(result)

# Using lambda with other functions
numbers = [(1, 2), (3, 4), (5, 6)]
sums = list(map(lambda pair: pair[0] + pair[1], numbers))
print(sums)
```

### Expected Output
```
8
[3, 7, 11]
```

### Common Mistakes
- Forgetting the colon after the parameters
- Using lambda for complex logic (should only be used for simple operations)

---

## Problem 2: Use map() to double all numbers in a list

### Solution
```python
# Using map() with lambda to double numbers
numbers = [1, 2, 3, 4, 5]
doubled = list(map(lambda x: x * 2, numbers))
print(doubled)

# Alternative using map() with a function
def double(x):
    return x * 2

doubled_alt = list(map(double, numbers))
print(doubled_alt)
```

### Expected Output
```
[2, 4, 6, 8, 10]
[2, 4, 6, 8, 10]
```

### Common Mistakes
- Forgetting to convert map() result to list (map returns an iterator)
- Using incorrect lambda syntax

---

## Problem 3: Use filter() to keep only even numbers

### Solution
```python
# Using filter() to keep only even numbers
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)

# Alternative using filter() with a function
def is_even(x):
    return x % 2 == 0

evens_alt = list(filter(is_even, numbers))
print(evens_alt)

# Using list comprehension (more Pythonic)
evens_comp = [x for x in numbers if x % 2 == 0]
print(evens_comp)
```

### Expected Output
```
[2, 4, 6, 8, 10]
[2, 4, 6, 8, 10]
[2, 4, 6, 8, 10]
```

### Common Mistakes
- Not converting filter() to list
- Using x == 0 instead of x % 2 == 0 for even check

---

## Problem 4: Write a list comprehension with a condition

### Solution
```python
# List comprehension with condition
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Keep only numbers greater than 5 and less than 10
result = [x for x in numbers if 5 < x < 10]
print(result)

# Squared values of even numbers
squared_evens = [x**2 for x in numbers if x % 2 == 0]
print(squared_evens)

# Filter and transform
grades = [85, 92, 78, 95, 88, 76, 91]
passing_grades = [g for g in grades if g >= 80]
print(passing_grades)

# Complex condition
numbers2 = [10, 15, 20, 25, 30, 35, 40]
divisible_by_5_and_greater_20 = [x for x in numbers2 if x % 5 == 0 and x > 20]
print(divisible_by_5_and_greater_20)
```

### Expected Output
```
[6, 7, 8, 9]
[4, 16, 36, 64, 100]
[85, 92, 95, 88, 91]
[25, 30, 35, 40]
```

### Common Mistakes
- Placing the condition in the wrong part of the comprehension
- Complex conditions that should be in separate variables

---

## Problem 5: Write a recursive factorial function

### Solution
```python
# Recursive factorial function
def factorial(n):
    """
    Calculate factorial of n recursively
    Base case: factorial(0) = 1 or factorial(1) = 1
    Recursive case: n! = n * (n-1)!
    """
    # Base case
    if n <= 1:
        return 1
    # Recursive case
    return n * factorial(n - 1)

# Test the function
print(f"5! = {factorial(5)}")
print(f"0! = {factorial(0)}")
print(f"10! = {factorial(10)}")

# Calculate factorials for multiple values
for i in range(1, 6):
    print(f"{i}! = {factorial(i)}")
```

### Expected Output
```
5! = 120
0! = 1
10! = 3628800
1! = 1
2! = 2
3! = 6
4! = 24
5! = 120
```

### Common Mistakes
- Forgetting the base case (causes infinite recursion)
- Incorrect base case condition

---

## Problem 6: Use zip() to combine two lists into pairs

### Solution
```python
# Using zip() to combine two lists
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

# Combine into pairs
pairs = list(zip(names, ages))
print(pairs)

# Iterate through pairs
print("\nIterating through pairs:")
for name, age in zip(names, ages):
    print(f"{name}: {age} years old")

# Zip more than two lists
cities = ["NYC", "LA", "Chicago"]
for name, age, city in zip(names, ages, cities):
    print(f"{name}, {age}, {city}")

# Using zip with unequal length lists
list1 = [1, 2, 3, 4, 5]
list2 = ['a', 'b', 'c']
result = list(zip(list1, list2))
print(f"\nZipping unequal lists: {result}")
```

### Expected Output
```
[('Alice', 25), ('Bob', 30), ('Charlie', 35)]

Iterating through pairs:
Alice: 25 years old
Bob: 30 years old
Charlie: 35 years old
Alice, 25, NYC
Bob, 30, LA
Charlie, 35, Chicago

Zipping unequal lists: [(1, 'a'), (2, 'b'), (3, 'c')]
```

### Common Mistakes
- Forgetting to convert zip() result to list for printing
- Not understanding that zip stops at the shortest list

---

## Problem 7: Write a dictionary comprehension

### Solution
```python
# Dictionary comprehension
numbers = [1, 2, 3, 4, 5]

# Create dict with number as key and square as value
squares = {x: x**2 for x in numbers}
print(squares)

# Create dict with filtering
evens = {x: x**2 for x in numbers if x % 2 == 0}
print(evens)

# Convert lists to dictionary
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
person_dict = {name: age for name, age in zip(names, ages)}
print(person_dict)

# Dictionary comprehension with string manipulation
words = ["apple", "banana", "cherry"]
word_lengths = {word: len(word) for word in words}
print(word_lengths)

# Dictionary comprehension with conditional value
numbers2 = [1, 2, 3, 4, 5, 6]
number_type = {x: "even" if x % 2 == 0 else "odd" for x in numbers2}
print(number_type)
```

### Expected Output
```
{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
{2: 4, 4: 16}
{'Alice': 25, 'Bob': 30, 'Charlie': 35}
{'apple': 5, 'banana': 6, 'cherry': 6}
{1: 'odd', 2: 'even', 3: 'odd', 4: 'even', 5: 'odd', 6: 'even'}
```

### Common Mistakes
- Incorrect syntax (using = instead of : between key and value)
- Confused with list comprehension syntax

---

## Problem 8: Write memoized Fibonacci

### Solution
```python
# Memoized Fibonacci using decorator
def memoize(func):
    """Decorator that caches function results"""
    cache = {}
    def wrapper(n):
        if n not in cache:
            cache[n] = func(n)
        return cache[n]
    return wrapper

@memoize
def fibonacci(n):
    """
    Calculate nth Fibonacci number with memoization
    Fibonacci: 0, 1, 1, 2, 3, 5, 8, 13...
    """
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

# Test the memoized function
print("Fibonacci sequence:")
for i in range(10):
    print(f"fib({i}) = {fibonacci(i)}")

# Large Fibonacci number (would be slow without memoization)
print(f"\nfib(35) = {fibonacci(35)}")

# Alternative using dictionary for memoization
def fibonacci_dict(n, memo=None):
    """Fibonacci with manual memoization using dictionary"""
    if memo is None:
        memo = {}

    if n in memo:
        return memo[n]

    if n <= 1:
        return n

    memo[n] = fibonacci_dict(n - 1, memo) + fibonacci_dict(n - 2, memo)
    return memo[n]

print(f"\nfib(35) with dict memo = {fibonacci_dict(35)}")
```

### Expected Output
```
Fibonacci sequence:
fib(0) = 0
fib(1) = 1
fib(2) = 1
fib(3) = 2
fib(4) = 3
fib(5) = 5
fib(6) = 8
fib(7) = 13
fib(8) = 21
fib(9) = 34

fib(35) = 9227465

fib(35) with dict memo = 9227465
```

### Common Mistakes
- Not properly implementing the cache
- Forgetting to check cache before recursive call

---

## Problem 9: Write binary search recursively

### Solution
```python
# Recursive binary search
def binary_search_recursive(arr, target, left=0, right=None):
    """
    Search for target in sorted array using binary search
    Time complexity: O(log n)
    """
    if right is None:
        right = len(arr) - 1

    if left > right:
        return -1  # Target not found

    mid = (left + right) // 2

    if arr[mid] == target:
        return mid  # Found at index mid
    elif arr[mid] < target:
        # Target is in the right half
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        # Target is in the left half
        return binary_search_recursive(arr, target, left, mid - 1)

# Test binary search
sorted_numbers = [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78]

# Search for existing elements
print("Searching for existing elements:")
for target in [5, 38, 67]:
    index = binary_search_recursive(sorted_numbers, target)
    print(f"Target {target} found at index {index}")

# Search for non-existing elements
print("\nSearching for non-existing elements:")
for target in [10, 100, 3]:
    index = binary_search_recursive(sorted_numbers, target)
    print(f"Target {target}: index {index}")

# Performance comparison with linear search
def linear_search(arr, target):
    """Linear search: O(n)"""
    for i, val in enumerate(arr):
        if val == target:
            return i
    return -1

# Both should find the same targets
print("\nComparison:")
test_targets = [8, 45, 100]
for target in test_targets:
    linear_idx = linear_search(sorted_numbers, target)
    binary_idx = binary_search_recursive(sorted_numbers, target)
    print(f"Target {target}: linear={linear_idx}, binary={binary_idx}")
```

### Expected Output
```
Searching for existing elements:
Target 5 found at index 1
Target 38 found at index 6
Target 67 found at index 9

Searching for non-existing elements:
Target 10: index -1
Target 100: index -1
Target 3: index -1

Comparison:
Target 8: linear=2, binary=2
Target 45: linear=7, binary=7
Target 100: linear=-1, binary=-1
```

### Common Mistakes
- Off-by-one errors with midpoint calculation
- Forgetting base case (left > right)

---

## Problem 10: Create a decorator that validates function arguments

### Solution
```python
# Decorator that validates function arguments
def validate_positive(*expected_types):
    """Decorator to validate that arguments are positive numbers"""
    def decorator(func):
        def wrapper(*args, **kwargs):
            for i, arg in enumerate(args):
                if not isinstance(arg, (int, float)):
                    raise TypeError(f"Argument {i} must be a number, got {type(arg).__name__}")
                if arg < 0:
                    raise ValueError(f"Argument {i} must be positive, got {arg}")
            return func(*args, **kwargs)
        return wrapper
    return decorator

# Decorator for type checking
def validate_types(*types):
    """Decorator to validate argument types"""
    def decorator(func):
        def wrapper(*args, **kwargs):
            for i, (arg, expected_type) in enumerate(zip(args, types)):
                if not isinstance(arg, expected_type):
                    raise TypeError(f"Argument {i} must be {expected_type.__name__}, got {type(arg).__name__}")
            return func(*args, **kwargs)
        return wrapper
    return decorator

# Decorator for range validation
def validate_range(min_val, max_val):
    """Decorator to validate argument is within range"""
    def decorator(func):
        def wrapper(value):
            if not (min_val <= value <= max_val):
                raise ValueError(f"Argument must be between {min_val} and {max_val}, got {value}")
            return func(value)
        return wrapper
    return decorator

# Test decorators
@validate_positive()
def add_positive(a, b):
    """Add two positive numbers"""
    return a + b

@validate_types(str, int)
def repeat_string(text, times):
    """Repeat a string n times"""
    return text * times

@validate_range(0, 100)
def grade_letter(score):
    """Convert score to letter grade"""
    if score >= 90:
        return 'A'
    elif score >= 80:
        return 'B'
    elif score >= 70:
        return 'C'
    elif score >= 60:
        return 'D'
    else:
        return 'F'

# Valid calls
print("Valid calls:")
print(f"add_positive(5, 10) = {add_positive(5, 10)}")
print(f"repeat_string('Hi', 3) = {repeat_string('Hi', 3)}")
print(f"grade_letter(85) = {grade_letter(85)}")

# Invalid calls
print("\nInvalid calls:")
try:
    add_positive(5, -10)
except ValueError as e:
    print(f"Error: {e}")

try:
    repeat_string("Hello", "5")
except TypeError as e:
    print(f"Error: {e}")

try:
    grade_letter(150)
except ValueError as e:
    print(f"Error: {e}")
```

### Expected Output
```
Valid calls:
add_positive(5, 10) = 15
repeat_string('Hi', 3) = HiHiHi
grade_letter(85) = B

Invalid calls:
Error: Argument 1 must be positive, got -10
Error: Argument 1 must be int, got str
Error: Argument must be between 0 and 100, got 150
```

### Common Mistakes
- Not properly preserving function metadata (@functools.wraps)
- Incorrect error message formatting

---

## Problem 11: Write a function composition tool

### Solution
```python
# Function composition tool
def compose(*functions):
    """
    Compose multiple functions into a single function
    compose(f, g, h)(x) = f(g(h(x)))
    """
    def composed(x):
        result = x
        for func in reversed(functions):
            result = func(result)
        return result
    return composed

# Alternative using reduce
from functools import reduce

def compose_alt(*functions):
    """Alternative composition using reduce"""
    return reduce(lambda f, g: lambda x: f(g(x)), functions)

# Test functions
def add_five(x):
    return x + 5

def multiply_by_two(x):
    return x * 2

def square(x):
    return x ** 2

def negate(x):
    return -x

# Create composed functions
print("Function composition:")
# Compose: add_five -> multiply_by_two -> square
composed1 = compose(square, multiply_by_two, add_five)
result1 = composed1(3)
print(f"compose(square, *2, +5)(3) = {result1}")
# Breakdown: 3 + 5 = 8, 8 * 2 = 16, 16^2 = 256

# Compose: negate -> add_five -> multiply_by_two
composed2 = compose(multiply_by_two, add_five, negate)
result2 = composed2(10)
print(f"compose(*2, +5, negate)(10) = {result2}")
# Breakdown: -10 + 5 = -5, -5 * 2 = -10

# Pipe function (reverse order of composition)
def pipe(*functions):
    """
    Pipe functions: pipe(f, g, h)(x) = h(g(f(x)))
    """
    def piped(x):
        result = x
        for func in functions:
            result = func(result)
        return result
    return piped

print("\nFunction piping:")
piped = pipe(add_five, multiply_by_two, square)
result3 = piped(3)
print(f"pipe(+5, *2, square)(3) = {result3}")
# Breakdown: 3 + 5 = 8, 8 * 2 = 16, 16^2 = 256

# Practical example with string functions
def uppercase(s):
    return s.upper()

def add_exclamation(s):
    return s + "!"

def reverse_string(s):
    return s[::-1]

string_transform = compose(reverse_string, add_exclamation, uppercase)
result4 = string_transform("hello")
print(f"\nString composition: {result4}")
# Breakdown: "hello" -> "HELLO" -> "HELLO!" -> "!OLLEH"
```

### Expected Output
```
Function composition:
compose(square, *2, +5)(3) = 256
compose(*2, +5, negate)(10) = -10

Function piping:
pipe(+5, *2, square)(3) = 256

String composition: !OLLEH
```

### Common Mistakes
- Reversing the order of functions (composition order matters!)
- Not understanding the difference between composition and piping

---

## Problem 12: Implement merge sort with Big O analysis

### Solution
```python
# Merge sort implementation
def merge_sort(arr):
    """
    Merge sort algorithm
    Time Complexity: O(n log n) in all cases
    Space Complexity: O(n) for temporary arrays
    Stable: Yes (maintains relative order of equal elements)
    """
    if len(arr) <= 1:
        return arr

    # Divide: split array in half
    mid = len(arr) // 2
    left = arr[:mid]
    right = arr[mid:]

    # Conquer: recursively sort both halves
    left_sorted = merge_sort(left)
    right_sorted = merge_sort(right)

    # Combine: merge the sorted halves
    return merge(left_sorted, right_sorted)

def merge(left, right):
    """Merge two sorted arrays into one sorted array"""
    result = []
    i = j = 0

    # Compare elements and add the smaller one
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    # Add remaining elements
    result.extend(left[i:])
    result.extend(right[j:])

    return result

# Test merge sort
print("Merge Sort Examples:")
test_arrays = [
    [64, 34, 25, 12, 22, 11, 90],
    [5, 2, 8, 1, 9],
    [3],
    [2, 1],
    [1, 2, 3, 4, 5]  # Already sorted
]

for arr in test_arrays:
    sorted_arr = merge_sort(arr)
    print(f"merge_sort({arr}) = {sorted_arr}")

# Big O Analysis
print("\n--- Big O Analysis ---")
print("Time Complexity:")
print("  Best Case: O(n log n)")
print("  Average Case: O(n log n)")
print("  Worst Case: O(n log n)")
print("\nSpace Complexity: O(n)")
print("  Requires temporary arrays for merging")
print("\nStability: Stable")
print("  Equal elements maintain their relative order")

# Comparison with other sorts
print("\n--- Comparison with Bubble Sort ---")
def bubble_sort(arr):
    """Bubble sort: O(n²) - for comparison"""
    arr = arr.copy()
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

large_arr = [64, 34, 25, 12, 22, 11, 90, 88, 45, 50]

import time
# Test merge sort time
start = time.time()
result_merge = merge_sort(large_arr)
time_merge = time.time() - start

# Test bubble sort time
start = time.time()
result_bubble = bubble_sort(large_arr)
time_bubble = time.time() - start

print(f"Merge Sort Time: {time_merge:.6f} seconds")
print(f"Bubble Sort Time: {time_bubble:.6f} seconds")
print(f"Results Match: {result_merge == result_bubble}")
```

### Expected Output
```
Merge Sort Examples:
merge_sort([64, 34, 25, 12, 22, 11, 90]) = [11, 12, 22, 25, 34, 64, 90]
merge_sort([5, 2, 8, 1, 9]) = [1, 2, 5, 8, 9]
merge_sort([3]) = [3]
merge_sort([2, 1]) = [1, 2]
merge_sort([1, 2, 3, 4, 5]) = [1, 2, 3, 4, 5]

--- Big O Analysis ---
Time Complexity:
  Best Case: O(n log n)
  Average Case: O(n log n)
  Worst Case: O(n log n)

Space Complexity: O(n)
  Requires temporary arrays for merging

Stability: Stable
  Equal elements maintain their relative order

--- Comparison with Bubble Sort ---
Merge Sort Time: 0.000123 seconds
Bubble Sort Time: 0.000456 seconds
Results Match: True
```

### Common Mistakes
- Not properly merging the sorted arrays
- Incorrect division of the array

---

## Problem 13: Create a caching decorator for expensive functions

### Solution
```python
import time
from functools import wraps

# Simple caching decorator
def cache(func):
    """Decorator that caches function results"""
    cache_dict = {}

    @wraps(func)
    def wrapper(*args, **kwargs):
        # Create cache key from arguments
        key = (args, tuple(sorted(kwargs.items())))

        if key not in cache_dict:
            cache_dict[key] = func(*args, **kwargs)
        return cache_dict[key]

    wrapper.cache_clear = lambda: cache_dict.clear()
    wrapper.cache_info = lambda: cache_dict

    return wrapper

# Time-based caching decorator
def cache_with_timeout(timeout_seconds):
    """Decorator that caches results for a specified duration"""
    def decorator(func):
        cache_dict = {}
        cache_time = {}

        @wraps(func)
        def wrapper(*args, **kwargs):
            key = (args, tuple(sorted(kwargs.items())))
            current_time = time.time()

            # Check if result is in cache and not expired
            if key in cache_dict:
                if current_time - cache_time[key] < timeout_seconds:
                    return cache_dict[key]

            # Compute and cache result
            result = func(*args, **kwargs)
            cache_dict[key] = result
            cache_time[key] = current_time
            return result

        return wrapper
    return decorator

# Expensive function simulations
@cache
def expensive_computation(n):
    """Simulates an expensive computation"""
    print(f"Computing factorial({n})...")
    time.sleep(0.5)  # Simulate computation time
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result

@cache_with_timeout(2)
def fetch_weather(city):
    """Simulates fetching weather data (expires after 2 seconds)"""
    print(f"Fetching weather for {city}...")
    time.sleep(0.3)  # Simulate API call
    return f"Sunny, 75°F in {city}"

# Test caching
print("=== Simple Caching ===")
print("First call:")
print(f"5! = {expensive_computation(5)}")

print("\nSecond call (cached):")
print(f"5! = {expensive_computation(5)}")

print("\nDifferent argument:")
print(f"6! = {expensive_computation(6)}")

print("\nCache info:", expensive_computation.cache_info())

print("\n=== Time-based Caching ===")
print("First call:")
print(fetch_weather("New York"))

print("\nImmediate second call (cached):")
print(fetch_weather("New York"))

print("\nWait 2.5 seconds...")
time.sleep(2.5)

print("After timeout (recalculated):")
print(fetch_weather("New York"))
```

### Expected Output
```
=== Simple Caching ===
First call:
Computing factorial(5)...
5! = 120

Second call (cached):
5! = 120

Different argument:
Computing factorial(6)...
6! = 720

Cache info: {((5,), ()): 120, ((6,), ()): 720}

=== Time-based Caching ===
First call:
Fetching weather for New York...
Sunny, 75°F in New York

Immediate second call (cached):
Sunny, 75°F in New York

Wait 2.5 seconds...
After timeout (recalculated):
Fetching weather for New York...
Sunny, 75°F in New York
```

### Common Mistakes
- Not using functools.wraps (loses function metadata)
- Incorrect cache key generation with kwargs

---

## Problem 14: Flatten a deeply nested list recursively

### Solution
```python
# Flatten nested list recursively
def flatten(nested_list):
    """
    Flatten a deeply nested list recursively
    Time Complexity: O(n) where n is total elements
    """
    result = []

    for item in nested_list:
        if isinstance(item, list):
            # Recursively flatten nested lists
            result.extend(flatten(item))
        else:
            # Add non-list items to result
            result.append(item)

    return result

# Alternative using generator for memory efficiency
def flatten_generator(nested_list):
    """Memory-efficient version using generator"""
    for item in nested_list:
        if isinstance(item, list):
            yield from flatten_generator(item)
        else:
            yield item

# Test cases
print("Flatten Nested Lists:")

test_cases = [
    [1, [2, 3]],
    [1, [2, [3, 4]]],
    [[[1, 2], [3, 4]], [[5, 6], [7, 8]]],
    [1, 2, 3],
    [],
    [1, [2, [3, [4, [5]]]]]
]

for test in test_cases:
    flattened = flatten(test)
    print(f"flatten({test}) = {flattened}")

# Using generator version
print("\n=== Using Generator ===")
nested = [1, [2, [3, [4, 5]]]]
flat_list = list(flatten_generator(nested))
print(f"flatten_generator({nested}) = {flat_list}")

# Mixed types
print("\n=== Mixed Types ===")
mixed = [1, "hello", [2, 3.5], [["nested"], True]]
flattened_mixed = flatten(mixed)
print(f"flatten({mixed}) = {flattened_mixed}")

# One-liner using list comprehension (less readable)
print("\n=== List Comprehension Approach ===")
def flatten_comp(lst):
    return [x for item in lst for x in (flatten_comp(item) if isinstance(item, list) else [item])]

print(f"flatten_comp([1, [2, [3, 4]]]) = {flatten_comp([1, [2, [3, 4]]])}")
```

### Expected Output
```
Flatten Nested Lists:
flatten([1, [2, 3]]) = [1, 2, 3]
flatten([1, [2, [3, 4]]]) = [1, 2, 3, 4]
flatten([[[1, 2], [3, 4]], [[5, 6], [7, 8]]]) = [1, 2, 3, 4, 5, 6, 7, 8]
flatten([1, 2, 3]) = [1, 2, 3]
flatten([]) = []
flatten([1, [2, [3, [4, [5]]]]]) = [1, 2, 3, 4, 5]

=== Using Generator ===
flatten_generator([1, [2, [3, [4, 5]]]]) = [1, 2, 3, 4, 5]

=== Mixed Types ===
flatten([1, 'hello', [2, 3.5], [['nested'], True]]) = [1, 'hello', 2, 3.5, 'nested', True]

=== List Comprehension Approach ===
flatten_comp([1, [2, [3, 4]]]) = [1, 2, 3, 4]
```

### Common Mistakes
- Not checking isinstance(item, list) before recursing
- Using append instead of extend for recursive results

---

## Problem 15: Analyze and optimize an algorithm from O(n²) to O(n log n)

### Solution
```python
import time

# O(n²) - Inefficient approach
def find_pairs_naive(arr, target_sum):
    """
    Find all pairs in array that sum to target
    Time Complexity: O(n²) - nested loops
    Space Complexity: O(1) (ignoring output)
    """
    pairs = []
    n = len(arr)
    for i in range(n):
        for j in range(i + 1, n):
            if arr[i] + arr[j] == target_sum:
                pairs.append((arr[i], arr[j]))
    return pairs

# O(n log n) - Optimized approach using sorting
def find_pairs_optimized(arr, target_sum):
    """
    Find all pairs in array that sum to target
    Time Complexity: O(n log n) - sorting dominates
    Space Complexity: O(n) - for sorted array
    """
    arr_sorted = sorted(arr)
    pairs = []
    left = 0
    right = len(arr_sorted) - 1

    while left < right:
        current_sum = arr_sorted[left] + arr_sorted[right]
        if current_sum == target_sum:
            pairs.append((arr_sorted[left], arr_sorted[right]))
            left += 1
            right -= 1
        elif current_sum < target_sum:
            left += 1
        else:
            right -= 1

    return pairs

# O(n) - Hash-based approach (best if we only need count)
def find_pairs_hash(arr, target_sum):
    """
    Find all pairs in array that sum to target
    Time Complexity: O(n) - single pass with hash lookup
    Space Complexity: O(n) - hash map
    """
    seen = set()
    pairs = []

    for num in arr:
        complement = target_sum - num
        if complement in seen:
            pairs.append((complement, num))
        seen.add(num)

    return pairs

# Test cases
print("=== Find Pairs with Sum ===")
test_arr = [2, 7, 11, 15, 3, 6, 4, 1, 8]
target = 9

print(f"Array: {test_arr}")
print(f"Target Sum: {target}")

result_naive = find_pairs_naive(test_arr, target)
result_optimized = find_pairs_optimized(test_arr, target)
result_hash = find_pairs_hash(test_arr, target)

print(f"\nNaive O(n²): {result_naive}")
print(f"Optimized O(n log n): {result_optimized}")
print(f"Hash O(n): {result_hash}")

# Performance comparison
print("\n=== Performance Comparison ===")
import random
large_arr = [random.randint(1, 1000) for _ in range(10000)]
target_sum = 1000

# Naive approach
start = time.time()
result1 = find_pairs_naive(large_arr, target_sum)
time_naive = time.time() - start

# Optimized approach
start = time.time()
result2 = find_pairs_optimized(large_arr, target_sum)
time_optimized = time.time() - start

# Hash approach
start = time.time()
result3 = find_pairs_hash(large_arr, target_sum)
time_hash = time.time() - start

print(f"Array size: {len(large_arr)}")
print(f"Naive O(n²) time: {time_naive:.4f} seconds")
print(f"Optimized O(n log n) time: {time_optimized:.6f} seconds")
print(f"Hash O(n) time: {time_hash:.6f} seconds")
print(f"\nSpeedup (naive vs optimized): {time_naive / time_optimized:.1f}x")
print(f"Speedup (optimized vs hash): {time_optimized / time_hash:.1f}x")

# Algorithm Analysis
print("\n=== Complexity Analysis ===")
print("Algorithm Comparison:")
print("1. Naive (Nested Loops)")
print("   Time: O(n²)")
print("   Space: O(1)")
print("   Pros: Simple, no extra space")
print("   Cons: Very slow on large datasets")
print()
print("2. Optimized (Sorting + Two Pointers)")
print("   Time: O(n log n) dominated by sorting")
print("   Space: O(n) for sorted array")
print("   Pros: Faster for large datasets")
print("   Cons: Requires extra space")
print()
print("3. Hash-based")
print("   Time: O(n)")
print("   Space: O(n)")
print("   Pros: Fastest for single pass")
print("   Cons: Hash map overhead, uses space")
```

### Expected Output
```
=== Find Pairs with Sum ===
Array: [2, 7, 11, 15, 3, 6, 4, 1, 8]
Target Sum: 9

Naive O(n²): [(2, 7), (3, 6), (8, 1)]
Optimized O(n log n): [(1, 8), (2, 7), (3, 6)]
Hash O(n): [(2, 7), (3, 6), (1, 8)]

=== Performance Comparison ===
Array size: 10000
Naive O(n²) time: 2.3456 seconds
Optimized O(n log n) time: 0.0234 seconds
Hash O(n) time: 0.0089 seconds

Speedup (naive vs optimized): 100.2x
Speedup (optimized vs hash): 2.6x

=== Complexity Analysis ===
Algorithm Comparison:
1. Naive (Nested Loops)
   Time: O(n²)
   Space: O(1)
   Pros: Simple, no extra space
   Cons: Very slow on large datasets

2. Optimized (Sorting + Two Pointers)
   Time: O(n log n) dominated by sorting
   Space: O(n) for sorted array
   Pros: Faster for large datasets
   Cons: Requires extra space

3. Hash-based
   Time: O(n)
   Space: O(n)
   Pros: Fastest for single pass
   Cons: Hash map overhead, uses space
```

### Common Mistakes
- Not understanding that sorting is O(n log n)
- Thinking two-pointer requires pre-existing sorted input for all use cases
- Not considering space-time tradeoff with hash approach
