# Day 6: Advanced List Techniques

**Learning Target:** I can use advanced list operations like `zip()`, `map()`, and functional approaches.

---

## Key Concepts

**`zip()`** combines multiple iterables element-by-element, creating pairs (or tuples of n elements if n iterables are zipped).

**`map()`** applies a function to every element of an iterable, returning a new iterable.

**`filter()`** keeps only elements that satisfy a condition.

**`any()` and `all()`** return True if any or all elements satisfy a condition.

These functional programming tools make your code more expressive and Pythonic.

---

## Code Examples

```python
# zip() - combining lists
names = ["Alice", "Bob", "Charlie"]
ages = [15, 16, 15]
grades = ["A", "B", "C"]

# Zip creates tuples of paired elements
pairs = list(zip(names, ages, grades))
print(pairs)  # [('Alice', 15, 'A'), ('Bob', 16, 'B'), ('Charlie', 15, 'C')]

# Zip in a loop
for name, age, grade in zip(names, ages, grades):
    print(f"{name} is {age} and has grade {grade}")

# map() - applying a function
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# filter() - keeping elements that match a condition
numbers = [1, 2, 3, 4, 5, 6, 7, 8]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6, 8]

# any() and all()
nums = [1, 2, 3, 4, 5]
print(any(x > 4 for x in nums))   # True (at least one > 4)
print(all(x > 0 for x in nums))   # True (all are > 0)

# Unzipping with zip
pairs = [('Alice', 15), ('Bob', 16), ('Charlie', 15)]
names, ages = zip(*pairs)
print(names)  # ('Alice', 'Bob', 'Charlie')
print(ages)   # (15, 16, 15)
```

---

## Guided Practice

**Activity: Working with Parallel Data**

1. Create three lists: student names, test scores, and assignment grades
2. Use `zip()` to combine them and print them nicely formatted
3. Use `map()` to increase all test scores by a fixed percentage
4. Use `filter()` to find students with test scores above 85
5. Use `all()` to check if all students passed (score ≥ 70)

---

## Practice Problems

**Beginner:** Given two lists `a = [1, 2, 3]` and `b = [4, 5, 6]`, use `zip()` to combine them into a list of tuples.

**Intermediate:** Write a function that takes a list of numbers and returns a new list where each number is tripled, using `map()` (or list comprehension).

**Challenge:** Write a function `transpose(matrix)` that takes a 2D list (list of lists) and returns the transposed version. For example, `[[1, 2, 3], [4, 5, 6]]` becomes `[[1, 4], [2, 5], [3, 6]]`. (Hint: use `zip()`)

<details>
<summary>💡 Hints</summary>

- Beginner: list(zip(a, b)) converts the zip object to a list
- Intermediate: Define a lambda function or use a named function with map()
- Challenge: zip(*matrix) unpacks the matrix rows

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Beginner
a = [1, 2, 3]
b = [4, 5, 6]
result = list(zip(a, b))  # [(1, 4), (2, 5), (3, 6)]

# Intermediate
def triple_numbers(numbers):
    return list(map(lambda x: x * 3, numbers))

# Or with list comprehension:
def triple_numbers(numbers):
    return [x * 3 for x in numbers]

# Challenge
def transpose(matrix):
    return [list(row) for row in zip(*matrix)]
```

</details>
