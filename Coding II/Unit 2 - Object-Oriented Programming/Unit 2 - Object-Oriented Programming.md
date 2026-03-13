# Unit 2: Object-Oriented Programming
> Master the principles of object-oriented design: classes, objects, inheritance, and polymorphism. Write scalable, maintainable code.

##  Unit Overview
- **Duration:** 9 days / 3 weeks
- **Key Concepts:** Classes and objects, encapsulation, inheritance, polymorphism, special methods, and design patterns
- **Big Idea:** Objects combine data and behavior—a powerful way to model real-world entities and build complex programs
- **TN Standard:** 9-12.CCI.1 — Use an object-oriented programming language with classes and objects

##  Learning Targets
- I can define classes with attributes and methods
- I can create objects and call methods on them
- I can understand the difference between class and instance variables
- I can implement encapsulation with private attributes and properties
- I can create inheritance hierarchies and use super()
- I can override methods and implement polymorphism
- I can use special methods (__str__, __repr__, __len__, __eq__)
- I can design complete object-oriented programs

---

# Day 1: Introduction to OOP
**Learning Target:** I can define classes and create objects with attributes and methods.

### Key Concepts
**Object-oriented programming (OOP)** organizes code around objects that combine data (attributes) and behavior (methods).

**Class:** A blueprint defining the structure of objects.
**Object (instance):** An individual example of a class.
**Attribute:** A variable that belongs to an object.
**Method:** A function that belongs to an object.

Think of a class like a blueprint for a car, and each car you build from that blueprint is an object.

### Code Examples
```python
# Define a class
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def bark(self):
        print(f"{self.name} says woof!")

    def age_in_dog_years(self):
        return self.age * 7

# Create objects (instances)
dog1 = Dog("Buddy", 3)
dog2 = Dog("Max", 5)

# Access attributes
print(dog1.name)  # "Buddy"

# Call methods
dog1.bark()  # "Buddy says woof!"
print(dog2.age_in_dog_years())  # 35
```

### Guided Practice
Create a Student class with name and grade attributes. Add a method that prints a greeting.

### Practice Problems
**Problem 1 — Beginner:** Create a simple Circle class with a radius attribute and a method to calculate area.

**Problem 2 — Intermediate:** Create a BankAccount class with balance, deposit(), and withdraw() methods.

**Problem 3 — Challenge:** Create a Book class with title, author, and pages. Add methods for a summary and reading progress.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

# Problem 2
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount
```
</details>

---

# Day 2: Defining Classes & __init__
**Learning Target:** I can define constructors and initialize objects with attributes.

### Key Concepts
The `__init__` method (constructor) initializes objects when created. The first parameter is always `self`, referring to the object being created.

`self` allows methods to access and modify the object's data.

### Code Examples
```python
class Car:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year
        self.odometer = 0

    def drive(self, distance):
        self.odometer += distance
        print(f"Drove {distance} miles. Total: {self.odometer}")

car = Car("Toyota", "Camry", 2020)
print(car.make)  # "Toyota"
car.drive(50)    # Drove 50 miles. Total: 50
```

### Guided Practice
Create a Movie class that initializes title, director, and year released. Add a method to display movie info.

### Practice Problems
**Problem 1 — Beginner:** Create a Rectangle class with width and height. Initialize in __init__.

**Problem 2 — Intermediate:** Create a Person class that tracks name, birth_year. Add a method to calculate age.

**Problem 3 — Challenge:** Create a VideoGame class tracking title, genre, release_year, and playtime_hours. Add methods to update playtime.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

# Problem 2
class Person:
    def __init__(self, name, birth_year):
        self.name = name
        self.birth_year = birth_year

    def age(self):
        return 2024 - self.birth_year
```
</details>

---

# Day 3: Instance Methods
**Learning Target:** I can define and call instance methods that operate on object data.

### Key Concepts
Instance methods are functions defined in a class that operate on instance data. They have access to `self` and can modify the object's state.

