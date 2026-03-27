# Day 3: The __init__ Constructor
**Learning Target:** I can use __init__ to initialize object attributes automatically when an object is created.

### Key Concepts

**Constructor (__init__):** A special method that runs automatically when an object is created. It initializes the object's initial state (attributes). The name `__init__` uses double underscores on each side.

**Dunder Method:** Short for "double underscore" method. These are special methods in Python that have names like `__init__`, `__str__`, etc., and provide special behavior.

**Initialization:** Setting up the initial values of an object's attributes when it is first created.

**Parameter:** Values passed to a method (or constructor) to configure how it behaves. In `__init__`, parameters are used to set initial attribute values.

### Code Examples

```python
# Without __init__ (old way)
class Dog:
    def bark(self):
        print("Woof!")

dog = Dog()
dog.name = "Buddy"  # Must set manually
dog.age = 3

# With __init__ (modern way)
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def bark(self):
        print("Woof!")

dog = Dog("Buddy", 3)  # Attributes set automatically
print(dog.name)  # Buddy
print(dog.age)   # 3

# Student class with __init__
class Student:
    def __init__(self, name, grade, gpa):
        self.name = name
        self.grade = grade
        self.gpa = gpa

    def print_info(self):
        print(f"Name: {self.name}, Grade: {self.grade}, GPA: {self.gpa}")

student1 = Student("Alice", 10, 3.8)
student1.print_info()  # Name: Alice, Grade: 10, GPA: 3.8

student2 = Student("Bob", 11, 3.5)
student2.print_info()  # Name: Bob, Grade: 11, GPA: 3.5

# Car class with __init__
class Car:
    def __init__(self, brand, model, year):
        self.brand = brand
        self.model = model
        self.year = year
        self.mileage = 0  # Start with 0 mileage

    def drive(self, miles):
        self.mileage = self.mileage + miles
        print(f"Drove {miles} miles")

    def show_info(self):
        print(f"{self.year} {self.brand} {self.model} - {self.mileage} miles")

car1 = Car("Toyota", "Camry", 2022)
car1.show_info()  # 2022 Toyota Camry - 0 miles
car1.drive(50)
car1.show_info()  # 2022 Toyota Camry - 50 miles

# Rectangle class with __init__
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

    def display(self):
        print(f"Rectangle: {self.width} x {self.height}")
        print(f"Area: {self.area()}")
        print(f"Perimeter: {self.perimeter()}")

rect1 = Rectangle(5, 3)
rect1.display()
# Rectangle: 5 x 3
# Area: 15
# Perimeter: 16

rect2 = Rectangle(10, 8)
rect2.display()
# Rectangle: 10 x 8
# Area: 80
# Perimeter: 36

# BankAccount with __init__ and default values
class BankAccount:
    def __init__(self, holder, initial_balance=0):
        self.holder = holder
        self.balance = initial_balance

    def deposit(self, amount):
        self.balance = self.balance + amount
        print(f"${amount} deposited. Balance: ${self.balance}")

    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance = self.balance - amount
            print(f"${amount} withdrawn. Balance: ${self.balance}")
        else:
            print("Insufficient funds!")

    def show_balance(self):
        print(f"{self.holder}'s balance: ${self.balance}")

account1 = BankAccount("Alice")  # Starting with 0
account1.show_balance()  # Alice's balance: $0
account1.deposit(1000)

account2 = BankAccount("Bob", 500)  # Starting with 500
account2.show_balance()  # Bob's balance: $500
account2.withdraw(100)

# Book class with __init__
class Book:
    def __init__(self, title, author, pages, year):
        self.title = title
        self.author = author
        self.pages = pages
        self.year = year

    def summary(self):
        return f"{self.title} by {self.author} ({self.year})"

    def is_long(self):
        return self.pages > 300

book1 = Book("The Great Gatsby", "F. Scott Fitzgerald", 180, 1925)
print(book1.summary())  # The Great Gatsby by F. Scott Fitzgerald (1925)
print(f"Is long? {book1.is_long()}")  # Is long? False

book2 = Book("It", "Stephen King", 1138, 1986)
print(book2.summary())  # It by Stephen King (1986)
print(f"Is long? {book2.is_long()}")  # Is long? True

# Circle class with __init__
import math

class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

    def circumference(self):
        return 2 * math.pi * self.radius

    def info(self):
        print(f"Circle with radius {self.radius}")
        print(f"Area: {self.area():.2f}")
        print(f"Circumference: {self.circumference():.2f}")

circle = Circle(5)
circle.info()
# Circle with radius 5
# Area: 78.50
# Circumference: 31.42
```

