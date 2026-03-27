# Unit 1: Data Structures — Practice Bank

This document contains 20 practice problems at three difficulty levels, complete with starter code and solutions.

---

## Beginner Problems (Foundational Skills)

### Problem 1.1: List Indexing and Slicing
Create a list of 7 numbers. Use indexing to print the first, middle, and last elements. Then use slicing to print the first half and last half.

```python
# Starter code:
numbers = [10, 20, 30, 40, 50, 60, 70]

# Your code here:
first = # TODO
middle = # TODO
last = # TODO
first_half = # TODO
last_half = # TODO

print(f"First: {first}, Middle: {middle}, Last: {last}")
print(f"First half: {first_half}, Last half: {last_half}")
```

**Solution:**
```python
numbers = [10, 20, 30, 40, 50, 60, 70]
first = numbers[0]
middle = numbers[len(numbers) // 2]
last = numbers[-1]
first_half = numbers[:4]
last_half = numbers[4:]

# Or more elegantly:
middle = numbers[3]  # Since we know length is 7
```

---

### Problem 1.2: Dictionary Creation and Access
Create a dictionary for a book with keys: title, author, year, pages. Then access and modify values.

```python
# Starter code:
book = # TODO: Create dictionary

# Add code to:
# 1. Print the title
# 2. Change the year to 2020
# 3. Add a new key "rating" with value 4.5
# 4. Print the entire dictionary

```

**Solution:**
```python
book = {
    "title": "Python 101",
    "author": "Guido",
    "year": 2015,
    "pages": 350
}

print(book["title"])
book["year"] = 2020
book["rating"] = 4.5
print(book)
```

---

### Problem 1.3: List Methods
Given a list of numbers, use list methods to: append a new number, remove a number, sort the list, and reverse it.

```python
# Starter code:
numbers = [5, 2, 8, 1, 9]

# Your code:
# 1. Append 10
# 2. Remove 1
# 3. Sort ascending
# 4. Print the result
```

**Solution:**
```python
numbers = [5, 2, 8, 1, 9]
numbers.append(10)
numbers.remove(1)
numbers.sort()
print(numbers)  # [2, 5, 8, 9, 10]
```

---

### Problem 1.4: Tuple Creation and Unpacking
Create a tuple representing a point (x, y). Unpack it into variables. Create a named tuple for a point with x, y coordinates.

```python
# Starter code:
point = # TODO: Create tuple
x, y = # TODO: Unpack

print(f"Point: ({x}, {y})")

# Named tuple:
from collections import namedtuple
Point = # TODO: Define named tuple
p = # TODO: Create Point instance
print(f"Point.x = {p.x}, Point.y = {p.y}")
```

**Solution:**
```python
point = (10, 20)
x, y = point
print(f"Point: ({x}, {y})")

from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(10, 20)
print(f"Point.x = {p.x}, Point.y = {p.y}")
```

---

### Problem 1.5: Set Operations
Create two sets of numbers. Find their union, intersection, and difference.

```python
# Starter code:
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

# Calculate:
union = # TODO
intersection = # TODO
difference = # TODO

print(f"Union: {union}")
print(f"Intersection: {intersection}")
print(f"Difference (set1 - set2): {difference}")
```

**Solution:**
```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

union = set1 | set2
intersection = set1 & set2
difference = set1 - set2

print(f"Union: {union}")  # {1, 2, 3, 4, 5, 6}
print(f"Intersection: {intersection}")  # {3, 4}
print(f"Difference: {difference}")  # {1, 2}
```

---

## Intermediate Problems (Application & Synthesis)

### Problem 2.1: List Comprehension for Transformation
Given a list of numbers, use list comprehensions to create: squares, even numbers only, and numbers greater than 5.

```python
# Starter code:
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

squares = # TODO: List comprehension
evens = # TODO: List comprehension with condition
greater_than_5 = # TODO: List comprehension with condition

print(f"Squares: {squares}")
print(f"Evens: {evens}")
print(f"Greater than 5: {greater_than_5}")
```

**Solution:**
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

squares = [x**2 for x in numbers]
evens = [x for x in numbers if x % 2 == 0]
greater_than_5 = [x for x in numbers if x > 5]
```

---

### Problem 2.2: Dictionary from Parallel Lists
Given two lists (names and ages), create a dictionary using `zip()`.

```python
# Starter code:
names = ["Alice", "Bob", "Charlie"]
ages = [15, 16, 17]

# Create dictionary using zip:
person_ages = # TODO

# Add code to look up each person's age
for name in names:
    print(f"{name}: {person_ages[name]}")