### Code Examples
```python
class Playlist:
    def __init__(self, name):
        self.name = name
        self.songs = []

    def add_song(self, song):
        self.songs.append(song)
        print(f"Added '{song}' to {self.name}")

    def remove_song(self, song):
        if song in self.songs:
            self.songs.remove(song)

    def play(self):
        for song in self.songs:
            print(f"Playing {song}")

    def song_count(self):
        return len(self.songs)

playlist = Playlist("Rock Classics")
playlist.add_song("Bohemian Rhapsody")
playlist.add_song("Stairway to Heaven")
print(playlist.song_count())  # 2
playlist.play()
```

### Guided Practice
Create a TodoList class with methods to add tasks, complete tasks, and display all tasks.

### Practice Problems
**Problem 1 — Beginner:** Create a Stack class with push() and pop() methods.

**Problem 2 — Intermediate:** Create a Library class that tracks books and allows adding/removing/searching.

**Problem 3 — Challenge:** Create a ShoppingCart class with methods to add items, remove items, calculate total price with tax.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop()

# Problem 2
class Library:
    def __init__(self):
        self.books = []

    def add_book(self, title):
        self.books.append(title)

    def search(self, title):
        return title in self.books
```
</details>

---

# Day 4: Class vs Instance Variables
**Learning Target:** I can distinguish between class variables and instance variables and use them appropriately.

### Key Concepts
**Instance variables** are unique to each object: `self.name`.
**Class variables** are shared by all instances of a class. Define them outside __init__.

### Code Examples
```python
class Student:
    school = "Lincoln High"  # Class variable—shared by all students

    def __init__(self, name):
        self.name = name  # Instance variable—unique to each student
        self.grade = 9

student1 = Student("Alice")
student2 = Student("Bob")

print(student1.name)      # "Alice"
print(student2.name)      # "Bob"
print(student1.school)    # "Lincoln High"—same for both
print(Student.school)     # Access class variable from class itself

# Modifying class variable
Student.school = "Washington High"
print(student1.school)    # "Washington High"—changes for all
```

### Guided Practice
Create a Car class with a class variable tracking the number of cars created. Update it when each car is created.

### Practice Problems
**Problem 1 — Beginner:** Create a Counter class with a class variable that counts instances created.

**Problem 2 — Intermediate:** Create a Game with a class variable for high score and instance variables for player data.

**Problem 3 — Challenge:** Create an Employee class with salary (class variable), name, and id. Track and display company-wide info.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Counter:
    count = 0

    def __init__(self):
        Counter.count += 1

# Problem 2
class Game:
    high_score = 0

    def __init__(self, player_name):
        self.player_name = player_name
        self.score = 0
```
</details>

---

# Day 5: Encapsulation & Properties
**Learning Target:** I can implement encapsulation using private attributes and @property decorator.

### Key Concepts
**Encapsulation** hides internal details and exposes only what's necessary.

**Private attributes** (prefix with _) are intended for internal use only.
**Properties** provide controlled access to attributes using getters and setters via @property.

### Code Examples
```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance  # Private attribute

    @property
    def balance(self):
        return self._balance

    @balance.setter
    def balance(self, amount):
        if amount < 0:
            print("Error: Balance cannot be negative")
            return
        self._balance = amount

    def deposit(self, amount):
        if amount > 0:
            self._balance += amount

account = BankAccount(1000)
print(account.balance)  # 1000
account.deposit(500)
print(account.balance)  # 1500
account.balance = -100  # "Error: Balance cannot be negative"
```

### Guided Practice
Create a Temperature class that stores temperature in Celsius but provides properties to get/set in Fahrenheit.

### Practice Problems
**Problem 1 — Beginner:** Create a Student class with a private _gpa that only accepts values 0-4.0.

**Problem 2 — Intermediate:** Create a Box class with height, width, depth properties that validate positive numbers.

**Problem 3 — Challenge:** Create a User class with private password that validates strength (length, characters).

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Student:
    def __init__(self, name, gpa):
        self._gpa = gpa

    @property
    def gpa(self):
        return self._gpa

    @gpa.setter
    def gpa(self, value):
        if 0 <= value <= 4.0:
            self._gpa = value
