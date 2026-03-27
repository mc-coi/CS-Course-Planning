# Day 14: Generators and yield

**Learning Target:** I can write generator functions using yield to create iterators that produce values on-demand (lazy evaluation).

---

## Key Concepts

**Generator** — A function that uses `yield` to produce values one at a time instead of returning all at once. Generators are lazy — they compute values only when needed.

**yield** — A keyword that pauses the function, returns a value, and remembers where it paused. Next call resumes from where it paused.

**Iterator** — An object with `__next__()` method that produces values one at a time. Generators are iterators.

**Lazy Evaluation** — Computing values only when needed, not upfront. Saves memory and improves performance.

**Generator Expression** — Like a list comprehension, but with parentheses instead of brackets: `(x ** 2 for x in range(10))`.

**Why generators matter:**
- **Memory efficient** — Don't store all values at once
- **Infinite sequences** — Can create infinite iterators
- **Cleaner code** — Simpler than writing iterator classes
- **Performance** — Only compute what you use

---

## Code Examples

```python
# Example 1: Simple generator
def count_up_to(n):
    i = 1
    while i <= n:
        yield i  # Pause and return i
        i += 1

counter = count_up_to(3)
print(next(counter))  # Output: 1
print(next(counter))  # Output: 2
print(next(counter))  # Output: 3
# print(next(counter))  # Would raise StopIteration

# Example 2: Generator in a loop
def count_up_to(n):
    i = 1
    while i <= n:
        yield i
        i += 1

for num in count_up_to(5):
    print(num, end=" ")  # Output: 1 2 3 4 5

# Example 3: Generator vs. list (memory comparison)
# Bad: Creates entire list in memory
def get_numbers_list(n):
    result = []
    for i in range(n):
        result.append(i)
    return result

# Good: Creates values on demand
def get_numbers_generator(n):
    for i in range(n):
        yield i

# For small n, doesn't matter. For large n, generator is much better.
numbers = get_numbers_generator(1000000)  # Doesn't create 1M items!

# Example 4: Infinite sequence
def infinite_counter():
    i = 0
    while True:
        yield i
        i += 1

counter = infinite_counter()
for _ in range(5):
    print(next(counter), end=" ")  # Output: 0 1 2 3 4

# Example 5: Fibonacci generator
def fibonacci(limit):
    a, b = 0, 1
    while a < limit:
        yield a
        a, b = b, a + b

for fib in fibonacci(50):
    print(fib, end=" ")  # Output: 0 1 1 2 3 5 8 13 21 34

# Example 6: Generator expression (like list comprehension but lazy)
# List comprehension: computes all values at once
list_comp = [x ** 2 for x in range(5)]
print(list(list_comp))  # [0, 1, 4, 9, 16]

# Generator expression: computes on demand
gen_expr = (x ** 2 for x in range(5))
print(next(gen_expr))  # 0
print(next(gen_expr))  # 1
print(next(gen_expr))  # 4

# Example 7: Generator for reading large files line by line
def read_large_file(filepath):
    with open(filepath) as file:
        for line in file:
            yield line.strip()

# Usage: Process one line at a time, no need to load entire file
# for line in read_large_file("large_file.txt"):
#     process(line)

# Example 8: Generator with send() (two-way communication)
def echo_generator():
    while True:
        value = yield
        if value is not None:
            print(f"Received: {value}")

gen = echo_generator()
next(gen)  # Start the generator
gen.send("Hello")  # Send data to generator
gen.send("World")  # Output: Received: World

# Example 9: Pipeline with generators
def numbers():
    for i in range(10):
        yield i

def even_only(numbers):
    for num in numbers:
        if num % 2 == 0:
            yield num

def double(numbers):
    for num in numbers:
        yield num * 2

# Chain generators together (very efficient!)
for result in double(even_only(numbers())):
    print(result, end=" ")  # Output: 0 4 8 12 16

# Example 10: Range alternative using generators
def my_range(start, end):
    while start < end:
        yield start
        start += 1

for i in my_range(0, 5):
    print(i, end=" ")  # Output: 0 1 2 3 4
```

---

## Guided Practice

**Step 1:** Write a simple generator that yields numbers from 1 to 5.
```python
def count_to_five():
    for i in range(1, 6):
        yield i

for num in count_to_five():
    print(num, end=" ")  # Should print: 1 2 3 4 5
```

**Step 2:** Write a generator that yields squares of numbers.
```python
def squares(n):
    for i in range(n):
        yield i ** 2

for sq in squares(5):
    print(sq, end=" ")  # Should print: 0 1 4 9 16
```

**Step 3:** Write a generator that yields Fibonacci numbers up to a limit.
```python
def fibonacci(limit):
    a, b = 0, 1
    while a < limit:
        yield a
        a, b = b, a + b

for fib in fibonacci(50):
    print(fib, end=" ")  # Should print: 0 1 1 2 3 5 8 13 21 34
```

**Step 4:** Use a generator expression instead of a list comprehension.
```python
# Original: [x * 2 for x in range(5)]
gen = (x * 2 for x in range(5))
print(list(gen))  # Should print: [0, 2, 4, 6, 8]
```

---

## Practice Problems

**Beginner:** Write a generator that yields all even numbers up to a given limit.

**Intermediate:** Write a generator that reads lines from a list and yields only non-empty lines.

**Challenge:** Write a generator pipeline that filters and transforms data. For example: generate numbers, filter evens, square them, and return only those < 100.

<details>
<summary>💡 Hints</summary>
- For Beginner: Use `if num % 2 == 0: yield num`
- For Intermediate: Check `if line:` or `if line.strip():`
- For Challenge: Chain multiple generators together
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def even_numbers(limit):
    for i in range(limit):
        if i % 2 == 0:
            yield i

for num in even_numbers(10):
    print(num, end=" ")  # Output: 0 2 4 6 8

# Intermediate
def non_empty_lines(lines):
    for line in lines:
        if line.strip():
            yield line.strip()

lines = ["hello", "", "world", "  ", "python"]
for line in non_empty_lines(lines):
    print(line)  # hello, world, python

# Challenge
def numbers():
    for i in range(20):
        yield i

def filter_even(nums):
    for n in nums:
        if n % 2 == 0:
            yield n

def square_and_filter(nums):
    for n in nums:
        squared = n ** 2
        if squared < 100:
            yield squared

for result in square_and_filter(filter_even(numbers())):
    print(result, end=" ")  # Output: 0 4 16 36 64
```
</details>
