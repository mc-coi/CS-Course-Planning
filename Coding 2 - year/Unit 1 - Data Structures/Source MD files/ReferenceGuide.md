# Unit 1: Data Structures — Quick Reference Guide

---

## Lists

### Creation
```python
empty = []
with_values = [1, 2, 3]
mixed = [1, "hello", 3.14, True]
from_range = list(range(1, 6))
repeated = [0] * 5
```

### Accessing Elements
```python
lst = [10, 20, 30, 40, 50]
lst[0]      # 10 (first)
lst[-1]     # 50 (last)
lst[1:4]    # [20, 30, 40] (slice)
lst[::2]    # [10, 30, 50] (every 2nd)
lst[::-1]   # [50, 40, 30, 20, 10] (reversed)
```

### Modifying Lists
```python
lst.append(60)           # Add to end: [10, 20, ..., 60]
lst.extend([70, 80])     # Add multiple: [..., 70, 80]
lst.insert(1, 15)        # Insert at position 1
lst.remove(20)           # Remove by value
lst.pop()                # Remove and return last
lst.pop(0)               # Remove and return first
lst.sort()               # Sort in place
lst.reverse()            # Reverse in place
lst.clear()              # Remove all elements
```

### Iteration
```python
for item in lst:
    print(item)

for i, item in enumerate(lst):
    print(f"{i}: {item}")

for i in range(len(lst)):
    print(lst[i])
```

### List Comprehension
```python
squares = [x**2 for x in range(5)]
evens = [x for x in range(10) if x % 2 == 0]
pairs = [(x, y) for x in range(3) for y in range(3)]
```

### Useful Methods
```python
len(lst)          # Number of elements
lst.count(item)   # Count occurrences
lst.index(item)   # First index of item
lst.copy()        # Shallow copy
lst.sort(reverse=True)  # Sort descending
```

---

## Tuples

### Creation
```python
empty = ()
single = (1,)           # Note the comma!
pair = (1, 2)
from_list = tuple([1, 2, 3])
```

### Accessing Elements
```python
t = (10, 20, 30)
t[0]        # 10
t[-1]       # 30
t[1:]       # (20, 30)
```

### Unpacking
```python
x, y = (1, 2)
a, b, c = (10, 20, 30)
first, *middle, last = (1, 2, 3, 4, 5)  # first=1, middle=[2,3,4], last=5
```

### Named Tuples
```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(10, 20)
print(p.x, p.y)     # 10 20

Student = namedtuple('Student', ['name', 'grade', 'gpa'])
alice = Student("Alice", 10, 3.8)
```

### Use Cases
- Immutable data that shouldn't change
- Return multiple values from functions
- Use as dictionary keys
- Slight performance advantage over lists

---

## Dictionaries

### Creation
```python
empty = {}
with_values = {"name": "Alice", "age": 15}
from_pairs = dict(name="Bob", age=16)
from_zip = dict(zip(keys, values))
```

### Accessing Values
```python
d = {"name": "Alice", "age": 15}
d["name"]           # "Alice"
d.get("name")       # "Alice"
d.get("gpa", 3.5)   # 3.5 (default if missing)
```

### Modifying Dictionaries
```python
d["age"] = 16           # Modify existing
d["gpa"] = 3.8          # Add new
d.pop("age")            # Remove and return value
del d["age"]            # Remove (no return)
d.update({"city": "NYC"})  # Merge
d.clear()               # Remove all
```

### Iteration
```python
for key in d:
    print(key)

for value in d.values():
    print(value)

for key, value in d.items():
    print(f"{key}: {value}")
```

### Dictionary Comprehension
```python
squares = {x: x**2 for x in range(5)}
evens = {x: x**2 for x in range(10) if x % 2 == 0}
inverted = {v: k for k, v in original.items()}
```

### Useful Methods
```python
d.keys()            # All keys
d.values()          # All values
d.items()           # Key-value pairs
d.get(key, default) # Safe access
d.pop(key)          # Remove and return
d.setdefault(key, default)  # Set if missing
d.copy()            # Shallow copy
```

### Nested Dictionaries
```python
student = {
    "name": "Alice",
    "grades": {"Math": 95, "English": 87}
}

student["grades"]["Math"]  # 95
student.get("gpa", {}).get("value", "N/A")  # Safe access
```

---

## Sets

### Creation
```python
empty = set()  # NOT {} (that's dict!)
from_list = {1, 1, 2, 2, 3}  # {1, 2, 3}
from_range = set(range(5))
```

### Modifying Sets
```python
s = {1, 2, 3}
s.add(4)        # Add element
s.remove(2)     # Remove (error if missing)
s.discard(2)    # Remove (no error if missing)
s.pop()         # Remove and return arbitrary element
s.clear()       # Remove all
```

