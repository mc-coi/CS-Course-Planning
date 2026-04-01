# Unit 2 - Object-Oriented Programming: Answer Key

## Problem 1: Create a simple class with an __init__ and one method

### Solution
```python
# Simple class with __init__ and one method
class Dog:
    def __init__(self, name, age):
        """Initialize a Dog with name and age"""
        self.name = name
        self.age = age

    def bark(self):
        """Make the dog bark"""
        return f"{self.name} says Woof!"

# Create an instance and use it
dog = Dog("Buddy", 3)
print(dog.bark())
```

### Expected Output
```
Buddy says Woof!
```

### Common Mistakes
- Forgetting self parameter in methods
- Not using self to refer to instance attributes

---

## Problem 2: Create an object and call one of its methods

### Solution
```python
# Define a simple class
class Car:
    def __init__(self, make, model):
        self.make = make
        self.model = model

    def describe(self):
        return f"{self.make} {self.model}"

# Create an object and call its method
my_car = Car("Toyota", "Camry")
print(my_car.describe())
```

### Expected Output
```
Toyota Camry
```

### Common Mistakes
- Forgetting parentheses when calling a method
- Calling a method without creating an instance first

---

## Problem 3: Add attributes to a class in __init__

### Solution
```python
# Class with multiple attributes in __init__
class Student:
    def __init__(self, name, student_id, gpa, major):
        """Initialize a Student with multiple attributes"""
        self.name = name
        self.student_id = student_id
        self.gpa = gpa
        self.major = major

    def display_info(self):
        """Display student information"""
        print(f"Name: {self.name}")
        print(f"ID: {self.student_id}")
        print(f"GPA: {self.gpa}")
        print(f"Major: {self.major}")

# Create a student and display info
student = Student("Alice", 12345, 3.8, "Computer Science")
student.display_info()
```

### Expected Output
```
Name: Alice
ID: 12345
GPA: 3.8
Major: Computer Science
```

### Common Mistakes
- Not initializing all attributes in __init__
- Mixing up the order of parameters

---

## Problem 4: Create a parent class and child class with inheritance

### Solution
```python
# Parent class
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "Some generic sound"

# Child class that inherits from Animal
class Cat(Animal):
    def __init__(self, name, color):
        super().__init__(name)
        self.color = color

    def speak(self):
        return f"{self.name} meows"

# Create instances
animal = Animal("Generic")
cat = Cat("Whiskers", "orange")

print(animal.speak())
print(cat.speak())
print(f"Cat name: {cat.name}, color: {cat.color}")
```

### Expected Output
```
Some generic sound
Whiskers meows
Cat name: Whiskers, color: orange
```

### Common Mistakes
- Forgetting to call super().__init__() in child class
- Not properly inheriting parent methods

---

## Problem 5: Override a method from a parent class

### Solution
```python
# Parent class with a method
class Vehicle:
    def __init__(self, brand):
        self.brand = brand

    def start(self):
        return f"{self.brand} vehicle is starting"

# Child class overriding the method
class Motorcycle(Vehicle):
    def start(self):
        """Override parent method with different behavior"""
        return f"{self.brand} motorcycle roars to life!"

# Another child class with different override
class ElectricCar(Vehicle):
    def start(self):
        return f"{self.brand} electric car quietly powers on"

# Test the overridden methods
bike = Motorcycle("Harley")
car = ElectricCar("Tesla")

print(bike.start())
print(car.start())
```

### Expected Output
```
Harley motorcycle roars to life!
Tesla electric car quietly powers on
```

### Common Mistakes
- Forgetting the method signature must match the parent class
- Not understanding that the child version completely replaces the parent version

---

## Problem 6: Create a class with a private attribute using @property

