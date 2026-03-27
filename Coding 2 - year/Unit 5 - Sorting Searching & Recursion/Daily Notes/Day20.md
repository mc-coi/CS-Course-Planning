# Day 20: Sorting with sorted() & Advanced Key Functions

**Learning Target:** I can use complex key functions and solve sorting challenges with built-in Python sort.

---

## Key Concepts

**Key Function:**
- A function passed to `key=` that extracts a "comparison value" from each element
- Applied once per element during sorting
- Dramatically simplifies complex sorting problems

**Lambda vs. Regular Functions:**
```python
sorted(data, key=lambda x: x[1])       # Quick lambda
sorted(data, key=operator.itemgetter(1)) # More efficient for tuples
```

**Common Key Functions:**
- `str.lower` — case-insensitive string sort
- `len` — sort by length
- `abs` — sort by absolute value
- `operator.itemgetter(index)` — extract item from tuple/dict
- Custom lambda — any transformation

---

## Code Examples

```python
# Advanced key function examples

# 1. Sorting with multiple sort orders
records = [
    ('Alice', 25, 60000),
    ('Bob', 30, 55000),
    ('Charlie', 25, 65000)
]

# Sort by age (ascending), then salary (descending)
sorted_records = sorted(records, key=lambda r: (r[1], -r[2]))
print(sorted_records)
# Output: [('Alice', 25, 60000), ('Charlie', 25, 65000), ('Bob', 30, 55000)]

# 2. Sorting with custom object
class Product:
    def __init__(self, name, price, rating):
        self.name = name
        self.price = price
        self.rating = rating

    def __repr__(self):
        return f"{self.name}: ${self.price} ({self.rating}★)"

products = [
    Product('Laptop', 1000, 4.5),
    Product('Mouse', 25, 4.8),
    Product('Monitor', 300, 4.2)
]

# Sort by rating (descending), then price (ascending)
best_deals = sorted(products, key=lambda p: (-p.rating, p.price))
print(best_deals)

# 3. Case-insensitive sorting with original case preserved
names = ['alice', 'Charlie', 'bob', 'Diana']
sorted_names = sorted(names, key=str.lower)
print(sorted_names)  # ['alice', 'bob', 'Charlie', 'Diana']

# 4. Sorting a list of paths
import os
paths = ['/home/user/file.txt', '/home/user/docs/notes.txt', '/home/file2.txt']

# Sort by filename only
sorted_paths = sorted(paths, key=os.path.basename)
print(sorted_paths)

# 5. Natural sort (1, 2, 10 instead of 1, 10, 2)
import re

def natural_sort_key(text):
    """Convert text to list of alternating strings and integers."""
    return [int(c) if c.isdigit() else c for c in re.split('([0-9]+)', text)]

filenames = ['file1.txt', 'file10.txt', 'file2.txt', 'file20.txt']
natural_sorted = sorted(filenames, key=natural_sort_key)
print(natural_sorted)  # ['file1.txt', 'file2.txt', 'file10.txt', 'file20.txt']

# 6. Sorting with operator module (efficient for tuples)
import operator

# Sort tuples by second element
data = [(1, 'zebra'), (2, 'apple'), (3, 'banana')]
sorted_data = sorted(data, key=operator.itemgetter(1))
# More efficient than: sorted(data, key=lambda x: x[1])

# 7. Multi-key sorting with operator
# Sort by third element, then first element
sorted_data = sorted(data, key=operator.itemgetter(2, 0))

# 8. Stable sort demonstration
students = [
    ('Alice', 'A', 90),
    ('Bob', 'B', 80),
    ('Charlie', 'A', 88),
    ('Diana', 'B', 85)
]

# Sort by grade first
sorted_students = sorted(students, key=lambda s: s[1])
print("By grade:", sorted_students)

# Sort by grade, then by score (stable maintains original grade order for ties)
sorted_students = sorted(students, key=lambda s: (s[1], -s[2]))
print("By grade & score:", sorted_students)

# 9. Sorting with string methods
words = ['Python', 'JAVA', 'javascript', 'Ruby']

# Case-insensitive
sorted_words = sorted(words, key=str.lower)
print(sorted_words)

# 10. Complex real-world example: Sorting search results
search_results = [
    {'title': 'Python Basics', 'relevance': 0.95, 'views': 1000},
    {'title': 'Advanced Python', 'relevance': 0.90, 'views': 500},
    {'title': 'Python Tips', 'relevance': 0.90, 'views': 2000}
]

# Sort by relevance (descending), then views (descending)
sorted_results = sorted(search_results,
                        key=lambda r: (-r['relevance'], -r['views']))

for result in sorted_results:
    print(f"{result['title']}: {result['relevance']} ({result['views']} views)")

# 11. Decorate-sort-undecorate pattern (for complex sorting)
def complex_sort_key(item):
    """Example: sort by custom weighted score."""
    name, age, salary = item
    # Weight: age (descending) * 0.3 + salary (ascending) * 0.7
    score = -age * 0.3 + (salary / 1000) * 0.7
    return score

people = [
    ('Alice', 30, 50000),
    ('Bob', 25, 60000),
    ('Charlie', 30, 55000)
]

sorted_people = sorted(people, key=complex_sort_key)

# 12. When to use .sort() vs. sorted()
arr = [3, 1, 4, 1, 5]

# Use sorted() when:
#   - You need to keep original list
#   - Working with non-list iterables (tuples, sets, generators)
#   - Chaining methods

result = sorted(arr)
print([x * 2 for x in sorted(arr)])

# Use .sort() when:
#   - You want to modify list in-place (saves memory)
#   - You're done with the original order

arr.sort()
print(arr)  # arr is now sorted
```