### Set Operations
```python
set_a = {1, 2, 3}
set_b = {3, 4, 5}

union = set_a | set_b          # {1, 2, 3, 4, 5}
intersection = set_a & set_b   # {3}
difference = set_a - set_b     # {1, 2}
sym_diff = set_a ^ set_b       # {1, 2, 4, 5}
```

### Comparison
```python
{1, 2}.issubset({1, 2, 3})          # True
{1, 2, 3}.issuperset({1, 2})        # True
{1, 2} == {1, 2}                    # True
{1, 2}.isdisjoint({3, 4})           # True (no common)
```

### Iteration
```python
for item in s:
    print(item)
```

### Frozensets
```python
fs = frozenset([1, 2, 3])
# Immutable - can be dict key or in sets
d = {fs: "immutable"}
```

---

## When to Use Each Structure

| Task | Best Structure | Why |
|------|---|---|
| Ordered sequence | List | Indexed access, mutable |
| Fast membership test | Set | O(1) lookup |
| Lookup by name | Dictionary | Key-based access |
| Immutable data | Tuple | Can't be modified |
| Dictionary key | Tuple/Frozenset | Lists aren't hashable |
| Remove duplicates | Set | Unique elements |
| Preserve order + unique | List + set tracking | Can't do both with single |
| Grid/matrix | List of lists | 2D indexing |
| Key-value pairs | Dictionary | Natural representation |
| Multiple return values | Tuple | Clean unpacking |

---

## Common Patterns

### Remove Duplicates (Preserve Order)
```python
seen = set()
result = []
for item in original:
    if item not in seen:
        seen.add(item)
        result.append(item)
```

### Count Frequencies
```python
freq = {}
for item in lst:
    freq[item] = freq.get(item, 0) + 1
```

### Group by Value
```python
from collections import defaultdict
groups = defaultdict(list)
for item in items:
    groups[item.category].append(item)
```

### Invert Dictionary
```python
inverted = {v: k for k, v in original.items()}
```

### Zip Lists Together
```python
names = ["Alice", "Bob"]
ages = [15, 16]
for name, age in zip(names, ages):
    print(f"{name}: {age}")
```

### Flatten Nested List
```python
flat = [item for sublist in nested for item in sublist]
```

### Merge Dictionaries
```python
merged = {**dict1, **dict2}
# Or: merged = dict1.copy(); merged.update(dict2)
```

---

## Performance Considerations

| Operation | List | Dict | Set |
|-----------|------|------|-----|
| Access by index/key | O(1) | O(1) | N/A |
| Membership test | O(n) | O(1) | O(1) |
| Insert | O(n) | O(1) | O(1) |
| Delete | O(n) | O(1) | O(1) |
| Iteration | O(n) | O(n) | O(n) |

---

## Gotchas & Common Mistakes

### Mistake 1: Modifying while iterating
```python
# WRONG:
for item in lst:
    if bad(item):
        lst.remove(item)

# RIGHT:
lst = [item for item in lst if not bad(item)]
```

### Mistake 2: Dictionary reference vs. copy
```python
# WRONG:
new_dict = old_dict
new_dict["key"] = "value"  # Modifies old_dict too!

# RIGHT:
new_dict = old_dict.copy()
```

### Mistake 3: Empty set creation
```python
# WRONG:
empty = {}  # This is a dict!

# RIGHT:
empty = set()
```

### Mistake 4: Single element tuple
```python
# WRONG:
single = (1)  # This is just 1 (int), not a tuple!

# RIGHT:
single = (1,)  # Note the comma
```

### Mistake 5: List as dict key
```python
# WRONG:
d = {[1, 2]: "value"}  # TypeError: unhashable type

# RIGHT:
d = {(1, 2): "value"}  # Use tuple
```

---

## Quick Syntax Cheat Sheet

| Task | Syntax |
|------|--------|
| Create list | `[1, 2, 3]` or `list()` |
| Create tuple | `(1, 2, 3)` or `tuple()` |
| Create dict | `{"key": "value"}` or `dict()` |
| Create set | `{1, 2, 3}` or `set()` |
| Slice | `lst[start:stop:step]` |
| Comprehension | `[expr for item in iter if condition]` |
| Dict comprehension | `{key: value for item in iter}` |
| Unpack | `a, b, c = (1, 2, 3)` |
| Iterate | `for item in container:` |
| Enumerate | `for i, item in enumerate(lst):` |
| Zip | `for a, b in zip(list1, list2):` |
| Membership | `if item in container:` |

