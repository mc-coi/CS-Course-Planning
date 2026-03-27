# Day 21: Unit Review & Assessment Preparation

**Learning Target:** I can synthesize all unit concepts and prepare for the assessment.

---

## Unit Overview & Key Concepts

**Lists:** Ordered, mutable, indexed access, `.append()`, `.remove()`, slicing, comprehensions

**Tuples:** Ordered, immutable, can be dict keys, unpacking, named tuples

**Dictionaries:** Key-value pairs, fast lookup, `.get()`, iteration with `.items()`, nested dicts

**Sets:** Unordered, unique elements, fast membership test, set operations (union, intersection, difference)

**When to use each:**
- Lists: Ordered sequences you'll modify
- Tuples: Fixed data, dictionary keys, return multiple values
- Dicts: Lookup by meaningful key
- Sets: Unique elements, membership testing

---

## Comprehensive Review Checklist

### Lists (Days 1-6)
- [ ] Create lists with `[]` and `list()`
- [ ] Access elements by index (positive and negative)
- [ ] Slice lists with `[start:stop:step]`
- [ ] Modify lists with `.append()`, `.insert()`, `.remove()`, `.pop()`
- [ ] Iterate with `for`, use `enumerate()`
- [ ] Use list comprehensions effectively
- [ ] Understand `.extend()` vs `.append()`

### 2D Lists (Days 7-8)
- [ ] Create and access 2D lists (matrices)
- [ ] Iterate through rows and columns
- [ ] Work with jagged arrays
- [ ] Flatten nested lists

### Tuples (Days 9-10)
- [ ] Create tuples (note the comma for single elements!)
- [ ] Understand immutability
- [ ] Use tuple unpacking
- [ ] Create and use named tuples
- [ ] Use tuples as dictionary keys

### Dictionaries (Days 11-14)
- [ ] Create and access dictionaries
- [ ] Use `.get()` for safe access
- [ ] Modify dictionaries
- [ ] Iterate with `.keys()`, `.values()`, `.items()`
- [ ] Use `.pop()`, `.update()`, `.setdefault()`
- [ ] Work with nested dictionaries
- [ ] Create dictionaries with comprehensions
- [ ] Use dictionary unpacking `{**d1, **d2}`

### Sets (Days 15-16)
- [ ] Create sets and frozensets
- [ ] Add and remove elements
- [ ] Use membership testing (`in`)
- [ ] Perform set operations (union, intersection, difference)
- [ ] Use frozensets as dictionary keys
- [ ] Understand set vs list performance

### Data Structure Selection (Day 17)
- [ ] Choose appropriate structures for problems
- [ ] Justify choices based on operations needed
- [ ] Consider performance implications

### Projects (Days 18-19)
- [ ] Design systems using multiple data structures
- [ ] Implement practical applications
- [ ] Test thoroughly with edge cases

---

## Practice Problems by Topic

### Basic List Operations
1. Create a list and use indexing, slicing, and methods
2. Write a function to find the max element
3. Filter a list using list comprehension

### Dictionaries
1. Create a phone book and look up numbers
2. Count word frequencies
3. Merge two dictionaries

### Nested Structures
1. Work with student records
2. Access deeply nested values
3. Iterate through nested structures

### Sets
1. Remove duplicates from a list
2. Find common elements between lists
3. Use sets for fast membership testing

### Mixed Data Structures
1. Design a system using multiple structures
2. Choose appropriate structures for a problem
3. Justify your choices

---

## Quick Reference

### List Methods
```python
.append(x)      # Add to end
.extend(list)   # Add all from another list
.insert(i, x)   # Insert at position
.remove(x)      # Remove by value
.pop(i)         # Remove and return at index
.sort()         # Sort in place
.reverse()      # Reverse in place
.count(x)       # Count occurrences
.index(x)       # Find index of first occurrence
.copy()         # Create a shallow copy
```

### Dictionary Methods
```python
.keys()         # Get all keys
.values()       # Get all values
.items()        # Get key-value pairs
.get(k, default)  # Safe access
.pop(k)         # Remove and return
.update(dict)   # Merge
.setdefault(k, v)  # Set if missing
.clear()        # Remove all
.copy()         # Create a shallow copy
```

### Set Operations
```python
.add(x)         # Add element
.remove(x)      # Remove (error if missing)
.discard(x)     # Remove (no error)
.union(other)   # All elements from both
.intersection(other)  # Common elements
.difference(other)    # In first but not second
.issubset(other)      # All in other?
```

---

## Sample Review Questions

1. **What's the difference between `.append()` and `.extend()`?**
   - `.append()` adds one item; `.extend()` adds all items from an iterable

2. **When should you use a tuple instead of a list?**
   - When data shouldn't change, or when you need to use it as a dictionary key

3. **What does `my_dict.get("key", "default")` do?**
   - Returns the value if key exists, otherwise returns "default"

4. **How do you create an empty set?**
   - `set()` (not `{}`, which creates an empty dict)

5. **What's the time complexity of checking if an element is in a set vs. a list?**
   - Set: O(1); List: O(n)

---

## Test Format Preview

Tomorrow's assessment will include:
- **Part 1:** Multiple choice on data structure concepts
- **Part 2:** Short answer questions
- **Part 3:** Coding problems (write functions or classes)
- **Part 4:** Reflection questions

**Study tips:**
- Review your daily practice problems
- Test your understanding by writing code
- Consider edge cases (empty inputs, duplicates, etc.)
- Practice explaining your choices

---

## Guided Practice

Work through these problems:

1. **List:** Given `[1, 2, 3, 4, 5]`, use slicing to create `[3, 4, 5]`
2. **Dictionary:** Create a dict from two lists of keys and values using `zip()`
3. **Set:** Find elements that are in list1 but not in list2
4. **Nested:** Access the city in `person = {"address": {"city": "NYC"}}`
5. **Comprehension:** Create a list of squares for numbers 1-10
6. **Tuple:** Unpack `(1, 2, 3)` into variables
7. **Mixed:** Design a data structure for a library (books, authors, genres)

---

## Mental Preparation

- Review any topics that felt uncertain
- Practice explaining concepts out loud
- Test your code to ensure it works
- Remember to handle edge cases
- Ask questions if anything is unclear

**Good luck on the assessment!**
