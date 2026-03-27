# Unit 1: Data Structures
> Master Python's fundamental data structures: lists, tuples, dictionaries, and sets. Learn to store, manipulate, and organize information efficiently.

##  Unit Overview
- **Duration:** 6 days / 2 weeks
- **Key Concepts:** Lists (creation, indexing, slicing, methods), tuples (immutable sequences), dictionaries (key-value pairs), sets (unique collections), and choosing appropriate data structures
- **Big Idea:** Different data structures organize information in different ways—choosing the right one makes your programs simpler and more efficient
- **TN Standard:** 9-12.CCI.2 — Use and manipulate collection data structures

##  Learning Targets
- I can create lists, access elements, and use list methods (append, remove, sort, len)
- I can use list slicing and understand nested lists
- I can create and use tuples and understand why they're immutable
- I can create dictionaries and perform key-value operations
- I can create and manipulate sets and understand set operations
- I can choose appropriate data structures for different problems

---

# Day 1: Review & Lists (Creation, Indexing, Slicing, Methods)
**Learning Target:** I can create lists, access elements using indexing and slicing, and use built-in list methods.

### Key Concepts
A **list** is an ordered, mutable (changeable) collection of items. Lists can contain any data type: integers, strings, floats, even other lists. Elements are accessed by **index**, starting at 0.

**Indexing:** Access a single element using its position
- `numbers[0]` gets the first element
- `numbers[-1]` gets the last element (negative indexing counts backward)

**Slicing:** Extract a sub-list using `list[start:stop:step]`
- `numbers[1:4]` gets elements at indices 1, 2, 3 (stop is exclusive)
- `numbers[::2]` gets every 2nd element
- `numbers[::-1]` reverses the list

**Common list methods:**
- `append(item)` — add to end
- `insert(index, item)` — insert at specific position
- `remove(item)` — remove first occurrence of value
- `pop(index)` — remove and return element at index
- `sort()` — sort in place
- `reverse()` — reverse in place
- `len(list)` — get length
- `list.count(item)` — count occurrences
- `list.index(item)` — find first index of item

### Code Examples
```python
# Creating lists
numbers = [1, 2, 3, 4, 5]
fruits = ["apple", "banana", "cherry"]
mixed = [1, "hello", 3.14, True]
empty = []

# Indexing
print(numbers[0])     # 1
print(numbers[-1])    # 5
print(numbers[2])     # 3

# Slicing
print(numbers[1:4])   # [2, 3, 4]
print(numbers[:3])    # [1, 2, 3]
print(numbers[2:])    # [3, 4, 5]
print(numbers[::2])   # [1, 3, 5]
print(numbers[::-1])  # [5, 4, 3, 2, 1]

# List methods
fruits = ["apple", "banana"]
fruits.append("cherry")           # ["apple", "banana", "cherry"]
fruits.insert(1, "date")          # ["apple", "date", "banana", "cherry"]
fruits.remove("date")             # ["apple", "banana", "cherry"]
item = fruits.pop()               # ["apple", "banana"], item = "cherry"

# Sorting
numbers = [3, 1, 4, 1, 5, 9]
numbers.sort()                    # [1, 1, 3, 4, 5, 9]
print(len(numbers))               # 6
print(numbers.count(1))           # 2
print(numbers.index(4))           # 2

# Iterating through a list
for fruit in fruits:
    print(fruit)

# Using range to create a list
range_list = list(range(10))      # [0, 1, 2, ..., 9]
```

### Guided Practice
Create a shopping list program:
1. Start with a list of 5 grocery items
2. Print the first and last items
3. Slice out the middle 3 items
4. Add a new item
5. Remove an item by index
6. Sort the list and print it
7. Reverse and print it

### Practice Problems
**Problem 1 — Beginner:** Create a list of your 5 favorite numbers, then print each one using a loop.

```python
# Starter code
numbers = []

for num in numbers:
    print(num)
```

**Problem 2 — Intermediate:** Create a list, add 3 elements, remove one, then print the final list and its length.

**Problem 3 — Challenge:** Create a list of 10 integers. Using slicing, print the first 3, last 3, every other element, and the reversed list.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use square brackets and commas to separate values
- Problem 2: Remember to use methods like append() and remove()
- Problem 3: Remember negative indexing and step values in slicing
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
numbers = [5, 10, 15, 20, 25]
for num in numbers:
    print(num)

