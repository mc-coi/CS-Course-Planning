# Day 12: Sets — Creation, Add, Remove, Membership Testing
**Learning Target:** I can create sets, add and remove elements, and test membership efficiently.

### Key Concepts

**Set**: An unordered, mutable collection of unique elements. Duplicate values are automatically removed, making sets ideal for membership testing and eliminating duplicates.

**Unordered**: Sets do not maintain insertion order (though this is implementation-dependent). You cannot access elements by index like lists.

**Unique Elements**: Each element in a set appears only once. Adding a duplicate has no effect. This property makes sets perfect for deduplication.

**Membership Testing**: Checking if an element is in a set using `in` is O(1) average case, much faster than list searching.

**Set Operations**: Sets support mathematical operations like union, intersection, and difference, making them powerful for logical operations on collections.

**Hashable Elements**: Only hashable types (immutable) can be added to sets: strings, numbers, tuples. Lists and dictionaries cannot be set elements.

### Code Examples

```python
# Creating sets
empty_set = set()  # Note: {} creates empty dict, not set
single_set = {1}
numbers = {1, 2, 3, 4, 5}
words = {"apple", "banana", "cherry"}
mixed = {1, "hello", 3.14, True}

print(numbers)        # Output: {1, 2, 3, 4, 5} (order not guaranteed)
print(words)          # Output: {'apple', 'banana', 'cherry'}

# Duplicates are automatically removed
duplicate_set = {1, 2, 2, 3, 3, 3}
print(duplicate_set)  # Output: {1, 2, 3}

# Creating set from other iterables
from_list = set([1, 2, 3, 2, 1])
print(from_list)      # Output: {1, 2, 3}

from_string = set("hello")
print(from_string)    # Output: {'h', 'e', 'l', 'o'}

from_range = set(range(5))
print(from_range)     # Output: {0, 1, 2, 3, 4}

# add() - add single element
fruits = {"apple", "banana"}
fruits.add("cherry")
print(fruits)         # Output: {'apple', 'banana', 'cherry'}

# Adding duplicate has no effect
fruits.add("apple")
print(fruits)         # Output: {'apple', 'banana', 'cherry'} (unchanged)

# remove() - remove element, raises KeyError if not found
colors = {"red", "green", "blue"}
colors.remove("red")
print(colors)         # Output: {'green', 'blue'}

# remove() with error handling
try:
    colors.remove("yellow")
except KeyError:
    print("Color not found!")

# discard() - remove safely (no error if not found)
colors.discard("yellow")
print(colors)         # Output: {'green', 'blue'} (no error)

colors.discard("green")
print(colors)         # Output: {'blue'}

# pop() - remove and return an arbitrary element
items = {1, 2, 3, 4, 5}
removed = items.pop()
print(removed)        # Output: some element (unpredictable)
print(items)          # Output: remaining elements

# Membership testing
numbers = {1, 2, 3, 4, 5}
print(3 in numbers)   # Output: True
print(10 in numbers)  # Output: False
print(2 not in numbers)  # Output: False

# Length
print(len(numbers))   # Output: 5

# Iterating through set
for number in numbers:
    print(number)     # Prints each number (order not guaranteed)

# clear() - remove all elements
temp_set = {1, 2, 3}
temp_set.clear()
print(temp_set)       # Output: set()

# Checking if element is in set (O(1) vs O(n) for list)
numbers = {1, 2, 3, 4, 5}
if 3 in numbers:
    print("3 is in the set")  # Output: 3 is in the set

# Converting between collections
original_list = [1, 2, 2, 3, 3, 3, 4]
unique_set = set(original_list)
back_to_list = list(unique_set)
print(back_to_list)   # Output: [1, 2, 3, 4] (order may vary)

# Removing duplicates from a list
numbers = [1, 2, 3, 2, 1, 4, 5, 4]
unique = list(set(numbers))
print(unique)         # Output: [1, 2, 3, 4, 5] (order not guaranteed)

# Preserving order while removing duplicates
def remove_duplicates_ordered(lst):
    seen = set()
    result = []
    for item in lst:
        if item not in seen:
            seen.add(item)
            result.append(item)
    return result

numbers = [1, 2, 3, 2, 1, 4, 5, 4]
unique = remove_duplicates_ordered(numbers)
print(unique)         # Output: [1, 2, 3, 4, 5] (order preserved)

# Finding unique elements
words = ["apple", "banana", "apple", "cherry", "banana"]
unique_words = set(words)
print(f"Unique words: {len(unique_words)}")  # Output: Unique words: 3

# Counting unique values
text = "mississippi"
unique_letters = set(text)
print(f"Unique letters in '{text}': {unique_letters}")

# Checking for common elements
set1 = {1, 2, 3}
set2 = {3, 4, 5}
common = 3 in set1 and 3 in set2
print(common)         # Output: True

# Finding all vowels in a word
word = "hello"
vowels = {'a', 'e', 'i', 'o', 'u'}
found_vowels = set(word) & vowels
print(f"Vowels in '{word}': {found_vowels}")

# Real-world example: tracking visited pages
visited = set()
pages = [1, 2, 3, 2, 1, 4, 5, 4]

for page in pages:
    if page not in visited:
        visited.add(page)
        print(f"Visiting page {page}")

print(f"Total unique pages visited: {len(visited)}")

# Real-world example: tag system
post_tags = {"python", "programming", "tutorial"}
post_tags.add("beginner")
print(post_tags)

post_tags.remove("tutorial")
print(post_tags)
```

