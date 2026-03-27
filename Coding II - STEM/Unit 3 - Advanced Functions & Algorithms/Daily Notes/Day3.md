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

---
