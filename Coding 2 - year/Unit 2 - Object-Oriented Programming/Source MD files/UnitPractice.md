# Unit 2: Object-Oriented Programming — Practice Problems

## Overview
This file contains 20 practice problems across three difficulty levels:
- **Beginner (Problems 1-7):** Basic class definition, simple inheritance
- **Intermediate (Problems 8-15):** Properties, special methods, polymorphism
- **Challenge (Problems 16-20):** Design patterns, composition, advanced OOP

---

## Beginner Level

### Problem 1: Circle Class
Create a `Circle` class with:
- Constructor that takes `radius`
- Methods: `area()`, `circumference()`, `__str__()`

**Starter Code:**
```python
class Circle:
    def __init__(self, radius):
        # Your code here
        pass

    def area(self):
        # Your code here
        pass

    def circumference(self):
        # Your code here
        pass

    def __str__(self):
        # Your code here
        pass

# Test
circle = Circle(5)
print(circle)  # Expected: Circle with radius 5
print(circle.area())  # Expected: ~78.54
print(circle.circumference())  # Expected: ~31.42
```

<details>
<summary>Answer</summary>

```python
import math

class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

    def circumference(self):
        return 2 * math.pi * self.radius

    def __str__(self):
        return f"Circle with radius {self.radius}"

# Test
circle = Circle(5)
print(circle)  # Circle with radius 5
print(f"{circle.area():.2f}")  # 78.50
print(f"{circle.circumference():.2f}")  # 31.42
```

</details>

---

### Problem 2: Student Class with Class Variable
Create a `Student` class with:
- Instance variables: `name`, `gpa`
- Class variable: `total_students` (incremented on each new student)
- Method: `__str__()` that returns formatted info

**Starter Code:**
```python
class Student:
    total_students = 0

    def __init__(self, name, gpa):
        # Your code here
        pass

    def __str__(self):
        # Your code here
        pass

# Test
s1 = Student("Alice", 3.9)
s2 = Student("Bob", 3.5)
print(s1)  # Expected: Alice (GPA: 3.9)
print(Student.total_students)  # Expected: 2
```

<details>
<summary>Answer</summary>

```python
class Student:
    total_students = 0

    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa
        Student.total_students += 1

    def __str__(self):
        return f"{self.name} (GPA: {self.gpa})"

# Test
s1 = Student("Alice", 3.9)
s2 = Student("Bob", 3.5)
print(s1)  # Alice (GPA: 3.9)
print(Student.total_students)  # 2
```

</details>

---

### Problem 3: Rectangle Class
Create a `Rectangle` class with:
- Constructor taking `width` and `height`
- Properties: `area`, `perimeter`
- Method: `is_square()` returns True if width == height

**Starter Code:**
```python
class Rectangle:
    def __init__(self, width, height):
        # Your code here
        pass

    # Define area as a property
    # Define perimeter as a property
    # Define is_square method

# Test
rect = Rectangle(5, 10)
print(rect.area)  # Expected: 50
print(rect.perimeter)  # Expected: 30
print(rect.is_square())  # Expected: False

square = Rectangle(4, 4)
print(square.is_square())  # Expected: True
```

<details>
<summary>Answer</summary>

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    @property
    def area(self):
        return self.width * self.height

    @property
    def perimeter(self):
        return 2 * (self.width + self.height)

    def is_square(self):
        return self.width == self.height

# Test
rect = Rectangle(5, 10)
print(rect.area)  # 50
print(rect.perimeter)  # 30
print(rect.is_square())  # False

square = Rectangle(4, 4)
print(square.is_square())  # True
```

</details>

---

### Problem 4: Simple Inheritance — Animal
Create a parent class `Animal` with:
- Constructor: `name`, `age`
- Method: `speak()` returns "Some sound"
- Method: `birthday()` increments age

Create a child class `Dog(Animal)` with:
- Override `speak()` to return "Woof!"

**Starter Code:**
```python
class Animal:
    def __init__(self, name, age):
        # Your code here
        pass

    def speak(self):
        # Your code here
        pass

    def birthday(self):
        # Your code here
        pass