### Guided Practice

**Warm-up (5 minutes):**
1. Create a set with 5 numbers
2. Add a new element
3. Check if an element is in the set
4. Remove an element safely using discard()

**Activity (35 minutes):**
1. Create sets from different data types
2. Practice add() and remove() operations
3. Test membership with in operator
4. Remove duplicates from a list
5. Preserve order while deduplicating
6. Find unique elements in data
7. Iterate through sets
8. Convert between sets and lists

**Challenge (10 minutes):**
Create a program that tracks unique website visits and calculates statistics.

### Practice Problems

**Problem 1 — Beginner:** Basic set operations
```python
# TODO: Create a set with 5 numbers
# TODO: Add a new element
# TODO: Remove an element
# TODO: Check if a number is in the set
# TODO: Print the set and its length
```

**Problem 2 — Intermediate:** Remove duplicates
```python
# Given a list with duplicates:
data = [1, 2, 3, 2, 1, 4, 5, 4, 3]

# TODO: Remove duplicates using set()
# TODO: Remove duplicates while preserving order
# TODO: Count how many unique values
```

**Problem 3 — Challenge:** Find unique characters
```python
# Given these strings:
text1 = "hello"
text2 = "world"

# TODO: Find all unique characters in both strings combined
# TODO: Find characters that appear in both strings
# TODO: Find characters unique to each string
# TODO: Count total unique characters
```

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Create with curly braces or set()
- add() and remove() are methods
- Use `in` for membership testing

**Problem 2:**
- set(list) removes duplicates but loses order
- Use a loop with a set to track seen items
- len() gives total unique values

**Problem 3:**
- Convert strings to sets
- & operator finds intersection (common characters)
- - operator finds difference (unique to one)

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
numbers = {1, 2, 3, 4, 5}
numbers.add(6)
numbers.remove(1)
print(3 in numbers)
print(numbers, len(numbers))

# Problem 2
data = [1, 2, 3, 2, 1, 4, 5, 4, 3]
unique = set(data)
print(unique)

unique_ordered = []
seen = set()
for x in data:
    if x not in seen:
        unique_ordered.append(x)
        seen.add(x)
print(unique_ordered)
print(len(unique))

# Problem 3
set1 = set("hello")
set2 = set("world")
all_chars = set1 | set2
common = set1 & set2
unique1 = set1 - set2
unique2 = set2 - set1
print(f"All: {all_chars}, Common: {common}")
```

</details>
