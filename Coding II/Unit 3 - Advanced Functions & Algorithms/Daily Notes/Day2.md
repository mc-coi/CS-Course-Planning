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

---