### Solution
```python
# Class with a private attribute using @property decorator
class BankAccount:
    def __init__(self, owner, initial_balance):
        self.owner = owner
        self._balance = initial_balance  # Private attribute

    @property
    def balance(self):
        """Get the account balance"""
        return self._balance

    @balance.setter
    def balance(self, amount):
        """Set the balance with validation"""
        if amount < 0:
            print("Error: Balance cannot be negative")
        else:
            self._balance = amount

    def deposit(self, amount):
        self.balance = self._balance + amount
        print(f"Deposited ${amount}. New balance: ${self._balance}")

# Create account and use property
account = BankAccount("John", 1000)
print(f"Balance: ${account.balance}")
account.deposit(500)
```

### Expected Output
```
Balance: $1000
Deposited $500. New balance: $1500
```

### Common Mistakes
- Confusing property syntax with regular methods
- Trying to directly access private attributes (_balance) instead of using property getter

---

## Problem 7: Implement __str__ for a class

### Solution
```python
# Class with __str__ implementation
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages

    def __str__(self):
        """Return a user-friendly string representation"""
        return f"'{self.title}' by {self.author} ({self.pages} pages)"

# Create a book and print it
book = Book("1984", "George Orwell", 328)
print(book)
print(str(book))

# In a list
books = [
    Book("The Great Gatsby", "F. Scott Fitzgerald", 180),
    Book("To Kill a Mockingbird", "Harper Lee", 281)
]
for book in books:
    print(book)
```

### Expected Output
```
'1984' by George Orwell (328 pages)
'1984' by George Orwell (328 pages)
'The Great Gatsby' by F. Scott Fitzgerald (180 pages)
'To Kill a Mockingbird' by Harper Lee (281 pages)
```

### Common Mistakes
- Using __repr__ instead of __str__ (different purposes)
- Not returning a string from __str__

---

## Problem 8: Create a multi-level hierarchy with multiple subclasses

### Solution
```python
# Base class
class Shape:
    def __init__(self, name):
        self.name = name

    def area(self):
        pass

# First level subclass
class Polygon(Shape):
    def __init__(self, name, sides):
        super().__init__(name)
        self.sides = sides

# Second level subclasses
class Rectangle(Polygon):
    def __init__(self, width, height):
        super().__init__("Rectangle", 4)
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Triangle(Polygon):
    def __init__(self, base, height):
        super().__init__("Triangle", 3)
        self.base = base
        self.height = height

    def area(self):
        return 0.5 * self.base * self.height

class Circle(Shape):
    def __init__(self, radius):
        super().__init__("Circle")
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

# Test the hierarchy
shapes = [
    Rectangle(5, 10),
    Triangle(4, 8),
    Circle(3)
]

for shape in shapes:
    print(f"{shape.name} area: {shape.area():.2f}")
```

### Expected Output
```
Rectangle area: 50.00
Triangle area: 16.00
Circle area: 28.27
```

### Common Mistakes
- Incorrect use of super() in multi-level inheritance
- Not properly initializing parent attributes

---

## Problem 9: Implement multiple dunder methods in a custom class

### Solution
```python
# Class with multiple dunder methods
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        """Return string representation"""
        return f"Vector({self.x}, {self.y})"

    def __repr__(self):
        """Return developer representation"""
        return f"Vector(x={self.x}, y={self.y})"

    def __add__(self, other):
        """Add two vectors"""
        return Vector(self.x + other.x, self.y + other.y)

    def __sub__(self, other):
        """Subtract two vectors"""
        return Vector(self.x - other.x, self.y - other.y)

    def __mul__(self, scalar):
        """Multiply vector by scalar"""
        return Vector(self.x * scalar, self.y * scalar)

    def __eq__(self, other):
        """Check if two vectors are equal"""
        return self.x == other.x and self.y == other.y

    def __lt__(self, other):
        """Compare magnitude of vectors"""
        return (self.x**2 + self.y**2) < (other.x**2 + other.y**2)

# Test the dunder methods
v1 = Vector(3, 4)
v2 = Vector(1, 2)

print(f"v1: {v1}")
print(f"v1 + v2: {v1 + v2}")
print(f"v1 - v2: {v1 - v2}")
print(f"v1 * 2: {v1 * 2}")
print(f"v1 == Vector(3, 4): {v1 == Vector(3, 4)}")
print(f"v1 < v2: {v1 < v2}")
```

