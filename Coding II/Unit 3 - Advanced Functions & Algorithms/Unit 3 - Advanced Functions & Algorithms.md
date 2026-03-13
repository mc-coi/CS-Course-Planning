# Unit 3: Advanced Functions & Algorithms
> Write powerful, flexible code using lambda functions, higher-order functions, recursion, and algorithmic thinking.

##  Unit Overview
- **Duration:** 9 days / 3 weeks
- **Key Concepts:** Lambda functions, map/filter/zip, list/dict comprehensions, recursion, pseudocode, Big O notation, decorators, and functional programming
- **Big Idea:** Advanced function techniques enable concise, efficient solutions to complex problems
- **TN Standard:** 9-12.CCI.3 — Design and implement algorithms

##  Learning Targets
- I can write and use lambda functions
- I can use higher-order functions (map, filter, zip)
- I can write list and dictionary comprehensions
- I can think recursively and solve problems with recursion
- I can analyze algorithm complexity using Big O notation
- I can use decorators and closures
- I can apply functional programming patterns

---

# Day 1: Lambda Functions
**Learning Target:** I can write and use lambda functions for short, anonymous functions.

### Key Concepts
**Lambda functions** are small anonymous functions. Syntax: `lambda arguments: expression`

Use lambdas for simple operations where defining a full function is overkill.

### Code Examples
```python
# Basic lambda
square = lambda x: x ** 2
print(square(5))  # 25

# Lambda with multiple arguments
add = lambda x, y: x + y
print(add(3, 4))  # 7

# Lambda with conditionals
max_val = lambda a, b: a if a > b else b
print(max_val(10, 20))  # 20

# Lambdas in sorted()
students = [("Alice", 95), ("Bob", 87), ("Charlie", 92)]
sorted_by_grade = sorted(students, key=lambda s: s[1])
print(sorted_by_grade)

# Lambdas with lists
numbers = [1, 2, 3, 4, 5]
doubled = list(map(lambda x: x * 2, numbers))
print(doubled)  # [2, 4, 6, 8, 10]
```

### Guided Practice
Write lambdas for: double a number, check if even, convert Celsius to Fahrenheit.

### Practice Problems
**Problem 1 — Beginner:** Write a lambda that returns the absolute value of a number.

**Problem 2 — Intermediate:** Use a lambda with sorted() to sort a list of dictionaries by a specific key.

**Problem 3 — Challenge:** Write a lambda that returns the maximum of three numbers.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
abs_val = lambda x: x if x >= 0 else -x

# Problem 2
people = [{"name": "Alice", "age": 30}, {"name": "Bob", "age": 25}]
sorted_people = sorted(people, key=lambda p: p["age"])

# Problem 3
max_three = lambda a, b, c: max(a, max(b, c))
```
</details>

---

# Day 2: Higher-Order Functions (map, filter, zip)
**Learning Target:** I can use map, filter, and zip to operate on collections functionally.

### Key Concepts
**Higher-order functions** take functions as arguments or return functions.

- `map(function, iterable)` — apply function to each item
- `filter(function, iterable)` — keep items where function returns True
- `zip(*iterables)` — combine multiple iterables

### Code Examples
```python
numbers = [1, 2, 3, 4, 5]

# map() — apply function to each item
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# filter() — keep items where condition is True
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4]

# zip() — combine lists
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
pairs = list(zip(names, ages))
print(pairs)  # [("Alice", 25), ("Bob", 30), ("Charlie", 35)]

# Combining them
names = ["Zach", "Alice", "Bob"]
ages = [17, 25, 30]
result = dict(zip(names, ages))
print(result)  # {"Zach": 17, "Alice": 25, "Bob": 30}
```

### Guided Practice
Create lists of numbers and strings. Use map() to transform, filter() to select, and zip() to combine.

### Practice Problems
**Problem 1 — Beginner:** Use filter() to get only positive numbers from a list.

**Problem 2 — Intermediate:** Use map() and filter() together to get squared even numbers.

**Problem 3 — Challenge:** Create a function that pairs students with grades using zip().

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
numbers = [-5, -2, 0, 3, 7]
positive = list(filter(lambda x: x > 0, numbers))

# Problem 2
numbers = [1, 2, 3, 4, 5, 6]
result = list(filter(lambda x: x > 0, map(lambda x: x ** 2, [n for n in numbers if n % 2 == 0])))

# Problem 3
students = ["Zach", "Alice", "Bob"]
grades = [95, 88, 92]
pairings = list(zip(students, grades))
```
</details>