### Guided Practice

**Activity: Create a Person Class with __init__**

Follow these steps:

1. Create a `Person` class with an `__init__` method that takes `name`, `age`, and `email`
2. Store these as attributes
3. Add a method `celebrate_birthday()` that increases age by 1
4. Add a method `display_info()` that prints all information
5. Create 3 person objects using different initial values
6. Call methods on each person

**Expected Output:**
```
Name: Alice, Age: 25, Email: alice@example.com
Name: Bob, Age: 30, Email: bob@example.com
Name: Charlie, Age: 22, Email: charlie@example.com
Alice is now 26 years old
```

**Solution:**
```python
class Person:
    def __init__(self, name, age, email):
        self.name = name
        self.age = age
        self.email = email

    def celebrate_birthday(self):
        self.age = self.age + 1
        print(f"{self.name} is now {self.age} years old")

    def display_info(self):
        print(f"Name: {self.name}, Age: {self.age}, Email: {self.email}")

person1 = Person("Alice", 25, "alice@example.com")
person1.display_info()

person2 = Person("Bob", 30, "bob@example.com")
person2.display_info()

person3 = Person("Charlie", 22, "charlie@example.com")
person3.display_info()

person1.celebrate_birthday()
```

### Practice Problems

**Problem 1 — Beginner:** Create a `Phone` class with an `__init__` method that takes `brand`, `model`, and `color`. Add a method that prints "Making a call". Create 2 phone objects and call the method on each.

**Problem 2 — Intermediate:** Create a `Product` class with `__init__` taking `name`, `price`, and `quantity`. Add methods to: (1) `calculate_total()` (price × quantity), (2) `apply_discount(percent)` that reduces the price, and (3) `display_info()`. Create multiple products and test the methods.

**Problem 3 — Challenge:** Create a `Library` class that manages books. The `__init__` should initialize an empty list of books. Add methods to: (1) `add_book(title, author)`, (2) `find_by_author(author)` (return list of books), (3) `total_books()`, and (4) `display_all()`. Create a library, add several books, and test all methods.

<details>
<summary>💡 Hints</summary>

**Hint 1:** For Problem 1, make sure your `__init__` method has exactly 4 parameters: `self`, `brand`, `model`, and `color`.

**Hint 2:** For Problem 2, use `self.price` in the `apply_discount()` method to modify the price. Remember that `percent` is a decimal (0.1 for 10% off).

**Hint 3:** For Problem 3, use a list (like `self.books = []`) to store books. Store each book as a dictionary or a tuple so you can track both title and author.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Phone:
    def __init__(self, brand, model, color):
        self.brand = brand
        self.model = model
        self.color = color

    def make_call(self):
        print(f"Making a call on {self.brand} {self.model}")

phone1 = Phone("Apple", "iPhone 14", "black")
phone1.make_call()

phone2 = Phone("Samsung", "Galaxy S23", "blue")
phone2.make_call()

# Problem 2
class Product:
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity

    def calculate_total(self):
        return self.price * self.quantity

    def apply_discount(self, percent):
        discount = self.price * percent
        self.price = self.price - discount

    def display_info(self):
        total = self.calculate_total()
        print(f"{self.name}: ${self.price:.2f} x {self.quantity} = ${total:.2f}")

product1 = Product("Laptop", 1000, 2)
product1.display_info()
product1.apply_discount(0.1)
product1.display_info()

# Problem 3
class Library:
    def __init__(self):
        self.books = []

    def add_book(self, title, author):
        self.books.append({"title": title, "author": author})

    def find_by_author(self, author):
        result = []
        for book in self.books:
            if book["author"] == author:
                result.append(book["title"])
        return result

    def total_books(self):
        return len(self.books)

    def display_all(self):
        for book in self.books:
            print(f"{book['title']} by {book['author']}")

library = Library()
library.add_book("To Kill a Mockingbird", "Harper Lee")
library.add_book("1984", "George Orwell")
library.add_book("Brave New World", "Aldous Huxley")
library.add_book("Animal Farm", "George Orwell")

print(f"Total books: {library.total_books()}")
library.display_all()
print(f"Books by George Orwell: {library.find_by_author('George Orwell')}")
```

</details>
