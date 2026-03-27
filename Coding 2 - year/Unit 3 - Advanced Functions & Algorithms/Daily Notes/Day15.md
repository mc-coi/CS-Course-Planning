# Day 15: Generator Expressions and Iterator Patterns

**Learning Target:** I can use generator expressions and understand the iterator protocol to write efficient code.

---

## Key Concepts

**Generator Expression** — Syntax: `(expr for item in iterable [if condition])`. Like list comprehension but lazy — values computed on demand.

**Iterator Protocol** — Objects that implement `__iter__()` and `__next__()` are iterators. `for` loops use this protocol.

**Iterable** — An object that implements `__iter__()`, returning an iterator.

**Generator vs. Iterator:**
- All generators are iterators
- Not all iterators are generators
- Generators are simpler to write than custom iterator classes

**When to use generator expressions:**
- Filtering/transforming large datasets
- Processing one item at a time
- Creating simple, readable lazy sequences

---

## Code Examples

```python
# Example 1: Generator expression basics
# List comprehension (eager - computes all upfront)
squares_list = [x ** 2 for x in range(5)]
print(squares_list)  # [0, 1, 4, 9, 16]

# Generator expression (lazy - computes on demand)
squares_gen = (x ** 2 for x in range(5))
print(squares_gen)   # <generator object...>
print(list(squares_gen))  # [0, 1, 4, 9, 16] (convert to list to see)

# Example 2: Memory efficiency with large datasets
import sys

# List uses much more memory
list_comp = [x * 2 for x in range(1000000)]
print(f"List size: {sys.getsizeof(list_comp)} bytes")

# Generator uses minimal memory
gen_expr = (x * 2 for x in range(1000000))
print(f"Generator size: {sys.getsizeof(gen_expr)} bytes")

# Example 3: Generator expression with condition
numbers = range(20)
# Get only even numbers squared
even_squares = (x ** 2 for x in numbers if x % 2 == 0)

for val in even_squares:
    print(val, end=" ")  # 0 4 16 36 64 100 144 196 256 324

# Example 4: Chaining generator expressions
numbers = range(10)
filtered = (x for x in numbers if x > 3)
squared = (x ** 2 for x in filtered)
result = list(squared)
print(result)  # [16, 25, 36, 49, 64, 81]

# Example 5: Custom iterator class
class CountUp:
    def __init__(self, max):
        self.max = max
        self.current = 0
    
    def __iter__(self):
        return self  # Iterator protocol
    
    def __next__(self):
        if self.current < self.max:
            self.current += 1
            return self.current
        else:
            raise StopIteration

counter = CountUp(3)
for num in counter:
    print(num, end=" ")  # 1 2 3

# Example 6: Iterator vs. Generator (same functionality)
# Using iterator class
class FibonacciIterator:
    def __init__(self, limit):
        self.limit = limit
        self.a, self.b = 0, 1
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.a < self.limit:
            value = self.a
            self.a, self.b = self.b, self.a + self.b
            return value
        else:
            raise StopIteration

# Using generator (much simpler!)
def fibonacci_generator(limit):
    a, b = 0, 1
    while a < limit:
        yield a
        a, b = b, a + b

# Both produce the same results, but generator is cleaner

# Example 7: Generator expression with map and filter
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Traditional: map and filter (returns iterators)
doubled = map(lambda x: x * 2, numbers)
evens = filter(lambda x: x % 2 == 0, doubled)

# Generator expression (clearer)
result = (x * 2 for x in numbers if x % 2 == 0)

# Both are equivalent in functionality

# Example 8: Generator expression in function calls
def process(items):
    for item in items:
        print(f"Processing {item}")
        yield item * 2

# Pass generator expression directly (memory efficient!)
results = process(x for x in range(5) if x % 2 == 0)
print(list(results))  # [0, 4, 8]

# Example 9: Using generators with sum, max, min
numbers = (x * 2 for x in range(100) if x % 3 == 0)
print(sum(numbers))  # Efficient: doesn't store all values

# Example 10: Nested generator expressions
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Flatten matrix lazily
flattened = (x for row in matrix for x in row)
print(list(flattened))  # [1, 2, 3, 4, 5, 6, 7, 8, 9]

# Same but with filter
non_diagonal = (x for row in matrix for x in row if x % 2 == 1)
print(list(non_diagonal))  # [1, 3, 5, 7, 9]
```

---

## Guided Practice

**Step 1:** Create a generator expression that squares numbers from 1 to 10.
```python
squares = (x ** 2 for x in range(1, 11))
print(list(squares))
# Should print: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

**Step 2:** Create a generator expression that filters only even numbers from a range.
```python
evens = (x for x in range(20) if x % 2 == 0)
print(list(evens))
# Should print: [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

**Step 3:** Create a generator expression that combines filtering and transformation.
```python
# Get double of even numbers only
result = (x * 2 for x in range(10) if x % 2 == 0)
print(list(result))
# Should print: [0, 4, 8, 12, 16]
```

**Step 4:** Use a generator expression with sum() efficiently.
```python
# Sum of squares of odd numbers up to 20
total = sum(x ** 2 for x in range(20) if x % 2 == 1)
print(total)
# Should print: 1 + 9 + 25 + 49 + 81 + 121 + 169 + 225 + 289 + 361 = 1210
```

---

## Practice Problems

**Beginner:** Create a generator expression that yields multiples of 3 up to 30.

**Intermediate:** Create a generator expression that processes a list of strings and yields only words longer than 3 characters in uppercase.

**Challenge:** Create a generator expression that flattens a nested list of lists and yields only elements greater than 5.

<details>
<summary>💡 Hints</summary>
- For Beginner: `(x for x in range(0, 31, 3))`
- For Intermediate: `(word.upper() for word in words if len(word) > 3)`
- For Challenge: Use nested loop: `(x for row in lists for x in row if x > 5)`
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
multiples = (x for x in range(0, 31, 3))
print(list(multiples))  # Output: [0, 3, 6, 9, 12, 15, 18, 21, 24, 27, 30]

# Intermediate
words = ["hi", "hello", "world", "a", "python"]
long_upper = (word.upper() for word in words if len(word) > 3)
print(list(long_upper))  # Output: ['HELLO', 'WORLD', 'PYTHON']

# Challenge
nested = [[1, 8, 3], [9, 2, 6], [5, 10, 4]]
filtered = (x for row in nested for x in row if x > 5)
print(list(filtered))  # Output: [8, 9, 6, 10]
```
</details>
