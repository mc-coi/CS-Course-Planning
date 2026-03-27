# Day 18: Special Methods — __len__, __eq__, __add__, __lt__
**Learning Target:** I can implement comparison and arithmetic special methods to make objects behave like built-in types.

### Key Concepts

**__len__():** Returns the length of an object (called by len()).

**__eq__():** Compares two objects for equality (called by ==).

**__lt__():** Checks if one object is less than another (called by <).

**__add__():** Adds two objects (called by +).

**__sub__(), __mul__(), __div__():** Other arithmetic operations.

**Operator Overloading:** Making custom objects work with Python operators.

### Code Examples

```python
# __len__() example
class Playlist:
    def __init__(self, name, songs):
        self.name = name
        self.songs = songs

    def __len__(self):
        return len(self.songs)

playlist = Playlist("My Favorites", ["Song1", "Song2", "Song3"])
print(len(playlist))  # 3

# __eq__() example
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __eq__(self, other):
        if not isinstance(other, Person):
            return False
        return self.name == other.name and self.age == other.age

p1 = Person("Alice", 30)
p2 = Person("Alice", 30)
p3 = Person("Bob", 30)

print(p1 == p2)  # True
print(p1 == p3)  # False
print(p1 == "Alice")  # False

# __lt__() example
class Student:
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa

    def __lt__(self, other):
        return self.gpa < other.gpa

s1 = Student("Alice", 3.8)
s2 = Student("Bob", 3.5)
s3 = Student("Charlie", 3.8)

print(s1 < s2)  # False (3.8 < 3.5 is False)
print(s2 < s1)  # True (3.5 < 3.8 is True)
print(s1 < s3)  # False (3.8 < 3.8 is False)

# Sorting with custom comparison
students = [s1, s2, s3]
sorted_students = sorted(students)  # Uses __lt__()
for s in sorted_students:
    print(f"{s.name}: {s.gpa}")

# __add__() example
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)
v2 = Vector(3, 4)
v3 = v1 + v2
print(v3)  # Vector(4, 6)

# Money/Currency example
class Money:
    def __init__(self, amount):
        self.amount = amount

    def __add__(self, other):
        return Money(self.amount + other.amount)

    def __sub__(self, other):
        return Money(self.amount - other.amount)

    def __mul__(self, multiplier):
        return Money(self.amount * multiplier)

    def __eq__(self, other):
        return self.amount == other.amount

    def __lt__(self, other):
        return self.amount < other.amount

    def __repr__(self):
        return f"${self.amount:.2f}"

m1 = Money(100)
m2 = Money(50)
print(m1 + m2)  # $150.00
print(m1 - m2)  # $50.00
print(m1 * 2)   # $200.00
print(m1 > m2)  # True
print(m1 == Money(100))  # True

# String concatenation with objects
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

    def __add__(self, other):
        return f"{self.title} and {other.title}"

    def __repr__(self):
        return f"{self.title} by {self.author}"

book1 = Book("1984", "George Orwell")
book2 = Book("Animal Farm", "George Orwell")
print(book1 + book2)  # 1984 and Animal Farm

# Complex number example
class ComplexNumber:
    def __init__(self, real, imag):
        self.real = real
        self.imag = imag

    def __add__(self, other):
        return ComplexNumber(
            self.real + other.real,
            self.imag + other.imag
        )

    def __sub__(self, other):
        return ComplexNumber(
            self.real - other.real,
            self.imag - other.imag
        )

    def __eq__(self, other):
        return self.real == other.real and self.imag == other.imag

    def __repr__(self):
        sign = "+" if self.imag >= 0 else ""
        return f"{self.real}{sign}{self.imag}i"

c1 = ComplexNumber(3, 4)
c2 = ComplexNumber(1, 2)
print(c1 + c2)  # 4+6i
print(c1 - c2)  # 2+2i
print(c1 == ComplexNumber(3, 4))  # True

# Fraction example
class Fraction:
    def __init__(self, numerator, denominator):
        self.numerator = numerator
        self.denominator = denominator

    def __add__(self, other):
        num = self.numerator * other.denominator + other.numerator * self.denominator
        denom = self.denominator * other.denominator
        return Fraction(num, denom)

    def __eq__(self, other):
        return (self.numerator * other.denominator ==
                other.numerator * self.denominator)

    def __lt__(self, other):
        return (self.numerator * other.denominator <
                other.numerator * self.denominator)

    def __repr__(self):
        return f"{self.numerator}/{self.denominator}"

f1 = Fraction(1, 2)
f2 = Fraction(1, 3)
print(f1 + f2)  # 5/6
print(f1 < f2)  # False
print(f2 < f1)  # True

# Date comparison
class Date:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day

    def __lt__(self, other):
        if self.year != other.year:
            return self.year < other.year
        if self.month != other.month:
            return self.month < other.month
        return self.day < other.day

    def __eq__(self, other):
        return (self.year == other.year and
                self.month == other.month and
                self.day == other.day)

    def __repr__(self):
        return f"{self.year}-{self.month:02d}-{self.day:02d}"

d1 = Date(2024, 3, 25)
d2 = Date(2024, 3, 20)
d3 = Date(2024, 3, 25)

print(d1 < d2)  # False
print(d2 < d1)  # True
print(d1 == d3)  # True

dates = [d1, d2, d3]
sorted_dates = sorted(dates)
for date in sorted_dates:
    print(date)

# Point distance and comparison
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def distance_from_origin(self):
        return (self.x**2 + self.y**2)**0.5

    def __lt__(self, other):
        return self.distance_from_origin() < other.distance_from_origin()

    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

    def __repr__(self):
        return f"({self.x}, {self.y})"

p1 = Point(3, 4)
p2 = Point(1, 1)
p3 = Point(3, 4)

print(p1 < p2)  # False (distance 5 > distance 1.41)
print(p2 < p1)  # True
print(p1 == p3)  # True
print(p1 + p2)  # (4, 5)

# Sorting points by distance
points = [p1, p2, p3, Point(5, 0)]
sorted_points = sorted(points)
for p in sorted_points:
    print(f"{p}: distance {p.distance_from_origin():.2f}")
```