### Expected Output
```
v1: Vector(3, 4)
v1 + v2: Vector(4, 6)
v1 - v2: Vector(2, 2)
v1 * 2: Vector(6, 8)
v1 == Vector(3, 4): True
v1 < v2: False
```

### Common Mistakes
- Incorrect method signatures for dunder methods
- Forgetting self parameter in dunder methods

---

## Problem 10: Design a complete class system for a real-world entity (University with Students and Courses)

### Solution
```python
# University system with Students and Courses
class Course:
    def __init__(self, course_id, name, credits):
        self.course_id = course_id
        self.name = name
        self.credits = credits
        self.students = []

    def add_student(self, student):
        if student not in self.students:
            self.students.append(student)

    def __str__(self):
        return f"{self.course_id}: {self.name} ({self.credits} credits)"

class Student:
    def __init__(self, student_id, name, major):
        self.student_id = student_id
        self.name = name
        self.major = major
        self.courses = []
        self.grades = {}

    def enroll(self, course):
        if course not in self.courses:
            self.courses.append(course)
            course.add_student(self)

    def add_grade(self, course, grade):
        self.grades[course.course_id] = grade

    def calculate_gpa(self):
        if not self.grades:
            return 0
        return sum(self.grades.values()) / len(self.grades)

    def __str__(self):
        return f"{self.name} ({self.student_id}) - {self.major}"

class University:
    def __init__(self, name):
        self.name = name
        self.students = []
        self.courses = []

    def add_student(self, student):
        self.students.append(student)

    def add_course(self, course):
        self.courses.append(course)

    def get_student_by_id(self, student_id):
        for student in self.students:
            if student.student_id == student_id:
                return student
        return None

# Test the system
uni = University("Tech University")

# Create courses
cs101 = Course("CS101", "Intro to Python", 3)
cs102 = Course("CS102", "Data Structures", 4)

uni.add_course(cs101)
uni.add_course(cs102)

# Create students
alice = Student("S001", "Alice", "Computer Science")
bob = Student("S002", "Bob", "Computer Science")

uni.add_student(alice)
uni.add_student(bob)

# Enroll students
alice.enroll(cs101)
alice.enroll(cs102)
bob.enroll(cs101)

# Add grades
alice.add_grade(cs101, 4.0)
alice.add_grade(cs102, 3.8)
bob.add_grade(cs101, 3.7)

# Display information
print(f"University: {uni.name}")
print(f"\nCourses:")
for course in uni.courses:
    print(f"  {course}")

print(f"\nStudents:")
for student in uni.students:
    print(f"  {student} - GPA: {student.calculate_gpa():.2f}")
    print(f"    Enrolled in: {[c.name for c in student.courses]}")
```

### Expected Output
```
University: Tech University

Courses:
  CS101: Intro to Python (3 credits)
  CS102: Data Structures (4 credits)

Students:
  Alice (S001) - Computer Science - GPA: 3.90
    Enrolled in: ['Intro to Python', 'Data Structures']
  Bob (S002) - Computer Science - GPA: 3.70
    Enrolled in: ['Intro to Python']
```

### Common Mistakes
- Not properly managing relationships between classes
- Forgetting to prevent duplicate enrollments

---

## Problem 11: Create a shape system where different shapes calculate area differently

