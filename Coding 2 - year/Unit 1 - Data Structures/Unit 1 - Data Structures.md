# Unit 1: Data Structures

> Master the fundamental data structures in Python and learn when to use each for different problems.

---

## Unit Overview

- **Duration:** 22 days (~4.5 weeks)
- **Standard:** 9-12.CCI.2 — Use and manipulate collection data structures
- **Big Idea:** Choosing the right data structure is fundamental to writing efficient, clean code. Different structures excel at different tasks.

### Key Concepts
- Lists: ordered, mutable, indexed access
- Tuples: ordered, immutable, hashable
- Dictionaries: unordered key-value pairs, fast lookup
- Sets: unordered unique elements, fast membership testing
- Nested structures: combining data structures for complex data

### Learning Targets
- I can create, access, and modify lists using multiple methods
- I can use list comprehensions to transform data concisely
- I can work with 2D lists and nested data structures
- I can create and unpack tuples and use them as dictionary keys
- I can create dictionaries, access values safely, and iterate effectively
- I can use sets for efficient membership testing and set operations
- I can choose appropriate data structures for different problems
- I can design practical systems using multiple data structures

---

# Day 1: Introduction to Lists & Creation

**Learning Target:** I can create and initialize lists in Python using multiple methods.

---

## Key Concepts

**Lists** are **ordered, mutable collections** that can store multiple values of any type. Think of a list like a numbered shopping list where you can read, modify, and reorder items.

**Mutability** means you can change the list after creating it (add, remove, or modify items). This distinguishes lists from other data structures you'll encounter later.

**Why lists matter:** Lists are one of the most fundamental data structures in programming. They let you store related data together and process it systematically. In real life, you use lists constantly: to-do lists, grade lists, inventory lists, etc.

---

## Code Examples

```python
# Creating lists with square brackets and commas
fruits = ["apple", "banana", "cherry"]
print(fruits)  # ['apple', 'banana', 'cherry']

# Lists can contain mixed types
mixed = [1, "hello", 3.14, True]
print(mixed)  # [1, 'hello', 3.14, True]

# Creating an empty list
empty_list = []
print(empty_list)  # []

# Using the list() constructor
numbers = list(range(1, 6))
print(numbers)  # [1, 2, 3, 4, 5]

# Creating a list of the same value repeated
zeros = [0] * 5
print(zeros)  # [0, 0, 0, 0, 0]
```

---

## Guided Practice

**Activity: Build a Student List**

1. Create a list called `students` with 4 classmates' names
2. Print the list to verify it was created correctly
3. Create an empty list called `attendance` that you'll fill later
4. Create a list called `test_scores` with 5 random numbers between 0-100
5. Print all three lists and describe what each one represents

---

## Practice Problems

**Beginner:** Create a list of your 5 favorite movies and print it.

**Intermediate:** Create three separate lists (names, ages, grades) that represent data for 3 students. Then print a statement that uses data from all three lists: "Alice is 15 years old and has a B grade."

**Challenge:** Write a function `create_multiplication_table(n)` that returns a list of the first 10 multiples of `n`.

---

# Day 2: List Indexing & Accessing Elements

**Learning Target:** I can access and modify individual list elements using positive and negative indexing.

---

## Key Concepts

**Indexing** is how you retrieve a specific element from a list using its position. In Python, **indexing starts at 0**, not 1. The first element is at index 0, the second at index 1, and so on.

**Positive indexing** counts from the beginning: `list[0]`, `list[1]`, etc.

**Negative indexing** counts from the end: `list[-1]` gets the last element, `list[-2]` gets the second-to-last, etc.

**IndexError** occurs when you try to access an index that doesn't exist.

---

## Code Examples

```python
fruits = ["apple", "banana", "cherry", "date"]

# Positive indexing
print(fruits[0])   # "apple"
print(fruits[2])   # "cherry"

# Negative indexing
print(fruits[-1])  # "date"
print(fruits[-2])  # "cherry"

# Modifying elements
fruits[1] = "blueberry"

# Check list length
print(len(fruits))  # 4
```

---

# Day 3: List Slicing

**Learning Target:** I can use slice notation to extract subsets of a list.

---

## Key Concepts

**Slicing** creates a new list containing a subset of elements. Syntax: `list[start:stop:step]`
- **start:** beginning index (inclusive, defaults to 0)
- **stop:** ending index (exclusive, defaults to end)
- **step:** interval between elements (defaults to 1)