---

# Day 3: List & Dictionary Comprehensions (Advanced)
**Learning Target:** I can write advanced comprehensions with conditions and nested structures.

### Key Concepts
Comprehensions are powerful tools for creating and transforming collections.

Syntax: `[expression for item in iterable if condition]`

Dictionary comprehensions: `{key: value for item in iterable if condition}`

### Code Examples
```python
# List comprehension with condition
numbers = [1, 2, 3, 4, 5, 6]
evens = [x for x in numbers if x % 2 == 0]
print(evens)  # [2, 4, 6]

# Nested comprehension
matrix = [[i + j for j in range(3)] for i in range(3)]
print(matrix)  # [[0, 1, 2], [1, 2, 3], [2, 3, 4]]

# Dictionary comprehension
fruits = {"apple": 1.5, "banana": 0.5, "orange": 1.0}
expensive = {k: v for k, v in fruits.items() if v >= 1.0}
print(expensive)  # {"apple": 1.5, "orange": 1.0}

# Transform keys and values
prices = {"a": 10, "b": 20, "c": 15}
doubled = {k: v * 2 for k, v in prices.items()}
print(doubled)  # {"a": 20, "b": 40, "c": 30}

# Flatten nested list
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened = [num for row in matrix for num in row]
print(flattened)  # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Guided Practice
Create comprehensions that: square odd numbers, filter strings by length, create dictionaries from lists.

### Practice Problems
**Problem 1 — Beginner:** Create a list comprehension that doubles all numbers.

**Problem 2 — Intermediate:** Create a dictionary comprehension from two lists.

**Problem 3 — Challenge:** Flatten a 2D matrix using a single comprehension.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
numbers = [1, 2, 3, 4, 5]
doubled = [x * 2 for x in numbers]

# Problem 2
names = ["Alice", "Bob"]
ages = [25, 30]
data = {name: age for name, age in zip(names, ages)}

# Problem 3
matrix = [[1, 2], [3, 4]]
flat = [val for row in matrix for val in row]
```
</details>

---

# Day 4: Recursion Introduction
**Learning Target:** I can understand recursion and write simple recursive functions.

### Key Concepts
**Recursion:** A function calling itself to solve a problem.

**Base case:** When to stop (prevents infinite loops)
**Recursive case:** Function calls itself with simpler input

### Code Examples
```python
# Factorial: 5! = 5 * 4 * 3 * 2 * 1
def factorial(n):
    if n == 0 or n == 1:  # Base case
        return 1
    else:  # Recursive case
        return n * factorial(n - 1)

print(factorial(5))  # 120

# Countdown
def countdown(n):
    if n == 0:
        print("Blastoff!")
    else:
        print(n)
        countdown(n - 1)

countdown(3)  # Prints: 3, 2, 1, Blastoff!

# Sum of numbers
def sum_list(numbers):
    if len(numbers) == 0:  # Base case
        return 0
    else:  # Recursive case
        return numbers[0] + sum_list(numbers[1:])

print(sum_list([1, 2, 3, 4]))  # 10
```

### Guided Practice
Write recursive functions for: sum of digits, power, search in list.

### Practice Problems
**Problem 1 — Beginner:** Write a recursive function that calculates 2^n.

**Problem 2 — Intermediate:** Write a recursive function to find the maximum value in a list.

**Problem 3 — Challenge:** Write a recursive function to count occurrences of a value in a nested list.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
def power(base, exp):
    if exp == 0:
        return 1
    return base * power(base, exp - 1)

# Problem 2
def max_list(lst):
    if len(lst) == 1:
        return lst[0]
    return max(lst[0], max_list(lst[1:]))

# Problem 3
def count_recursive(lst, target):
    if not lst:
        return 0
    count = 0
    if isinstance(lst[0], list):
        count += count_recursive(lst[0], target)
    elif lst[0] == target:
        count += 1
    return count + count_recursive(lst[1:], target)
```
</details>

---

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

# Day 6: Algorithm Design & Pseudocode
**Learning Target:** I can design algorithms using pseudocode and problem decomposition.

### Key Concepts
**Pseudocode:** English-like code describing algorithm logic (not runnable code).

**Problem decomposition:** Break problems into smaller, solvable parts.

### Code Examples
```
Pseudocode Example: Find Maximum in List

FUNCTION findMax(list):
    IF list is empty:
        RETURN error

    max = first element of list

    FOR each remaining element in list:
        IF element > max:
            SET max = element

    RETURN max

