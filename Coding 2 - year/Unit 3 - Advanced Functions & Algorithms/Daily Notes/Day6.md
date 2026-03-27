# Day 6: Higher-Order Functions Review and Comprehensions Intro

**Learning Target:** I can choose between map/filter/reduce and comprehensions, and understand when to use each approach.

---

## Key Concepts

**Comparison: Functional vs. Pythonic:**
- **Functional approach:** Use `map()`, `filter()`, `reduce()` (common in other languages)
- **Pythonic approach:** Use list/dict comprehensions (favored in Python for readability)

**Both are valid!** The choice depends on:
- **Readability:** Comprehensions are often clearer to Python developers
- **Performance:** Comprehensions are typically faster
- **Complexity:** For complex transformations, sometimes a loop is clearest

**List Comprehension** — A concise way to create lists by applying an expression to each item in an iterable. Basic syntax: `[expression for item in iterable]`

**When to use comprehensions:** Most of the time in Python! They're more readable than map/filter chains.

**When to use map/filter/reduce:** 
- When passing existing functions (like `int`, `str.upper`)
- When the logic is already written as a function
- When working with functional programming paradigms

---

## Code Examples

```python
# Example 1: List comprehension vs. map()
numbers = [1, 2, 3, 4, 5]

# Using map()
squared_map = list(map(lambda x: x ** 2, numbers))
print(squared_map)  # [1, 4, 9, 16, 25]

# Using comprehension (more Pythonic)
squared_comp = [x ** 2 for x in numbers]
print(squared_comp)  # [1, 4, 9, 16, 25]

# Example 2: List comprehension vs. filter()
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Using filter()
evens_filter = list(filter(lambda x: x % 2 == 0, numbers))
print(evens_filter)  # [2, 4, 6, 8, 10]

# Using comprehension (clearer!)
evens_comp = [x for x in numbers if x % 2 == 0]
print(evens_comp)  # [2, 4, 6, 8, 10]

# Example 3: Dictionary comprehension (similar idea)
words = ["cat", "elephant", "dog", "python"]
length_dict = {word: len(word) for word in words}
print(length_dict)
# Output: {'cat': 3, 'elephant': 8, 'dog': 3, 'python': 6}

# Example 4: Comprehension with condition
numbers = [1, 2, 3, 4, 5]
# Transform and filter in one go
result = [x * 2 for x in numbers if x > 2]
print(result)  # [6, 8, 10]

# Example 5: When map/filter make sense - using built-in functions
string_numbers = ["1", "2", "3", "4", "5"]
# Using map with int (cleaner than lambda)
integers = list(map(int, string_numbers))
print(integers)  # [1, 2, 3, 4, 5]

# Using strings with str.upper
words = ["hello", "world"]
uppercase = list(map(str.upper, words))
print(uppercase)  # ['HELLO', 'WORLD']

# Example 6: Real-world refactoring
# BEFORE (functional, harder to read)
from functools import reduce
student_data = [
    {"name": "Alice", "grade": 11, "gpa": 3.8},
    {"name": "Bob", "grade": 10, "gpa": 3.5},
    {"name": "Charlie", "grade": 11, "gpa": 3.9},
]

high_achievers = list(filter(lambda s: s["gpa"] > 3.7, student_data))
names = list(map(lambda s: s["name"], high_achievers))
print(names)  # ['Alice', 'Charlie']

# AFTER (Pythonic, clearer)
high_achievers = [s for s in student_data if s["gpa"] > 3.7]
names = [s["name"] for s in high_achievers]
print(names)  # ['Alice', 'Charlie']

# Example 7: reduce() - often best replaced by built-ins
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# Using reduce
total_reduce = reduce(lambda x, y: x + y, numbers)
print(total_reduce)  # 15

# Using sum (built-in, clearer)
total_sum = sum(numbers)
print(total_sum)  # 15

# Example 8: Nested list comprehension
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
# Flatten the matrix
flattened = [x for row in matrix for x in row]
print(flattened)  # [1, 2, 3, 4, 5, 6, 7, 8, 9]

# Example 9: Set and dictionary comprehensions
words = ["cat", "dog", "elephant", "cat", "dog"]
# Set comprehension (removes duplicates)
unique_words = {word for word in words}
print(unique_words)  # {'cat', 'dog', 'elephant'}

# Dict comprehension
word_lengths = {word: len(word) for word in unique_words}
print(word_lengths)  # {'cat': 3, 'dog': 3, 'elephant': 8}
```

---

## Guided Practice

**Step 1:** Convert this `map()` to a list comprehension:
```python
# Original
numbers = [1, 2, 3, 4, 5]
doubled = list(map(lambda x: x * 2, numbers))

# Converted
doubled = [x * 2 for x in numbers]
print(doubled)  # Should print: [2, 4, 6, 8, 10]
```

**Step 2:** Convert this `filter()` to a list comprehension:
```python
# Original
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
odds = list(filter(lambda x: x % 2 == 1, numbers))

# Converted
odds = [x for x in numbers if x % 2 == 1]
print(odds)  # Should print: [1, 3, 5, 7, 9]
```

**Step 3:** Write a dictionary comprehension that maps each word to its length.
```python
words = ["python", "code", "algorithm"]
word_lengths = {word: len(word) for word in words}
print(word_lengths)
# Should print: {'python': 6, 'code': 4, 'algorithm': 9}
```

**Step 4:** Rewrite this complex functional code more clearly:
```python
# Original (hard to read)
# data = list(filter(lambda x: x > 5, map(lambda x: x * 2, [1, 2, 3, 4, 5, 6])))

# Clearer approach
data = [x * 2 for x in [1, 2, 3, 4, 5, 6] if x * 2 > 5]
print(data)  # Should print: [6, 8, 10, 12]
```

---

## Practice Problems

**Beginner:** Convert a `map()` function to a comprehension. Start with converting `list(map(lambda x: x + 1, [1, 2, 3]))`.

**Intermediate:** Create a dictionary comprehension from a list of names that maps each name to its length.

**Challenge:** Write a list comprehension that extracts all student names from a list of student dictionaries where the GPA is above 3.5.

<details>
<summary>💡 Hints</summary>
- For Beginner: `[expression for item in iterable]`
- For Intermediate: Use dictionary syntax `{key: value for item in iterable}`
- For Challenge: Include the `if` condition at the end: `[... for student in students if ...]`
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
result = [x + 1 for x in [1, 2, 3]]
print(result)  # Output: [2, 3, 4]

# Intermediate
names = ["Alice", "Bob", "Charlie"]
name_lengths = {name: len(name) for name in names}
print(name_lengths)  # Output: {'Alice': 5, 'Bob': 3, 'Charlie': 7}

# Challenge
students = [
    {"name": "Alice", "gpa": 3.8},
    {"name": "Bob", "gpa": 3.2},
    {"name": "Charlie", "gpa": 3.9},
]
high_performers = [s["name"] for s in students if s["gpa"] > 3.5]
print(high_performers)  # Output: ['Alice', 'Charlie']
```
</details>