```
</details>

---

# Day 6: Inheritance
**Learning Target:** I can create class hierarchies using inheritance and call parent methods with super().

### Key Concepts
**Inheritance** allows a child class to inherit attributes and methods from a parent class.

Use `super()` to call parent methods.

### Code Examples
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        print(f"{self.name} makes a sound")

class Dog(Animal):
    def speak(self):
        print(f"{self.name} barks")

class Cat(Animal):
    def speak(self):
        print(f"{self.name} meows")

dog = Dog("Rex")
dog.speak()  # "Rex barks"

cat = Cat("Whiskers")
cat.speak()  # "Whiskers meows"
```

### Guided Practice
Create a Shape parent class and Rectangle/Circle child classes with area() methods.

### Practice Problems
**Problem 1 — Beginner:** Create a Vehicle class and Car/Motorcycle child classes.

**Problem 2 — Intermediate:** Create an Employee parent and Manager/Developer child classes.

**Problem 3 — Challenge:** Create a multi-level inheritance: Animal > Mammal > Dog.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Vehicle:
    def __init__(self, make):
        self.make = make

class Car(Vehicle):
    def __init__(self, make, doors):
        super().__init__(make)
        self.doors = doors

# Problem 2
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def get_info(self):
        return f"{self.name}: ${self.salary}"

class Manager(Employee):
    def __init__(self, name, salary, team_size):
        super().__init__(name, salary)
        self.team_size = team_size
```
</details>

---

# Day 7: Polymorphism & Method Overriding
**Learning Target:** I can override methods and implement polymorphism.

### Key Concepts
**Polymorphism** means "many forms." Multiple classes can have the same method name with different implementations.

### Code Examples
```python
class Shape:
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

shapes = [Rectangle(5, 10), Circle(3)]
for shape in shapes:
    print(shape.area())  # Calls the right area() for each type
```

### Guided Practice
Create an Employee hierarchy where different employee types calculate pay differently.

### Practice Problems
**Problem 1 — Beginner:** Create a method in parent that child classes override.

**Problem 2 — Intermediate:** Create multiple shapes that override a common method.

**Problem 3 — Challenge:** Create a media player with different format classes (MP3, Video, Audio) that handle playback differently.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 & 2 covered in code example

# Problem 3 (partial)
class MediaPlayer:
    def play(self):
        pass

class MP3Player(MediaPlayer):
    def play(self):
        print("Playing audio file...")
```
</details>

---

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

# Day 9: OOP Project Day — Bank Account System
**Learning Target:** I can design and implement a complete object-oriented program.

### Project Overview
Build a banking system with:
- Account class with deposit, withdraw, transfer
- CheckingAccount and SavingsAccount subclasses
- Interest calculation for savings
- Transaction history
- Account statements

### Requirements
- Use inheritance (parent Account class)
- Implement encapsulation (private balance)
- Use properties for controlled access
- Implement __str__ for account display
- Track multiple accounts

### Scaffold & Starter Code
```python
class Account:
    def __init__(self, holder, balance):
        self.holder = holder
        self._balance = balance
        self.transactions = []

    @property
    def balance(self):
        return self._balance

    def deposit(self, amount):
        self._balance += amount
        self.transactions.append(f"Deposit: +${amount}")

    def withdraw(self, amount):
        if amount <= self._balance:
            self._balance -= amount
            self.transactions.append(f"Withdraw: -${amount}")
        else:
            print("Insufficient funds")

    def __str__(self):
        return f"{self.holder}: ${self._balance:.2f}"

class SavingsAccount(Account):
    def __init__(self, holder, balance, interest_rate):
        super().__init__(holder, balance)
        self.interest_rate = interest_rate

    def apply_interest(self):
        interest = self._balance * self.interest_rate
        self.deposit(interest)

# Test
account = SavingsAccount("Zach McCoy", 1000, 0.05)
account.deposit(500)
account.apply_interest()
print(account)
```