class Dog(Animal):
    def speak(self):
        # Your code here
        pass

# Test
dog = Dog("Rex", 3)
print(dog.speak())  # Expected: Woof!
print(dog.age)  # Expected: 3
dog.birthday()
print(dog.age)  # Expected: 4
```

<details>
<summary>Answer</summary>

```python
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def speak(self):
        return "Some sound"

    def birthday(self):
        self.age += 1

class Dog(Animal):
    def speak(self):
        return "Woof!"

# Test
dog = Dog("Rex", 3)
print(dog.speak())  # Woof!
print(dog.age)  # 3
dog.birthday()
print(dog.age)  # 4
```

</details>

---

### Problem 5: Bank Account with Getters/Setters
Create a `BankAccount` class with:
- Private `__balance` attribute
- `@property` balance getter
- `@balance.setter` that validates (must be >= 0)
- Methods: `deposit(amount)`, `withdraw(amount)`

**Starter Code:**
```python
class BankAccount:
    def __init__(self, balance):
        # Your code here
        pass

    @property
    def balance(self):
        # Your code here
        pass

    @balance.setter
    def balance(self, amount):
        # Your code here
        pass

    def deposit(self, amount):
        # Your code here
        pass

    def withdraw(self, amount):
        # Your code here
        pass

# Test
account = BankAccount(1000)
print(account.balance)  # Expected: 1000
account.deposit(500)
print(account.balance)  # Expected: 1500
account.withdraw(200)
print(account.balance)  # Expected: 1300
# account.balance = -100  # Should raise ValueError
```

<details>
<summary>Answer</summary>

```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance

    @property
    def balance(self):
        return self._balance

    @balance.setter
    def balance(self, amount):
        if amount < 0:
            raise ValueError("Balance cannot be negative")
        self._balance = amount

    def deposit(self, amount):
        if amount > 0:
            self.balance = self._balance + amount

    def withdraw(self, amount):
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

</details>

---

### Problem 6: @classmethod Example
Create a `Temperature` class with:
- Instance variable: `celsius`
- `@classmethod` method: `from_fahrenheit(fahrenheit)` creates instance
- `@property`: `fahrenheit` returns Fahrenheit equivalent
- `__str__()` method

**Starter Code:**
```python
class Temperature:
    def __init__(self, celsius):
        # Your code here
        pass

    @classmethod
    def from_fahrenheit(cls, fahrenheit):
        # Your code here
        pass

    @property
    def fahrenheit(self):
        # Your code here
        pass

    def __str__(self):
        # Your code here
        pass

# Test
t1 = Temperature(0)
print(t1)  # Expected: 0°C / 32.0°F
t2 = Temperature.from_fahrenheit(68)
print(t2)  # Expected: 20.0°C / 68°F
```

<details>
<summary>Answer</summary>

```python
class Temperature:
    def __init__(self, celsius):
        self.celsius = celsius

    @classmethod
    def from_fahrenheit(cls, fahrenheit):
        celsius = (fahrenheit - 32) * 5/9
        return cls(celsius)

    @property
    def fahrenheit(self):
        return (self.celsius * 9/5) + 32

    def __str__(self):
        return f"{self.celsius}°C / {self.fahrenheit}°F"

# Test
t1 = Temperature(0)
print(t1)  # 0°C / 32.0°F
t2 = Temperature.from_fahrenheit(68)
print(t2)  # 20.0°C / 68.0°F
```

</details>

---

### Problem 7: Static Method
Create a `MathHelper` class with:
- `@staticmethod` method: `is_prime(n)` returns True if prime
- `@staticmethod` method: `factorial(n)` returns factorial
- Can be called without creating an instance

