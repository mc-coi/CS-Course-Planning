# Unit 1: Data Structures — Complete Answer Key

---

## Beginner Problems

---

## Problem 1.1: List Indexing and Slicing

### Solution
```python
numbers = [10, 20, 30, 40, 50, 60, 70]

first = numbers[0]           # First element
middle = numbers[len(numbers) // 2]  # Middle element (index 3)
last = numbers[-1]           # Last element
first_half = numbers[:4]     # First 4 elements (index 0-3)
last_half = numbers[4:]      # Last 3 elements (index 4-6)

print(f"First: {first}, Middle: {middle}, Last: {last}")
print(f"First half: {first_half}, Last half: {last_half}")
```

### Expected Output
```
First: 10, Middle: 40, Last: 70
First half: [10, 20, 30, 40], Last half: [50, 60, 70]
```

### Common Mistakes
- Using `len(numbers) / 2` instead of `len(numbers) // 2` (results in float)
- Forgetting that negative indices count from the end (-1 is last element)
- Using `numbers[4]` instead of `numbers[4:]` for the last half (would give single element)

---

## Problem 1.2: Dictionary Creation and Access

### Solution
```python
book = {
    "title": "Python 101",
    "author": "Guido",
    "year": 2015,
    "pages": 350
}

print(book["title"])  # Print the title
book["year"] = 2020   # Modify the year
book["rating"] = 4.5  # Add new key-value pair
print(book)           # Print entire dictionary
```

### Expected Output
```
Python 101
{'title': 'Python 101', 'author': 'Guido', 'year': 2020, 'pages': 350, 'rating': 4.5}
```

### Common Mistakes
- Using `book.title` instead of `book["title"]` for access (dot notation only works for attributes)
- Forgetting quotes around dictionary keys when accessing them
- Not updating the variable, just accessing it (e.g., `book["year"]` without assignment)

---

## Problem 1.3: List Methods

### Solution
```python
numbers = [5, 2, 8, 1, 9]

numbers.append(10)   # Add 10 to end
numbers.remove(1)    # Remove the value 1
numbers.sort()       # Sort in ascending order

print(numbers)
```

### Expected Output
```
[2, 5, 8, 9, 10]
```

### Common Mistakes
- Using `numbers.remove(2)` instead of `numbers.remove(1)` (removes by value, not index)
- Trying to use `numbers.sort()` and expecting a return value; `.sort()` modifies in-place
- Forgetting that `.append()` adds to the end, not beginning

---

## Problem 1.4: Tuple Creation and Unpacking

### Solution
```python
point = (10, 20)
x, y = point

print(f"Point: ({x}, {y})")

from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(10, 20)
print(f"Point.x = {p.x}, Point.y = {p.y}")
```

### Expected Output
```
Point: (10, 20)
Point.x = 10, Point.y = 20
```

### Common Mistakes
- Trying to unpack with wrong number of variables (e.g., `x, y, z = point` fails)
- Forgetting that tuples are immutable—cannot modify after creation
- Using `namedtuple('Point', 'x y')` (string) instead of `['x', 'y']` (list) for fields—both work, but list is clearer

---

## Problem 1.5: Set Operations

### Solution
```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

union = set1 | set2              # Union: {1, 2, 3, 4, 5, 6}
intersection = set1 & set2       # Intersection: {3, 4}
difference = set1 - set2         # Difference: {1, 2}

print(f"Union: {union}")
print(f"Intersection: {intersection}")
print(f"Difference (set1 - set2): {difference}")
```

### Expected Output
```
Union: {1, 2, 3, 4, 5, 6}
Intersection: {3, 4}
Difference (set1 - set2): {1, 2}
```

### Common Mistakes
- Confusing `set1 | set2` (union) with `set1 & set2` (intersection)
- Forgetting that sets are unordered—output order may vary but contents will match
- Using `set1 - set2` vs `set2 - set1` (order matters for difference operations)

---

## Intermediate Problems

---

## Problem 2.1: List Comprehension for Transformation

### Solution
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

squares = [x**2 for x in numbers]                    # [1, 4, 9, 16, ...]
evens = [x for x in numbers if x % 2 == 0]         # [2, 4, 6, 8, 10]
greater_than_5 = [x for x in numbers if x > 5]     # [6, 7, 8, 9, 10]

print(f"Squares: {squares}")
print(f"Evens: {evens}")
print(f"Greater than 5: {greater_than_5}")
```

### Expected Output
```
Squares: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
Evens: [2, 4, 6, 8, 10]
Greater than 5: [6, 7, 8, 9, 10]
```

### Common Mistakes
- Using `if x % 2 == 1` for evens instead of `== 0` (1 is odd)
- Forgetting to square the variable: `[x for x in numbers]` instead of `[x**2 for ...]`
- Placing condition before the for clause: `[if x > 5 for x in numbers]` is invalid syntax

---

## Problem 2.2: Dictionary from Parallel Lists

### Solution
```python
names = ["Alice", "Bob", "Charlie"]
ages = [15, 16, 17]