### Solution
```python
import math

# Base shape class
class Shape:
    def __init__(self, name):
        self.name = name

    def area(self):
        raise NotImplementedError("Subclass must implement area()")

    def __str__(self):
        return f"{self.name} with area {self.area():.2f}"

# Specific shapes
class Circle(Shape):
    def __init__(self, radius):
        super().__init__("Circle")
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

class Rectangle(Shape):
    def __init__(self, width, height):
        super().__init__("Rectangle")
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Triangle(Shape):
    def __init__(self, base, height):
        super().__init__("Triangle")
        self.base = base
        self.height = height

    def area(self):
        return 0.5 * self.base * self.height

class Ellipse(Shape):
    def __init__(self, major_axis, minor_axis):
        super().__init__("Ellipse")
        self.major = major_axis
        self.minor = minor_axis

    def area(self):
        return math.pi * self.major * self.minor

# Test the shape system
shapes = [
    Circle(5),
    Rectangle(4, 6),
    Triangle(8, 5),
    Ellipse(5, 3)
]

print("Shapes and their areas:")
for shape in shapes:
    print(shape)

# Find the shape with the largest area
largest = max(shapes, key=lambda s: s.area())
print(f"\nLargest shape: {largest}")
```

### Expected Output
```
Shapes and their areas:
Circle with area 78.54
Rectangle with area 24.00
Triangle with area 20.00
Ellipse with area 47.12

Largest shape: Circle with area 78.54
```

### Common Mistakes
- Not using polymorphism correctly (different implementations for different shapes)
- Forgetting to handle the base class properly

---

## Problem 12: Implement a game character system with different character types

### Solution
```python
# Base character class
class Character:
    def __init__(self, name, health, mana):
        self.name = name
        self.health = health
        self.max_health = health
        self.mana = mana
        self.max_mana = mana

    def take_damage(self, damage):
        self.health -= damage
        if self.health < 0:
            self.health = 0

    def heal(self, amount):
        self.health = min(self.health + amount, self.max_health)

    def attack(self, target):
        raise NotImplementedError("Subclass must implement attack()")

    def display_stats(self):
        print(f"{self.name}: HP {self.health}/{self.max_health}, Mana {self.mana}/{self.max_mana}")

# Specific character types
class Warrior(Character):
    def __init__(self, name):
        super().__init__(name, 150, 20)
        self.strength = 15

    def attack(self, target):
        damage = self.strength * 1.2
        print(f"{self.name} swings sword at {target.name}! Damage: {damage:.0f}")
        target.take_damage(damage)

class Mage(Character):
    def __init__(self, name):
        super().__init__(name, 80, 100)
        self.intelligence = 18

    def attack(self, target):
        if self.mana >= 20:
            damage = self.intelligence * 1.5
            self.mana -= 20
            print(f"{self.name} casts fireball at {target.name}! Damage: {damage:.0f}")
            target.take_damage(damage)
        else:
            print(f"{self.name} doesn't have enough mana!")

class Archer(Character):
    def __init__(self, name):
        super().__init__(name, 100, 40)
        self.dexterity = 16

    def attack(self, target):
        damage = self.dexterity * 1.3
        print(f"{self.name} shoots arrow at {target.name}! Damage: {damage:.0f}")
        target.take_damage(damage)

# Battle simulation
warrior = Warrior("Conan")
mage = Mage("Merlin")
archer = Archer("Robin")

print("Initial Stats:")
warrior.display_stats()
mage.display_stats()
archer.display_stats()

print("\nBattle!")
warrior.attack(mage)
mage.display_stats()

mage.attack(archer)
archer.display_stats()

archer.attack(warrior)
warrior.display_stats()
```

### Expected Output
```
Initial Stats:
Conan: HP 150/150, Mana 20/20
Merlin: HP 80/100, Mana 100/100
Robin: HP 100/100, Mana 40/40

Battle!
Conan swings sword at Merlin! Damage: 18
Merlin: HP 62/80, Mana 100/100
Merlin casts fireball at Robin! Damage: 27
Robin: HP 73/100, Mana 40/40
Robin shoots arrow at Conan! Damage: 21
Conan: HP 129/150, Mana 20/20
```

### Common Mistakes
- Not properly using polymorphism in attack methods
- Not managing resources (mana, health) correctly

---

## Problem 13: Build a library system with Books, Members, and Loans