---

## Code Examples

```python
numbers = [10, 20, 30, 40, 50, 60, 70, 80]

# Basic slicing
print(numbers[0:3])    # [10, 20, 30]
print(numbers[2:5])    # [30, 40, 50]

# Omitting start or stop
print(numbers[:3])     # [10, 20, 30]
print(numbers[5:])     # [60, 70, 80]

# Using step
print(numbers[::2])    # [10, 30, 50, 70]

# Reversing
print(numbers[::-1])   # [80, 70, 60, 50, 40, 30, 20, 10]
```

---

# Day 4: List Methods & Iteration

**Learning Target:** I can use list methods and iterate through lists with loops.

---

## Key Concepts

**List methods** are functions that operate on lists:
- `.append(x)` — adds x to the end
- `.insert(i, x)` — inserts x at index i
- `.remove(x)` — removes the first occurrence of x
- `.pop(i)` — removes and returns element at index i
- `.extend(other_list)` — adds all elements from another list
- `.sort()` — sorts in-place
- `.reverse()` — reverses in-place

**Iteration** is looping through list elements. The for loop is the most Pythonic way.

---

## Code Examples

```python
# Append and extend
fruits = ["apple", "banana"]
fruits.append("cherry")
fruits.extend(["date", "fig"])

# Remove and pop
fruits.remove("banana")
last = fruits.pop()

# Count and index
numbers = [1, 2, 3, 2, 4, 2, 5]
print(numbers.count(2))         # 3
print(numbers.index(3))         # 2

# Iteration
for fruit in fruits:
    print(f"I like {fruit}")

# Iteration with index
for i, fruit in enumerate(fruits):
    print(f"Index {i}: {fruit}")
```

---

# Day 5: List Comprehensions

**Learning Target:** I can create lists concisely using list comprehension syntax.

---

## Key Concepts

**List comprehension** is a compact way to create a new list. Syntax: `[expression for item in iterable]`

They are more readable, more efficient, and more Pythonic than loops. Syntax variations:
- Basic: `[expr for item in list]`
- With condition: `[expr for item in list if condition]`
- Nested loops: `[expr for item in list1 for item2 in list2]`

---

## Code Examples

```python
# Basic list comprehension
numbers = [1, 2, 3, 4, 5]
squared = [x**2 for x in numbers]
print(squared)  # [1, 4, 9, 16, 25]

# With condition
evens = [x for x in numbers if x % 2 == 0]
print(evens)  # [2, 4]

# Complex expression
words = ["python", "java", "go"]
lengths = [len(word) for word in words]
print(lengths)  # [6, 4, 2]

# Nested comprehension
grid = [[0 for _ in range(3)] for _ in range(3)]
```

---

# Day 6: Advanced List Techniques

**Learning Target:** I can use advanced list operations like `zip()`, `map()`, and functional approaches.

---

## Key Concepts

**`zip()`** combines multiple iterables element-by-element.

**`map()`** applies a function to every element.

**`filter()`** keeps only elements that satisfy a condition.

**`any()` and `all()`** test conditions across elements.

---

## Code Examples

```python
# zip() - combining lists
names = ["Alice", "Bob", "Charlie"]
ages = [15, 16, 15]
for name, age in zip(names, ages):
    print(f"{name} is {age}")

# map() - applying a function
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))

# filter() - keeping elements
evens = list(filter(lambda x: x % 2 == 0, numbers))

# any() and all()
nums = [1, 2, 3, 4, 5]
print(any(x > 4 for x in nums))   # True
print(all(x > 0 for x in nums))   # True
```

---

# Day 7: 2D Lists & Nested Structures

**Learning Target:** I can create, access, and iterate through 2D lists (lists of lists).

---

## Key Concepts

**2D lists** (nested lists or matrices) are lists containing other lists. Useful for representing tabular data.

**Accessing elements** requires two indices: `matrix[i][j]` where i is row, j is column.

**Row-major order** (Python standard) stores data row-by-row.

---

## Code Examples

```python
# Creating a 2D list
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Accessing elements
print(matrix[0][0])  # 1
print(matrix[1][2])  # 6

# Creating 2D list of zeros
zeros = [[0 for _ in range(3)] for _ in range(3)]

# Iterating with indices
for i in range(len(matrix)):
    for j in range(len(matrix[i])):
        print(f"matrix[{i}][{j}] = {matrix[i][j]}")

# Using enumerate
for i, row in enumerate(matrix):
    for j, val in enumerate(row):
        print(f"({i}, {j}) -> {val}")
```

