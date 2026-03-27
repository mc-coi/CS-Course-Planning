# Day 17: Special Methods — __str__ & __repr__
**Learning Target:** I can implement special methods to control how objects are displayed and represented as strings.

### Key Concepts

**Special Methods (Dunder Methods):** Methods with double underscores that provide special functionality. Python calls them automatically in certain situations.

**__str__():** Returns a user-friendly string representation (called by str() and print()).

**__repr__():** Returns a developer-friendly string representation (called by repr() and in interactive mode).

**String Representation:** How objects appear when converted to strings or printed.

**Debugging Aid:** Good __repr__() implementations help debug code by showing object state clearly.

### Code Examples

```python
# Without special methods
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

p = Person("Alice", 30)
print(p)  # <__main__.Person object at 0x...>
print(str(p))  # <__main__.Person object at 0x...>

# With __str__()
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name}, age {self.age}"

p = Person("Alice", 30)
print(p)  # Alice, age 30
print(str(p))  # Alice, age 30

# With __repr__()
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __repr__(self):
        return f"Person('{self.name}', {self.age})"

p = Person("Alice", 30)
print(repr(p))  # Person('Alice', 30)

# In interactive mode:
# >>> p
# Person('Alice', 30)

# Both __str__() and __repr__()
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages

    def __str__(self):
        return f"{self.title} by {self.author}"

    def __repr__(self):
        return f"Book('{self.title}', '{self.author}', {self.pages})"

book = Book("1984", "George Orwell", 328)
print(book)  # 1984 by George Orwell (uses __str__)
print(repr(book))  # Book('1984', 'George Orwell', 328) (uses __repr__)

# Product example
class Product:
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity

    def __str__(self):
        return f"{self.name} - ${self.price:.2f} (qty: {self.quantity})"

    def __repr__(self):
        return f"Product(name='{self.name}', price={self.price}, quantity={self.quantity})"

prod = Product("Laptop", 999.99, 5)
print(prod)  # Laptop - $999.99 (qty: 5)
print(repr(prod))  # Product(name='Laptop', price=999.99, quantity=5)

# In a list:
products = [
    Product("Mouse", 29.99, 10),
    Product("Keyboard", 79.99, 3)
]
print(products)  # [Product(name='Mouse', ...), Product(name='Keyboard', ...)]

# Student example with status
class Student:
    def __init__(self, name, student_id, gpa):
        self.name = name
        self.student_id = student_id
        self.gpa = gpa

    def __str__(self):
        status = "Dean's List" if self.gpa >= 3.5 else "Regular"
        return f"{self.name} ({self.student_id}) - GPA: {self.gpa} [{status}]"

    def __repr__(self):
        return f"Student(name='{self.name}', id='{self.student_id}', gpa={self.gpa})"

student = Student("Bob", "S001", 3.8)
print(student)  # Bob (S001) - GPA: 3.8 [Dean's List]
print(repr(student))  # Student(name='Bob', id='S001', gpa=3.8)

# Time example
class Time:
    def __init__(self, hours, minutes, seconds):
        self.hours = hours
        self.minutes = minutes
        self.seconds = seconds

    def __str__(self):
        return f"{self.hours:02d}:{self.minutes:02d}:{self.seconds:02d}"

    def __repr__(self):
        return f"Time({self.hours}, {self.minutes}, {self.seconds})"

time = Time(14, 30, 45)
print(time)  # 14:30:45
print(repr(time))  # Time(14, 30, 45)

# Date example
class Date:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day

    def __str__(self):
        months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun",
                  "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
        return f"{months[self.month-1]} {self.day}, {self.year}"

    def __repr__(self):
        return f"Date({self.year}, {self.month}, {self.day})"

date = Date(2024, 3, 25)
print(date)  # Mar 25, 2024
print(repr(date))  # Date(2024, 3, 25)

# Vector example
class Vector:
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z

    def __str__(self):
        return f"({self.x}, {self.y}, {self.z})"

    def __repr__(self):
        return f"Vector({self.x}, {self.y}, {self.z})"

v = Vector(1, 2, 3)
print(v)  # (1, 2, 3)
print(repr(v))  # Vector(1, 2, 3)

# BankAccount example
class BankAccount:
    def __init__(self, holder, balance):
        self.holder = holder
        self._balance = balance

    def __str__(self):
        return f"{self.holder}: ${self._balance:.2f}"

    def __repr__(self):
        return f"BankAccount(holder='{self.holder}', balance={self._balance})"

account = BankAccount("Alice", 1500.50)
print(account)  # Alice: $1500.50
print(repr(account))  # BankAccount(holder='Alice', balance=1500.5)

# List of objects
accounts = [
    BankAccount("Alice", 1000),
    BankAccount("Bob", 2500),
    BankAccount("Charlie", 1500)
]

for account in accounts:
    print(account)
# Alice: $1000.00
# Bob: $2500.00
# Charlie: $1500.00

# Point example with distance display
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"Point at ({self.x}, {self.y})"

    def __repr__(self):
        return f"Point(x={self.x}, y={self.y})"

    def distance_from_origin(self):
        import math
        return math.sqrt(self.x**2 + self.y**2)

point = Point(3, 4)
print(point)  # Point at (3, 4)
print(repr(point))  # Point(x=3, y=4)
print(f"Distance: {point.distance_from_origin()}")
```

