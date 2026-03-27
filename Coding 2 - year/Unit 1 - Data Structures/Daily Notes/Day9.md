# Day 9: Tuples & Immutability

**Learning Target:** I can create tuples and understand why immutability matters.

---

## Key Concepts

**Tuples** are **ordered, immutable collections** similar to lists, but you cannot change them after creation. They use parentheses `()` instead of square brackets `[]`.

**Immutability** means once created, you cannot add, remove, or modify elements. This makes tuples safer for data that shouldn't change and faster than lists.

**When to use tuples:** Use tuples when you want to ensure data stays constant, when you need to use them as dictionary keys, or when you want a small performance boost.

**Empty tuple syntax:** `()` creates an empty tuple; `(1,)` creates a 1-element tuple (the comma is required!).

---

## Code Examples

```python
# Creating tuples
empty_tuple = ()
single = (42,)        # Note the comma!
pair = (1, 2)
triple = (1, 2, 3)

# Tuple packing
coordinates = (10, 20)
person = ("Alice", 15, "Math")

# Accessing elements (like lists)
print(coordinates[0])  # 10
print(person[-1])      # "Math"

# Slicing (like lists)
print(triple[1:])      # (2, 3)

# Why immutable?
try:
    single[0] = 100    # TypeError: 'tuple' object does not support item assignment
except TypeError as e:
    print(f"Error: {e}")

# Unpacking (very Pythonic!)
x, y = coordinates
print(f"x={x}, y={y}")  # x=10, y=20

# Unpacking with multiple values
name, age, subject = person
print(f"{name} is {age} in {subject}")

# Unpacking with *
first, *middle, last = (1, 2, 3, 4, 5)
print(first, middle, last)  # 1 [2, 3, 4] 5

# Using in loops
for item in triple:
    print(item)

# Tuples as dictionary keys (lists cannot!)
locations = {(0, 0): "origin", (1, 1): "diagonal"}
print(locations[(0, 0)])  # "origin"
```

---

## Guided Practice

**Activity: Working with Coordinates and Records**

1. Create a tuple for a point: `point = (5, 10)`
2. Unpack it into x and y variables
3. Create a tuple for a person: `person = ("Dave", 16, "Chemistry")`
4. Unpack it and print each element
5. Create a dictionary using tuples as keys
6. Try to modify a tuple element and catch the error gracefully
7. Create a function that returns a tuple of results

---

## Practice Problems

**Beginner:** Create a tuple with 3 elements and unpack it into 3 variables. Print the variables.

**Intermediate:** Write a function `swap(a, b)` that uses tuple packing/unpacking to swap two values and return them in a tuple.

**Challenge:** Write a function `find_extremes(numbers)` that returns a tuple of (min, max, average) for a list of numbers.

<details>
<summary>💡 Hints</summary>

- Beginner: Use the syntax `a, b, c = my_tuple`
- Intermediate: Pack the swapped values into a tuple: `return (b, a)`
- Challenge: Use built-in min(), max(), and sum() functions

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Beginner
my_tuple = (10, 20, 30)
a, b, c = my_tuple
print(a, b, c)

# Intermediate
def swap(a, b):
    return (b, a)

# Challenge
def find_extremes(numbers):
    return (min(numbers), max(numbers), sum(numbers) / len(numbers))
```

</details>