person_ages = dict(zip(names, ages))  # {'Alice': 15, 'Bob': 16, 'Charlie': 17}

for name in names:
    print(f"{name}: {person_ages[name]}")
```

### Expected Output
```
Alice: 15
Bob: 16
Charlie: 17
```

### Common Mistakes
- Forgetting `dict()` wrapper—`zip()` returns iterator, need to convert to dict
- Confusing which list maps to keys vs values (names→keys, ages→values)
- Lists having different lengths—`zip()` stops at shortest list

---

## Problem 2.3: Nested Dictionary Access

### Solution
```python
student = {
    "name": "Alice",
    "grades": {
        "Math": 95,
        "English": 87,
        "Science": 92
    }
}

# Safe access using .get() with defaults
english_grade = student.get("grades", {}).get("English", "N/A")
missing_grade = student.get("grades", {}).get("History", "Not found")

print(f"English grade: {english_grade}")
print(f"Missing grade: {missing_grade}")
```

### Expected Output
```
English grade: 87
Missing grade: Not found
```

### Common Mistakes
- Using `student["grades"]["History"]` without .get() (KeyError if key missing)
- Not chaining .get() properly—`.get("grades")` alone returns None if key missing
- Providing wrong default—should be string "N/A" not integer 0

---

## Problem 2.4: Count Frequencies

### Solution
```python
text = "programming"

# Method 1: Using dictionary with .get()
freq = {}
for char in text:
    freq[char] = freq.get(char, 0) + 1

print(freq)

# Method 2: Using Counter (simpler)
from collections import Counter
freq = Counter(text)
print(dict(freq))
```

### Expected Output
```
{'p': 1, 'r': 2, 'o': 1, 'g': 2, 'a': 1, 'm': 2, 'i': 1, 'n': 1}
{'p': 1, 'r': 2, 'o': 1, 'g': 2, 'a': 1, 'm': 2, 'i': 1, 'n': 1}
```

### Common Mistakes
- Using `freq[char] += 1` without initializing with 0 first (KeyError)
- Using `freq.get(char, 1)` instead of `freq.get(char, 0)` (adds 1+1=2 on first occurrence)
- Forgetting `freq.get(char, 0)` entirely and trying direct increment

---

## Problem 2.5: Remove Duplicates Preserving Order

### Solution
```python
items = [1, 2, 2, 3, 1, 4, 3, 5]

# Method 1: Using set to track seen items
seen = set()
unique_items = []
for item in items:
    if item not in seen:
        seen.add(item)
        unique_items.append(item)

print(unique_items)  # [1, 2, 3, 4, 5]

# Method 2: If order doesn't matter (simpler)
unique_items2 = list(dict.fromkeys(items))  # Preserves order in Python 3.7+
print(unique_items2)  # [1, 2, 3, 4, 5]
```

### Expected Output
```
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5]
```

### Common Mistakes
- Using `list(set(items))` which loses the original order: [1, 2, 3, 4, 5] order is random
- Not using a set to track seen items (O(n²) time if checking `item in unique_items`)
- Forgetting to `add()` item to seen set after appending

---

## Challenge Problems

---

## Problem 3.1: Transpose a 2D List

### Solution
```python
def transpose(matrix):
    """Transpose a 2D list (swap rows and columns)."""
    return [list(row) for row in zip(*matrix)]

# Test
matrix = [
    [1, 2, 3],
    [4, 5, 6]
]
transposed = transpose(matrix)
print(transposed)  # [[1, 4], [2, 5], [3, 6]]
```

### Expected Output
```
[[1, 4], [2, 5], [3, 6]]
```

### Common Mistakes
- Using `[[matrix[i][j] for i in range(len(matrix))] for j in range(len(matrix[0]))]` works but is verbose
- Forgetting that `zip(*matrix)` unpacks rows and pairs them by column
- Returning tuples instead of lists: `[row for row in zip(*matrix)]` returns list of tuples

---

## Problem 3.2: Grade Analysis System

### Solution
```python
def analyze_grades(grades_dict):
    """
    Analyze student grades.
    Args: grades_dict = {"student_name": [grade1, grade2, ...]}
    Returns: dict with analysis results
    """
    # Calculate averages for each student
    averages = {name: sum(grades) / len(grades)
                for name, grades in grades_dict.items()}

    # Class average
    class_average = sum(averages.values()) / len(averages)

    # Top student (highest average)
    top_student = max(averages, key=averages.get)

    # Struggling students (average < 70)
    struggling = [name for name, avg in averages.items() if avg < 70]

    return {
        "averages": averages,
        "class_average": class_average,
        "top_student": top_student,
        "struggling_students": struggling
    }

