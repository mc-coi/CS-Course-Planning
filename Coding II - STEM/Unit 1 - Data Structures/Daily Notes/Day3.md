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
