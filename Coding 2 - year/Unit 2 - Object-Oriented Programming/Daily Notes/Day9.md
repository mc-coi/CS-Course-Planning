# Day 9: Review — Classes, Encapsulation
**Learning Target:** I can demonstrate mastery of classes, constructors, encapsulation, and properties.

### Review Guide

#### Core Concepts Check

**Classes and Objects:**
- A class is a blueprint, an object is an instance of that blueprint
- Use `__init__` to initialize objects with starting values
- Use `self` to refer to the specific object being worked with

**Instance vs Class Variables:**
- Instance variables (set in `__init__`) are unique to each object
- Class variables (set in class body) are shared by all instances

**Methods:**
- Define actions that objects can perform
- Use `self.attribute` to access object data
- Methods receive `self` as the first parameter automatically

**Encapsulation:**
- Private attributes use `_prefix` by convention
- Protect data from unwanted external modification
- Use getters and setters to control access

**Properties:**
- Use `@property` decorator for cleaner attribute access
- Combine with validation in setters
- Allow `obj.attr` syntax instead of `obj.get_attr()`

#### Practice Problems

**Problem 1 — Fundamental Concepts:**

What will this code output?

```python
class Car:
    count = 0

    def __init__(self, brand):
        self.brand = brand
        Car.count = Car.count + 1

car1 = Car("Toyota")
car2 = Car("Honda")
car3 = Car("Ford")

print(Car.count)
print(car1.brand)
print(car2.brand)
```

**Answer:**
```
3
Toyota
Honda
```

**Problem 2 — Methods and Self:**

Write the output:

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

rect = Rectangle(5, 3)
print(f"Area: {rect.area()}")
print(f"Perimeter: {rect.perimeter()}")
```

**Answer:**
```
Area: 15
Perimeter: 16
```

**Problem 3 — Encapsulation:**

Fix this code to use proper encapsulation:

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance  # Problem: direct access

    def display(self):
        print(f"Balance: ${self.balance}")

account = BankAccount(1000)
account.balance = -500  # Problem: invalid state!
account.display()
```

**Solution:**

```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance  # Private

    @property
    def balance(self):
        return self._balance

    @balance.setter
    def balance(self, value):
        if value >= 0:
            self._balance = value
        else:
            print("Invalid: balance cannot be negative!")

    def display(self):
        print(f"Balance: ${self._balance}")

account = BankAccount(1000)
account.balance = -500  # Rejected!
account.balance = 500   # Accepted
account.display()  # Balance: $500
```

#### Quick Reference

**Class Structure:**
```python
class ClassName:
    # Class variable (shared)
    class_var = value

    # Constructor
    def __init__(self, param1, param2):
        # Instance variables (unique per object)
        self.instance_var1 = param1
        self._private_var = param2

    # Method
    def method_name(self):
        return self.instance_var1

    # Property with getter
    @property
    def prop_name(self):
        return self._private_var

    # Property with setter
    @prop_name.setter
    def prop_name(self, value):
        if valid(value):
            self._private_var = value
```

**Creating Objects:**
```python
obj = ClassName(arg1, arg2)
obj.method_name()
print(obj.instance_var1)
```

### Comprehensive Review Problem

**Build a Library Management System:**

Create three classes:

1. **Book Class:**
   - Attributes: title, author, isbn, pages (all private except title)
   - Property: pages (read-only)
   - Method: summary() that returns a string description

2. **Librarian Class:**
   - Attribute: name, employee_id (private)
   - Property: employee_id (read-only)
   - Method: check_out_book(book, patron) that logs the transaction

3. **Library Class:**
   - Class variable: total_books (count)
   - Attributes: name, books (list of Book objects)
   - Methods: add_book(), find_book(title), list_all_books()