**Starter Code:**
```python
class MathHelper:
    @staticmethod
    def is_prime(n):
        # Your code here
        pass

    @staticmethod
    def factorial(n):
        # Your code here
        pass

# Test
print(MathHelper.is_prime(7))  # Expected: True
print(MathHelper.is_prime(10))  # Expected: False
print(MathHelper.factorial(5))  # Expected: 120
```

<details>
<summary>Answer</summary>

```python
class MathHelper:
    @staticmethod
    def is_prime(n):
        if n < 2:
            return False
        for i in range(2, int(n**0.5) + 1):
            if n % i == 0:
                return False
        return True

    @staticmethod
    def factorial(n):
        if n < 0:
            return None
        if n == 0 or n == 1:
            return 1
        result = 1
        for i in range(2, n + 1):
            result *= i
        return result

# Test
print(MathHelper.is_prime(7))  # True
print(MathHelper.is_prime(10))  # False
print(MathHelper.factorial(5))  # 120
```

</details>

---

## Intermediate Level

### Problem 8: Special Methods — Comparison
Create a `Person` class with:
- `name` and `age` attributes
- `__eq__(other)` — equal if same name
- `__lt__(other)` — less than if younger
- `__str__()`

**Starter Code:**
```python
class Person:
    def __init__(self, name, age):
        # Your code here
        pass

    def __eq__(self, other):
        # Your code here
        pass

    def __lt__(self, other):
        # Your code here
        pass

    def __str__(self):
        # Your code here
        pass

# Test
p1 = Person("Alice", 30)
p2 = Person("Bob", 25)
p3 = Person("Alice", 40)

print(p1 == p3)  # Expected: True (same name)
print(p1 < p2)  # Expected: False (Alice older)
print(p2 < p1)  # Expected: True (Bob younger)
```

<details>
<summary>Answer</summary>

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __eq__(self, other):
        return self.name == other.name

    def __lt__(self, other):
        return self.age < other.age

    def __str__(self):
        return f"{self.name} ({self.age})"

# Test
p1 = Person("Alice", 30)
p2 = Person("Bob", 25)
p3 = Person("Alice", 40)

print(p1 == p3)  # True
print(p1 < p2)  # False
print(p2 < p1)  # True
```

</details>

---

### Problem 9: Special Methods — Operators
Create a `ComplexNumber` class with:
- `real` and `imag` attributes
- `__add__(other)` for addition
- `__mul__(other)` for multiplication
- `__str__()` for display (e.g., "3+4j")

**Starter Code:**
```python
class ComplexNumber:
    def __init__(self, real, imag):
        # Your code here
        pass

    def __add__(self, other):
        # Your code here
        pass

    def __mul__(self, other):
        # Your code here
        pass

    def __str__(self):
        # Your code here
        pass

# Test
c1 = ComplexNumber(3, 4)
c2 = ComplexNumber(1, 2)
print(c1 + c2)  # Expected: 4+6j
print(c1 * c2)  # Expected: -5+10j (3*1 + 3*2j + 4j*1 + 4j*2j = 3 + 6j + 4j - 8 = -5+10j)
```

<details>
<summary>Answer</summary>

```python
class ComplexNumber:
    def __init__(self, real, imag):
        self.real = real
        self.imag = imag

    def __add__(self, other):
        return ComplexNumber(
            self.real + other.real,
            self.imag + other.imag
        )

    def __mul__(self, other):
        # (a + bi)(c + di) = ac - bd + (ad + bc)i
        real = self.real * other.real - self.imag * other.imag
        imag = self.real * other.imag + self.imag * other.real
        return ComplexNumber(real, imag)

    def __str__(self):
        sign = '+' if self.imag >= 0 else ''
        return f"{self.real}{sign}{self.imag}j"

