# Day 4: Higher-Order Functions - map() and filter()

**Learning Target:** I can use map() and filter() to transform and select elements from sequences using functions.

---

## Key Concepts

**Higher-Order Function** — A function that takes another function as an argument or returns a function. `map()` and `filter()` are built-in higher-order functions.

**map(function, iterable)** — Applies a function to every element in an iterable and returns a new iterable (iterator) of the results. It transforms each item.

**filter(function, iterable)** — Applies a function to every element and returns a new iterable with only the elements where the function returns `True`. It selects items.

**Important:** Both `map()` and `filter()` return iterator objects, not lists. You often need to convert them with `list()` to see the results.

**When to use map():** When you want to transform every element in a sequence (e.g., convert all strings to uppercase, square all numbers).

**When to use filter():** When you want to keep only certain elements from a sequence (e.g., keep only even numbers, keep only non-empty strings).

---

## Code Examples

```python
# Example 1: map() - transform every element
numbers = [1, 2, 3, 4, 5]
squared = map(lambda x: x ** 2, numbers)
print(list(squared))  # Output: [1, 4, 9, 16, 25]

# Example 2: map() with a named function
def celsius_to_fahrenheit(c):
    return (c * 9/5) + 32

celsius_temps = [0, 10, 20, 30]
fahrenheit_temps = map(celsius_to_fahrenheit, celsius_temps)
print(list(fahrenheit_temps))  # Output: [32.0, 50.0, 68.0, 86.0]

# Example 3: filter() - select elements
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = filter(lambda x: x % 2 == 0, numbers)
print(list(evens))  # Output: [2, 4, 6, 8, 10]

# Example 4: filter() with a named function
def is_long_word(word):
    return len(word) > 4

words = ["cat", "elephant", "dog", "python", "bird"]
long_words = filter(is_long_word, words)
print(list(long_words))  # Output: ['elephant', 'python']

# Example 5: Chaining map() and filter()
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
# Get only even numbers, then square them
result = list(map(lambda x: x ** 2, filter(lambda x: x % 2 == 0, numbers)))
print(result)  # Output: [4, 16, 36, 64, 100]

# Example 6: map() with multiple iterables
list1 = [1, 2, 3]
list2 = [4, 5, 6]
sums = map(lambda x, y: x + y, list1, list2)
print(list(sums))  # Output: [5, 7, 9]

# Example 7: Real-world example - processing user data
users = [
    {"name": "Alice", "age": 25},
    {"name": "Bob", "age": 17},
    {"name": "Charlie", "age": 30},
]

# Extract just names using map
names = list(map(lambda u: u["name"], users))
print(names)  # Output: ['Alice', 'Bob', 'Charlie']

# Filter adults (18+)
adults = list(filter(lambda u: u["age"] >= 18, users))
print(adults)  # Output: [{'name': 'Alice', 'age': 25}, {'name': 'Charlie', 'age': 30}]

# Example 8: Converting strings to numbers
string_numbers = ["1", "2", "3", "4", "5"]
int_numbers = list(map(int, string_numbers))
print(int_numbers)  # Output: [1, 2, 3, 4, 5]

strings = [" hello ", "  world  ", "python"]
trimmed = list(map(str.strip, strings))
print(trimmed)  # Output: ['hello', 'world', 'python']
```

---

## Guided Practice

**Step 1:** Use `map()` to convert a list of temperatures from Celsius to Fahrenheit.
```python
celsius = [0, 10, 20, 30, 40]
fahrenheit = list(map(lambda c: (c * 9/5) + 32, celsius))
print(fahrenheit)  # Should print: [32.0, 50.0, 68.0, 86.0, 104.0]
```

**Step 2:** Use `filter()` to keep only words longer than 4 characters.
```python
words = ["cat", "elephant", "dog", "python", "ant", "butterfly"]
long_words = list(filter(lambda w: len(w) > 4, words))
print(long_words)  # Should print: ['elephant', 'python', 'butterfly']
```

**Step 3:** Use `map()` to convert a list of strings to integers.
```python
string_nums = ["10", "20", "30", "40"]
integers = list(map(int, string_nums))
print(integers)  # Should print: [10, 20, 30, 40]
```

**Step 4:** Chain `filter()` and `map()` to get the squares of only even numbers.
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8]
result = list(map(lambda x: x ** 2, filter(lambda x: x % 2 == 0, numbers)))
print(result)  # Should print: [4, 16, 36, 64]
```

**Step 5:** Use `map()` to extract a specific field from a list of dictionaries.
```python
students = [
    {"name": "Alice", "grade": 11},
    {"name": "Bob", "grade": 10},
    {"name": "Charlie", "grade": 11},
]
names = list(map(lambda s: s["name"], students))
print(names)  # Should print: ['Alice', 'Bob', 'Charlie']
```

---

## Practice Problems

**Beginner:** Use `map()` to double every number in a list.

**Intermediate:** Use `filter()` to keep only strings that contain the letter "a", then use `map()` to convert them all to uppercase.

**Challenge:** Create a function that takes a list of products (with price and discount fields) and returns the final prices after applying discounts using `map()`.

<details>
<summary>💡 Hints</summary>
- For Beginner: `map(lambda x: x * 2, numbers)`
- For Intermediate: Chain `filter()` and `map()` together
- For Challenge: Create a lambda that calculates `price * (1 - discount)`
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
numbers = [1, 2, 3, 4, 5]
doubled = list(map(lambda x: x * 2, numbers))
print(doubled)  # Output: [2, 4, 6, 8, 10]

# Intermediate
words = ["apple", "banana", "cherry", "date", "elephant"]
result = list(map(str.upper, filter(lambda w: "a" in w, words)))
print(result)  # Output: ['APPLE', 'BANANA', 'DATE']

# Challenge
def apply_discounts(products):
    return list(map(lambda p: p["price"] * (1 - p["discount"]), products))

products = [
    {"name": "Book", "price": 20, "discount": 0.1},
    {"name": "Pen", "price": 5, "discount": 0.2},
]
final_prices = apply_discounts(products)
print(final_prices)  # Output: [18.0, 4.0]
```
</details>
