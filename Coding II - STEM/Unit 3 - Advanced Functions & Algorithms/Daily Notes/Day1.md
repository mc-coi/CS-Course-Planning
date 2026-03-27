# Day 1: Lambda Functions
**Learning Target:** I can write and use lambda functions for short, anonymous functions.

### Key Concepts
**Lambda functions** are small anonymous functions. Syntax: `lambda arguments: expression`

Use lambdas for simple operations where defining a full function is overkill.

### Code Examples
```python
# Basic lambda
square = lambda x: x ** 2
print(square(5))  # 25

# Lambda with multiple arguments
add = lambda x, y: x + y
print(add(3, 4))  # 7

# Lambda with conditionals
max_val = lambda a, b: a if a > b else b
print(max_val(10, 20))  # 20

# Lambdas in sorted()
students = [("Alice", 95), ("Bob", 87), ("Charlie", 92)]
sorted_by_grade = sorted(students, key=lambda s: s[1])
print(sorted_by_grade)

# Lambdas with lists
numbers = [1, 2, 3, 4, 5]
doubled = list(map(lambda x: x * 2, numbers))
print(doubled)  # [2, 4, 6, 8, 10]
```

### Guided Practice
Write lambdas for: double a number, check if even, convert Celsius to Fahrenheit.

### Practice Problems
**Problem 1 — Beginner:** Write a lambda that returns the absolute value of a number.

**Problem 2 — Intermediate:** Use a lambda with sorted() to sort a list of dictionaries by a specific key.

**Problem 3 — Challenge:** Write a lambda that returns the maximum of three numbers.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
abs_val = lambda x: x if x >= 0 else -x

# Problem 2
people = [{"name": "Alice", "age": 30}, {"name": "Bob", "age": 25}]
sorted_people = sorted(people, key=lambda p: p["age"])

# Problem 3
max_three = lambda a, b, c: max(a, max(b, c))
```
</details>

---

---
