# Day 1: Lambda Functions and Anonymous Functions

**Learning Target:** I can write and use lambda functions to create simple, anonymous functions for one-time or callback operations.

---

## Key Concepts

**Lambda Functions** are small, unnamed functions created with the `lambda` keyword. They're useful when you need a quick function without formally defining it with `def`. Think of them as "throwaway" functions—perfect for passing to other functions or filtering data.

**Anonymous Function** means a function without a name. Lambda functions are always anonymous. They're stored in variables or passed directly to other functions.

**Single Expression** — Lambda functions can only contain ONE expression (no multi-line code or statements like loops or if-blocks). The result of that expression is automatically returned.

**When to use lambdas:**
- Passing a function as an argument to another function
- Simple, one-off operations
- When the logic is straightforward and fits on one line

**When NOT to use lambdas:**
- Complex logic (use `def` instead for readability)
- When you need multiple statements or loops

---

## Code Examples

```python
# Basic lambda syntax
# lambda arguments: expression

# Example 1: Simple lambda that adds two numbers
add = lambda x, y: x + y
print(add(3, 5))  # Output: 8

# Example 2: Lambda with single argument
square = lambda x: x ** 2
print(square(4))  # Output: 16

# Example 3: Lambda with multiple arguments
greet = lambda name, age: f"{name} is {age} years old"
print(greet("Alice", 15))  # Output: Alice is 15 years old

# Example 4: Lambda in a list (sorting by custom criteria)
students = [("Bob", 85), ("Alice", 92), ("Charlie", 78)]
# Sort by score (second element)
sorted_students = sorted(students, key=lambda student: student[1])
print(sorted_students)
# Output: [('Charlie', 78), ('Bob', 85), ('Alice', 92)]

# Example 5: Lambda with conditional expression
is_even = lambda x: "even" if x % 2 == 0 else "odd"
print(is_even(7))  # Output: odd
```

---

## Guided Practice

**Step 1:** Write a lambda function that takes a single number and returns it multiplied by 2.
```python
double = lambda x: x * 2
print(double(10))  # Should print: 20
```

**Step 2:** Write a lambda function that takes two strings and concatenates them with a space between.
```python
combine = lambda s1, s2: s1 + " " + s2
print(combine("Hello", "World"))  # Should print: Hello World
```

**Step 3:** Use a lambda with the `sorted()` function to sort a list of words by their length.
```python
words = ["python", "code", "algorithm"]
sorted_words = sorted(words, key=lambda word: len(word))
print(sorted_words)  # Should print: ['code', 'python', 'algorithm']
```

**Step 4:** Write a lambda that checks if a number is positive and returns a boolean.
```python
is_positive = lambda x: x > 0
print(is_positive(-5))   # Should print: False
print(is_positive(10))   # Should print: True
```

**Step 5:** Create a lambda that calculates the area of a rectangle given width and height.
```python
area = lambda w, h: w * h
print(area(5, 7))  # Should print: 35
```

---

## Practice Problems

**Beginner:** Write a lambda function called `add_ten` that takes a number and returns the number plus 10. Test it with the value 5.

**Intermediate:** Write a lambda function that takes a list of numbers and use it to sort a list of tuples by their first element. Example: `[(3, "a"), (1, "b"), (2, "c")]` should become `[(1, "b"), (2, "c"), (3, "a")]`.

**Challenge:** Write a lambda function that takes a dictionary and filters it to only return keys with values greater than 50. (Hint: Use this with a built-in function you'll learn soon!)

<details>
<summary>💡 Hints</summary>
- For Beginner: Store the lambda in a variable and call it
- For Intermediate: Use `sorted()` with `key=lambda`; focus on the first element of each tuple
- For Challenge: Think about what you'll need from the dictionary (keys, values, items)
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
add_ten = lambda x: x + 10
print(add_ten(5))  # Output: 15

# Intermediate
tuples = [(3, "a"), (1, "b"), (2, "c")]
sorted_tuples = sorted(tuples, key=lambda t: t[0])
print(sorted_tuples)  # Output: [(1, 'b'), (2, 'c'), (3, 'a')]

# Challenge (preview of next topic!)
data = {"apple": 45, "banana": 80, "cherry": 60}
# This is a sneak peek at dictionary filtering - we'll learn the proper approach tomorrow!
result = {k: v for k, v in data.items() if v > 50}
print(result)  # Output: {'banana': 80, 'cherry': 60}
```
</details>