# Problem 2 Example
inventory = []
inventory.append("milk")
inventory.append("eggs")
inventory.append("bread")
inventory.remove("eggs")
print(inventory)       # ['milk', 'bread']
print(len(inventory))  # 2

# Problem 3 Example
nums = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
print(nums[:3])        # [10, 20, 30]
print(nums[-3:])       # [80, 90, 100]
print(nums[::2])       # [10, 30, 50, 70, 90]
print(nums[::-1])      # [100, 90, 80, ..., 10]
```
</details>

---

# Day 2: List Operations (List Comprehensions, Nested Lists, 2D Lists)
**Learning Target:** I can use list comprehensions and work with nested and 2D lists effectively.

### Key Concepts
**List comprehension** is a concise way to create lists. Instead of looping, you use bracket notation:
```
[expression for item in list if condition]
```

**Nested lists** are lists containing other lists. Use multiple indices to access: `matrix[row][col]`

**2D lists (matrices)** are lists of lists representing rows and columns—useful for grids, game boards, and tables.

### Code Examples
```python
# List comprehension—create squares of numbers 1-5
squares = [x**2 for x in range(1, 6)]      # [1, 4, 9, 16, 25]

# List comprehension with condition
evens = [x for x in range(1, 11) if x % 2 == 0]  # [2, 4, 6, 8, 10]

# List comprehension with transformation
names = ["alice", "bob", "charlie"]
capitalized = [name.upper() for name in names]   # ["ALICE", "BOB", "CHARLIE"]

# Nested lists
student_scores = [
    ["Alice", 95],
    ["Bob", 87],
    ["Charlie", 92]
]
print(student_scores[0])      # ["Alice", 95]
print(student_scores[0][1])   # 95

# 2D list (matrix)
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
print(matrix[0])              # [1, 2, 3]
print(matrix[1][2])           # 6

# Iterating through 2D list
for row in matrix:
    for element in row:
        print(element, end=" ")  # Prints: 1 2 3 4 5 6 7 8 9

# Creating a 2D list with list comprehension
board = [[0 for _ in range(3)] for _ in range(3)]  # 3x3 grid of zeros
```

### Guided Practice
Create a program that:
1. Uses list comprehension to create a list of cubes (1³, 2³, 3³, etc.) for 1-10
2. Creates a 3x3 matrix of numbers 1-9
3. Prints the element at position [1][2]
4. Prints the entire second row
5. Iterates through the matrix and prints each row

### Practice Problems
**Problem 1 — Beginner:** Use list comprehension to create a list of all numbers from 1-20 that are divisible by 3.

**Problem 2 — Intermediate:** Create a 2x3 matrix (2 rows, 3 columns) and access the element at position [1][2].

**Problem 3 — Challenge:** Create a program that generates a 4x4 multiplication table using nested list comprehension.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `if x % 3 == 0` condition
- Problem 2: Matrix[row][col] where rows/cols start at 0
- Problem 3: Use nested comprehension: `[[i*j for j in ...] for i in ...]`
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
divisible_by_3 = [x for x in range(1, 21) if x % 3 == 0]
print(divisible_by_3)  # [3, 6, 9, 12, 15, 18]

# Problem 2 Example
matrix = [[1, 2, 3], [4, 5, 6]]
print(matrix[1][2])    # 6

# Problem 3 Example
table = [[i*j for j in range(1, 5)] for i in range(1, 5)]
for row in table:
    print(row)
```
</details>

---

# Day 3: Tuples (Immutable Sequences, Packing/Unpacking)
**Learning Target:** I can create and use tuples and understand when to use them instead of lists.

### Key Concepts
A **tuple** is like a list, but **immutable** (cannot be changed after creation). Tuples use parentheses `()` instead of brackets.

**Why tuples?**
- Immutability prevents accidental modifications
- Slightly faster and use less memory than lists
- Can be used as dictionary keys (lists cannot)
- Function return multiple values

**Packing:** Assigning multiple values to a tuple
```python
point = (3, 5)
```

**Unpacking:** Extracting values from a tuple into separate variables
```python
x, y = point       # x = 3, y = 5
```

