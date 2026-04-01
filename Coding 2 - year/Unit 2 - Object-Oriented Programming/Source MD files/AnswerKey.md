# Unit 2: Object-Oriented Programming — Complete Answer Key

---

## Beginner Level

---

## Problem 1: Circle Class

### Solution
```python
import math

class Circle:
    """Calculate circle properties."""

    def __init__(self, radius):
        self.radius = radius

    def area(self):
        """Calculate circle area."""
        return math.pi * self.radius ** 2

    def circumference(self):
        """Calculate circle circumference."""
        return 2 * math.pi * self.radius

    def __str__(self):
        """String representation."""
        return f"Circle with radius {self.radius}"

# Test
circle = Circle(5)
print(circle)                      # Circle with radius 5
print(f"{circle.area():.2f}")      # 78.50
print(f"{circle.circumference():.2f}")  # 31.42
```

### Expected Output
```
Circle with radius 5
78.50
31.42
```

### Common Mistakes
- Using `math.pi * self.radius * 2` for circumference instead of `2 * math.pi * self.radius` (both correct but different order)
- Forgetting to import `math` module
- Not returning values from methods (just printing inside them)
- Using `r` instead of `self.radius` in calculations

---

## Problem 2: Student Class with Class Variable

### Solution
```python
class Student:
    """Student class with class variable tracking."""
    total_students = 0

    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa
        Student.total_students += 1  # Increment class variable

    def __str__(self):
        """String representation."""
        return f"{self.name} (GPA: {self.gpa})"

# Test
s1 = Student("Alice", 3.9)
s2 = Student("Bob", 3.5)
print(s1)                  # Alice (GPA: 3.9)
print(Student.total_students)  # 2
```

### Expected Output
```
Alice (GPA: 3.9)
2
```

### Common Mistakes
- Using `self.total_students += 1` instead of `Student.total_students += 1` (would create instance variable)
- Not incrementing in `__init__` (increment should happen every time student is created)
- Resetting total_students when creating each instance (should only initialize once)

---

## Problem 3: Rectangle Class

### Solution
```python
class Rectangle:
    """Rectangle with calculated properties."""

    def __init__(self, width, height):
        self.width = width
        self.height = height

    @property
    def area(self):
        """Calculate area (read-only property)."""
        return self.width * self.height

    @property
    def perimeter(self):
        """Calculate perimeter (read-only property)."""
        return 2 * (self.width + self.height)

    def is_square(self):
        """Check if rectangle is a square."""
        return self.width == self.height

# Test
rect = Rectangle(5, 10)
print(rect.area)       # 50
print(rect.perimeter)  # 30
print(rect.is_square())  # False

square = Rectangle(4, 4)
print(square.is_square())  # True
```

### Expected Output
```
50
30
False
True
```

### Common Mistakes
- Using `def area(self):` instead of `@property` decorator (would require calling `area()`)
- Calculating perimeter as `2 * (self.width * self.height)` instead of `2 * (self.width + self.height)`
- Not using `@property` decorator (would need to call methods like `rect.area()`)
- Using `self.width != self.height` for is_square (should be `==`)

---

## Problem 4: Simple Inheritance — Animal

### Solution
```python
class Animal:
    """Parent class for animals."""

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def speak(self):
        """Default speak method."""
        return "Some sound"

    def birthday(self):
        """Increment age."""
        self.age += 1

class Dog(Animal):
    """Dog subclass."""

    def speak(self):
        """Override speak method."""
        return "Woof!"

# Test
dog = Dog("Rex", 3)
print(dog.speak())  # Woof!
print(dog.age)      # 3
dog.birthday()
print(dog.age)      # 4
```

### Expected Output
```
Woof!
3
4
```