Python implementation:
def find_max(lst):
    if not lst:
        return None
    max_val = lst[0]
    for num in lst[1:]:
        if num > max_val:
            max_val = num
    return max_val
```

### Guided Practice
Write pseudocode for: bubble sort, linear search, counting duplicates.

### Practice Problems
**Problem 1 — Beginner:** Write pseudocode for summing all numbers in a list.

**Problem 2 — Intermediate:** Write pseudocode for sorting a list (any method).

**Problem 3 — Challenge:** Write pseudocode for finding common elements between two lists.

<details>
<summary>✅ Sample Answers</summary>

```
Problem 1:
FUNCTION sumList(numbers):
    total = 0
    FOR each number in numbers:
        ADD number to total
    RETURN total

Problem 2:
FUNCTION bubbleSort(list):
    FOR i = 0 to length - 1:
        FOR j = 0 to length - i - 1:
            IF list[j] > list[j+1]:
                SWAP list[j] and list[j+1]
    RETURN list
```
</details>

---

# Day 7: Complexity Analysis (Big O Notation)
**Learning Target:** I can analyze algorithm complexity and choose appropriate algorithms.

### Key Concepts
**Big O notation** describes how algorithm performance scales with input size.

- O(1) — Constant time (instant)
- O(n) — Linear time (proportional to input)
- O(n²) — Quadratic time (exponential slowdown)
- O(log n) — Logarithmic time (very fast for large inputs)
- O(n log n) — Efficient sorting

### Code Examples
```python
# O(1) — Constant time
def get_first(lst):
    return lst[0]

# O(n) — Linear time
def sum_all(lst):
    total = 0
    for num in lst:
        total += num
    return total

# O(n²) — Quadratic time (nested loops)
def bubble_sort(lst):
    for i in range(len(lst)):
        for j in range(len(lst) - 1):
            if lst[j] > lst[j + 1]:
                lst[j], lst[j + 1] = lst[j + 1], lst[j]

