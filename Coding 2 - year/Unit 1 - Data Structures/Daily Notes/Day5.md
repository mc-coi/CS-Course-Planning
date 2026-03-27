# Day 5: List Comprehensions

**Learning Target:** I can create lists concisely using list comprehension syntax.

---

## Key Concepts

**List comprehension** is a compact way to create a new list by applying an expression to each element of an existing list. The syntax is `[expression for item in iterable]`.

**Why use list comprehensions:** They are more readable, more efficient, and more Pythonic than writing loops to build lists. They also allow filtering with conditions.

**Syntax variations:**
- Basic: `[expr for item in list]`
- With condition: `[expr for item in list if condition]`
- With nested loops: `[expr for item in list1 for item2 in list2]`

---

## Code Examples

```python
# Basic list comprehension
numbers = [1, 2, 3, 4, 5]
squared = [x**2 for x in numbers]
print(squared)  # [1, 4, 9, 16, 25]

# Equivalent traditional way
squared_traditional = []
for x in numbers:
    squared_traditional.append(x**2)

# With condition (filter)
numbers = [1, 2, 3, 4, 5, 6, 7, 8]
evens = [x for x in numbers if x % 2 == 0]
print(evens)  # [2, 4, 6, 8]

# Complex expression
words = ["python", "java", "go"]
lengths = [len(word) for word in words]
print(lengths)  # [6, 4, 2]

# With string operations
words = ["hello", "world"]
upper = [word.upper() for word in words]
print(upper)  # ['HELLO', 'WORLD']

# Nested list comprehension (creating a grid)
grid = [[0 for _ in range(3)] for _ in range(3)]
print(grid)  # [[0, 0, 0], [0, 0, 0], [0, 0, 0]]
```

---

## Guided Practice

**Activity: Transform Data with List Comprehension**

1. Create a list of student scores: `scores = [85, 92, 78, 95, 88, 91]`
2. Use list comprehension to add 5 bonus points to each score
3. Use list comprehension to create a list of only passing grades (≥80)
4. Use list comprehension to create a list of letter grades based on scores
5. Compare your comprehensions to how you'd write them with loops

---

## Practice Problems

**Beginner:** Use list comprehension to create a list of integers from 1 to 10 and another that contains the double of each.

**Intermediate:** Given `words = ["apple", "banana", "cherry", "date"]`, use list comprehension to create a list of tuples where each tuple is (word, length). For example, `[("apple", 5), ("banana", 6), ...]`

**Challenge:** Create a list comprehension that generates all pairs (i, j) where i and j are from 1 to 4 and i < j. The result should be `[(1, 2), (1, 3), (1, 4), (2, 3), (2, 4), (3, 4)]`.

<details>
<summary>💡 Hints</summary>

- Beginner: Use [x for x in range(1, 11)] and [2*x for x in range(1, 11)]
- Intermediate: Use (word, len(word)) as the expression
- Challenge: Use nested for loops in your comprehension with an if condition

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Beginner
numbers = [x for x in range(1, 11)]
doubled = [2*x for x in range(1, 11)]

# Intermediate
words = ["apple", "banana", "cherry", "date"]
pairs = [(word, len(word)) for word in words]

# Challenge
pairs = [(i, j) for i in range(1, 5) for j in range(1, 5) if i < j]
```

</details>