```

**Solution:**
```python
names = ["Alice", "Bob", "Charlie"]
ages = [15, 16, 17]

person_ages = dict(zip(names, ages))
# Or: {name: age for name, age in zip(names, ages)}

for name in names:
    print(f"{name}: {person_ages[name]}")
```

---

### Problem 2.3: Nested Dictionary Access
Create a dictionary representing a student with nested grade information. Access deeply nested values safely.

```python
# Starter code:
student = {
    "name": "Alice",
    "grades": {
        "Math": 95,
        "English": 87,
        "Science": 92
    }
}

# Access safely:
english_grade = # TODO: Use .get() for safe access
missing_grade = # TODO: Use .get() with default for missing subject

print(f"English grade: {english_grade}")
print(f"Missing grade: {missing_grade}")
```

**Solution:**
```python
student = {
    "name": "Alice",
    "grades": {
        "Math": 95,
        "English": 87,
        "Science": 92
    }
}

english_grade = student.get("grades", {}).get("English", "N/A")
missing_grade = student.get("grades", {}).get("History", "Not found")

print(f"English grade: {english_grade}")
print(f"Missing grade: {missing_grade}")
```

---

### Problem 2.4: Count Frequencies
Given a string, count the frequency of each character using a dictionary.

```python
# Starter code:
text = "programming"

# Count character frequencies:
freq = {}
for char in text:
    # TODO: Build frequency dictionary

print(freq)
# Expected: {'p': 1, 'r': 2, 'o': 1, 'g': 2, 'a': 1, 'm': 2, 'i': 1, 'n': 1}

# Bonus: Use .get() to count
```

**Solution:**
```python
text = "programming"

freq = {}
for char in text:
    freq[char] = freq.get(char, 0) + 1

print(freq)

# Or with Counter:
from collections import Counter
freq = Counter(text)
```

---

### Problem 2.5: Remove Duplicates Preserving Order
Remove duplicates from a list while preserving the original order.

```python
# Starter code:
items = [1, 2, 2, 3, 1, 4, 3, 5]

# Remove duplicates while preserving order:
unique_items = # TODO

print(unique_items)  # Expected: [1, 2, 3, 4, 5]
```

**Solution:**
```python
items = [1, 2, 2, 3, 1, 4, 3, 5]

# Method 1: Using set tracking
seen = set()
unique_items = []
for item in items:
    if item not in seen:
        seen.add(item)
        unique_items.append(item)

# Method 2: If order doesn't matter, just use set
unique_items = list(set(items))
```

---

## Challenge Problems (Synthesis & Creativity)

### Problem 3.1: Transpose a 2D List
Write a function to transpose a matrix (swap rows and columns).

```python
# Starter code:
def transpose(matrix):
    """Transpose a 2D list."""
    # TODO: Implement
    pass

# Test:
matrix = [
    [1, 2, 3],
    [4, 5, 6]
]
transposed = transpose(matrix)
# Expected:
# [
#     [1, 4],
#     [2, 5],
#     [3, 6]
# ]
print(transposed)
```

**Solution:**
```python
def transpose(matrix):
    return [list(row) for row in zip(*matrix)]

# Or using nested comprehension:
def transpose(matrix):
    return [[matrix[i][j] for i in range(len(matrix))] 
            for j in range(len(matrix[0]))]
```

---

### Problem 3.2: Grade Analysis System
Create a system to analyze student grades. Calculate averages, find top students, find struggling students.

```python
# Starter code:
def analyze_grades(grades_dict):
    """
    Analyze grades.
    Args: grades_dict = {"student_name": [grade1, grade2, ...]}
    Returns: dict with analysis results
    """
    # TODO: Calculate class average
    # TODO: Find top student (highest average)
    # TODO: Find struggling students (average < 70)
    # TODO: Return results as dictionary
    pass

# Test:
grades = {
    "Alice": [95, 92, 88],
    "Bob": [65, 70, 68],
    "Charlie": [88, 85, 90]
}

results = analyze_grades(grades)
print(results)
```

**Solution:**
```python
def analyze_grades(grades_dict):
    averages = {name: sum(grades)/len(grades) 
                for name, grades in grades_dict.items()}
    
    class_average = sum(averages.values()) / len(averages)
    top_student = max(averages, key=averages.get)
    struggling = [name for name, avg in averages.items() if avg < 70]
    
    return {
        "averages": averages,
        "class_average": class_average,
        "top_student": top_student,
        "struggling_students": struggling
    }
```

---

### Problem 3.3: Find Anagrams
Given a list of words, group them by anagrams.

```python
# Starter code:
def find_anagrams(words):
    """Group words that are anagrams of each other."""
    # TODO: Group anagrams
    # Hint: Sort the letters in each word - anagrams have same sorted letters
    pass

