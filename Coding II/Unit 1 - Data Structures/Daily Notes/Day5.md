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
