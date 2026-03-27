# Day 19: Python's Built-in Sorting & Timsort

**Learning Target:** I can use Python's sorted() and .sort() effectively and understand why Timsort is so fast.

---

## Key Concepts

**Python's Sorting Algorithm: Timsort**
- **Hybrid:** Combines insertion sort and merge sort
- **Adaptive:** Finds natural "runs" (sorted sequences) in the data
- **Stable:** Preserves relative order of equal elements
- **Time:** O(n) best case (already sorted), O(n log n) average/worst
- **Space:** O(n) for merging
- **Real-world:** Faster than pure merge or quick sort on real data

**When to Use sorted() vs. .sort():**
```python
sorted(iterable)        # Returns new sorted list, works on any iterable
list.sort()             # Sorts in-place, only on lists, returns None
```

---

## Code Examples

```python
# Basic usage
numbers = [5, 2, 8, 1, 9, 3]

# sorted() - creates new list
sorted_nums = sorted(numbers)
print(sorted_nums)  # [1, 2, 3, 5, 8, 9]
print(numbers)      # [5, 2, 8, 1, 9, 3] (unchanged)

# .sort() - modifies in-place
numbers.sort()
print(numbers)      # [1, 2, 3, 5, 8, 9]

# Reverse sorting
print(sorted(numbers, reverse=True))  # [9, 8, 5, 3, 2, 1]
numbers.sort(reverse=True)             # Modifies in-place

# Custom sorting with key parameter
students = [
    {'name': 'Alice', 'grade': 85},
    {'name': 'Bob', 'grade': 92},
    {'name': 'Charlie', 'grade': 78}
]

# Sort by grade
by_grade = sorted(students, key=lambda s: s['grade'])
print(by_grade)  # Sorted by grade

# Sort by name
by_name = sorted(students, key=lambda s: s['name'])
print(by_name)  # Sorted by name

# Custom key with functions
words = ['python', 'java', 'c', 'javascript']

# Sort by length
by_length = sorted(words, key=len)
print(by_length)  # ['c', 'java', 'python', 'javascript']

# Sort by custom function
def custom_key(word):
    return (len(word), word)  # Length, then alphabetical

sorted_words = sorted(words, key=custom_key)

# Sorting complex objects
class Student:
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa

    def __repr__(self):
        return f"Student({self.name}, {self.gpa})"

students_obj = [
    Student('Alice', 3.9),
    Student('Bob', 3.5),
    Student('Charlie', 3.7)
]

# Sort by GPA
by_gpa = sorted(students_obj, key=lambda s: s.gpa)
print(by_gpa)

# Multi-level sorting
people = [
    ('Alice', 25, 5000),
    ('Bob', 30, 6000),
    ('Charlie', 25, 5500)
]

# Sort by age, then by salary
sorted_people = sorted(people, key=lambda p: (p[1], p[2]))

# Case-insensitive string sorting
words = ['Python', 'apple', 'Zebra', 'banana']
case_insensitive = sorted(words, key=str.lower)
print(case_insensitive)  # ['apple', 'banana', 'Python', 'Zebra']

# Stability demonstration
data = [(1, 'a'), (2, 'b'), (1, 'c'), (2, 'd')]
sorted_data = sorted(data, key=lambda x: x[0])
# Result: [(1, 'a'), (1, 'c'), (2, 'b'), (2, 'd')]
# Notice: (1, 'a') comes before (1, 'c'), preserving original order

# Performance comparison
import time

def compare_builtin_vs_manual():
    arr = list(range(10000, 0, -1))  # Worst case

    # Built-in sort
    start = time.time()
    result = sorted(arr)
    builtin_time = time.time() - start

    # Quick sort (O(n log n) average)
    def quick_sort(a):
        if len(a) <= 1:
            return a
        pivot = a[len(a) // 2]
        left = [x for x in a if x < pivot]
        middle = [x for x in a if x == pivot]
        right = [x for x in a if x > pivot]
        return quick_sort(left) + middle + quick_sort(right)

    start = time.time()
    result = quick_sort(arr)
    manual_time = time.time() - start

    print(f"Built-in (Timsort): {builtin_time:.6f}s")
    print(f"Quick sort:         {manual_time:.6f}s")
    print(f"Built-in is {manual_time/builtin_time:.1f}x faster")

# Why Timsort wins
print("""
Timsort advantages:
1. Detects sorted sequences ("runs") and preserves them
2. Uses insertion sort on small runs (very fast for small data)
3. Merges runs intelligently (stable, predictable)
4. O(n) on sorted data (huge advantage for real data)
5. Highly optimized C implementation
""")
```

---

## Guided Practice

**Activity 1: Understanding key Parameter**

```python
# Sort tuples
people = [('Alice', 25), ('Bob', 30), ('Charlie', 25)]

# By first element (name)
sorted(people, key=lambda p: p[0])

# By second element (age)
sorted(people, key=lambda p: p[1])

# By age, then name
sorted(people, key=lambda p: (p[1], p[0]))
```

What's the sorted order for each?

**Activity 2: Stability Test**

Create a list with duplicate keys:
```python
data = [(2, 'first'), (1, 'a'), (2, 'second'), (1, 'b')]
```

Sort by first element. Do the second elements maintain relative order? (Yes, because Python's sort is stable.)

**Activity 3: Real-World Key Usage**

For a list of dictionaries representing transactions:
```python
transactions = [
    {'date': '2024-01-15', 'amount': 100},
    {'date': '2024-01-10', 'amount': 200},
    {'date': '2024-01-15', 'amount': 150}
]
```

Sort by date, then by amount.

---

## Practice Problems

**Beginner:** Sort a list of dictionaries by one field using sorted() with a key parameter.

**Intermediate:** Sort a list of strings by multiple criteria: first by length, then alphabetically within same length.

**Challenge:** Create a custom comparator class that can be used with sorted(). Make it compare objects by multiple fields with different sort orders (ascending/descending).

<details>
<summary>💡 Hints</summary>
- **Beginner:** Use `key=lambda d: d['field_name']`
- **Intermediate:** `key=lambda s: (len(s), s)` creates a tuple for multi-level sorting
- **Challenge:** Define __lt__, __le__, __gt__, __ge__ methods, or use functools.cmp_to_key
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
students = [
    {'name': 'Alice', 'gpa': 3.9},
    {'name': 'Bob', 'gpa': 3.5}
]
sorted_students = sorted(students, key=lambda s: s['gpa'], reverse=True)

# Intermediate
words = ['cat', 'a', 'hello', 'hi', 'on']
sorted_words = sorted(words, key=lambda w: (len(w), w))
# Result: ['a', 'hi', 'on', 'cat', 'hello']

# Challenge
from functools import cmp_to_key

def compare_tuples(a, b):
    # Compare by first element (ascending), then second (descending)
    if a[0] != b[0]:
        return a[0] - b[0]
    return b[1] - a[1]

data = [(1, 5), (2, 3), (1, 8), (2, 1)]
sorted_data = sorted(data, key=cmp_to_key(compare_tuples))
```
</details>