---

# Day 8: Nested Lists & Complex Data

**Learning Target:** I can work with deeply nested lists and represent complex data structures.

---

## Key Concepts

**Deeply nested lists** go beyond 2D—you can have lists of lists of lists, etc.

**Jagged arrays** have rows of different lengths.

**Flattening** converts nested lists into a single flat list.

---

## Code Examples

```python
# 2D representation
student_data = [
    ["Alice", [85, 92, 88]],
    ["Bob", [78, 81, 79]],
    ["Charlie", [95, 92, 98]]
]

print(student_data[0][0])      # "Alice"
print(student_data[0][1][1])   # 92

# Flattening
nested = [[1, 2], [3, 4], [5, 6]]
flat = [item for row in nested for item in row]
print(flat)  # [1, 2, 3, 4, 5, 6]

# Deep nesting
deep_nested = [[[1, 2], [3]], [[4, 5, 6]]]
flat_deep = [item for row in deep_nested for subrow in row for item in subrow]
```

---

# Day 9: Tuples & Immutability

**Learning Target:** I can create tuples and understand why immutability matters.

---

## Key Concepts

**Tuples** are **ordered, immutable collections** similar to lists but use parentheses `()`.

**Immutability** means once created, you cannot add, remove, or modify elements. This makes them safer and faster.

**When to use tuples:**
- When data shouldn't change
- When you need to use them as dictionary keys
- When you want a slight performance boost

---

## Code Examples

```python
# Creating tuples
empty = ()
single = (42,)           # Note the comma!
pair = (1, 2)

# Accessing elements
print(pair[0])   # 1
print(pair[-1])  # 2

# Unpacking
x, y = pair
print(f"x={x}, y={y}")

# Unpacking with *
first, *middle, last = (1, 2, 3, 4, 5)

# Using as dictionary key
locations = {(0, 0): "origin", (1, 1): "diagonal"}
```

---

# Day 10: Tuple Use Cases & Named Tuples

**Learning Target:** I can use tuples effectively in real-world scenarios and leverage named tuples for clarity.

---

## Key Concepts

**Tuple use cases:**
- Return multiple values from a function
- Use as dictionary keys
- Protect data from modification
- Iteration with unpacking

**Named tuples** combine tuple immutability with dictionary-like named access.

---

## Code Examples

```python
from collections import namedtuple

# Regular tuple vs named tuple
result = (42, "success", 0.95)
status_code, message, confidence = result

QueryResult = namedtuple('QueryResult', ['status_code', 'message', 'confidence'])
result = QueryResult(42, "success", 0.95)
print(result.status_code)   # 42

# Multiple return values
def divide_with_remainder(a, b):
    return (a // b, a % b)

quotient, remainder = divide_with_remainder(17, 5)

# Using tuples as dict keys
graph = {
    (0, 0): [(1, 0), (0, 1)],
    (1, 0): [(0, 0), (1, 1)]
}
```

---

# Day 11: Dictionaries — Creation & Access

**Learning Target:** I can create dictionaries and access values using keys.

---

## Key Concepts

**Dictionaries** are **unordered, mutable collections** that store key-value pairs. They use keys to access values, not numeric indices.

**Keys** must be unique and immutable (strings, numbers, tuples).

**When to use dictionaries:** Look up values by name rather than position.

---

## Code Examples

```python
# Creating dictionaries
empty_dict = {}
student = {"name": "Alice", "age": 15, "grade": "A"}

# Using dict() constructor
person = dict(name="Bob", age=16, city="NYC")

# Accessing values
print(student["name"])      # "Alice"
print(student.get("age"))   # 15
print(student.get("gpa", 3.5))  # 3.5 (default)

# Modifying values
student["age"] = 16
student["gpa"] = 3.8

# Checking existence
if "name" in student:
    print(f"Student name is {student['name']}")
```

---

# Day 12: Dictionary Methods & Iteration

**Learning Target:** I can use dictionary methods effectively and iterate through dictionaries.

---

## Key Concepts