# Test
c1 = ComplexNumber(3, 4)
c2 = ComplexNumber(1, 2)
print(c1 + c2)  # 4+6j
print(c1 * c2)  # -5+10j
```

</details>

---

### Problem 10: Polymorphism with Inheritance
Create a parent `Vehicle` class and child classes `Car` and `Motorcycle`:
- `Vehicle`: method `accelerate()` returns "Speed increasing"
- `Car`: override `accelerate()` to return "Car accelerating smoothly"
- `Motorcycle`: override `accelerate()` to return "Motorcycle wheelie!"
- Test polymorphism

**Starter Code:**
```python
class Vehicle:
    def accelerate(self):
        # Your code here
        pass

class Car(Vehicle):
    def accelerate(self):
        # Your code here
        pass

class Motorcycle(Vehicle):
    def accelerate(self):
        # Your code here
        pass

# Test (polymorphism)
vehicles = [Car(), Motorcycle(), Vehicle()]
for vehicle in vehicles:
    print(vehicle.accelerate())
```

<details>
<summary>Answer</summary>

```python
class Vehicle:
    def accelerate(self):
        return "Speed increasing"

class Car(Vehicle):
    def accelerate(self):
        return "Car accelerating smoothly"

class Motorcycle(Vehicle):
    def accelerate(self):
        return "Motorcycle wheelie!"

# Test (polymorphism)
vehicles = [Car(), Motorcycle(), Vehicle()]
for vehicle in vehicles:
    print(vehicle.accelerate())
# Output:
# Car accelerating smoothly
# Motorcycle wheelie!
# Speed increasing
```

</details>

---

### Problem 11: Super() with Inheritance
Create a `Vehicle` class and `ElectricCar` subclass:
- `Vehicle.__init__()` takes `brand`
- `ElectricCar.__init__()` takes `brand` and `battery_capacity`
- Use `super().__init__()` to call parent constructor
- Both classes have a `__str__()` method

**Starter Code:**
```python
class Vehicle:
    def __init__(self, brand):
        # Your code here
        pass

    def __str__(self):
        # Your code here
        pass

class ElectricCar(Vehicle):
    def __init__(self, brand, battery_capacity):
        # Your code here
        pass

    def __str__(self):
        # Your code here
        pass

# Test
car = ElectricCar("Tesla", 100)
print(car)  # Expected: Tesla electric car with 100 kWh battery
```

<details>
<summary>Answer</summary>

```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand

    def __str__(self):
        return f"{self.brand} vehicle"

class ElectricCar(Vehicle):
    def __init__(self, brand, battery_capacity):
        super().__init__(brand)
        self.battery_capacity = battery_capacity

    def __str__(self):
        return f"{self.brand} electric car with {self.battery_capacity} kWh battery"

# Test
car = ElectricCar("Tesla", 100)
print(car)  # Tesla electric car with 100 kWh battery
```

</details>

---

### Problem 12: Iterator Protocol
Create a `Countdown` class that iterates from `start` down to 1:
- Implement `__iter__()`
- Implement `__next__()`
- Should work with `for` loops

**Starter Code:**
```python
class Countdown:
    def __init__(self, start):
        # Your code here
        pass

    def __iter__(self):
        # Your code here
        pass

    def __next__(self):
        # Your code here
        pass

# Test
for num in Countdown(5):
    print(num, end=' ')
# Expected: 5 4 3 2 1
```

<details>
<summary>Answer</summary>

```python
class Countdown:
    def __init__(self, start):
        self.start = start
        self.current = start

    def __iter__(self):
        self.current = self.start
        return self

    def __next__(self):
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

</details>

---

### Problem 13: List-like Class with __getitem__ and __len__
Create a `Playlist` class:
- `__init__()` takes a list of song names
- `__len__()` returns number of songs
- `__getitem__(index)` returns song at index
- `__str__()` displays playlist

**Starter Code:**
```python
class Playlist:
    def __init__(self, songs):
        # Your code here
        pass

    def __len__(self):
        # Your code here
        pass

    def __getitem__(self, index):
        # Your code here
        pass

    def __str__(self):
        # Your code here
        pass

# Test
playlist = Playlist(["Song A", "Song B", "Song C"])
print(len(playlist))  # Expected: 3
print(playlist[0])  # Expected: Song A
print(playlist)  # Expected: Playlist: Song A, Song B, Song C
```

