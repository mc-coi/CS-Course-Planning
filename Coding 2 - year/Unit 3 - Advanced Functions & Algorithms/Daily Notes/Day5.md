# Day 5: Higher-Order Functions - zip() and reduce()

**Learning Target:** I can use zip() to combine sequences and reduce() to accumulate values from an iterable.

---

## Key Concepts

**zip(iterable1, iterable2, ...)** — Combines multiple iterables element-by-element. Returns an iterator of tuples, where each tuple contains one element from each input iterable. Stops when the shortest iterable is exhausted.

**reduce(function, iterable)** — Applies a function cumulatively to items in an iterable to reduce it to a single value. Requires `from functools import reduce`.

**Accumulator** — In reduce(), the intermediate result that gets passed forward along with the next value.

**reduce() workflow:**
1. Apply function to first two elements → result
2. Apply function to result and third element → new result
3. Continue until all elements are processed

---

## Code Examples

```python
# Example 1: zip() - combine two lists
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 28]
combined = zip(names, ages)
print(list(combined))
# Output: [('Alice', 25), ('Bob', 30), ('Charlie', 28)]

# Example 2: zip() with unequal lengths
list1 = [1, 2, 3, 4]
list2 = ['a', 'b', 'c']
combined = zip(list1, list2)
print(list(combined))
# Output: [(1, 'a'), (2, 'b'), (3, 'c')]  -- stops at shortest

# Example 3: Unpacking zip() in a loop
names = ["Alice", "Bob"]
scores = [95, 87]
for name, score in zip(names, scores):
    print(f"{name}: {score}")
# Output:
# Alice: 95
# Bob: 87

# Example 4: zip() with multiple iterables
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']
list3 = [10, 20, 30]
combined = list(zip(list1, list2, list3))
print(combined)
# Output: [(1, 'a', 10), (2, 'b', 20), (3, 'c', 30)]

# Example 5: reduce() - sum all numbers
from functools import reduce

numbers = [1, 2, 3, 4, 5]
total = reduce(lambda x, y: x + y, numbers)
print(total)  # Output: 15

# Example 6: reduce() - find product
numbers = [1, 2, 3, 4]
product = reduce(lambda x, y: x * y, numbers)
print(product)  # Output: 24

# Example 7: reduce() - find maximum
numbers = [3, 7, 2, 9, 1, 5]
maximum = reduce(lambda x, y: x if x > y else y, numbers)
print(maximum)  # Output: 9

# Example 8: reduce() with initial value
from functools import reduce

numbers = [1, 2, 3, 4, 5]
total = reduce(lambda x, y: x + y, numbers, 0)  # 0 is initial value
print(total)  # Output: 15

# With initial value, it's safer (works on empty lists)
empty = []
total = reduce(lambda x, y: x + y, empty, 0)
print(total)  # Output: 0

# Example 9: Real-world example - calculate purchase total
items = [
    {"name": "Book", "price": 15, "quantity": 2},
    {"name": "Pen", "price": 2, "quantity": 5},
    {"name": "Notebook", "price": 4, "quantity": 3},
]

# Extract prices with quantities
prices = map(lambda item: item["price"] * item["quantity"], items)
total_cost = reduce(lambda x, y: x + y, prices)
print(total_cost)  # Output: 53

# Example 10: Using zip() to create a dictionary
keys = ["name", "age", "city"]
values = ["Alice", 25, "New York"]
person = dict(zip(keys, values))
print(person)
# Output: {'name': 'Alice', 'age': 25, 'city': 'New York'}
```

---

## Guided Practice

**Step 1:** Use `zip()` to pair names with scores.
```python
names = ["Alex", "Jordan", "Casey"]
scores = [88, 92, 85]
pairs = list(zip(names, scores))
print(pairs)  # Should print: [('Alex', 88), ('Jordan', 92), ('Casey', 85)]
```

**Step 2:** Use `reduce()` to find the sum of a list of numbers.
```python
from functools import reduce

numbers = [10, 20, 30, 40]
total = reduce(lambda x, y: x + y, numbers)
print(total)  # Should print: 100
```

**Step 3:** Use `zip()` in a loop to print names and their corresponding grades.
```python
names = ["Alice", "Bob", "Charlie"]
grades = ["A", "B", "A"]
for name, grade in zip(names, grades):
    print(f"{name}: {grade}")
# Should print:
# Alice: A
# Bob: B
# Charlie: A
```

**Step 4:** Use `reduce()` to find the maximum value in a list.
```python
from functools import reduce

numbers = [5, 2, 9, 1, 7]
max_value = reduce(lambda x, y: x if x > y else y, numbers)
print(max_value)  # Should print: 9
```

**Step 5:** Create a dictionary from two lists using `zip()` and `dict()`.
```python
products = ["apple", "banana", "orange"]
prices = [1.20, 0.50, 0.75]
price_dict = dict(zip(products, prices))
print(price_dict)
# Should print: {'apple': 1.2, 'banana': 0.5, 'orange': 0.75}
```

---

## Practice Problems

**Beginner:** Use `zip()` to combine a list of student names with a list of their test scores, then iterate through the pairs and print them.

**Intermediate:** Use `reduce()` to concatenate all strings in a list into one long string with spaces between words.

**Challenge:** Create a function that takes two lists (keys and values) and returns a dictionary. Handle the case where lists are different lengths gracefully.

<details>
<summary>💡 Hints</summary>
- For Beginner: Use `zip()` to pair them, then iterate with `for name, score in pairs`
- For Intermediate: Use `lambda x, y: x + " " + y` with reduce
- For Challenge: Use `zip()` and `dict()`, but consider what happens with different lengths
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
names = ["Alex", "Jordan", "Casey"]
scores = [88, 92, 85]
pairs = list(zip(names, scores))
for name, score in pairs:
    print(f"{name}: {score}")

# Intermediate
from functools import reduce

words = ["hello", "world", "python"]
sentence = reduce(lambda x, y: x + " " + y, words)
print(sentence)  # Output: hello world python

# Challenge
def combine_lists(keys, values):
    return dict(zip(keys, values))

result = combine_lists(["a", "b", "c"], [1, 2, 3, 4])
print(result)  # Output: {'a': 1, 'b': 2, 'c': 3}
# Note: Extra value (4) is ignored because zip stops at shortest
```
</details>