**Dictionary methods:**
- `.keys()` — all keys
- `.values()` — all values
- `.items()` — key-value pairs
- `.pop(key)` — remove and return
- `.get(key, default)` — safe access
- `.update(dict)` — merge
- `.setdefault(key, default)` — set if missing
- `.clear()` — remove all

---

## Code Examples

```python
inventory = {"apples": 10, "bananas": 5, "oranges": 8}

# Iterate through keys
for fruit in inventory:
    print(f"{fruit}: {inventory[fruit]}")

# Iterate through values
for count in inventory.values():
    print(count)

# Iterate through key-value pairs (most Pythonic)
for fruit, count in inventory.items():
    print(f"{fruit}: {count}")

# .pop() - remove and get value
removed = inventory.pop("bananas")

# .setdefault()
inventory.setdefault("lemons", 3)

# .update() - merge
inventory.update({"kiwis": 2, "mangos": 4})
```

---

# Day 13: Nested Dictionaries & Complex Structures

**Learning Target:** I can work with nested dictionaries and represent complex hierarchical data.

---

## Key Concepts

**Nested dictionaries** contain other dictionaries as values. Perfect for hierarchical data.

**Access pattern:** Use chained brackets or `.get()` for safe access.

**When to nest:** Data with natural hierarchy (school → classes → students → grades).

---

## Code Examples

```python
# Nested dictionary
school = {
    "name": "Central High",
    "classes": {
        "Math": {
            "teacher": "Dr. Smith",
            "students": ["Alice", "Bob"]
        },
        "English": {
            "teacher": "Ms. Jones",
            "students": ["Alice", "David"]
        }
    }
}

# Accessing nested values
print(school["name"])
print(school["classes"]["Math"]["teacher"])

# Safe access
teacher = school.get("classes", {}).get("Math", {}).get("teacher", "Unknown")

# Iterating through nested dicts
for class_name, class_info in school["classes"].items():
    print(f"{class_name}: {class_info['teacher']}")
```

---

# Day 14: Dictionary Comprehensions & Advanced Techniques

**Learning Target:** I can create dictionaries concisely using comprehensions and advanced patterns.

---

## Key Concepts

**Dictionary comprehensions** create dictionaries in a single expression: `{key: value for item in iterable}`

**Advanced patterns:** defaultdict, Counter (from collections) for specialized behaviors.

---

## Code Examples

```python
# Basic dictionary comprehension
squares = {x: x**2 for x in range(5)}

# With condition
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}

# From list to dictionary
data = [("apple", 5), ("banana", 3)]
inventory = {fruit: count for fruit, count in data}

# Invert a dictionary
word_freq = {"hello": 5, "world": 3}
freq_word = {count: word for word, count in word_freq.items()}

# Using Counter
from collections import Counter
text = "hello world hello python"
word_counts = Counter(text.split())

# Using defaultdict
from collections import defaultdict
word_lists = defaultdict(list)
for word, length in [("cat", 3), ("dog", 3), ("bird", 4)]:
    word_lists[length].append(word)
```

---

# Day 15: Sets & Set Operations

**Learning Target:** I can use sets for efficient membership testing and set operations.

---

## Key Concepts

**Sets** are **unordered, mutable collections of unique elements**. Optimized for membership testing.

**Key properties:**
- No duplicates
- No indexing
- Efficient membership testing with `in` operator

**Set operations:** union, intersection, difference, symmetric difference.

---

## Code Examples

```python
# Creating sets
numbers = {1, 2, 3, 4, 5}
empty_set = set()  # NOT {}!

# From list (removes duplicates)
unique = set([1, 1, 2, 2, 3])
print(unique)  # {1, 2, 3}

# Membership testing
if 3 in numbers:
    print("3 is in the set")

# Adding and removing
numbers.add(6)
numbers.remove(5)

# Set operations
set_a = {1, 2, 3, 4}
set_b = {3, 4, 5, 6}

union = set_a | set_b           # {1, 2, 3, 4, 5, 6}
intersection = set_a & set_b    # {3, 4}
difference = set_a - set_b      # {1, 2}
sym_diff = set_a ^ set_b        # {1, 2, 5, 6}
```

---

# Day 16: Frozensets & Set Use Cases

**Learning Target:** I can use frozensets and apply sets to real-world problems.

---

## Key Concepts

**Frozensets** are immutable sets. Can be used as dictionary keys or in other sets.

**Real-world uses:**
- Removing duplicates
- Fast membership testing
- Finding common/unique elements
- Permissions and privileges