<details>
<summary>Answer</summary>

```python
class Playlist:
    def __init__(self, songs):
        self.songs = songs

    def __len__(self):
        return len(self.songs)

    def __getitem__(self, index):
        return self.songs[index]

    def __str__(self):
        return f"Playlist: {', '.join(self.songs)}"

# Test
playlist = Playlist(["Song A", "Song B", "Song C"])
print(len(playlist))  # 3
print(playlist[0])  # Song A
print(playlist)  # Playlist: Song A, Song B, Song C
```

</details>

---

### Problem 14: Abstract Class
Create an abstract `Animal` class (using `abc` module):
- `@abstractmethod` method: `make_sound()`
- `@abstractmethod` method: `move()`
- Concrete method: `sleep()` returns "Zzz..."

Create concrete subclasses `Dog` and `Bird`.

**Starter Code:**
```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        pass

    @abstractmethod
    def move(self):
        pass

    def sleep(self):
        # Your code here
        pass

class Dog(Animal):
    def make_sound(self):
        # Your code here
        pass

    def move(self):
        # Your code here
        pass

class Bird(Animal):
    def make_sound(self):
        # Your code here
        pass

    def move(self):
        # Your code here
        pass

# Test
animals = [Dog(), Bird()]
for animal in animals:
    print(animal.make_sound())
    print(animal.move())
    print(animal.sleep())
```

<details>
<summary>Answer</summary>

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        pass

    @abstractmethod
    def move(self):
        pass

    def sleep(self):
        return "Zzz..."

class Dog(Animal):
    def make_sound(self):
        return "Woof!"

    def move(self):
        return "Running on four legs"

class Bird(Animal):
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
# Output:
# Woof!
# Running on four legs
# Zzz...
# Tweet!
# Flying
# Zzz...
```

</details>

---

### Problem 15: Composition — Building a Complete System
Create a `Library` class composed of `Book` objects:
- `Book`: attributes `title`, `author`, `isbn`
- `Library`: manages list of books
  - `add_book(book)`
  - `remove_book(isbn)`
  - `find_by_author(author)` returns list
  - `__str__()` displays all books

**Starter Code:**
```python
class Book:
    def __init__(self, title, author, isbn):
        # Your code here
        pass

    def __str__(self):
        # Your code here
        pass

class Library:
    def __init__(self):
        # Your code here
        pass

    def add_book(self, book):
        # Your code here
        pass

    def remove_book(self, isbn):
        # Your code here
        pass

    def find_by_author(self, author):
        # Your code here
        pass

    def __str__(self):
        # Your code here
        pass

# Test
library = Library()
book1 = Book("1984", "George Orwell", "123456")
book2 = Book("Animal Farm", "George Orwell", "123457")
library.add_book(book1)
library.add_book(book2)
print(library.find_by_author("George Orwell"))  # Expected: 2 books
```

<details>
<summary>Answer</summary>

```python
class Book:
    def __init__(self, title, author, isbn):
        self.title = title
        self.author = author
        self.isbn = isbn

    def __str__(self):
        return f"{self.title} by {self.author}"

class Library:
    def __init__(self):
        self.books = []

    def add_book(self, book):
        self.books.append(book)

    def remove_book(self, isbn):
        self.books = [b for b in self.books if b.isbn != isbn]

    def find_by_author(self, author):
        return [b for b in self.books if b.author == author]

    def __str__(self):
        return "\n".join(str(book) for book in self.books)