---

## Guided Practice

**Activity 1: Multi-Level Sorting**

Given:
```python
employees = [
    ('Alice', 'Sales', 50000),
    ('Bob', 'IT', 60000),
    ('Charlie', 'Sales', 55000),
    ('Diana', 'IT', 58000)
]
```

Sort by department (ascending), then by salary (descending within each department).

**Activity 2: Custom Key Development**

Write a key function that sorts phone numbers in format "(XXX) XXX-XXXX" by area code first, then local exchange.

**Activity 3: Performance Impact**

For large data, discuss: Does the key function get called once per element or multiple times? (Answer: Once per element, so efficiency matters.)

---

## Practice Problems

**Beginner:** Sort a list of tuples (name, age) by age. Then sort by age, then by name alphabetically.

**Intermediate:** Sort a list of dictionaries with various key combinations and sort orders (some ascending, some descending).

**Challenge:** Implement natural sorting for file names with embedded numbers. Sort ['file1.txt', 'file10.txt', 'file2.txt'] in human-readable order.

<details>
<summary>💡 Hints</summary>
- **Beginner:** `sorted(tuples, key=lambda t: t[1])` for age; for multi-key use `key=lambda t: (t[1], t[0])`
- **Intermediate:** Use tuples with negation for descending: `key=lambda d: (d['dept'], -d['salary'])`
- **Challenge:** Split on numbers using regex, convert numbers to integers for proper comparison
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
employees = [('Alice', 25), ('Bob', 30), ('Charlie', 25)]
sorted_employees = sorted(employees, key=lambda e: (e[1], e[0]))

# Intermediate
people = [
    {'dept': 'Sales', 'salary': 50000},
    {'dept': 'IT', 'salary': 60000},
    {'dept': 'Sales', 'salary': 55000}
]
sorted_people = sorted(people, key=lambda p: (p['dept'], -p['salary']))

# Challenge
import re

def natural_key(filename):
    return [int(text) if text.isdigit() else text
            for text in re.split('([0-9]+)', filename)]

files = ['file1.txt', 'file10.txt', 'file2.txt']
sorted_files = sorted(files, key=natural_key)
```
</details>
