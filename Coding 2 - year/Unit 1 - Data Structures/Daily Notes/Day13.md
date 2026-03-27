# Day 13: Set Operations — Union, Intersection, Difference, Frozensets
**Learning Target:** I can perform mathematical set operations and understand frozensets for immutable sets.

### Key Concepts

**Union**: Combines all elements from two sets. Operator: `|` or method: `.union()`

**Intersection**: Finds elements common to both sets. Operator: `&` or method: `.intersection()`

**Difference**: Finds elements in the first set but not in the second. Operator: `-` or method: `.difference()`

**Symmetric Difference**: Finds elements in either set but not in both. Operator: `^` or method: `.symmetric_difference()`

**Frozenset**: An immutable version of a set. Useful as dictionary keys or set elements where mutability is not needed.

**Set Relationships**: Checking if sets are subsets, supersets, or disjoint using methods or comparison operators.

### Code Examples

```python
# Union - all elements from both sets
set1 = {1, 2, 3}
set2 = {3, 4, 5}
union = set1 | set2
print(union)           # Output: {1, 2, 3, 4, 5}

union2 = set1.union(set2)
print(union2)          # Output: {1, 2, 3, 4, 5}

# Intersection - elements in both sets
intersection = set1 & set2
print(intersection)    # Output: {3}

intersection2 = set1.intersection(set2)
print(intersection2)   # Output: {3}

# Difference - elements in first set but not second
difference = set1 - set2
print(difference)      # Output: {1, 2}

difference2 = set1.difference(set2)
print(difference2)     # Output: {1, 2}

# Symmetric difference - elements in either but not both
sym_diff = set1 ^ set2
print(sym_diff)        # Output: {1, 2, 4, 5}

sym_diff2 = set1.symmetric_difference(set2)
print(sym_diff2)       # Output: {1, 2, 4, 5}

# Subset and superset
set_a = {1, 2}
set_b = {1, 2, 3, 4}
print(set_a <= set_b)  # Output: True (set_a is subset)
print(set_a.issubset(set_b))  # Output: True

print(set_b >= set_a)  # Output: True (set_b is superset)
print(set_b.issuperset(set_a))  # Output: True

# Disjoint - no common elements
set_x = {1, 2, 3}
set_y = {4, 5, 6}
print(set_x.isdisjoint(set_y))  # Output: True

# Frozenset - immutable set
frozen = frozenset([1, 2, 3])
print(frozen)          # Output: frozenset({1, 2, 3})

# Frozenset as dictionary key
locations = {
    frozenset([1, 2]): "A",
    frozenset([3, 4]): "B"
}
print(locations[frozenset([1, 2])])  # Output: A

# Frozenset in a set (sets of sets)
set_of_sets = {frozenset([1, 2]), frozenset([3, 4])}
print(set_of_sets)

# Set operations preserve immutability
frozen1 = frozenset([1, 2, 3])
frozen2 = frozenset([3, 4, 5])
union = frozen1 | frozen2
print(union)           # Output: frozenset({1, 2, 3, 4, 5})

# Real-world example: finding common interests
alice_interests = {"python", "gaming", "music", "cooking"}
bob_interests = {"python", "gaming", "sports", "reading"}

common = alice_interests & bob_interests
print(f"Common interests: {common}")

unique_alice = alice_interests - bob_interests
print(f"Only Alice: {unique_alice}")

unique_bob = bob_interests - alice_interests
print(f"Only Bob: {unique_bob}")

all_interests = alice_interests | bob_interests
print(f"All interests: {all_interests}")

# Real-world example: analyzing user tags
user1_tags = {"python", "web", "tutorial"}
user2_tags = {"python", "data-science", "tutorial"}
user3_tags = {"java", "web", "tutorial"}

common_all = user1_tags & user2_tags & user3_tags
print(f"Tags all users share: {common_all}")

# Checking if users have overlapping interests
def have_common_interest(tags1, tags2):
    return len(tags1 & tags2) > 0

print(have_common_interest(user1_tags, user2_tags))

# Multiple set operations
set_a = {1, 2, 3, 4}
set_b = {3, 4, 5, 6}
set_c = {4, 6, 7, 8}

# Find elements in A but not in B or C
exclusive_a = set_a - set_b - set_c
print(exclusive_a)     # Output: {1, 2}

# Find elements common to all three
common_all = set_a & set_b & set_c
print(common_all)      # Output: {4}

# Update operations (modify in place)
original = {1, 2, 3}
original |= {3, 4, 5}  # Union update
print(original)        # Output: {1, 2, 3, 4, 5}

original &= {3, 4, 5}  # Intersection update
print(original)        # Output: {3, 4, 5}

original -= {5}        # Difference update
print(original)        # Output: {3, 4}

# Copy a set
original = {1, 2, 3}
copy = original.copy()
copy.add(4)
print(original)        # Output: {1, 2, 3}
print(copy)            # Output: {1, 2, 3, 4}

# Finding group overlaps
group1 = {"Alice", "Bob", "Charlie"}
group2 = {"Charlie", "Diana", "Eve"}
group3 = {"Alice", "Diana", "Frank"}

in_all_groups = group1 & group2 & group3
print(f"In all groups: {in_all_groups}")

in_at_least_two = (group1 & group2) | (group2 & group3) | (group1 & group3)
print(f"In at least 2 groups: {in_at_least_two}")

# Set comprehension (like list comprehension)
squares = {x**2 for x in range(5)}
print(squares)         # Output: {0, 1, 4, 9, 16}

evens = {x for x in range(10) if x % 2 == 0}
print(evens)           # Output: {0, 2, 4, 6, 8}
```