### Code Examples
```python
# Creating tuples
point = (3, 5)
colors = ("red", "green", "blue")
single = (42,)              # Must have comma for single-element tuple!
empty = ()

# Accessing tuple elements (like lists)
print(point[0])             # 3
print(colors[-1])           # "blue"
print(colors[1:])           # ("green", "blue")

# Tuples are immutable
point = (3, 5)
# point[0] = 10  # This would cause an error!

# Packing and unpacking
coordinates = (10, 20, 30)
x, y, z = coordinates       # Unpacking
print(x, y, z)              # 10 20 30

# Swapping variables with unpacking
a, b = 5, 10
a, b = b, a                 # Now a = 10, b = 5

# Returning multiple values (using tuples)
def get_dimensions():
    return (1920, 1080)     # Return tuple

width, height = get_dimensions()

# Tuple methods
t = (1, 2, 2, 3)
print(t.count(2))           # 2
print(t.index(3))           # 3

# Tuples as dictionary keys
location = (40.7128, -74.0060)  # (latitude, longitude)
# cities = {location: "New York"}  # This works!
# cities = {[1, 2]: "error"}       # This would fail—lists can't be keys
```

### Guided Practice
Create a program that:
1. Creates a tuple with 3 colors
2. Unpacks them into separate variables
3. Attempts to modify the tuple (show the error message)
4. Creates a function that returns multiple values as a tuple
5. Unpacks the returned tuple

### Practice Problems
**Problem 1 — Beginner:** Create a tuple with your name, age, and favorite food. Print each value.

**Problem 2 — Intermediate:** Write a function that returns a tuple of (min, max, average) for a list of numbers. Call it and unpack the results.

**Problem 3 — Challenge:** Create a dictionary where tuple coordinates (x, y) are keys and place names are values. Print them.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use parentheses and commas
- Problem 2: Return (min(list), max(list), sum(list)/len(list))
- Problem 3: Keys must be immutable—tuples work, lists don't
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
info = ("Zach McCoy", 17, "pizza")
name, age, food = info
print(name, age, food)  # Zach McCoy 17 pizza

# Problem 2 Example
def statistics(numbers):
    return (min(numbers), max(numbers), sum(numbers)/len(numbers))

numbers = [1, 5, 3, 9, 2]
min_val, max_val, avg_val = statistics(numbers)
print(f"Min: {min_val}, Max: {max_val}, Avg: {avg_val}")

# Problem 3 Example
locations = {(40.7, -74.0): "New York", (51.5, -0.1): "London"}
print(locations[(40.7, -74.0)])  # New York
```
</details>

---

# Day 4: Dictionaries (Key-Value Pairs, Creating, Accessing, Updating)
**Learning Target:** I can create dictionaries and perform key-value operations efficiently.

### Key Concepts
A **dictionary** stores data as key-value pairs. Use curly braces `{}` and colons to separate keys from values.

**Keys** must be immutable (strings, numbers, tuples). **Values** can be anything.

**Common operations:**
- Access: `dict[key]`
- Add/update: `dict[key] = value`
- Delete: `del dict[key]` or `dict.pop(key)`
- Check existence: `"key" in dict`
- Iterate: `for key in dict:` or `for key, value in dict.items():`

**Useful methods:**
- `.keys()` — get all keys
- `.values()` — get all values
- `.items()` — get key-value pairs as tuples
- `.get(key, default)` — safely access with default
- `.update(other_dict)` — merge dictionaries

### Code Examples
```python
# Creating dictionaries
student = {
    "name": "Zach McCoy",
    "grade": 11,
    "gpa": 3.8,
    "subjects": ["Math", "Python", "Physics"]
}

# Accessing values
print(student["name"])          # "Zach McCoy"
print(student["grade"])         # 11

# Safe access with default
print(student.get("age", "N/A"))  # "N/A" (age doesn't exist)

# Adding/updating
student["age"] = 17
student["gpa"] = 3.9            # Update existing

# Deleting
del student["subjects"]
# or
removed_value = student.pop("age")

# Checking if key exists
if "name" in student:
    print(student["name"])

# Iterating through keys
for key in student:
    print(key, student[key])

# Iterating through key-value pairs
for key, value in student.items():
    print(f"{key}: {value}")

# Iterating through values only
for value in student.values():
    print(value)

# Creating dictionary from lists
keys = ["a", "b", "c"]
values = [1, 2, 3]
dictionary = dict(zip(keys, values))  # {"a": 1, "b": 2, "c": 3}