# O(log n) — Binary search (must be sorted)
def binary_search(sorted_lst, target):
    low, high = 0, len(sorted_lst) - 1
    while low <= high:
        mid = (low + high) // 2
        if sorted_lst[mid] == target:
            return mid
        elif sorted_lst[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

# Comparing performance
import time

big_list = list(range(100000))

# Linear search: O(n)
start = time.time()
for item in big_list:
    if item == 50000:
        break
print(f"Linear: {time.time() - start}")

# Binary search: O(log n)
start = time.time()
binary_search(big_list, 50000)
print(f"Binary: {time.time() - start}")
```

### Guided Practice
Identify Big O for various code snippets. Compare algorithm efficiency.

### Practice Problems
**Problem 1 — Beginner:** What is the Big O of checking if a number is in a list?

**Problem 2 — Intermediate:** Compare bubble sort vs merge sort complexity.

**Problem 3 — Challenge:** Optimize an O(n²) algorithm to O(n log n) if possible.

<details>
<summary>✅ Sample Answers</summary>

```
Problem 1: O(n) — must check each element

Problem 2: Bubble sort O(n²), Merge sort O(n log n)

Problem 3: Use sorting + efficient algorithms instead of nested loops
```
</details>

---

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

# Day 9: Project Day — Recursive Calculator & Algorithm Showcase
**Learning Target:** I can apply advanced function techniques to build a complete program.

### Project Overview
Build a calculator demonstrating:
- Lambda functions and higher-order functions
- Recursion for complex calculations
- Algorithm efficiency
- Decorators for timing/logging

### Requirements
- Support basic operations (+, -, *, /)
- Implement exponentiation with recursion
- Use lambda for operation selection
- Time operations to show efficiency
- Create a menu-driven interface

### Scaffold & Starter Code
```python
import time

# Decorator for timing
def timer(func):
    def wrapper(*args):
        start = time.time()
        result = func(*args)
        elapsed = time.time() - start
        print(f"Result: {result} (Computed in {elapsed:.6f}s)")
        return result
    return wrapper

# Recursive power (demonstrates recursion)
@timer
def power_recursive(base, exp):
    if exp == 0:
        return 1
    return base * power_recursive(base, exp - 1)

# Lambda-based operations
operations = {
    '+': lambda x, y: x + y,
    '-': lambda x, y: x - y,
    '*': lambda x, y: x * y,
    '/': lambda x, y: x / y if y != 0 else "Error: Division by zero"
}

# Higher-order function for filtering
def filter_results(results, threshold):
    return list(filter(lambda r: r > threshold, results))

# Main program
def main():
    while True:
        print("\n--- Calculator ---")
        print("1. Basic calculation")
        print("2. Power (recursive)")
        print("3. Exit")

        choice = input("Select: ")

        if choice == "1":
            op = input("Operation (+, -, *, /): ")
            x = float(input("First number: "))
            y = float(input("Second number: "))
            result = operations[op](x, y)
            print(f"Result: {result}")

        elif choice == "2":
            base = int(input("Base: "))
            exp = int(input("Exponent: "))
            power_recursive(base, exp)

        elif choice == "3":
            break

if __name__ == "__main__":
    main()
```

### Enhancement Ideas
- Fibonacci calculator with memoization
- Sorting algorithm comparison (show Big O)
- Scientific calculator functions
- History of operations

---

# Unit Practice Bank

1. **Beginner:** Write a lambda that adds two numbers.
2. **Beginner:** Use map() to double all numbers in a list.
3. **Beginner:** Use filter() to keep only even numbers.
4. **Intermediate:** Write a list comprehension with a condition.
5. **Intermediate:** Write a recursive factorial function.
6. **Intermediate:** Use zip() to combine two lists into pairs.
7. **Intermediate:** Write a dictionary comprehension.
8. **Challenge:** Write memoized Fibonacci.
9. **Challenge:** Write binary search recursively.
10. **Challenge:** Create a decorator that validates function arguments.
11. **Challenge:** Write a function composition tool.
12. **Challenge:** Implement merge sort with Big O analysis.
13. **Challenge:** Create a caching decorator for expensive functions.
14. **Challenge:** Flatten a deeply nested list recursively.
15. **Challenge:** Analyze and optimize an algorithm from O(n²) to O(n log n).

---

# Common Mistakes & How to Fix Them
| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Forgetting base case in recursion | RecursionError: maximum recursion depth | Always include base case |
| Using mutable default in function | Function mutates shared object | Use None as default, create inside |
| Lambda with multiple statements | Syntax error | Lambdas only take expressions, not statements |
| Infinite recursion | RecursionError | Ensure base case is reachable |
| Confusing map() returns iterator | Can't reuse map result | Wrap in list() or iterate only once |
| Complex comprehensions hard to read | Unreadable code | Use intermediate variables or regular loops |

---

# Unit Assessment Prep

**Review Questions:**

1. What is a lambda function? When would you use one?
2. Explain the difference between map(), filter(), and zip().
3. Write a list comprehension that squares numbers 1-5.
4. What is recursion? Give an example.
5. Explain the base case and recursive case.
6. What does Big O notation measure?
7. Compare O(n) and O(n²) complexity.
8. What is a decorator?
9. Explain what a closure is.
10. How would you optimize an O(n²) algorithm?

**Answers:**

1. A lambda is a small anonymous function. Use for simple operations with map(), filter(), sorted().
2. map() applies function to each item; filter() keeps items where function returns True; zip() combines iterables.
3. `[x**2 for x in range(1, 6)]` → `[1, 4, 9, 16, 25]`
4. Recursion is when a function calls itself. Example: factorial(n) = n * factorial(n-1)
5. Base case stops recursion; recursive case calls function with simpler input.
6. Big O measures how algorithm performance scales with input size.
7. O(n) is linear (fast); O(n²) is quadratic (slow for large inputs).
8. A decorator is a function that modifies another function's behavior.
9. A closure is a nested function that captures variables from its outer scope.
10. Use more efficient algorithm (sorting, binary search), reduce nested loops, use caching.

---

# Vocabulary & Quick Reference

**Key Terms:**
- **Lambda:** Anonymous function defined with lambda keyword
- **Higher-order function:** Function that takes/returns functions
- **Recursion:** Function calling itself
- **Base case:** Condition that stops recursion
- **Memoization:** Caching function results
- **Big O:** Notation for algorithm complexity
- **Closure:** Nested function capturing outer variables
- **Decorator:** Function that wraps another function
- **Pseudocode:** English-like description of algorithm

**Key Syntax:**
```python
# Lambda
square = lambda x: x ** 2

# map, filter, zip
map(func, iterable)
filter(condition, iterable)
zip(iter1, iter2)

# Comprehension
[x for x in range(10) if x % 2 == 0]

# Recursion
def factorial(n):
    return 1 if n <= 1 else n * factorial(n-1)

# Decorator
@decorator_name
def func():
    pass
```