### Guided Practice

**Warm-up (5 minutes):**
1. Create two sets with overlapping elements
2. Find their union using |
3. Find their intersection using &
4. Find the difference using -

**Activity (35 minutes):**
1. Practice all set operations with different data
2. Use frozensets as dictionary keys
3. Chain multiple set operations
4. Use set comprehensions
5. Apply operations to real data (interests, tags, groups)
6. Test subset/superset relationships
7. Use update operations

**Challenge (10 minutes):**
Create a program that analyzes relationships between multiple groups or categories.

### Practice Problems

**Problem 1 — Beginner:** Basic set operations
```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

# TODO: Find union
# TODO: Find intersection
# TODO: Find difference (set1 - set2)
# TODO: Print all results
```

**Problem 2 — Intermediate:** Frozensets and complex operations
```python
# TODO: Create a frozenset from a list
# TODO: Use it as a dictionary key
# TODO: Use it as an element in another set
# TODO: Perform set operations on frozensets
```

**Problem 3 — Challenge:** Multi-set analysis
```python
# Skills for different languages:
python_skills = {"OOP", "async", "data-science"}
java_skills = {"OOP", "threading", "enterprise"}
javascript_skills = {"async", "web", "node"}

# TODO: Find skills common to all three
# TODO: Find skills unique to each language
# TODO: Find skills shared by at least two languages
# TODO: Find all skills across all languages
```

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use |, &, - operators
- Or use .union(), .intersection(), .difference() methods

**Problem 2:**
- frozenset(list) creates immutable set
- Use as dict key: `{frozenset(...): value}`
- Set can contain frozensets

**Problem 3:**
- Intersection of all three: `python & java & javascript`
- Unique to one: `python - java - javascript`
- Shared by at least two: `(python & java) | (java & js) | (python & js)`

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}
print(set1 | set2)     # {1, 2, 3, 4, 5, 6}
print(set1 & set2)     # {3, 4}
print(set1 - set2)     # {1, 2}

# Problem 2
frozen = frozenset([1, 2, 3])
d = {frozen: "value"}
s = {frozenset([1, 2])}
union = frozen | frozenset([3, 4])

# Problem 3
python_skills = {"OOP", "async", "data-science"}
java_skills = {"OOP", "threading", "enterprise"}
javascript_skills = {"async", "web", "node"}

all_three = python_skills & java_skills & javascript_skills
print(all_three)

unique_python = python_skills - java_skills - javascript_skills
at_least_two = (python_skills & java_skills) | (java_skills & javascript_skills) | (python_skills & javascript_skills)
all_skills = python_skills | java_skills | javascript_skills
```

</details>