# Nested dictionaries
school = {
    "students": {
        "alice": {"grade": 10, "gpa": 3.9},
        "bob": {"grade": 11, "gpa": 3.7}
    },
    "teachers": ["Mr. Smith", "Ms. Johnson"]
}
print(school["students"]["alice"]["gpa"])  # 3.9
```

### Guided Practice
Create a student gradebook program:
1. Create a dictionary with student names as keys and GPA as values
2. Add a new student
3. Update an existing student's GPA
4. Print all students and their GPAs
5. Count how many students have GPA >= 3.5

### Practice Problems
**Problem 1 — Beginner:** Create a dictionary with 3 fruits as keys and their prices as values. Print one value.

**Problem 2 — Intermediate:** Create a dictionary of student names and grades. Add a new student, update an existing grade, and print all entries.

**Problem 3 — Challenge:** Create a nested dictionary representing a school with departments containing teacher names. Access and print a specific teacher.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use square brackets for access
- Problem 2: Use .items() for iterating
- Problem 3: Use multiple levels of square brackets for nested access
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
prices = {"apple": 0.99, "banana": 0.59, "orange": 1.29}
print(prices["apple"])  # 0.99

# Problem 2 Example
grades = {"Alice": 92, "Bob": 85}
grades["Charlie"] = 88  # Add
grades["Alice"] = 95    # Update
for name, grade in grades.items():
    print(f"{name}: {grade}")

# Problem 3 Example
school = {
    "math": ["Ms. Johnson", "Mr. Chen"],
    "english": ["Ms. Williams"]
}
print(school["math"][1])  # Mr. Chen
```
</details>

---

# Day 5: Sets & Advanced Collections (Sets, Frozensets, Set Operations, Choosing Data Structures)
**Learning Target:** I can create and use sets, perform set operations, and choose appropriate data structures.

### Key Concepts
A **set** is an unordered collection of unique values. Use curly braces `{}` or `set()`.

**Key properties:**
- No duplicates (automatically removes them)
- Unordered (no indexing)
- Mutable (add/remove items)

**Set operations:**
- `.add(item)` — add one item
- `.remove(item)` — remove (error if not found)
- `.discard(item)` — remove (no error if not found)
- `|` union (all items from both)
- `&` intersection (items in both)
- `-` difference (items in first but not second)
- `in` check membership

**Frozenset:** Immutable version of set; can be used as dictionary keys.

### Code Examples
```python
# Creating sets
fruits = {"apple", "banana", "cherry"}
numbers = {1, 2, 3, 4, 5}
empty_set = set()           # Note: {} is empty dict, not set!

# Removing duplicates
duplicate_list = [1, 1, 2, 2, 3, 3]
unique = set(duplicate_list)  # {1, 2, 3}

# Adding and removing
fruits = {"apple", "banana"}
fruits.add("cherry")        # {"apple", "banana", "cherry"}
fruits.remove("apple")      # {"banana", "cherry"}

# Set operations
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

union = set1 | set2         # {1, 2, 3, 4, 5, 6}
intersection = set1 & set2  # {3, 4}
difference = set1 - set2    # {1, 2}

# Membership testing
if 3 in set1:
    print("3 is in set1")

# Checking uniqueness
duplicate_ids = [101, 102, 101, 103, 102]
unique_ids = set(duplicate_ids)
print(len(unique_ids))      # 3

# Frozenset (immutable)
coords = frozenset([(1, 2), (3, 4)])
locations = {coords: "Starting points"}  # Can use as dict key

# Iterating through a set
for item in fruits:
    print(item)
```

### Choosing Data Structures
| Structure | Ordered | Mutable | Duplicates | Use Case |
|-----------|---------|---------|-----------|----------|
| **List** | Yes | Yes | Yes | General ordered collections, sequences |
| **Tuple** | Yes | No | Yes | Fixed data, immutable, function returns, dict keys |
| **Dictionary** | No* | Yes | N/A (keys unique) | Lookup by name/ID, mapping relationships |
| **Set** | No | Yes | No | Unique items, fast membership test, math operations |

*Python 3.7+: dictionaries maintain insertion order, but that's an implementation detail

### Guided Practice
Create a program that:
1. Creates two sets of numbers
2. Finds their union, intersection, and difference
3. Removes duplicates from a list using sets
4. Uses a set to count unique items in a sentence (split by words)

### Practice Problems
**Problem 1 — Beginner:** Create a set with 3 colors, add a new color, then print the set.

**Problem 2 — Intermediate:** Create two sets and find their intersection and difference using set operations.