**Starter Code:**
```python
class Book:
    def __init__(self, title, author, isbn, pages):
        self.title = title
        # YOUR CODE: make author, isbn, pages private

    # YOUR CODE: property for pages (read-only)

    def summary(self):
        # YOUR CODE
        pass

class Librarian:
    def __init__(self, name, employee_id):
        # YOUR CODE
        pass

    @property
    def employee_id(self):
        # YOUR CODE
        pass

    def check_out_book(self, book, patron):
        print(f"{book.title} checked out to {patron}")

class Library:
    total_books = 0

    def __init__(self, name):
        self.name = name
        self._books = []

    def add_book(self, book):
        self._books.append(book)
        Library.total_books = Library.total_books + 1

    def find_book(self, title):
        for book in self._books:
            if book.title.lower() == title.lower():
                return book
        return None

    def list_all_books(self):
        for book in self._books:
            print(book.summary())

# Test your code
book1 = Book("To Kill a Mockingbird", "Harper Lee", "978-0-06-112008-4", 281)
book2 = Book("1984", "George Orwell", "978-0-451-52494-2", 328)

library = Library("Central Library")
library.add_book(book1)
library.add_book(book2)

librarian = Librarian("Ms. Johnson", "LIB001")

print(f"Library: {library.name}")
print(f"Librarian: {librarian.employee_id}")
print(f"Total books: {Library.total_books}")
print()

library.list_all_books()

librarian.check_out_book(book1, "Alice")
```

**Solution:**
```python
class Book:
    def __init__(self, title, author, isbn, pages):
        self.title = title
        self._author = author
        self._isbn = isbn
        self._pages = pages

    @property
    def pages(self):
        return self._pages

    def summary(self):
        return f"{self.title} by {self._author} ({self._pages} pages, ISBN: {self._isbn})"

class Librarian:
    def __init__(self, name, employee_id):
        self._name = name
        self._employee_id = employee_id

    @property
    def employee_id(self):
        return self._employee_id

    def check_out_book(self, book, patron):
        print(f"{book.title} checked out to {patron}")

class Library:
    total_books = 0

    def __init__(self, name):
        self.name = name
        self._books = []

    def add_book(self, book):
        self._books.append(book)
        Library.total_books = Library.total_books + 1

    def find_book(self, title):
        for book in self._books:
            if book.title.lower() == title.lower():
                return book
        return None

    def list_all_books(self):
        for book in self._books:
            print(book.summary())

book1 = Book("To Kill a Mockingbird", "Harper Lee", "978-0-06-112008-4", 281)
book2 = Book("1984", "George Orwell", "978-0-451-52494-2", 328)

library = Library("Central Library")
library.add_book(book1)
library.add_book(book2)

librarian = Librarian("Ms. Johnson", "LIB001")

print(f"Library: {library.name}")
print(f"Librarian: {librarian.employee_id}")
print(f"Total books: {Library.total_books}")
print()

library.list_all_books()

librarian.check_out_book(book1, "Alice")
```

**Expected Output:**
```
Library: Central Library
Librarian: LIB001
Total books: 2

To Kill a Mockingbird by Harper Lee (281 pages, ISBN: 978-0-06-112008-4)
1984 by George Orwell (328 pages, ISBN: 978-0-451-52494-2)
To Kill a Mockingbird checked out to Alice
```

### Key Takeaways

1. **Classes bundle data and behavior together** — they're the foundation of OOP
2. **Constructors initialize objects** — use `__init__` to set up initial state
3. **Encapsulation protects data** — use private attributes and properties
4. **Instance variables are unique to each object** — class variables are shared
5. **Properties provide controlled access** — use `@property` with validation
6. **Methods represent object behavior** — they modify and query object state

### Self-Assessment

Rate your understanding:

- [ ] I can create classes with constructors and instance variables
- [ ] I can write and call methods with the self parameter
- [ ] I understand the difference between instance and class variables
- [ ] I can apply encapsulation using private attributes
- [ ] I can use properties with getters and setters
- [ ] I can validate data in property setters
- [ ] I can design complete, well-structured classes

If any items are unchecked, review that day's material before moving on!