---

## Code Examples

```python
# Frozenset
immutable = frozenset([1, 2, 3])

# Using as dictionary key
permissions = {
    frozenset(["read"]): "viewer",
    frozenset(["read", "write"]): "editor"
}

# Removing duplicates
duplicates = [1, 2, 2, 3, 3, 3]
unique = list(set(duplicates))

# Finding common interests
alice = {"music", "games", "reading"}
bob = {"music", "sports", "movies"}
common = alice & bob

# Finding unique elements
all_unique = set(list1) | set(list2) | set(list3)
```

---

# Day 17: Choosing the Right Data Structure

**Learning Target:** I can select and justify the appropriate data structure for different problems.

---

## Data Structure Comparison

| Task | Best Structure | Why |
|------|---|---|
| Ordered sequence | List | Indexed access, mutable |
| Fast membership | Set | O(1) lookup |
| Lookup by name | Dictionary | Key-based access |
| Immutable data | Tuple | Can't be modified |
| Dictionary key | Tuple/Frozenset | Lists aren't hashable |
| Remove duplicates | Set | Unique elements |
| Preserve order + unique | List + set tracking | Can't do both with single |

---

# Day 18: Data Structure Mini-Project — Student Gradebook

**Learning Target:** I can design and implement a practical system using multiple data structures.

This day covers building a complete gradebook system that tracks students, assignments, and grades.

---

# Day 19: Data Structure Mini-Project — Inventory System

**Learning Target:** I can apply data structures to build a practical inventory management system.

This day covers building a complete inventory system that tracks products, quantities, and prices.

---

# Day 20: Code Review & Debugging Workshop

**Learning Target:** I can review and debug code using data structures effectively.

Topics:
- Debugging list modifications during iteration
- Dictionary reference vs. copy issues
- Nested structure access errors
- Common data structure mistakes

---

# Day 21: Unit Review & Assessment Preparation

**Learning Target:** I can synthesize all unit concepts and prepare for the assessment.

**Study topics:**
- Lists, slicing, comprehensions
- Tuples and unpacking
- Dictionary access and iteration
- Set operations
- Nested structures
- Choosing appropriate structures
- Practice problems

---

# Day 22: Unit 1 Assessment — Data Structures

**Learning Target:** I can demonstrate mastery of lists, tuples, dictionaries, and sets through applied problem-solving.

See Day22.md for full assessment details.

---

## Unit Vocabulary & Quick Reference

### Lists
- **Mutability:** Can be changed after creation
- **Indexing:** Access by position (0-based)
- **Slicing:** Extract subset with [start:stop:step]
- **Comprehension:** [expr for item in list]

### Tuples
- **Immutability:** Cannot be changed
- **Hashable:** Can be dictionary keys
- **Unpacking:** a, b = (1, 2)
- **Named tuple:** From collections module

### Dictionaries
- **Key-value pairs:** Access by key, not position
- **Hashable keys:** Must be immutable
- **Get method:** Safe access with default
- **Comprehension:** {key: value for item in list}

### Sets
- **Unique elements:** No duplicates
- **Unordered:** No indexing
- **Fast membership:** O(1) lookup
- **Operations:** Union (|), intersection (&), difference (-)

---

## Performance Summary

| Operation | List | Dict | Set |
|-----------|------|------|-----|
| Access by index/key | O(1) | O(1) | N/A |
| Membership test | O(n) | O(1) | O(1) |
| Insert | O(n) | O(1) | O(1) |
| Delete | O(n) | O(1) | O(1) |
| Iteration | O(n) | O(n) | O(n) |

---

## Common Patterns

**Remove duplicates (preserve order):**
```python
seen = set()
result = []
for item in original:
    if item not in seen:
        seen.add(item)
        result.append(item)
```

**Count frequencies:**
```python
freq = {}
for item in lst:
    freq[item] = freq.get(item, 0) + 1
```

**Merge dictionaries:**
```python
merged = {**dict1, **dict2}
```

**Flatten nested list:**
```python
flat = [item for sublist in nested for item in sublist]
```

**Zip lists together:**
```python
for a, b in zip(list1, list2):
    print(a, b)
```

---

## Next Steps

After completing Unit 1, you'll be prepared for:
- Unit 2: Advanced Functions & Scope
- Working with real-world data structures
- Building more complex programs
- Optimizing code for performance