**Problem 3 — Challenge:** Given a list of student IDs with duplicates, use a set to find unique students, then create a dictionary mapping unique IDs to made-up names.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use set() constructor or {}
- Problem 2: Use & for intersection, - for difference
- Problem 3: Create unique IDs with set(), then dict with zip()
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
colors = {"red", "blue", "green"}
colors.add("yellow")
print(colors)  # {"red", "blue", "green", "yellow"}

# Problem 2 Example
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}
print(set1 & set2)  # {3, 4}
print(set1 - set2)  # {1, 2}

# Problem 3 Example
ids = [101, 102, 101, 103, 102, 104]
unique_ids = sorted(list(set(ids)))
names = ["Zach", "Alice", "Bob", "Charlie"]
id_dict = dict(zip(unique_ids, names))
print(id_dict)
```
</details>

---

# Day 6: Project Day — Student Grade Book
**Learning Target:** I can design and build a complete program using lists, dictionaries, and tuples.

### Project Overview
Build an interactive student gradebook that:
1. Stores student information (name, grade, GPA)
2. Adds new students
3. Updates grades
4. Calculates class statistics
5. Displays reports

### Requirements
- Use a list of dictionaries to store student data (or a dictionary of tuples)
- User menu with options: Add, Update, View All, Calculate Average, Exit
- Display students sorted by grade or name
- Calculate class average GPA
- Use appropriate data structures for each piece of information

### Scaffold & Starter Code
```python
# Student Grade Book Project

# Data structure: list of dictionaries
students = [
    {"name": "Alice", "grade": 95, "gpa": 3.9},
    {"name": "Bob", "grade": 87, "gpa": 3.5},
]

def add_student(name, grade, gpa):
    """Add a new student to the gradebook."""
    students.append({"name": name, "grade": grade, "gpa": gpa})

def view_all_students():
    """Display all students."""
    for i, student in enumerate(students, 1):
        print(f"{i}. {student['name']} - Grade: {student['grade']}, GPA: {student['gpa']}")

def calculate_class_average():
    """Calculate average grade and GPA."""
    if not students:
        print("No students yet.")
        return
    avg_grade = sum(s["grade"] for s in students) / len(students)
    avg_gpa = sum(s["gpa"] for s in students) / len(students)
    print(f"Class Average Grade: {avg_grade:.2f}")
    print(f"Class Average GPA: {avg_gpa:.2f}")

def main():
    while True:
        print("\n--- Student Gradebook ---")
        print("1. Add Student")
        print("2. View All Students")
        print("3. Calculate Class Average")
        print("4. Exit")
        choice = input("Select option: ")

        if choice == "1":
            name = input("Name: ")
            grade = int(input("Grade: "))
            gpa = float(input("GPA: "))
            add_student(name, grade, gpa)
            print("Student added!")
        elif choice == "2":
            view_all_students()
        elif choice == "3":
            calculate_class_average()
        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Invalid option.")

if __name__ == "__main__":
    main()