### Solution
```python
from datetime import datetime, timedelta

class Book:
    def __init__(self, isbn, title, author):
        self.isbn = isbn
        self.title = title
        self.author = author
        self.available = True

    def __str__(self):
        status = "Available" if self.available else "Checked Out"
        return f"{self.title} by {self.author} ({self.isbn}) - {status}"

class Member:
    def __init__(self, member_id, name):
        self.member_id = member_id
        self.name = name
        self.loans = []

    def __str__(self):
        return f"{self.name} (Member #{self.member_id})"

class Loan:
    def __init__(self, book, member, loan_days=14):
        self.book = book
        self.member = member
        self.loan_date = datetime.now()
        self.due_date = self.loan_date + timedelta(days=loan_days)
        self.returned = False

    def return_book(self):
        self.returned = True
        self.book.available = True

    def is_overdue(self):
        if not self.returned:
            return datetime.now() > self.due_date
        return False

    def __str__(self):
        status = "Returned" if self.returned else "Active"
        return f"{self.book.title} - {self.member.name} ({status})"

class Library:
    def __init__(self, name):
        self.name = name
        self.books = []
        self.members = []
        self.loans = []

    def add_book(self, book):
        self.books.append(book)

    def add_member(self, member):
        self.members.append(member)

    def checkout_book(self, isbn, member_id):
        book = next((b for b in self.books if b.isbn == isbn), None)
        member = next((m for m in self.members if m.member_id == member_id), None)

        if book and member and book.available:
            loan = Loan(book, member)
            self.loans.append(loan)
            book.available = False
            member.loans.append(loan)
            print(f"✓ {book.title} checked out to {member.name}")
        else:
            print("✗ Checkout failed")

    def return_book(self, isbn, member_id):
        loan = next((l for l in self.loans
                     if l.book.isbn == isbn and l.member.member_id == member_id
                     and not l.returned), None)
        if loan:
            loan.return_book()
            print(f"✓ {loan.book.title} returned by {loan.member.name}")
        else:
            print("✗ Return failed")

# Test the library system
lib = Library("City Library")

# Add books
lib.add_book(Book("978-0451524935", "1984", "George Orwell"))
lib.add_book(Book("978-0743273565", "The Great Gatsby", "F. Scott Fitzgerald"))
lib.add_book(Book("978-0061120084", "To Kill a Mockingbird", "Harper Lee"))

# Add members
lib.add_member(Member("M001", "Alice"))
lib.add_member(Member("M002", "Bob"))

# Checkout books
lib.checkout_book("978-0451524935", "M001")
lib.checkout_book("978-0743273565", "M002")

# Display loans
print("\nActive Loans:")
for loan in lib.loans:
    if not loan.returned:
        print(f"  {loan}")

# Return book
lib.return_book("978-0451524935", "M001")

print("\nAll Books:")
for book in lib.books:
    print(f"  {book}")
```

### Expected Output
```
✓ 1984 checked out to Alice
✓ The Great Gatsby checked out to Bob

Active Loans:
  1984 - Alice (Active)
  The Great Gatsby - Bob (Active)

✓ 1984 returned by Alice

All Books:
  1984 by George Orwell (978-0451524935) - Available
  The Great Gatsby by F. Scott Fitzgerald (978-0743273565) - Checked Out
  To Kill a Mockingbird by Harper Lee (978-0061120084) - Available
```

### Common Mistakes
- Not properly managing relationships between classes
- Forgetting to update book availability status

---

## Problem 14: Create an inventory system for a store

