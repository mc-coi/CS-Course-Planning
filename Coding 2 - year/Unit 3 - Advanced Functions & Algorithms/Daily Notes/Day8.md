# Day 8: Dictionary and Set Comprehensions Deep Dive

**Learning Target:** I can use dictionary and set comprehensions to transform and filter data into these structures efficiently.

---

## Key Concepts

**Dictionary Comprehension** — `{key_expr: value_expr for item in iterable}` creates a dictionary from an iterable.

**Set Comprehension** — `{expr for item in iterable}` creates a set (unique values) from an iterable.

**Key Difference from List:**
- List keeps duplicates and order
- Set removes duplicates automatically
- Dictionary maps keys to values

**Common patterns:**
- Invert a dictionary: `{v: k for k, v in dict.items()}`
- Filter a dictionary: `{k: v for k, v in dict.items() if condition}`
- Transform keys or values: `{transform(k): v for k, v in dict.items()}`

---

## Code Examples

```python
# Example 1: Basic dictionary comprehension
numbers = [1, 2, 3, 4, 5]
number_squares = {x: x ** 2 for x in numbers}
print(number_squares)  # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Example 2: Dictionary from two lists (zipping concept)
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 28]
person_dict = {name: age for name, age in zip(names, ages)}
print(person_dict)  # {'Alice': 25, 'Bob': 30, 'Charlie': 28}

# Example 3: Filtering dictionary
prices = {"apple": 1.20, "banana": 0.50, "cherry": 2.00, "date": 1.50}
expensive = {item: price for item, price in prices.items() if price > 1}
print(expensive)  # {'apple': 1.2, 'cherry': 2.0, 'date': 1.5}

# Example 4: Inverting a dictionary (swap keys and values)
person_dict = {'Alice': 25, 'Bob': 30, 'Charlie': 28}
age_to_name = {age: name for name, age in person_dict.items()}
print(age_to_name)  # {25: 'Alice', 30: 'Bob', 28: 'Charlie'}

# Example 5: Transforming keys and values
words = ["hello", "world", "python"]
# Map word to length and uppercase
transformed = {word.upper(): len(word) for word in words}
print(transformed)  # {'HELLO': 5, 'WORLD': 5, 'PYTHON': 6}

# Example 6: Basic set comprehension
numbers = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
unique_numbers = {x for x in numbers}
print(unique_numbers)  # {1, 2, 3, 4}

# Example 7: Set comprehension with transformation
words = ["apple", "banana", "apricot", "cherry"]
first_letters = {word[0] for word in words}
print(first_letters)  # {'a', 'b', 'c'}

# Example 8: Set comprehension with filtering
numbers = range(1, 11)
even_squares = {x ** 2 for x in numbers if x % 2 == 0}
print(even_squares)  # {4, 16, 36, 64, 100}

# Example 9: Real-world example - group words by length
words = ["cat", "elephant", "dog", "python", "ant", "butterfly"]
by_length = {}
for word in words:
    length = len(word)
    if length not in by_length:
        by_length[length] = []
    by_length[length].append(word)

# Same thing with comprehension (more complex but elegant)
by_length = {
    length: [word for word in words if len(word) == length]
    for length in set(len(w) for w in words)
}
print(by_length)
# {3: ['cat', 'dog', 'ant'], 6: ['python'], 8: ['elephant', 'butterfly']}

# Example 10: Nested structure transformation
students = {
    "Alice": [85, 90, 88],
    "Bob": [78, 82, 80],
    "Charlie": [92, 95, 90],
}
# Map students to their average scores
averages = {name: sum(scores) / len(scores) for name, scores in students.items()}
print(averages)  # {'Alice': 87.666..., 'Bob': 80.0, 'Charlie': 92.333...}

# Example 11: Set from dictionary keys
person_dict = {'Alice': 25, 'Bob': 30, 'Charlie': 28}
names_set = {name for name in person_dict}
print(names_set)  # {'Alice', 'Bob', 'Charlie'}

# Example 12: Multiple conditions in set comprehension
numbers = range(1, 21)
# Numbers divisible by 2 or 3
divisible = {x for x in numbers if x % 2 == 0 or x % 3 == 0}
print(divisible)  # {2, 3, 4, 6, 8, 9, 12, 15, 16, 18, 20}
```

---

## Guided Practice

**Step 1:** Create a dictionary that maps words to their lengths.
```python
words = ["python", "code", "learning"]
word_lengths = {word: len(word) for word in words}
print(word_lengths)
# Should print: {'python': 6, 'code': 4, 'learning': 8}
```

**Step 2:** Create a dictionary from a list of tuples.
```python
data = [("apple", 1.20), ("banana", 0.50), ("cherry", 2.00)]
fruit_prices = {fruit: price for fruit, price in data}
print(fruit_prices)
# Should print: {'apple': 1.2, 'banana': 0.5, 'cherry': 2.0}
```

**Step 3:** Invert a dictionary (swap keys and values).
```python
original = {"a": 1, "b": 2, "c": 3}
inverted = {v: k for k, v in original.items()}
print(inverted)
# Should print: {1: 'a', 2: 'b', 3: 'c'}
```

**Step 4:** Create a set of unique first letters from a list of words.
```python
words = ["apple", "apricot", "banana", "blueberry", "cherry"]
first_letters = {word[0] for word in words}
print(first_letters)
# Should print: {'a', 'b', 'c'}
```

**Step 5:** Filter a dictionary to keep only items with values above a threshold.
```python
scores = {"Alice": 85, "Bob": 72, "Charlie": 90, "Diana": 68}
high_scores = {name: score for name, score in scores.items() if score >= 80}
print(high_scores)
# Should print: {'Alice': 85, 'Charlie': 90}
```

---

## Practice Problems

**Beginner:** Create a dictionary mapping numbers 1-5 to their cubes.

**Intermediate:** Create a set of all vowels that appear in a list of words.

**Challenge:** Create a dictionary where keys are categories and values are lists of items in that category (from a list of items with categories).

<details>
<summary>💡 Hints</summary>
- For Beginner: `{x: x ** 3 for x in range(1, 6)}`
- For Intermediate: Flatten all letters and keep vowels: `{letter for word in words for letter in word if letter in "aeiou"}`
- For Challenge: Nested comprehension where value is itself a comprehension
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
cubes = {x: x ** 3 for x in range(1, 6)}
print(cubes)  # Output: {1: 1, 2: 8, 3: 27, 4: 64, 5: 125}

# Intermediate
words = ["apple", "banana", "elephant"]
vowels = {letter for word in words for letter in word if letter in "aeiou"}
print(vowels)  # Output: {'a', 'e', 'o'}

# Challenge
items = [
    {"name": "Apple", "category": "Fruit"},
    {"name": "Banana", "category": "Fruit"},
    {"name": "Carrot", "category": "Vegetable"},
]
by_category = {
    category: [item["name"] for item in items if item["category"] == category]
    for category in set(item["category"] for item in items)
}
print(by_category)
# Output: {'Fruit': ['Apple', 'Banana'], 'Vegetable': ['Carrot']}
```
</details>
