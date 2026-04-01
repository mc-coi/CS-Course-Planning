# Unit 3 Practice Problems: Advanced Functions & Algorithms

## Beginner Problems (1-8)

**Problem 1:** Write a lambda function that returns the absolute difference between two numbers.
```python
diff = lambda x, y: abs(x - y)
```

**Problem 2:** Use `map()` to convert a list of Celsius temperatures to Fahrenheit.
```python
celsius = [0, 10, 20, 30]
fahrenheit = list(map(lambda c: (c * 9/5) + 32, celsius))
```

**Problem 3:** Use `filter()` to keep only strings longer than 4 characters from a list.
```python
words = ["cat", "elephant", "dog", "python"]
long_words = list(filter(lambda w: len(w) > 4, words))
```

**Problem 4:** Create a list comprehension that squares all numbers from 1 to 10.
```python
squares = [x**2 for x in range(1, 11)]
```

**Problem 5:** Use `zip()` to pair names with ages and create a dictionary.
```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 28]
people = dict(zip(names, ages))
```

**Problem 6:** Write a simple recursive function to calculate factorial(n).
```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)
```

**Problem 7:** Create a set comprehension to extract unique first letters from a word list.
```python
words = ["apple", "apricot", "banana", "blueberry"]
first_letters = {word[0] for word in words}
```

**Problem 8:** Write a generator that yields numbers from 1 to n.
```python
def count_to(n):
    i = 1
    while i <= n:
        yield i
        i += 1
```

## Intermediate Problems (9-16)

**Problem 9:** Use `map()` and `filter()` together to get the squares of only even numbers from 1-10.
```python
numbers = range(1, 11)
result = list(map(lambda x: x**2, filter(lambda x: x % 2 == 0, numbers)))
```

**Problem 10:** Create a dictionary comprehension that maps words to their lengths.
```python
words = ["python", "code", "algorithm"]
lengths = {word: len(word) for word in words}
```

**Problem 11:** Flatten a nested list using recursion.
```python
def flatten(lst):
    result = []
    for item in lst:
        if isinstance(item, list):
            result.extend(flatten(item))
        else:
            result.append(item)
    return result
```

**Problem 12:** Write a recursive function to check if a string is a palindrome.
```python
def is_palindrome(s):
    s = s.lower().replace(" ", "")
    if len(s) <= 1:
        return True
    return s[0] == s[-1] and is_palindrome(s[1:-1])
```

**Problem 13:** Use `enumerate()` to print list items with their indices.
```python
for index, item in enumerate(["a", "b", "c"]):
    print(f"{index}: {item}")
```

**Problem 14:** Create a generator that yields Fibonacci numbers up to n.
```python
def fibonacci(limit):
    a, b = 0, 1
    while a < limit:
        yield a
        a, b = b, a + b
```

**Problem 15:** Write a nested list comprehension to flatten a 2D list.
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened = [x for row in matrix for x in row]
```

**Problem 16:** Use `zip()` with `map()` to multiply corresponding elements from two lists.
```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]
products = list(map(lambda x, y: x * y, list1, list2))
```

## Challenge Problems (17-20)

**Problem 17:** Write a recursive function to find the maximum value in a nested list.
```python
def max_in_nested(lst):
    max_val = float('-inf')
    for item in lst:
        if isinstance(item, list):
            max_val = max(max_val, max_in_nested(item))
        else:
            max_val = max(max_val, item)
    return max_val
```

**Problem 18:** Implement a decorator that measures and prints function execution time.
```python
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"Execution time: {end - start:.4f}s")
        return result
    return wrapper
```

**Problem 19:** Create a custom iterator class that generates the Fibonacci sequence.
```python
class FibonacciIterator:
    def __init__(self, limit):
        self.limit = limit
        self.a, self.b = 0, 1

    def __iter__(self):
        return self

    def __next__(self):
        if self.a > self.limit:
            raise StopIteration
        result = self.a
        self.a, self.b = self.b, self.a + self.b
        return result
```

**Problem 20:** Analyze the Big O complexity of a function and optimize it.
```python
# Inefficient: O(n²)
def has_duplicates_slow(lst):
    for i in range(len(lst)):
        for j in range(i + 1, len(lst)):
            if lst[i] == lst[j]:
                return True
    return False

# Efficient: O(n)
def has_duplicates_fast(lst):
    seen = set()
    for item in lst:
        if item in seen:
            return True
        seen.add(item)
    return False
```

---

## Solutions

<details>
<summary>All solutions are shown inline above. Here are complete implementations for reference:</summary>

```python
# Beginner solutions
print("=== BEGINNER ===")

# 1. Lambda for absolute difference
diff = lambda x, y: abs(x - y)
assert diff(5, 8) == 3

# 2. Map Celsius to Fahrenheit
celsius = [0, 10, 20, 30]
fahrenheit = list(map(lambda c: (c * 9/5) + 32, celsius))
assert fahrenheit[0] == 32.0

# 3. Filter long words
words = ["cat", "elephant", "dog", "python"]
long_words = list(filter(lambda w: len(w) > 4, words))
assert long_words == ["elephant", "python"]

# 4. List comprehension squares
squares = [x**2 for x in range(1, 11)]
assert squares == [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

# 5. Zip and dict
names = ["Alice", "Bob"]
ages = [25, 30]
people = dict(zip(names, ages))
assert people == {"Alice": 25, "Bob": 30}

# 6. Factorial
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)
assert factorial(5) == 120

# 7. Set comprehension
words = ["apple", "apricot", "banana"]
first_letters = {word[0] for word in words}
assert first_letters == {"a", "b"}

# 8. Generator
def count_to(n):
    i = 1
    while i <= n:
        yield i
        i += 1
assert list(count_to(3)) == [1, 2, 3]

print("✓ All beginner problems passed!")

# Intermediate solutions
print("\n=== INTERMEDIATE ===")

# 9. Map and filter
numbers = range(1, 11)
result = list(map(lambda x: x**2, filter(lambda x: x % 2 == 0, numbers)))
assert result == [4, 16, 36, 64, 100]

# 10. Dict comprehension
words = ["python", "code"]
lengths = {word: len(word) for word in words}
assert lengths == {"python": 6, "code": 4}

# 11. Flatten
def flatten(lst):
    result = []
    for item in lst:
        if isinstance(item, list):
            result.extend(flatten(item))
        else:
            result.append(item)
    return result
assert flatten([[1, 2], [3, [4, 5]]]) == [1, 2, 3, 4, 5]

# 12. Palindrome
def is_palindrome(s):
    s = s.lower().replace(" ", "")
    if len(s) <= 1:
        return True
    return s[0] == s[-1] and is_palindrome(s[1:-1])
assert is_palindrome("racecar") == True
assert is_palindrome("hello") == False

print("✓ All intermediate problems passed!")

# Challenge solutions
print("\n=== CHALLENGE ===")

# 17. Max in nested
def max_in_nested(lst):
    max_val = float('-inf')
    for item in lst:
        if isinstance(item, list):
            max_val = max(max_val, max_in_nested(item))
        else:
            max_val = max(max_val, item)
    return max_val
assert max_in_nested([1, [2, [3, 4]]]) == 4

# 20. Has duplicates
def has_duplicates_fast(lst):
    seen = set()
    for item in lst:
        if item in seen:
            return True
        seen.add(item)
    return False
assert has_duplicates_fast([1, 2, 3, 2]) == True
assert has_duplicates_fast([1, 2, 3, 4]) == False

print("✓ All challenge problems passed!")
```

</details>