### Solution
```python
# Product class
class Product:
    def __init__(self, product_id, name, price, quantity):
        self.product_id = product_id
        self.name = name
        self.price = price
        self.quantity = quantity

    def value(self):
        return self.price * self.quantity

    def __str__(self):
        return f"{self.name} (${self.price}) x{self.quantity} = ${self.value():.2f}"

# Inventory class
class Inventory:
    def __init__(self):
        self.products = {}

    def add_product(self, product):
        if product.product_id in self.products:
            self.products[product.product_id].quantity += product.quantity
        else:
            self.products[product.product_id] = product

    def remove_stock(self, product_id, quantity):
        if product_id in self.products:
            if self.products[product_id].quantity >= quantity:
                self.products[product_id].quantity -= quantity
                return True
        return False

    def add_stock(self, product_id, quantity):
        if product_id in self.products:
            self.products[product_id].quantity += quantity

    def get_product(self, product_id):
        return self.products.get(product_id)

    def total_inventory_value(self):
        return sum(p.value() for p in self.products.values())

    def list_low_stock(self, threshold=10):
        return [p for p in self.products.values() if p.quantity < threshold]

    def display_inventory(self):
        print("Current Inventory:")
        for product in self.products.values():
            print(f"  {product}")
        print(f"Total Inventory Value: ${self.total_inventory_value():.2f}")

# Store class
class Store:
    def __init__(self, name):
        self.name = name
        self.inventory = Inventory()

    def stock_product(self, product):
        self.inventory.add_product(product)
        print(f"✓ Stocked: {product.name}")

    def sell_item(self, product_id, quantity):
        product = self.inventory.get_product(product_id)
        if product and self.inventory.remove_stock(product_id, quantity):
            print(f"✓ Sold {quantity}x {product.name}")
            return True
        else:
            print(f"✗ Cannot sell {quantity}x of item {product_id}")
            return False

    def restock_item(self, product_id, quantity):
        self.inventory.add_stock(product_id, quantity)
        product = self.inventory.get_product(product_id)
        if product:
            print(f"✓ Restocked {quantity}x {product.name}")

# Test the inventory system
store = Store("TechStore")

# Add products
store.stock_product(Product("P001", "Laptop", 999.99, 5))
store.stock_product(Product("P002", "Mouse", 29.99, 50))
store.stock_product(Product("P003", "Keyboard", 79.99, 20))
store.stock_product(Product("P004", "Monitor", 299.99, 3))

store.inventory.display_inventory()

print("\n--- Sales Activity ---")
store.sell_item("P001", 1)
store.sell_item("P002", 10)
store.sell_item("P003", 18)

store.inventory.display_inventory()

print("\n--- Low Stock Items ---")
low_stock = store.inventory.list_low_stock(15)
for product in low_stock:
    print(f"  {product.name}: {product.quantity} units")

print("\n--- Restocking ---")
store.restock_item("P004", 5)
store.inventory.display_inventory()
```

### Expected Output
```
✓ Stocked: Laptop
✓ Stocked: Mouse
✓ Stocked: Keyboard
✓ Stocked: Monitor
Current Inventory:
  Laptop ($999.99) x5 = $4999.95
  Mouse ($29.99) x50 = $1499.50
  Keyboard ($79.99) x20 = $1599.80
  Monitor ($299.99) x3 = $899.97
Total Inventory Value: $8999.22

--- Sales Activity ---
✓ Sold 1x Laptop
✓ Sold 10x Mouse
✓ Sold 18x Keyboard

--- Low Stock Items ---
  Laptop: 4 units
  Keyboard: 2 units
  Monitor: 3 units

--- Restocking ---
✓ Restocked 5x Monitor
Current Inventory:
  Laptop ($999.99) x4 = $3999.96
  Mouse ($29.99) x40 = $1199.60
  Keyboard ($79.99) x2 = $159.98
  Monitor ($299.99) x8 = $2399.92
Total Inventory Value: $7759.46
```

### Common Mistakes
- Not properly updating quantity when items are sold
- Not checking if sufficient stock exists before removing items

---

## Problem 15: Design a music app with playlists, songs, and different audio formats