# Test
library = Library()
book1 = Book("1984", "George Orwell", "123456")
book2 = Book("Animal Farm", "George Orwell", "123457")
library.add_book(book1)
library.add_book(book2)
print(len(library.find_by_author("George Orwell")))  # 2
```

</details>

---

## Challenge Level

### Problem 16: Multi-level Inheritance Hierarchy
Create an inheritance hierarchy:
- `Animal` (parent)
  - `Mammal(Animal)` — has `warm_blooded = True`
  - `Dog(Mammal)` — specific implementation
  - `Cat(Mammal)` — specific implementation
  - `Reptile(Animal)` — has `warm_blooded = False`
  - `Snake(Reptile)` — specific implementation

Each should have appropriate `make_sound()` and `__str__()`.

**Starter Code:**
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def make_sound(self):
        return "Generic sound"

    def __str__(self):
        return f"{self.__class__.__name__}: {self.name}"

# Your code: Create Mammal, Dog, Cat, Reptile, Snake classes

# Test
animals = [
    Dog("Buddy"),
    Cat("Whiskers"),
    Snake("Scar")
]
for animal in animals:
    print(f"{animal} - {animal.make_sound()}")
```

<details>
<summary>Answer</summary>

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def make_sound(self):
        return "Generic sound"

    def __str__(self):
        return f"{self.__class__.__name__}: {self.name}"

class Mammal(Animal):
    warm_blooded = True

class Dog(Mammal):
    def make_sound(self):
        return "Woof!"

class Cat(Mammal):
    def make_sound(self):
        return "Meow!"

class Reptile(Animal):
    warm_blooded = False

class Snake(Reptile):
    def make_sound(self):
        return "Hisss!"

# Test
animals = [
    Dog("Buddy"),
    Cat("Whiskers"),
    Snake("Scar")
]
for animal in animals:
    print(f"{animal} - {animal.make_sound()}")
# Output:
# Dog: Buddy - Woof!
# Cat: Whiskers - Meow!
# Snake: Scar - Hisss!
```

</details>

---

### Problem 17: Singleton Pattern
Implement the Singleton design pattern:
- `DatabaseConnection` class that ensures only ONE instance exists
- All calls to `DatabaseConnection()` return the same instance
- Test that multiple "instances" are identical

**Starter Code:**
```python
class DatabaseConnection:
    _instance = None

    def __new__(cls):
        # Your code here
        pass

    def connect(self):
        return "Connected to database"

# Test
db1 = DatabaseConnection()
db2 = DatabaseConnection()
print(db1 is db2)  # Expected: True
```

<details>
<summary>Answer</summary>

```python
class DatabaseConnection:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

    def connect(self):
        return "Connected to database"

# Test
db1 = DatabaseConnection()
db2 = DatabaseConnection()
print(db1 is db2)  # True
print(db1.connect())  # Connected to database
```

</details>

---

### Problem 18: Factory Pattern
Implement the Factory pattern:
- `Animal` base class with abstract `speak()` method
- `AnimalFactory` class with `@staticmethod create_animal(animal_type)` method
- Factory should create appropriate subclass instances

**Starter Code:**
```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

# Your code: Add factory and animal subclasses

class AnimalFactory:
    @staticmethod
    def create_animal(animal_type):
        # Your code here
        pass

# Test
animals = [
    AnimalFactory.create_animal("dog"),
    AnimalFactory.create_animal("cat"),
    AnimalFactory.create_animal("duck")
]
for animal in animals:
    print(animal.speak())
```

<details>
<summary>Answer</summary>

```python
from abc import ABC, abstractmethod

class Animal(ABC):
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
    @staticmethod
    def create_animal(animal_type):
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
# Output:
# Woof!
# Meow!
# Quack!
```

</details>

---

### Problem 19: Custom Exception Class and Usage
Create a custom `InsufficientFundsError` exception and a `BankAccount` class that:
- Raises custom exception if withdrawal exceeds balance
- Has `deposit()` and `withdraw()` with proper error handling
- Demonstrates polymorphism with exception handling

**Starter Code:**
```python
class InsufficientFundsError(Exception):
    # Your code here
    pass

class BankAccount:
    def __init__(self, balance):
        # Your code here
        pass

    def withdraw(self, amount):
        # Your code here
        pass

    def deposit(self, amount):
        # Your code here
        pass

