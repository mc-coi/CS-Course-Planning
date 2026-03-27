# Day 3: Function Limitations and Best Practices

**Learning Target:** I can choose when to use lambdas vs. named functions, and apply best practices for readable, maintainable code.

---

## Key Concepts

**Readability Over Cleverness** — A clear, simple function definition is better than a complex lambda. If you're tempted to nest lambdas or make a lambda too long, use `def` instead.

**Lambda Limitations:**
- Only one expression allowed
- No loops, if-statements, or multi-line logic
- Can't have docstrings (for documentation)
- Can be harder to debug (error messages reference `<lambda>`, not a function name)

**Named Functions** (`def`) are better for:
- Complex logic
- Reusable code (used in multiple places)
- Self-documenting code (the name explains the purpose)
- Debugging (the function name appears in tracebacks)

**Key Takeaway:** Lambdas are tools for specific situations. Use them when they make your code simpler and clearer, not when they make it harder to read.

---

## Code Examples

```python
# Example 1: When lambda is GOOD (simple, one-time use)
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # Output: [1, 4, 9, 16, 25]

# Example 2: When lambda is BAD (should use def instead)
# DON'T DO THIS - too complex for a lambda
complex_func = lambda x: sum([i for i in range(1, x + 1)]) if x > 0 else 0

# INSTEAD, do this:
def sum_to_n(x):
    """Return the sum of integers from 1 to x."""
    if x > 0:
        return sum(range(1, x + 1))
    else:
        return 0

# Example 3: Named function for clarity
def is_adult(person):
    """Check if a person is an adult (18+)."""
    return person["age"] >= 18

students = [
    {"name": "Alice", "age": 17},
    {"name": "Bob", "age": 18},
    {"name": "Charlie", "age": 16},
]
adults = filter(is_adult, students)
print(list(adults))

# Example 4: Debugging advantage of named functions
def double(x):
    return x * 2

numbers = [1, 2, 3]
result = list(map(double, numbers))  # Error message will say "double"
# vs.
result = list(map(lambda x: x * 2, numbers))  # Error message will say "<lambda>"

# Example 5: When NOT to nest lambdas
# BAD - too complex to read
transform = lambda data: list(map(lambda x: x * 2 if x > 5 else x, filter(lambda y: y > 0, data)))

# GOOD - broken into steps
def process_numbers(data):
    """Process numbers: keep positive, then double if > 5."""
    positive = filter(lambda y: y > 0, data)
    return list(map(lambda x: x * 2 if x > 5 else x, positive))

# EVEN BETTER - no lambdas needed
def process_numbers_v2(data):
    """Process numbers: keep positive, then double if > 5."""
    result = []
    for num in data:
        if num > 0:
            if num > 5:
                result.append(num * 2)
            else:
                result.append(num)
    return result

# Example 6: Lambda is perfect for sorting
# This is a great use case!
movies = [
    {"title": "Inception", "year": 2010, "rating": 8.8},
    {"title": "Interstellar", "year": 2014, "rating": 8.6},
    {"title": "Dune", "year": 2021, "rating": 8.0},
]

by_year = sorted(movies, key=lambda m: m["year"])
print(by_year[0]["title"])  # Output: Inception
```

---

## Guided Practice

**Step 1:** You have a list of students with test scores. Sort them by score (highest first) using a lambda. When would this be a good use of lambda?
```python
students = [("Alice", 85), ("Bob", 92), ("Charlie", 78)]
sorted_students = sorted(students, key=lambda s: s[1], reverse=True)
print(sorted_students[0])  # Should print: ('Bob', 92)
```

**Step 2:** Rewrite this complex lambda as a named function:
```python
# Original (too complex)
# process = lambda x: x.upper().replace(" ", "_") if len(x) > 3 else x.lower()

def process_string(s):
    """Convert string: uppercase and replace spaces if longer than 3, else lowercase."""
    if len(s) > 3:
        return s.upper().replace(" ", "_")
    else:
        return s.lower()

print(process_string("hello world"))  # Should print: HELLO_WORLD
print(process_string("hi"))           # Should print: hi
```

**Step 3:** Decide: should this use a lambda or a named function? Why?
```python
def find_primes(numbers):
    """Return only prime numbers from a list."""
    def is_prime(n):
        if n < 2:
            return False
        for i in range(2, int(n ** 0.5) + 1):
            if n % i == 0:
                return False
        return True
    
    return [num for num in numbers if is_prime(num)]

primes = find_primes([2, 3, 4, 5, 6, 7, 8, 9, 10])
print(primes)  # Should print: [2, 3, 5, 7]
```

**Step 4:** Refactor this code for clarity:
```python
# Before (too many lambdas)
# data = [1, -5, 3, -2, 6]
# result = sorted(map(lambda x: x ** 2, filter(lambda y: y != 0, data)))

data = [1, -5, 3, -2, 6]
non_zero = [x for x in data if x != 0]
squared = [x ** 2 for x in non_zero]
result = sorted(squared)
print(result)  # Should print: [1, 4, 9, 25, 36]
```

---

## Practice Problems

**Beginner:** Rewrite this as a named function, then use it to sort a list:
```python
# Original: key=lambda x: len(x)
# New: Create a function called word_length() and use it as the key
```

**Intermediate:** Identify which of the following should use lambdas and which should use named functions:
1. Checking if a student is passing (grade >= 70)
2. Sorting a list of students by last name
3. Complex validation logic with multiple conditions
4. Quick one-time sort operation

**Challenge:** Refactor this code to be more readable:
```python
data = [{"x": 1, "y": 2}, {"x": 3, "y": 1}, {"x": 2, "y": 3}]
result = sorted(filter(lambda d: d["x"] + d["y"] > 3, data), key=lambda d: d["y"])
```

<details>
<summary>💡 Hints</summary>
- For Beginner: Create a function that returns `len(word)`, then pass it to sorted()
- For Intermediate: Think about reusability, clarity, and complexity
- For Challenge: Break it into smaller, named steps with meaningful variable names
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def word_length(word):
    return len(word)

words = ["python", "code", "algorithm"]
sorted_words = sorted(words, key=word_length)
print(sorted_words)  # Output: ['code', 'python', 'algorithm']

# Intermediate
# 1. Named function - reusable, clear logic
# 2. Lambda - sorting is a perfect use case
# 3. Named function - complex logic needs clarity
# 4. Lambda - one-time operation, simple

# Challenge
data = [{"x": 1, "y": 2}, {"x": 3, "y": 1}, {"x": 2, "y": 3}]

def sum_exceeds_threshold(d, threshold=3):
    return d["x"] + d["y"] > threshold

def get_y_value(d):
    return d["y"]

filtered = filter(lambda d: sum_exceeds_threshold(d), data)
result = sorted(filtered, key=get_y_value)
print(result)
```
</details>
