# Day 2: Passing Functions as Arguments

**Learning Target:** I can pass functions (including lambdas) as arguments to other functions and use them to customize behavior.

---

## Key Concepts

**Functions as First-Class Objects** — In Python, functions are objects just like integers or strings. You can assign them to variables, pass them to other functions, and return them from functions.

**Callback Function** — A function passed to another function to be called later. The receiving function "calls back" to your function at an appropriate time.

**Higher-Order Function** — A function that takes one or more functions as arguments, or returns a function. Examples: `sorted()`, `map()`, `filter()`.

**Key Point:** When passing a function, don't include parentheses! `sorted(items, key=len)` passes the `len` function itself, while `sorted(items, key=len())` tries to call `len()` immediately (which will error).

---

## Code Examples

```python
# Example 1: sorted() with a function as key
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
sorted_numbers = sorted(numbers)
print(sorted_numbers)  # Output: [1, 1, 2, 3, 4, 5, 6, 9]

# Sort by absolute value
numbers_with_negatives = [3, -5, 2, -1, 4]
sorted_by_absolute = sorted(numbers_with_negatives, key=abs)
print(sorted_by_absolute)  # Output: [-1, 2, 3, -5, 4]

# Example 2: Custom function as callback
def apply_operation(x, y, operation):
    """Takes two numbers and a function, applies the function to them"""
    return operation(x, y)

result = apply_operation(10, 5, lambda a, b: a + b)
print(result)  # Output: 15

result = apply_operation(10, 5, lambda a, b: a * b)
print(result)  # Output: 50

# Example 3: Sorting strings by custom criteria
words = ["banana", "pie", "zoo", "a"]
# Sort by length
sorted_by_length = sorted(words, key=len)
print(sorted_by_length)  # Output: ['a', 'pie', 'zoo', 'banana']

# Sort by last character
sorted_by_last = sorted(words, key=lambda w: w[-1])
print(sorted_by_last)  # Output: ['banana', 'pie', 'a', 'zoo']

# Example 4: Creating a function that uses a callback
def repeat_operation(func, value, times):
    """Repeatedly apply a function"""
    result = value
    for _ in range(times):
        result = func(result)
    return result

double = lambda x: x * 2
final_value = repeat_operation(double, 2, 5)
print(final_value)  # Output: 64 (2 -> 4 -> 8 -> 16 -> 32 -> 64)

# Example 5: Sorting complex data structures
students = [
    {"name": "Alice", "grade": 11, "gpa": 3.8},
    {"name": "Bob", "grade": 10, "gpa": 3.5},
    {"name": "Charlie", "grade": 11, "gpa": 3.9},
]

# Sort by GPA
by_gpa = sorted(students, key=lambda student: student["gpa"])
print(by_gpa[0]["name"])  # Output: Bob

# Sort by name
by_name = sorted(students, key=lambda s: s["name"])
print(by_name[0]["name"])  # Output: Alice
```

---

## Guided Practice

**Step 1:** Create a function called `process_numbers` that takes a list of numbers and a function, then applies the function to each number and returns the list of results.
```python
def process_numbers(numbers, func):
    return [func(num) for num in numbers]

result = process_numbers([1, 2, 3], lambda x: x * 2)
print(result)  # Should print: [2, 4, 6]
```

**Step 2:** Use the `sorted()` function to sort this list of dictionaries by the "age" key:
```python
people = [
    {"name": "Emma", "age": 25},
    {"name": "David", "age": 20},
    {"name": "Charlie", "age": 23},
]
sorted_people = sorted(people, key=lambda p: p["age"])
print(sorted_people[0]["name"])  # Should print: David
```

**Step 3:** Write a function that takes a list and a comparison function, and returns only items that pass the comparison.
```python
def filter_by_condition(items, condition):
    return [item for item in items if condition(item)]

numbers = [1, 5, 3, 8, 2, 9, 4]
evens = filter_by_condition(numbers, lambda x: x % 2 == 0)
print(evens)  # Should print: [8, 2, 4]
```

**Step 4:** Sort a list of tuples `(name, score)` by score in descending order.
```python
scores = [("Alice", 85), ("Bob", 92), ("Charlie", 78)]
sorted_scores = sorted(scores, key=lambda s: s[1], reverse=True)
print(sorted_scores[0])  # Should print: ('Bob', 92)
```

---

## Practice Problems

**Beginner:** Write a function called `apply_twice` that takes a function and a value, applies the function to the value twice, and returns the result. Test with `apply_twice(lambda x: x + 5, 10)` (should return 20).

**Intermediate:** Write a function called `conditional_map` that takes a list, a condition function, and a transformation function. It should apply the transformation only to items that pass the condition.

**Challenge:** Sort a list of objects by multiple criteria. For example, sort students by grade (descending), then by name (ascending) within each grade. (Hint: Tuples can be compared element-by-element!)

<details>
<summary>💡 Hints</summary>
- For Beginner: Apply the function once, then apply it to the result
- For Intermediate: Use a list comprehension with `if condition(item)`
- For Challenge: Return a tuple from the lambda: `lambda s: (s["grade"], s["name"])`
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def apply_twice(func, value):
    return func(func(value))

result = apply_twice(lambda x: x + 5, 10)
print(result)  # Output: 20

# Intermediate
def conditional_map(items, condition, transform):
    return [transform(item) for item in items if condition(item)]

numbers = [1, 2, 3, 4, 5, 6]
result = conditional_map(numbers, lambda x: x > 2, lambda x: x * 10)
print(result)  # Output: [30, 40, 50, 60]

# Challenge
students = [
    {"name": "Alice", "grade": 11},
    {"name": "Bob", "grade": 10},
    {"name": "Charlie", "grade": 11},
]
sorted_students = sorted(students, key=lambda s: (-s["grade"], s["name"]))
# Use negative for descending grade, normal for ascending name
```
</details>
