# Day 8: Special Methods
**Learning Target:** I can implement dunder methods (__str__, __repr__, __len__, __eq__).

### Key Concepts
**Dunder methods** (double underscore) allow objects to behave like built-in types.

- `__str__()` — user-friendly string representation
- `__repr__()` — developer-friendly representation
- `__len__()` — support len()
- `__eq__()` — support == comparison
- `__lt__()`, `__gt__()` — support <, >

### Code Examples
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name}, age {self.age}"

    def __repr__(self):
        return f"Person('{self.name}', {self.age})"

    def __eq__(self, other):
        return self.age == other.age

    def __lt__(self, other):
        return self.age < other.age

p1 = Person("Alice", 30)
p2 = Person("Bob", 25)

print(str(p1))    # "Alice, age 30"
print(repr(p1))   # "Person('Alice', 30)"
print(p1 == p2)   # False
print(p2 < p1)    # True (Bob is younger)
```

### Guided Practice
Create a Book class with __str__, __eq__ (compare by title), and __lt__ (compare by page count).

### Practice Problems
**Problem 1 — Beginner:** Add __str__ to a class you created earlier.

**Problem 2 — Intermediate:** Create a Vector class with __eq__, __lt__, and __len__.

**Problem 3 — Challenge:** Create a Money class with __str__, __add__, __sub__, __eq__, __lt__.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1: Already shown above

# Problem 2
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __len__(self):
        return int((self.x**2 + self.y**2) ** 0.5)

    def __str__(self):
        return f"({self.x}, {self.y})"
```
</details>

---