# Test
account = BankAccount(1000)
account.deposit(500)
try:
    account.withdraw(2000)
except InsufficientFundsError as e:
    print(f"Error: {e}")
```

<details>
<summary>Answer</summary>

```python
class InsufficientFundsError(Exception):
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        message = f"Cannot withdraw {amount}. Balance is {balance}"
        super().__init__(message)

class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def withdraw(self, amount):
        if amount > self.balance:
            raise InsufficientFundsError(self.balance, amount)
        self.balance -= amount
        return f"Withdrew {amount}. Balance: {self.balance}"

    def deposit(self, amount):
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

</details>

---

### Problem 20: Complete System Design
Build a `Library Management System` with:
- `Book` class: `title`, `author`, `isbn`, `copies`
- `Member` class: `name`, `member_id`, `borrowed_books`
- `Library` class managing both Books and Members
  - `add_book(book)`
  - `register_member(member)`
  - `borrow_book(member_id, isbn)` — decrements copies, adds to member
  - `return_book(member_id, isbn)` — increments copies, removes from member
  - `get_member_books(member_id)`
  - `__str__()` displays all books and members

**Starter Code:**
```python
class Book:
    def __init__(self, title, author, isbn, copies):
        # Your code here
        pass

    def __str__(self):
        # Your code here
        pass

class Member:
    def __init__(self, name, member_id):
        # Your code here
        pass

class Library:
    def __init__(self):
        # Your code here
        pass

    def add_book(self, book):
        # Your code here
        pass

    def register_member(self, member):
        # Your code here
        pass

    def borrow_book(self, member_id, isbn):
        # Your code here
        pass

    def return_book(self, member_id, isbn):
        # Your code here
        pass

    def get_member_books(self, member_id):
        # Your code here
        pass

# Test
library = Library()
book1 = Book("1984", "Orwell", "123", 2)
book2 = Book("Brave New World", "Huxley", "456", 1)
library.add_book(book1)
library.add_book(book2)

member1 = Member("Alice", "M001")
library.register_member(member1)

library.borrow_book("M001", "123")
print(library.get_member_books("M001"))  # Alice has 1984
library.return_book("M001", "123")
print(library.get_member_books("M001"))  # Alice has no books
```

<details>
<summary>Answer</summary>

```python
class Book:
    def __init__(self, title, author, isbn, copies):
        self.title = title
        self.author = author
        self.isbn = isbn
        self.copies = copies

    def __str__(self):
        return f"{self.title} by {self.author} ({self.copies} copies)"

class Member:
    def __init__(self, name, member_id):
        self.name = name
        self.member_id = member_id
        self.borrowed_books = []

    def __str__(self):
        return f"{self.name} (ID: {self.member_id})"

class Library:
    def __init__(self):
        self.books = {}  # isbn -> Book
        self.members = {}  # member_id -> Member

    def add_book(self, book):
        self.books[book.isbn] = book

    def register_member(self, member):
        self.members[member.member_id] = member

    def borrow_book(self, member_id, isbn):
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
        if member_id not in self.members or isbn not in self.books:
            return "Invalid member or book"

        member = self.members[member_id]
        if isbn not in member.borrowed_books:
            return f"{member.name} doesn't have this book"

        member.borrowed_books.remove(isbn)
        self.books[isbn].copies += 1
        return f"{member.name} returned '{self.books[isbn].title}'"

    def get_member_books(self, member_id):
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

</details>

---

## Summary Checklist

- [ ] Problems 1-7: Basic class, inheritance, getters/setters
- [ ] Problems 8-15: Special methods, polymorphism, iterators, composition
- [ ] Problems 16-20: Hierarchies, design patterns, custom exceptions, system design
- [ ] All code tested and produces expected output
- [ ] Understand when to use inheritance vs composition
- [ ] Comfortable with dunder methods and operator overloading
- [ ] Can implement abstract classes and interfaces

