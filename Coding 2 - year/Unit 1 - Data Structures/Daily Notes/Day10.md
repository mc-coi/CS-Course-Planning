# Day 10: Tuple Use Cases & Named Tuples

**Learning Target:** I can use tuples effectively in real-world scenarios and leverage named tuples for clarity.

---

## Key Concepts

**Tuple use cases:**
- Return multiple values from a function
- Use as dictionary keys (lists can't be keys)
- Protect data that shouldn't be modified
- Iteration in for loops with unpacking

**Named tuples** are a special type that combines tuple immutability with dictionary-like named access. They're more readable than positional tuples.

**`collections.namedtuple`** creates a lightweight tuple with named fields, making code self-documenting.

---

## Code Examples

```python
from collections import namedtuple

# Regular tuple (hard to remember what each index is)
result = (42, "success", 0.95)
status_code, message, confidence = result

# Named tuple (much clearer!)
QueryResult = namedtuple('QueryResult', ['status_code', 'message', 'confidence'])
result = QueryResult(42, "success", 0.95)
print(result.status_code)   # 42
print(result.message)       # "success"
print(result.confidence)    # 0.95

# Named tuple from a tuple
data = (10, 20)
Point = namedtuple('Point', ['x', 'y'])
p = Point(*data)  # Unpack and create
print(p.x, p.y)

# Multiple return values
def divide_with_remainder(a, b):
    return (a // b, a % b)

quotient, remainder = divide_with_remainder(17, 5)
print(f"{quotient} remainder {remainder}")

# Using tuples as dictionary keys
graph = {
    (0, 0): [(1, 0), (0, 1)],
    (1, 0): [(0, 0), (1, 1)],
    (0, 1): [(0, 0), (1, 1)]
}
print(graph[(0, 0)])  # [(1, 0), (0, 1)]

# Tuple immutability ensures consistency
Student = namedtuple('Student', ['name', 'grade', 'gpa'])
alice = Student("Alice", 10, 3.8)
print(alice)  # Student(name='Alice', grade=10, gpa=3.8)

# Creating multiple instances
students = [
    Student("Alice", 10, 3.8),
    Student("Bob", 10, 3.5),
    Student("Charlie", 11, 3.9)
]

for student in students:
    print(f"{student.name}: GPA {student.gpa}")
```

---

## Guided Practice

**Activity: Using Named Tuples for Clarity**

1. Define a named tuple for a book: `(title, author, year)`
2. Create 3 book instances
3. Create a dictionary with tuples as keys (e.g., ISBN as tuple)
4. Write a function that returns multiple values using a named tuple
5. Sort your books by year using the tuple data

---

## Practice Problems

**Beginner:** Create a named tuple called `Color` with fields `(name, red, green, blue)`. Create an instance for red `(255, 0, 0)` and print it.

**Intermediate:** Write a function `get_file_info(filename)` that returns a named tuple with `(name, extension, size_kb)` for a given filename.

**Challenge:** Create a game coordinate system using named tuples. Represent a chessboard square as `Square(row, col)` and write functions to find all valid knight moves from a given square.

<details>
<summary>💡 Hints</summary>

- Beginner: Use `namedtuple('Color', ['name', 'red', 'green', 'blue'])`
- Intermediate: Use string methods like .split() to extract parts of a filename
- Challenge: A knight moves in an L-shape: 2 squares in one direction, 1 in the other

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
from collections import namedtuple

# Beginner
Color = namedtuple('Color', ['name', 'red', 'green', 'blue'])
red = Color("red", 255, 0, 0)
print(red)

# Intermediate
def get_file_info(filename):
    FileInfo = namedtuple('FileInfo', ['name', 'extension', 'size_kb'])
    parts = filename.split('.')
    name = parts[0]
    extension = parts[1] if len(parts) > 1 else "no extension"
    return FileInfo(name, extension, 0)

# Challenge
Square = namedtuple('Square', ['row', 'col'])

def knight_moves(square):
    moves = []
    deltas = [(2, 1), (2, -1), (-2, 1), (-2, -1), 
              (1, 2), (1, -2), (-1, 2), (-1, -2)]
    for dr, dc in deltas:
        new_row, new_col = square.row + dr, square.col + dc
        if 0 <= new_row < 8 and 0 <= new_col < 8:
            moves.append(Square(new_row, new_col))
    return moves
```

</details>