### Guided Practice

**Activity: Implement Comparison for a Time Class**

Follow these steps:

1. Create `Time` class with hours, minutes, seconds
2. Implement `__lt__()` to compare times
3. Implement `__eq__()` to check equality
4. Implement `__add__()` to add times
5. Implement `__len__()` to return total seconds
6. Create list of times and sort them

**Solution:**
```python
class Time:
    def __init__(self, hours, minutes, seconds):
        self.hours = hours
        self.minutes = minutes
        self.seconds = seconds

    def __len__(self):
        return self.hours * 3600 + self.minutes * 60 + self.seconds

    def __eq__(self, other):
        return len(self) == len(other)

    def __lt__(self, other):
        return len(self) < len(other)

    def __add__(self, other):
        total_secs = len(self) + len(other)
        hours = total_secs // 3600
        minutes = (total_secs % 3600) // 60
        seconds = total_secs % 60
        return Time(hours, minutes, seconds)

    def __repr__(self):
        return f"{self.hours:02d}:{self.minutes:02d}:{self.seconds:02d}"

t1 = Time(1, 30, 45)
t2 = Time(0, 45, 20)
t3 = Time(1, 30, 45)

print(t1 < t2)  # False
print(t1 == t3)  # True
print(t1 + t2)  # 02:16:05
print(len(t1))  # 5445 seconds

times = [t1, t2, t3, Time(2, 0, 0)]
sorted_times = sorted(times)
for t in sorted_times:
    print(t)
```

### Practice Problems

**Problem 1 — Beginner:** Implement __len__() for a Playlist. Also implement __eq__() to compare playlists by song count.

**Problem 2 — Intermediate:** Create a Price class with currency amount. Implement __add__(), __sub__(), __mul__(), __eq__(), __lt__().

**Problem 3 — Challenge:** Create a Deck class. Implement __len__() for card count, __add__() to combine decks, __eq__() for comparison.

<details>
<summary>💡 Hints</summary>

**Hint 1:** In __add__(), __sub__(), etc., return a new object of the same type.

**Hint 2:** Check type in __eq__() before comparing to avoid errors.

**Hint 3:** For __lt__(), return True/False based on appropriate comparison logic.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Playlist:
    def __init__(self, name, songs):
        self.name = name
        self.songs = songs

    def __len__(self):
        return len(self.songs)

    def __eq__(self, other):
        return len(self) == len(other)

p1 = Playlist("Favorites", ["Song1", "Song2", "Song3"])
p2 = Playlist("Party", ["Song1", "Song2", "Song3"])
print(len(p1))
print(p1 == p2)

# Problem 2
class Price:
    def __init__(self, amount):
        self.amount = amount

    def __add__(self, other):
        return Price(self.amount + other.amount)

    def __sub__(self, other):
        return Price(self.amount - other.amount)

    def __mul__(self, factor):
        return Price(self.amount * factor)

    def __eq__(self, other):
        return self.amount == other.amount

    def __lt__(self, other):
        return self.amount < other.amount

    def __repr__(self):
        return f"${self.amount:.2f}"

p1 = Price(50)
p2 = Price(30)
print(p1 + p2)
print(p1 - p2)
print(p1 * 2)
print(p1 > p2)

# Problem 3
class Deck:
    def __init__(self, cards):
        self.cards = cards

    def __len__(self):
        return len(self.cards)

    def __add__(self, other):
        return Deck(self.cards + other.cards)

    def __eq__(self, other):
        return len(self) == len(other)

d1 = Deck(["A", "2", "3"])
d2 = Deck(["4", "5"])
print(len(d1))
print(d1 + d2)
print(d1 == Deck(["X", "Y", "Z"]))
```

</details>