### Common Mistakes
- Not inheriting from Animal: `class Dog:` instead of `class Dog(Animal):`
- Redefining `__init__` when not needed (Dog can use parent's)
- Not overriding speak() in Dog (would return "Some sound")
- Forgetting to call birthday() before checking age increase

---

## Problem 5: Bank Account with Getters/Setters

### Solution
```python
class BankAccount:
    """Bank account with private balance and validation."""

    def __init__(self, balance):
        self._balance = balance

    @property
    def balance(self):
        """Get balance (read-only from outside)."""
        return self._balance

    @balance.setter
    def balance(self, amount):
        """Set balance with validation."""
        if amount < 0:
            raise ValueError("Balance cannot be negative")
        self._balance = amount

    def deposit(self, amount):
        """Add money to account."""
        if amount > 0:
            self.balance = self._balance + amount

    def withdraw(self, amount):
        """Remove money from account."""
        if amount > 0 and amount <= self._balance:
            self.balance = self._balance - amount

# Test
account = BankAccount(1000)
print(account.balance)  # 1000
account.deposit(500)
print(account.balance)  # 1500
account.withdraw(200)
print(account.balance)  # 1300
```

### Expected Output
```
1000
1500
1300
```

### Common Mistakes
- Using `self.balance` without underscore prefix for private variable
- Not using `@property` and `@balance.setter` decorators
- Setter validation not raising error (should raise ValueError for negative)
- Using `self._balance` directly instead of property setter (bypasses validation)

---

## Problem 6: @classmethod Example

### Solution
```python
class Temperature:
    """Temperature with Celsius/Fahrenheit conversion."""

    def __init__(self, celsius):
        self.celsius = celsius

    @classmethod
    def from_fahrenheit(cls, fahrenheit):
        """Create Temperature from Fahrenheit."""
        celsius = (fahrenheit - 32) * 5 / 9
        return cls(celsius)

    @property
    def fahrenheit(self):
        """Get Fahrenheit equivalent."""
        return (self.celsius * 9 / 5) + 32

    def __str__(self):
        """String representation."""
        return f"{self.celsius}°C / {self.fahrenheit}°F"

# Test
t1 = Temperature(0)
print(t1)  # 0°C / 32.0°F
t2 = Temperature.from_fahrenheit(68)
print(t2)  # 20.0°C / 68.0°F
```

### Expected Output
```
0°C / 32.0°F
20.0°C / 68.0°F
```

### Common Mistakes
- Using `def from_fahrenheit(fahrenheit):` without `@classmethod` decorator
- Not using `cls(celsius)` to create instance (would reference undefined class)
- Formula wrong: `(fahrenheit - 32) * 9/5` instead of `(fahrenheit - 32) * 5/9`
- Not returning a Temperature instance from classmethod

---

## Problem 7: Static Method

### Solution
```python
class MathHelper:
    """Helper class with static math methods."""

    @staticmethod
    def is_prime(n):
        """Check if number is prime."""
        if n < 2:
            return False
        for i in range(2, int(n**0.5) + 1):
            if n % i == 0:
                return False
        return True

    @staticmethod
    def factorial(n):
        """Calculate factorial."""
        if n < 0:
            return None
        if n == 0 or n == 1:
            return 1
        result = 1
        for i in range(2, n + 1):
            result *= i
        return result

# Test
print(MathHelper.is_prime(7))      # True
print(MathHelper.is_prime(10))     # False
print(MathHelper.factorial(5))     # 120
```

### Expected Output
```
True
False
120
```

### Common Mistakes
- Not using `@staticmethod` decorator
- Including `self` parameter in static methods
- Checking divisibility up to `n` instead of `sqrt(n)` for primality
- Not handling n < 0 in factorial (should return None or raise error)

---

## Intermediate Level

---

## Problem 8: Special Methods — Comparison

### Solution
```python
class Person:
    """Person class with comparison operators."""

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __eq__(self, other):
        """Equal if same name."""
        return self.name == other.name

    def __lt__(self, other):
        """Less than if younger."""
        return self.age < other.age

    def __str__(self):
        """String representation."""
        return f"{self.name} ({self.age})"

# Test
p1 = Person("Alice", 30)
p2 = Person("Bob", 25)
p3 = Person("Alice", 40)

print(p1 == p3)  # True (same name)
print(p1 < p2)   # False (Alice older than Bob)
print(p2 < p1)   # True (Bob younger than Alice)
```

### Expected Output
```
True
False
True
```

### Common Mistakes
- Using `self == other` in `__eq__` (infinite recursion)
- Comparing age in `__eq__` instead of name
- Using `<=` instead of `<` in `__lt__`
- Not defining `__str__` for readable output

---

## Problem 9: Special Methods — Operators

### Solution
```python
class ComplexNumber:
    """Complex number with arithmetic operators."""

    def __init__(self, real, imag):
        self.real = real
        self.imag = imag

    def __add__(self, other):
        """Add two complex numbers."""
        return ComplexNumber(
            self.real + other.real,
            self.imag + other.imag
        )

    def __mul__(self, other):
        """Multiply two complex numbers: (a+bi)(c+di) = ac-bd + (ad+bc)i."""
        real = self.real * other.real - self.imag * other.imag
        imag = self.real * other.imag + self.imag * other.real
        return ComplexNumber(real, imag)

    def __str__(self):
        """String representation like 3+4j."""
        sign = '+' if self.imag >= 0 else ''
        return f"{self.real}{sign}{self.imag}j"

# Test
c1 = ComplexNumber(3, 4)
c2 = ComplexNumber(1, 2)
print(c1 + c2)  # 4+6j
print(c1 * c2)  # -5+10j
```

### Expected Output
```
4+6j
-5+10j
```

### Common Mistakes
- Multiplication formula wrong: using `ac + bd` instead of `ac - bd` for real part
- String representation showing `3+4j` when both positive, but `-3-4j` when negative (need to handle signs)
- Not returning new ComplexNumber instance from operations
- Confusing `__mul__` operator (multiplication) with something else

---

## Problem 10: Polymorphism with Inheritance

### Solution
```python
class Vehicle:
    """Parent class for vehicles."""

    def accelerate(self):
        """Default acceleration."""
        return "Speed increasing"

class Car(Vehicle):
    """Car subclass."""

    def accelerate(self):
        """Override acceleration."""
        return "Car accelerating smoothly"

class Motorcycle(Vehicle):
    """Motorcycle subclass."""

    def accelerate(self):
        """Override acceleration."""
        return "Motorcycle wheelie!"

# Test polymorphism
vehicles = [Car(), Motorcycle(), Vehicle()]
for vehicle in vehicles:
    print(vehicle.accelerate())
```

### Expected Output
```
Car accelerating smoothly
Motorcycle wheelie!
Speed increasing
```

### Common Mistakes
- Not overriding `accelerate()` in subclasses
- Calling parent method explicitly instead of relying on polymorphism
- Not understanding that same method name produces different output based on object type

---

## Problem 11: Super() with Inheritance

### Solution
```python
class Vehicle:
    """Parent vehicle class."""

    def __init__(self, brand):
        self.brand = brand

    def __str__(self):
        """String representation."""
        return f"{self.brand} vehicle"

class ElectricCar(Vehicle):
    """Electric car subclass."""

    def __init__(self, brand, battery_capacity):
        super().__init__(brand)          # Call parent __init__
        self.battery_capacity = battery_capacity

    def __str__(self):
        """String representation."""
        return f"{self.brand} electric car with {self.battery_capacity} kWh battery"

# Test
car = ElectricCar("Tesla", 100)
print(car)  # Tesla electric car with 100 kWh battery
```

### Expected Output
```
Tesla electric car with 100 kWh battery
```

### Common Mistakes
- Not calling `super().__init__(brand)` (parent initialization skipped)
- Using `Vehicle.__init__(self, brand)` instead of `super()` (less flexible)
- Not storing brand through parent initialization
- Not defining brand as instance variable in parent

---

## Problem 12: Iterator Protocol

### Solution
```python
class Countdown:
    """Iterator that counts down from start to 1."""

    def __init__(self, start):
        self.start = start
        self.current = start

    def __iter__(self):
        """Return iterator object (self)."""
        self.current = self.start
        return self

    def __next__(self):
        """Return next value or raise StopIteration."""
        if self.current < 1:
            raise StopIteration
        result = self.current
        self.current -= 1
        return result

# Test
for num in Countdown(5):
    print(num, end=' ')
# Output: 5 4 3 2 1
```

### Expected Output
```
5 4 3 2 1
```

### Common Mistakes
- Not implementing `__iter__()` (returns self)
- Not raising `StopIteration` when done
- Not decrementing `current` before returning in `__next__`
- Resetting `current = start` in `__next__` instead of `__iter__`

---

## Problem 13: List-like Class with __getitem__ and __len__

### Solution
```python
class Playlist:
    """List-like playlist class."""

    def __init__(self, songs):
        self.songs = songs

    def __len__(self):
        """Return number of songs."""
        return len(self.songs)

    def __getitem__(self, index):
        """Allow indexing like playlist[0]."""
        return self.songs[index]

    def __str__(self):
        """String representation."""
        return f"Playlist: {', '.join(self.songs)}"

# Test
playlist = Playlist(["Song A", "Song B", "Song C"])
print(len(playlist))  # 3
print(playlist[0])    # Song A
print(playlist)       # Playlist: Song A, Song B, Song C
```

### Expected Output
```
3
Song A
Playlist: Song A, Song B, Song C
```

### Common Mistakes
- Not implementing `__getitem__()` (cannot use indexing)
- Returning `self.songs` instead of `self.songs[index]` in `__getitem__`
- Not implementing `__len__()` (len() won't work)
- Using `self.songs[index]` directly instead of delegating

---

## Problem 14: Abstract Class

### Solution
```python
from abc import ABC, abstractmethod

class Animal(ABC):
    """Abstract animal class."""

    @abstractmethod
    def make_sound(self):
        """Make a sound (must be implemented by subclasses)."""
        pass

    @abstractmethod
    def move(self):
        """Move (must be implemented by subclasses)."""
        pass

    def sleep(self):
        """Concrete method available to all."""
        return "Zzz..."

class Dog(Animal):
    """Concrete dog class."""

    def make_sound(self):
        return "Woof!"

    def move(self):
        return "Running on four legs"

class Bird(Animal):
    """Concrete bird class."""

    def make_sound(self):
        return "Tweet!"

    def move(self):
        return "Flying"

# Test
animals = [Dog(), Bird()]
for animal in animals:
    print(animal.make_sound())
    print(animal.move())
    print(animal.sleep())
```

### Expected Output
```
Woof!
Running on four legs
Zzz...
Tweet!
Flying
Zzz...
```

### Common Mistakes
- Not inheriting from ABC
- Not implementing abstract methods in subclasses
- Using `pass` in abstract methods without `@abstractmethod` decorator
- Trying to instantiate abstract class directly: `Animal()`

---

## Problem 15: Composition — Building a Complete System

### Solution
```python
class Book:
    """Book class."""

    def __init__(self, title, author, isbn):
        self.title = title
        self.author = author
        self.isbn = isbn

    def __str__(self):
        return f"{self.title} by {self.author}"

class Library:
    """Library composed of books."""

    def __init__(self):
        self.books = []

    def add_book(self, book):
        """Add book to library."""
        self.books.append(book)

    def remove_book(self, isbn):
        """Remove book by ISBN."""
        self.books = [b for b in self.books if b.isbn != isbn]

    def find_by_author(self, author):
        """Find all books by author."""
        return [b for b in self.books if b.author == author]

    def __str__(self):
        """String representation."""
        return "\n".join(str(book) for book in self.books)

# Test
library = Library()
book1 = Book("1984", "George Orwell", "123456")
book2 = Book("Animal Farm", "George Orwell", "123457")
library.add_book(book1)
library.add_book(book2)

print(len(library.find_by_author("George Orwell")))  # 2
```

### Expected Output
```
2
```

### Common Mistakes
- Using inheritance instead of composition: `class Library(Book)` is wrong
- Not storing books in a list
- Not checking ISBN correctly in remove_book
- Trying to directly access book attributes instead of using object methods

---

## Challenge Level

---

## Problem 16: Multi-level Inheritance Hierarchy

### Solution
```python
class Animal:
    """Base animal class."""

    def __init__(self, name):
        self.name = name

    def make_sound(self):
        return "Generic sound"

    def __str__(self):
        return f"{self.__class__.__name__}: {self.name}"

class Mammal(Animal):
    """Mammal subclass."""
    warm_blooded = True

class Dog(Mammal):
    """Dog class."""

    def make_sound(self):
        return "Woof!"

class Cat(Mammal):
    """Cat class."""

    def make_sound(self):
        return "Meow!"

class Reptile(Animal):
    """Reptile subclass."""
    warm_blooded = False

class Snake(Reptile):
    """Snake class."""

    def make_sound(self):
        return "Hisss!"

# Test
animals = [Dog("Buddy"), Cat("Whiskers"), Snake("Scar")]
for animal in animals:
    print(f"{animal} - {animal.make_sound()}")
```

### Expected Output
```
Dog: Buddy - Woof!
Cat: Whiskers - Meow!
Snake: Scar - Hisss!
```

### Common Mistakes
- Not creating intermediate classes (Mammal, Reptile)
- Forgetting class variables like `warm_blooded`
- Not implementing make_sound() in specific subclasses
- Using wrong class name in `__str__` output

---

## Problem 17: Singleton Pattern

### Solution
```python
class DatabaseConnection:
    """Singleton pattern: ensures only one instance exists."""

    _instance = None

    def __new__(cls):
        """Control instance creation."""
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

    def connect(self):
        """Connect to database."""
        return "Connected to database"

# Test
db1 = DatabaseConnection()
db2 = DatabaseConnection()
print(db1 is db2)        # True (same instance)
print(db1.connect())     # Connected to database
```

### Expected Output
```
True
Connected to database
```

### Common Mistakes
- Not using `__new__` method (use `__init__` instead, which gets called multiple times)
- Not storing `_instance` as class variable
- Forgetting `super().__new__(cls)` to create the instance
- Returning wrong instance in `__new__`

---

## Problem 18: Factory Pattern

### Solution
```python
from abc import ABC, abstractmethod

class Animal(ABC):
    """Abstract animal class."""

    @abstractmethod
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

class Duck(Animal):
    def speak(self):
        return "Quack!"

class AnimalFactory:
    """Factory for creating animals."""

    @staticmethod
    def create_animal(animal_type):
        """Create animal based on type."""
        animals = {
            "dog": Dog,
            "cat": Cat,
            "duck": Duck
        }
        return animals.get(animal_type.lower(), Dog)()

# Test
animals = [
    AnimalFactory.create_animal("dog"),
    AnimalFactory.create_animal("cat"),
    AnimalFactory.create_animal("duck")
]
for animal in animals:
    print(animal.speak())
```

### Expected Output
```
Woof!
Meow!
Quack!
```

### Common Mistakes
- Not using dictionary to map types to classes
- Calling class directly instead of using factory
- Not handling unknown types (should default to Dog)
- Not using @staticmethod for factory method

---

## Problem 19: Custom Exception Class and Usage

### Solution
```python
class InsufficientFundsError(Exception):
    """Custom exception for insufficient funds."""

    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        message = f"Cannot withdraw {amount}. Balance is {balance}"
        super().__init__(message)

class BankAccount:
    """Bank account with custom exception."""

    def __init__(self, balance):
        self.balance = balance

    def withdraw(self, amount):
        """Withdraw money or raise custom exception."""
        if amount > self.balance:
            raise InsufficientFundsError(self.balance, amount)
        self.balance -= amount
        return f"Withdrew {amount}. Balance: {self.balance}"

    def deposit(self, amount):
        """Deposit money."""
        self.balance += amount
        return f"Deposited {amount}. Balance: {self.balance}"

# Test
account = BankAccount(1000)
print(account.deposit(500))

try:
    print(account.withdraw(2000))
except InsufficientFundsError as e:
    print(f"Error: {e}")
```

### Expected Output
```
Deposited 500. Balance: 1500
Error: Cannot withdraw 2000. Balance is 1500
```

### Common Mistakes
- Not inheriting from Exception class
- Not calling `super().__init__(message)` in custom exception
- Raising generic Exception instead of custom InsufficientFundsError
- Not storing exception details (balance, amount)

---

## Problem 20: Complete System Design

### Solution
```python
class Book:
    """Book with multiple copies available."""

    def __init__(self, title, author, isbn, copies):
        self.title = title
        self.author = author
        self.isbn = isbn
        self.copies = copies

    def __str__(self):
        return f"{self.title} by {self.author} ({self.copies} copies)"

class Member:
    """Library member."""

    def __init__(self, name, member_id):
        self.name = name
        self.member_id = member_id
        self.borrowed_books = []

    def __str__(self):
        return f"{self.name} (ID: {self.member_id})"

class Library:
    """Complete library management system."""

    def __init__(self):
        self.books = {}        # isbn -> Book
        self.members = {}      # member_id -> Member

    def add_book(self, book):
        """Add book to library."""
        self.books[book.isbn] = book

    def register_member(self, member):
        """Register new member."""
        self.members[member.member_id] = member

    def borrow_book(self, member_id, isbn):
        """Borrow book (check availability, deduct, track)."""
        if member_id not in self.members or isbn not in self.books:
            return "Invalid member or book"

        book = self.books[isbn]
        if book.copies <= 0:
            return "Book not available"

        member = self.members[member_id]
        book.copies -= 1
        member.borrowed_books.append(isbn)
        return f"{member.name} borrowed '{book.title}'"

    def return_book(self, member_id, isbn):
        """Return book (increment copies, remove from member)."""
        if member_id not in self.members or isbn not in self.books:
            return "Invalid member or book"

        member = self.members[member_id]
        if isbn not in member.borrowed_books:
            return f"{member.name} doesn't have this book"

        member.borrowed_books.remove(isbn)
        self.books[isbn].copies += 1
        return f"{member.name} returned '{self.books[isbn].title}'"

    def get_member_books(self, member_id):
        """Get list of books borrowed by member."""
        if member_id not in self.members:
            return []
        member = self.members[member_id]
        return [self.books[isbn].title for isbn in member.borrowed_books]

# Test
library = Library()
book1 = Book("1984", "Orwell", "123", 2)
book2 = Book("Brave New World", "Huxley", "456", 1)
library.add_book(book1)
library.add_book(book2)

member1 = Member("Alice", "M001")
library.register_member(member1)

print(library.borrow_book("M001", "123"))
print(library.get_member_books("M001"))  # ['1984']
print(library.return_book("M001", "123"))
print(library.get_member_books("M001"))  # []
```

### Expected Output
```
Alice borrowed '1984'
['1984']
Alice returned '1984'
[]
```

### Common Mistakes
- Not checking if book/member exists before operations
- Not tracking borrowed books on member
- Not decrementing/incrementing book copies correctly
- Not removing ISBN from borrowed_books on return
- Returning string message instead of book title from get_member_books

---