# Test:
words = ["listen", "silent", "hello", "elloh", "world", "list"]
result = find_anagrams(words)
print(result)
# Expected: {"eilnst": ["listen", "silent"], "ehllo": ["hello", "elloh"], "dlorw": ["world"], "ilts": ["list"]}
```

**Solution:**
```python
def find_anagrams(words):
    anagrams = {}
    for word in words:
        key = "".join(sorted(word))
        if key not in anagrams:
            anagrams[key] = []
        anagrams[key].append(word)
    return anagrams
```

---

### Problem 3.4: Vending Machine Inventory
Create a vending machine system that tracks products, prices, and quantities.

```python
# Starter code:
class VendingMachine:
    def __init__(self):
        # TODO: Initialize data structures
        pass
    
    def add_product(self, product_id, name, price, quantity):
        # TODO: Add product to inventory
        pass
    
    def buy_product(self, product_id, quantity):
        # TODO: Buy product (check stock, deduct, return cost)
        pass
    
    def restock(self, product_id, quantity):
        # TODO: Add quantity to existing product
        pass
    
    def get_inventory(self):
        # TODO: Return all products
        pass
    
    def get_product(self, product_id):
        # TODO: Get specific product info
        pass

# Test your implementation
vm = VendingMachine()
vm.add_product("A1", "Soda", 1.50, 10)
vm.add_product("A2", "Chips", 0.99, 20)

print(vm.get_product("A1"))
vm.buy_product("A1", 2)
print(vm.get_product("A1"))
```

**Solution:**
```python
class VendingMachine:
    def __init__(self):
        self.products = {}  # {product_id: {"name": ..., "price": ..., "quantity": ...}}
    
    def add_product(self, product_id, name, price, quantity):
        self.products[product_id] = {
            "name": name,
            "price": price,
            "quantity": quantity
        }
    
    def buy_product(self, product_id, quantity):
        if product_id not in self.products:
            return None
        if self.products[product_id]["quantity"] < quantity:
            return None
        self.products[product_id]["quantity"] -= quantity
        return quantity * self.products[product_id]["price"]
    
    def restock(self, product_id, quantity):
        if product_id in self.products:
            self.products[product_id]["quantity"] += quantity
    
    def get_inventory(self):
        return self.products
    
    def get_product(self, product_id):
        return self.products.get(product_id, None)
```

---

### Problem 3.5: Word Association Game
Create a system where words are associated with categories. Find all words in a category, find the category for a word, add associations.

```python
# Starter code:
class WordAssociation:
    def __init__(self):
        # TODO: Initialize data structures
        # Consider: {category: [words]} or {word: category}
        pass
    
    def add_association(self, word, category):
        # TODO: Add word to category
        pass
    
    def get_words_in_category(self, category):
        # TODO: Return all words in a category
        pass
    
    def get_category(self, word):
        # TODO: Return category for a word
        pass
    
    def get_all_categories(self):
        # TODO: Return all categories
        pass

# Test
game = WordAssociation()
game.add_association("Apple", "Fruit")
game.add_association("Banana", "Fruit")
game.add_association("Carrot", "Vegetable")

print(game.get_words_in_category("Fruit"))
print(game.get_category("Apple"))
```

**Solution:**
```python
class WordAssociation:
    def __init__(self):
        self.category_words = {}  # {category: [words]}
        self.word_category = {}   # {word: category}
    
    def add_association(self, word, category):
        if category not in self.category_words:
            self.category_words[category] = []
        self.category_words[category].append(word)
        self.word_category[word] = category
    
    def get_words_in_category(self, category):
        return self.category_words.get(category, [])
    
    def get_category(self, word):
        return self.word_category.get(word, None)
    
    def get_all_categories(self):
        return list(self.category_words.keys())
```

---

## Challenge Extensions

For each challenge problem, consider these extensions:

**Problem 3.1 (Transpose):**
- Handle non-rectangular matrices (jagged arrays)
- Create a function to rotate a matrix 90 degrees

**Problem 3.2 (Grades):**
- Add weighted grade calculation
- Track grade trends over time
- Export grades to different formats

**Problem 3.3 (Anagrams):**
- Find anagrams from a dictionary file
- Suggest word corrections based on anagrams

**Problem 3.4 (Vending Machine):**
- Add currency handling (coins, bills)
- Track sales history
- Generate sales reports

**Problem 3.5 (Word Association):**
- Make it bidirectional (word→category and category→word)
- Add multiple categories per word
- Add strength/confidence score to associations

