# Day 7: Advanced List and Dictionary Comprehensions

**Learning Target:** I can write complex list and dictionary comprehensions with nested loops and multiple conditions.

---

## Key Concepts

**Nested Comprehensions** — Comprehensions can contain loops within loops, allowing you to work with nested data structures like lists of lists or multiple iterables.

**Multiple Conditions** — Add multiple `if` statements to filter by different criteria.

**Syntax for complex comprehensions:**
- With condition: `[expr for item in iterable if condition]`
- With nested loop: `[expr for item in iterable1 for subitem in iterable2]`
- With multiple conditions: `[expr for item in iterable if cond1 if cond2]`

**Dictionary/Set Comprehensions** — Same logic applies to `{key: value for ...}` and `{item for ...}`.

---

## Code Examples

```python
# Example 1: Nested loop comprehension - create all pairs
list1 = [1, 2, 3]
list2 = ['a', 'b']
pairs = [(x, y) for x in list1 for y in list2]
print(pairs)
# Output: [(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b'), (3, 'a'), (3, 'b')]

# Example 2: Flatten a nested list
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened = [x for row in matrix for x in row]
print(flattened)  # [1, 2, 3, 4, 5, 6, 7, 8, 9]

# Example 3: Multiple conditions
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
# Numbers that are even AND greater than 4
result = [x for x in numbers if x % 2 == 0 if x > 4]
print(result)  # [6, 8, 10]

# Example 4: Nested comprehension with condition
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
# Get only even numbers from the matrix
evens = [x for row in matrix for x in row if x % 2 == 0]
print(evens)  # [2, 4, 6, 8]

# Example 5: Dictionary comprehension with nested structure
students = [
    {"name": "Alice", "scores": [85, 90, 88]},
    {"name": "Bob", "scores": [78, 82, 80]},
]
# Create dict mapping student names to average scores
averages = {
    s["name"]: sum(s["scores"]) / len(s["scores"]) 
    for s in students
}
print(averages)  # {'Alice': 87.67..., 'Bob': 80.0}

# Example 6: Dictionary comprehension with filtering
data = {"apple": 1.20, "banana": 0.50, "cherry": 2.00, "date": 1.50}
# Filter items over $1
expensive = {item: price for item, price in data.items() if price > 1}
print(expensive)  # {'apple': 1.2, 'cherry': 2.0, 'date': 1.5}

# Example 7: Transpose a matrix
matrix = [[1, 2, 3], [4, 5, 6]]
transposed = [[row[i] for row in matrix] for i in range(len(matrix[0]))]
print(transposed)  # [[1, 4], [2, 5], [3, 6]]

# Example 8: Set comprehension with filtering
words = ["apple", "banana", "apricot", "cherry", "blueberry"]
# Get all unique first letters from words starting with 'a' or 'b'
first_letters = {word[0] for word in words if word[0] in ['a', 'b']}
print(first_letters)  # {'a', 'b'}

# Example 9: Nested list comprehension (creating 2D structure)
# Create a 3x3 multiplication table
multiplication_table = [[i * j for j in range(1, 4)] for i in range(1, 4)]
print(multiplication_table)
# [[1, 2, 3], [2, 4, 6], [3, 6, 9]]

# Example 10: Complex real-world example
products = [
    {"name": "Laptop", "category": "Electronics", "price": 1200},
    {"name": "Mouse", "category": "Electronics", "price": 25},
    {"name": "Desk", "category": "Furniture", "price": 300},
    {"name": "Chair", "category": "Furniture", "price": 150},
]
# Get products by category
by_category = {
    category: [p["name"] for p in products if p["category"] == category]
    for category in set(p["category"] for p in products)
}
print(by_category)
# {'Electronics': ['Laptop', 'Mouse'], 'Furniture': ['Desk', 'Chair']}
```

---

## Guided Practice

**Step 1:** Create a list of all pairs (x, y) where x is from [1, 2, 3] and y is from ['a', 'b'].
```python
pairs = [(x, y) for x in [1, 2, 3] for y in ['a', 'b']]
print(pairs)
# Should print: [(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b'), (3, 'a'), (3, 'b')]
```

**Step 2:** Flatten this nested list: `[[1, 2], [3, 4], [5, 6]]`
```python
nested = [[1, 2], [3, 4], [5, 6]]
flattened = [x for row in nested for x in row]
print(flattened)
# Should print: [1, 2, 3, 4, 5, 6]
```

**Step 3:** Create a dictionary that maps numbers to their squares, but only for even numbers from 1-10.
```python
squares = {x: x ** 2 for x in range(1, 11) if x % 2 == 0}
print(squares)
# Should print: {2: 4, 4: 16, 6: 36, 8: 64, 10: 100}
```

**Step 4:** Get all even numbers from a 3x3 matrix.
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
evens = [x for row in matrix for x in row if x % 2 == 0]
print(evens)
# Should print: [2, 4, 6, 8]
```

**Step 5:** Create a dictionary from a list of tuples (name, score) that maps names to scores, but only includes scores >= 80.
```python
data = [("Alice", 85), ("Bob", 75), ("Charlie", 90), ("Diana", 78)]
high_scores = {name: score for name, score in data if score >= 80}
print(high_scores)
# Should print: {'Alice': 85, 'Charlie': 90}
```

---

## Practice Problems

**Beginner:** Write a list comprehension that creates pairs of (number, squared) for numbers 1-5.

**Intermediate:** Create a list of only the even numbers from a list of lists: `[[1, 2, 3], [4, 5, 6], [7, 8, 9]]`

**Challenge:** Create a dictionary that groups products by category from a list of product dictionaries. (Advanced grouping problem!)

<details>
<summary>💡 Hints</summary>
- For Beginner: Use two expressions in the tuple: `[(x, x ** 2) for x in range(1, 6)]`
- For Intermediate: Use nested loop: `[x for row in lists for x in row if ...]`
- For Challenge: Consider using nested comprehension within dict comprehension
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
result = [(x, x ** 2) for x in range(1, 6)]
print(result)  # Output: [(1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]

# Intermediate
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
evens = [x for row in matrix for x in row if x % 2 == 0]
print(evens)  # Output: [2, 4, 6, 8]

# Challenge
products = [
    {"name": "Apple", "category": "Fruit"},
    {"name": "Carrot", "category": "Vegetable"},
    {"name": "Banana", "category": "Fruit"},
]
by_category = {
    category: [p["name"] for p in products if p["category"] == category]
    for category in set(p["category"] for p in products)
}
print(by_category)
# Output: {'Fruit': ['Apple', 'Banana'], 'Vegetable': ['Carrot']}
```
</details>