### Solution
```python
# Song class
class Song:
    def __init__(self, title, artist, duration, format_type):
        self.title = title
        self.artist = artist
        self.duration = duration  # in seconds
        self.format = format_type  # mp3, flac, wav

    def __str__(self):
        minutes = self.duration // 60
        seconds = self.duration % 60
        return f"{self.title} - {self.artist} ({minutes}:{seconds:02d}) [{self.format}]"

# Playlist class
class Playlist:
    def __init__(self, name, owner):
        self.name = name
        self.owner = owner
        self.songs = []

    def add_song(self, song):
        self.songs.append(song)

    def remove_song(self, title):
        self.songs = [s for s in self.songs if s.title != title]

    def total_duration(self):
        return sum(s.duration for s in self.songs)

    def get_songs_by_artist(self, artist):
        return [s for s in self.songs if s.artist == artist]

    def display_playlist(self):
        print(f"Playlist: {self.name} (Owner: {self.owner})")
        if not self.songs:
            print("  (Empty)")
        else:
            for i, song in enumerate(self.songs, 1):
                print(f"  {i}. {song}")
        minutes = self.total_duration() // 60
        print(f"  Total Duration: {minutes} minutes")

# MusicApp class
class MusicApp:
    def __init__(self):
        self.playlists = {}
        self.library = []

    def add_song_to_library(self, song):
        self.library.append(song)

    def create_playlist(self, name, owner):
        playlist = Playlist(name, owner)
        self.playlists[name] = playlist
        return playlist

    def get_playlist(self, name):
        return self.playlists.get(name)

    def add_song_to_playlist(self, playlist_name, song):
        playlist = self.playlists.get(playlist_name)
        if playlist:
            playlist.add_song(song)
            return True
        return False

    def search_songs(self, query):
        """Search songs by title or artist"""
        results = [s for s in self.library
                   if query.lower() in s.title.lower() or query.lower() in s.artist.lower()]
        return results

    def get_format_count(self, format_type):
        """Count songs by format"""
        return sum(1 for s in self.library if s.format == format_type)

# Test the music app
app = MusicApp()

# Add songs to library
app.add_song_to_library(Song("Bohemian Rhapsody", "Queen", 354, "flac"))
app.add_song_to_library(Song("Stairway to Heaven", "Led Zeppelin", 482, "flac"))
app.add_song_to_library(Song("Imagine", "John Lennon", 183, "mp3"))
app.add_song_to_library(Song("Hey Jude", "The Beatles", 427, "mp3"))
app.add_song_to_library(Song("Hotel California", "Eagles", 391, "wav"))

# Create playlists
rock = app.create_playlist("Rock Classics", "DJ Mike")
rock.add_song(app.library[0])
rock.add_song(app.library[1])
rock.add_song(app.library[4])

chill = app.create_playlist("Chill Vibes", "User123")
chill.add_song(app.library[2])
chill.add_song(app.library[3])

# Display playlists
rock.display_playlist()
print()
chill.display_playlist()

# Search songs
print("\n--- Search Results for 'The Beatles' ---")
results = app.search_songs("The Beatles")
for song in results:
    print(f"  {song}")

# Format statistics
print("\n--- Format Count ---")
print(f"  MP3: {app.get_format_count('mp3')} songs")
print(f"  FLAC: {app.get_format_count('flac')} songs")
print(f"  WAV: {app.get_format_count('wav')} songs")
```

### Expected Output
```
Playlist: Rock Classics (Owner: DJ Mike)
  1. Bohemian Rhapsody - Queen (5:54) [flac]
  2. Stairway to Heaven - Led Zeppelin (8:02) [flac]
  3. Hotel California - Eagles (6:31) [wav]
  Total Duration: 20 minutes

Playlist: Chill Vibes (Owner: User123)
  1. Imagine - John Lennon (3:03) [mp3]
  2. Hey Jude - The Beatles (7:07) [mp3]
  Total Duration: 10 minutes

--- Search Results for 'The Beatles' ---
  Hey Jude - The Beatles (7:07) [mp3]

--- Format Count ---
  MP3: 2 songs
  FLAC: 2 songs
  WAV: 1 songs
```

### Common Mistakes
- Not properly managing song relationships with playlists
- Confusion between library and playlist (library is all songs, playlists are subsets)