```

### Enhancement Ideas
- Sort students by grade or GPA
- Find highest/lowest grade
- Remove a student
- Search for a student by name
- Save/load from a file (Unit 4)
- Add multiple grades per student (nested data structures)

---

# Unit Practice Bank

1. **Beginner:** Create a list of 5 numbers, print the first and last elements.
2. **Beginner:** Create a list, use append() to add 3 items, then print the list.
3. **Beginner:** Create a list of strings and print each one using a for loop.
4. **Beginner:** Use list slicing to extract the middle 3 elements from a list of 7 items.
5. **Beginner:** Create a tuple with 3 values and unpack them into separate variables.
6. **Intermediate:** Use list comprehension to create a list of squared numbers (1²-10²).
7. **Intermediate:** Create a 3x3 matrix and print the element at position [2][1].
8. **Intermediate:** Create a dictionary with 5 key-value pairs and iterate through them with .items().
9. **Intermediate:** Create two sets and find their union, intersection, and difference.
10. **Intermediate:** Write a function that returns multiple values as a tuple, then unpack the result.
11. **Challenge:** Create a nested dictionary representing a store with departments and products.
12. **Challenge:** Build a contacts book using a dictionary with nested information (phone, email, address).
13. **Challenge:** Given a list with duplicates, use a set to find unique items, then count each unique item.
14. **Challenge:** Create a program that generates and sorts a 2D list of student records.
15. **Challenge:** Use list and set operations to find common elements between multiple lists.

---

# Common Mistakes & How to Fix Them
| Mistake | What Happens | Fix |
|---------|--------------|-----|
| `empty = {}` thinking it's an empty set | It's actually an empty dictionary | Use `set()` for empty set |
| Trying to modify a tuple: `t[0] = 5` | TypeError: tuple does not support item assignment | Remember tuples are immutable; use lists instead |
| `list[5]` when list only has 3 elements | IndexError: list index out of range | Check list length first or use try/except |
| `dict["nonexistent_key"]` | KeyError: 'nonexistent_key' | Use `.get(key, default)` instead |
| Nested list bug: `matrix = [[0]*3]*3` | All rows are the same reference; modifying one affects all | Use `matrix = [[0 for _ in range(3)] for _ in range(3)]` |
| `set([1, 2, 2])` creates `{1, 2}` then trying to index | TypeError: 'set' object is not subscriptable | Remember sets don't support indexing; use lists |
| Forgetting the comma in single-element tuple: `t = (5)` | Creates integer, not tuple | Use `t = (5,)` |
| Modifying dict while iterating: `for k in d: del d[k]` | RuntimeError: dictionary changed size during iteration | Use list(d.keys()) or create a new dict |

---

# Unit Assessment Prep

**Review Questions:** Answer these to prepare for the unit assessment.

1. What is a list? What are the key differences between lists and tuples?
2. Explain indexing and slicing. What does `list[2:5]` return?
3. What does `list[-1]` represent? Give an example.
4. What is list comprehension? Write an example that creates squares of numbers 1-5.
5. How do you add an element to a list? How do you remove one?
6. What is a dictionary? How is it different from a list?
7. How do you access a dictionary value if you don't know if the key exists (safely)?
8. What is a set? Why would you use a set instead of a list?
9. Create a 2x2 matrix and explain how to access element at position [1][0].
10. When would you use a tuple instead of a list? Name three reasons.

**Answers:**

1. A list is an ordered, mutable collection that can hold any data type. Tuples are ordered but immutable (cannot be changed), and can be used as dictionary keys.
2. Indexing gets a single element by position: `list[0]` is first. Slicing extracts a sub-list: `list[2:5]` returns elements at indices 2, 3, 4 (stop is exclusive).
3. `list[-1]` gets the last element. Example: `nums = [1, 2, 3, 4]; nums[-1]` returns `4`.
4. List comprehension creates lists concisely. `[x**2 for x in range(1, 6)]` returns `[1, 4, 9, 16, 25]`.
5. Add with `.append(item)` or `.insert(index, item)`. Remove with `.remove(value)` or `.pop(index)`.
6. A dictionary stores key-value pairs. Lists are indexed by position; dictionaries are indexed by key (usually strings).
7. Use `.get(key, default_value)` which returns the value if the key exists, or the default if it doesn't.
8. A set is an unordered collection of unique items. Use sets when you need uniqueness, membership testing, or mathematical operations (union, intersection).
9. `matrix = [[1, 2], [3, 4]]`; element at [1][0] is `3` (second row, first column).
10. Use tuples when you need immutability (function returns, protecting data), as dictionary keys, or for slight performance improvement.

---

# Vocabulary & Quick Reference

**Key Terms:**
- **List:** Ordered, mutable collection of items in square brackets
- **Tuple:** Ordered, immutable collection in parentheses
- **Dictionary:** Unordered collection of key-value pairs in curly braces
- **Set:** Unordered collection of unique items
- **Index:** Position of an element, starting at 0
- **Slice:** Extract a subset of a sequence using start:stop:step
- **Key:** Unique identifier in a dictionary
- **Value:** Data associated with a key
- **Mutable:** Can be changed after creation
- **Immutable:** Cannot be changed after creation

**Key Syntax:**
```python
# Lists
list = [1, 2, 3]
list.append(4)
list[0] = 10
list[1:3]

# Tuples
tup = (1, 2, 3)
x, y, z = tup

# Dictionaries
dict = {"name": "Alice", "age": 25}
dict["age"] = 26
dict.get("name")

# Sets
s = {1, 2, 3}
s.add(4)
s1 | s2  # union
s1 & s2  # intersection

# List comprehension
[x**2 for x in range(5)]
[x for x in list if x > 5]
```

**Common Methods:**
- List: `.append()`, `.remove()`, `.pop()`, `.sort()`, `.reverse()`, `.count()`, `.index()`
- Dictionary: `.keys()`, `.values()`, `.items()`, `.get()`, `.pop()`, `.update()`
- Set: `.add()`, `.remove()`, `.discard()`, `.union()`, `.intersection()`, `.difference()`