### Guided Practice

**Activity: Implement String Methods for a Rectangle Class**

Follow these steps:

1. Create `Rectangle` class with width and height
2. Implement `__str__()` to show as: "Rectangle: 5 x 3"
3. Implement `__repr__()` to show as: "Rectangle(width=5, height=3)"
4. Create several rectangles and print them

**Solution:**
```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def __str__(self):
        return f"Rectangle: {self.width} x {self.height}"

    def __repr__(self):
        return f"Rectangle(width={self.width}, height={self.height})"

    def area(self):
        return self.width * self.height

rect1 = Rectangle(5, 3)
rect2 = Rectangle(10, 8)
rect3 = Rectangle(4, 4)

print(rect1)  # Rectangle: 5 x 3
print(repr(rect1))  # Rectangle(width=5, height=3)

rectangles = [rect1, rect2, rect3]
for r in rectangles:
    print(f"{r} - Area: {r.area()}")
```

### Practice Problems

**Problem 1 — Beginner:** Create a Car class with brand, model, year. Implement __str__() to show "2022 Toyota Camry" format.

**Problem 2 — Intermediate:** Create an Employee class with name, salary, department. Implement both __str__() (user-friendly) and __repr__() (code-friendly).

**Problem 3 — Challenge:** Create a GradeBook class. Implement __str__() to show summary, __repr__() to show recreatable form. Print a list of grade books.

<details>
<summary>💡 Hints</summary>

**Hint 1:** __str__() should be human-readable; __repr__() should be useful for developers.

**Hint 2:** Use string formatting (f-strings) to create nicely formatted output.

**Hint 3:** If you only implement __repr__(), Python will use it as fallback for __str__().

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Car:
    def __init__(self, brand, model, year):
        self.brand = brand
        self.model = model
        self.year = year

    def __str__(self):
        return f"{self.year} {self.brand} {self.model}"

car = Car("Toyota", "Camry", 2022)
print(car)

# Problem 2
class Employee:
    def __init__(self, name, salary, department):
        self.name = name
        self.salary = salary
        self.department = department

    def __str__(self):
        return f"{self.name} works in {self.department} (${self.salary})"

    def __repr__(self):
        return f"Employee(name='{self.name}', salary={self.salary}, department='{self.department}')"

emp = Employee("Alice", 60000, "Engineering")
print(emp)
print(repr(emp))

# Problem 3
class GradeBook:
    def __init__(self, student_name, grades):
        self.student_name = student_name
        self.grades = grades

    def __str__(self):
        avg = sum(self.grades) / len(self.grades) if self.grades else 0
        return f"{self.student_name}: {len(self.grades)} grades, avg {avg:.1f}"

    def __repr__(self):
        return f"GradeBook('{self.student_name}', {self.grades})"

books = [
    GradeBook("Alice", [90, 85, 92]),
    GradeBook("Bob", [78, 82, 80]),
    GradeBook("Charlie", [95, 98, 96])
]

for book in books:
    print(book)
```

</details>