# Test
grades = {
    "Alice": [95, 92, 88],
    "Bob": [65, 70, 68],
    "Charlie": [88, 85, 90]
}

results = analyze_grades(grades)
print(results)
```

### Expected Output
```
{
    'averages': {'Alice': 91.67, 'Bob': 67.67, 'Charlie': 87.67},
    'class_average': 82.33,
    'top_student': 'Alice',
    'struggling_students': ['Bob']
}
```

### Common Mistakes
- Calculating class average by averaging the sums instead of sum of all grades / count
- Using `min()` instead of `max()` for top student
- Using `>= 70` instead of `< 70` for struggling students
- Forgetting to return a dictionary of results

---

## Problem 3.3: Find Anagrams

### Solution
```python
def find_anagrams(words):
    """Group words that are anagrams of each other."""
    anagrams = {}
    for word in words:
        # Sort letters to create a key
        key = "".join(sorted(word))
        if key not in anagrams:
            anagrams[key] = []
        anagrams[key].append(word)
    return anagrams

# Test
words = ["listen", "silent", "hello", "elloh", "world", "list"]
result = find_anagrams(words)
print(result)
```

### Expected Output
```
{'eilnst': ['listen', 'silent'], 'ehllo': ['hello', 'elloh'], 'dlorw': ['world'], 'ilts': ['list']}
```

### Common Mistakes
- Using `sorted(word)` which returns a list, then needing `"".join()` to make a string key
- Using the unsorted word as key (won't group anagrams correctly)
- Case sensitivity: "Listen" vs "listen" won't match unless normalized to lower()

---

## Problem 3.4: Vending Machine Inventory

### Solution
```python
class VendingMachine:
    """Manage vending machine products and inventory."""

    def __init__(self):
        self.products = {}  # {product_id: {"name": ..., "price": ..., "quantity": ...}}

    def add_product(self, product_id, name, price, quantity):
        """Add a product to inventory."""
        self.products[product_id] = {
            "name": name,
            "price": price,
            "quantity": quantity
        }

    def buy_product(self, product_id, quantity):
        """Buy product. Return cost if successful, None if not possible."""
        if product_id not in self.products:
            return None
        if self.products[product_id]["quantity"] < quantity:
            return None

        self.products[product_id]["quantity"] -= quantity
        return quantity * self.products[product_id]["price"]

    def restock(self, product_id, quantity):
        """Add quantity to existing product."""
        if product_id in self.products:
            self.products[product_id]["quantity"] += quantity

    def get_inventory(self):
        """Return all products."""
        return self.products

    def get_product(self, product_id):
        """Get specific product info."""
        return self.products.get(product_id, None)

# Test
vm = VendingMachine()
vm.add_product("A1", "Soda", 1.50, 10)
vm.add_product("A2", "Chips", 0.99, 20)

print(vm.get_product("A1"))
print(vm.buy_product("A1", 2))
print(vm.get_product("A1"))
```

### Expected Output
```
{'name': 'Soda', 'price': 1.50, 'quantity': 10}
3.0
{'name': 'Soda', 'price': 1.50, 'quantity': 8}
```

### Common Mistakes
- Not checking if product exists before buying
- Not checking if sufficient quantity before allowing purchase
- Decrementing quantity after checking, not before returning cost
- Using wrong dictionary keys

---

## Problem 3.5: Word Association Game

### Solution
```python
class WordAssociation:
    """Manage word-to-category associations."""

    def __init__(self):
        self.category_words = {}  # {category: [words]}
        self.word_category = {}   # {word: category}

    def add_association(self, word, category):
        """Add word to a category."""
        if category not in self.category_words:
            self.category_words[category] = []
        self.category_words[category].append(word)
        self.word_category[word] = category

    def get_words_in_category(self, category):
        """Return all words in a category."""
        return self.category_words.get(category, [])

    def get_category(self, word):
        """Return category for a word."""
        return self.word_category.get(word, None)

    def get_all_categories(self):
        """Return all categories."""
        return list(self.category_words.keys())

# Test
game = WordAssociation()
game.add_association("Apple", "Fruit")
game.add_association("Banana", "Fruit")
game.add_association("Carrot", "Vegetable")

print(game.get_words_in_category("Fruit"))     # ['Apple', 'Banana']
print(game.get_category("Apple"))              # 'Fruit'
print(game.get_all_categories())               # ['Fruit', 'Vegetable']
```

### Expected Output
```
['Apple', 'Banana']
Fruit
['Fruit', 'Vegetable']
```

### Common Mistakes
- Only using one dictionary (category_words OR word_category) instead of both
- Not initializing the category list before appending words
- Using `word_category.get(word)` without default (returns None for missing keys)
- Returning string instead of list for `get_all_categories()`

---