### Enhancement Ideas
- Multiple accounts per person
- Monthly statements
- Transfer between accounts
- Overdraft protection
- Loan calculations

---

# Unit Practice Bank

1. **Beginner:** Create a simple class with an __init__ and one method.
2. **Beginner:** Create an object and call one of its methods.
3. **Beginner:** Add attributes to a class in __init__.
4. **Intermediate:** Create a parent class and child class with inheritance.
5. **Intermediate:** Override a method from a parent class.
6. **Intermediate:** Create a class with a private attribute using @property.
7. **Intermediate:** Implement __str__ for a class.
8. **Challenge:** Create a multi-level hierarchy with multiple subclasses.
9. **Challenge:** Implement multiple dunder methods in a custom class.
10. **Challenge:** Design a complete class system for a real-world entity (e.g., University with Students and Courses).
11. **Challenge:** Create a shape system where different shapes calculate area differently.
12. **Challenge:** Implement a game character system with different character types.
13. **Challenge:** Build a library system with Books, Members, and Loans.
14. **Challenge:** Create an inventory system for a store.
15. **Challenge:** Design a music app with playlists, songs, and different audio formats.

---

# Common Mistakes & How to Fix Them
| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Forgetting `self` in method definitions | NameError or TypeError | Always include `self` as first parameter |
| `self.variable` outside __init__ | Works but inconsistent | Initialize all attributes in __init__ |
| Not calling `super().__init__()` in child | Parent attributes not initialized | Always call super().__init__() when inheriting |
| Modifying class variable thinking it's instance variable | Changes affect all instances | Use self.name (instance) not ClassName.name |
| `def method(self):` then calling `method(obj, arg)` instead of `obj.method(arg)` | TypeError: too many arguments | Remember to use dot notation for method calls |
| Trying to access private attribute directly: `obj._balance = 1000` | Defeats encapsulation | Use properties via @property/@setter |
| Circular inheritance or invalid hierarchy | TypeError or logic errors | Use clear parent-child relationships (no cycles) |

---

# Unit Assessment Prep

**Review Questions:**

1. What is the difference between a class and an object?
2. What does __init__ do and why do methods need `self`?
3. Explain the difference between instance and class variables.
4. How do you implement encapsulation?
5. What is inheritance and why use it?
6. Explain method overriding with an example.
7. What is polymorphism?
8. List 3 dunder methods and their purposes.
9. When would you use @property instead of a regular method?
10. How do you call a parent method from a child class?

**Answers:**

1. A class is a blueprint; an object is an instance created from that blueprint.
2. __init__ initializes objects. self refers to the specific object being created/used.
3. Instance variables are unique to each object; class variables are shared by all instances.
4. Use private attributes (_name) and @property for controlled access.
5. Inheritance allows child classes to reuse code from parent classes, reducing repetition.
6. Method overriding replaces a parent method with a child version. Example: Animal.speak() → Dog.speak().
7. Polymorphism allows different classes to have the same method name with different behaviors.
8. __str__ (user-friendly display), __len__ (support len()), __eq__ (support ==).
9. When you need validation or transformation when getting/setting a value.
10. Use super().method_name().

---

# Vocabulary & Quick Reference

**Key Terms:**
- **Class:** Blueprint for creating objects
- **Object/Instance:** Individual example of a class
- **Attribute:** Variable belonging to an object
- **Method:** Function belonging to an object
- **self:** Reference to the current object
- **__init__:** Constructor method that initializes objects
- **Inheritance:** Child class inherits from parent class
- **Encapsulation:** Hiding internal details
- **Polymorphism:** Same method name, different implementations
- **Dunder method:** Special method like __str__ or __init__

**Key Syntax:**
```python
class ClassName:
    def __init__(self, param):
        self.attribute = param

    def method(self):
        return self.attribute

class Child(Parent):
    def __init__(self, param):
        super().__init__(param)

@property
def attribute(self):
    return self._attribute
```
