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

---

## Common Mistakes & How to Fix Them
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
