# Day 7: Python Built-in Sorting
**Learning Target:** I can use Python's efficient sorted() and list.sort() with key parameters.

### Key Concepts
Python uses Timsort (hybrid of merge+insertion) — very efficient
Always use built-in unless learning algorithms

`sorted()` returns new list
`list.sort()` modifies in place
`key` parameter for custom sorting

### Code Examples
```python
numbers = [64, 34, 25, 12, 22, 11, 90]

# Basic sorting
sorted_nums = sorted(numbers)
numbers.sort()  # In-place

# Reverse sorting
sorted_desc = sorted(numbers, reverse=True)

# Sorting strings
names = ["zach", "alice", "bob"]
sorted_names = sorted(names)  # Alphabetical

# Custom key
students = [("Alice", 95), ("Bob", 87), ("Charlie", 92)]
by_grade = sorted(students, key=lambda s: s[1])

# Dictionary sorting
people = [{"name": "Alice", "age": 30}, {"name": "Bob", "age": 25}]
by_age = sorted(people, key=lambda p: p["age"])
```

### Guided Practice
Sort various data structures using key parameter.

### Practice Problems
**Problem 1 — Beginner:** Sort a list of numbers.

**Problem 2 — Intermediate:** Sort complex objects with key.

**Problem 3 — Challenge:** Multi-level sorting (multiple keys).

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 3
students = [("Alice", 95, 10), ("Bob", 87, 9)]
# Sort by grade (desc), then by ID
sorted(students, key=lambda s: (-s[1], s[2]))
```
</details>

---

---
