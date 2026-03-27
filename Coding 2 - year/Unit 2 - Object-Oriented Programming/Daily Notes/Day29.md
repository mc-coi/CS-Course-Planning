# Day 29: Unit 2 Review — Object-Oriented Programming

**Learning Target:** I can review and consolidate all OOP concepts from Unit 2 in preparation for the unit assessment.

---

## Key Concepts Review

Today we review every major topic from Unit 2. Use this as a study guide and complete the practice exercises to solidify your understanding before tomorrow's assessment.

### 1. Classes and Objects
A **class** is a blueprint; an **object** is an instance built from that blueprint.

```python
class Dog:
    species = "Canis familiaris"   # class variable — shared by all instances

    def __init__(self, name, age):
        self.name = name           # instance variable — unique to each object
        self.age = age

    def bark(self):
        return f"{self.name} says Woof!"

buddy = Dog("Buddy", 3)
max_dog = Dog("Max", 5)
print(buddy.bark())          # Buddy says Woof!
print(Dog.species)           # Canis familiaris
```

### 2. Encapsulation — @property
Use `_` convention and `@property` to protect attributes:

```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance    # "private" by convention

    @property
    def balance(self):
        return self._balance

    @balance.setter
    def balance(self, amount):
        if amount < 0:
            raise ValueError("Balance cannot be negative")
        self._balance = amount
```

### 3. Inheritance and super()
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "..."

class Cat(Animal):
    def speak(self):              # method overriding
        return f"{self.name} says Meow!"

class Kitten(Cat):
    def __init__(self, name, age):
        super().__init__(name)    # call parent __init__
        self.age = age
```

### 4. Polymorphism
Same method name, different behavior:
```python
animals = [Dog("Rex", 2), Cat("Whiskers")]
for animal in animals:
    print(animal.speak())    # Each calls its own version
```

### 5. Dunder Methods
```python
class Vector:
    def __init__(self, x, y):
        self.x, self.y = x, y

    def __str__(self):    return f"Vector({self.x}, {self.y})"
    def __repr__(self):   return f"Vector(x={self.x}, y={self.y})"
    def __add__(self, other): return Vector(self.x + other.x, self.y + other.y)
    def __eq__(self, other):  return self.x == other.x and self.y == other.y
    def __len__(self):    return int((self.x**2 + self.y**2)**0.5)
```

### 6. Abstract Classes
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, r): self.r = r
    def area(self): return 3.14159 * self.r ** 2
# Shape()  ← TypeError: can't instantiate abstract class
```

---

## Review Activities

**Activity 1 — Flash Card Questions (5 min)**
Answer each without looking at your notes:
1. What is the difference between a class variable and an instance variable?
2. What does `super()` do?
3. Name three dunder methods and what they do.
4. What is polymorphism? Give an example.
5. What is the difference between composition and inheritance?

**Activity 2 — Code Trace (10 min)**
Trace this code and predict the output before running it:

```python
class Vehicle:
    wheels = 4
    def __init__(self, make, speed):
        self.make = make
        self.speed = speed
    def describe(self):
        return f"{self.make} goes {self.speed} mph"

class Motorcycle(Vehicle):
    wheels = 2
    def describe(self):
        return f"Motorcycle: {super().describe()}"

v = Vehicle("Toyota", 60)
m = Motorcycle("Harley", 90)
print(v.describe())
print(m.describe())
print(Vehicle.wheels)
print(m.wheels)
```

**Activity 3 — Fix the Bugs (10 min)**

```python
# Bug 1: Why does this fail?
class Counter:
    count = 0
    def increment(self):
        count += 1   # Bug here

# Bug 2: Why does this fail?
class Person:
    def __init__(name, age):   # Bug here
        self.name = name

# Bug 3: Why does this fail?
from abc import ABC, abstractmethod
class Animal(ABC):
    @abstractmethod
    def speak(self): pass

pet = Animal()   # Bug here
```

**Activity 4 — Mini Design Challenge (15 min)**
Design (pseudocode + brief code skeleton) a `Library` system with:
- `Book` class (title, author, ISBN, available)
- `Library` class that holds a list of books
- Methods: add_book, checkout_book, return_book, search_by_author
- Use encapsulation for the available status

---

## Practice Problems

**Beginner:** Create a `Rectangle` class with width and height. Add `__str__` to display dimensions and an `area()` method.

**Intermediate:** Create a `Vehicle` base class and two subclasses (`Car` and `Truck`). Override a `describe()` method in each. Create a list of mixed vehicles and call `describe()` on each.

**Challenge:** Implement a `Stack` class (LIFO data structure) with `push()`, `pop()`, `peek()`, and `is_empty()`. Add `__len__`, `__str__`, and `__repr__` dunder methods.

<details>
<summary>💡 Hints</summary>

- Beginner: `__str__` returns a string; `area()` returns width × height
- Intermediate: A list of parent-type objects can hold child-type objects in Python (polymorphism)
- Challenge: A stack is "last in, first out" — use a list internally and only add/remove from the end
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Beginner
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
    def __str__(self):
        return f"Rectangle({self.width}x{self.height})"
    def area(self):
        return self.width * self.height

# Intermediate
class Vehicle:
    def __init__(self, make, year):
        self.make = make
        self.year = year
    def describe(self):
        return f"{self.year} {self.make}"

class Car(Vehicle):
    def describe(self):
        return f"Car: {super().describe()}"

class Truck(Vehicle):
    def __init__(self, make, year, payload):
        super().__init__(make, year)
        self.payload = payload
    def describe(self):
        return f"Truck: {super().describe()}, payload: {self.payload} tons"

fleet = [Car("Honda", 2022), Truck("Ford", 2021, 5), Car("Tesla", 2023)]
for v in fleet:
    print(v.describe())

# Challenge
class Stack:
    def __init__(self):
        self._items = []
    def push(self, item):
        self._items.append(item)
    def pop(self):
        if self.is_empty():
            raise IndexError("pop from empty stack")
        return self._items.pop()
    def peek(self):
        if self.is_empty():
            raise IndexError("peek at empty stack")
        return self._items[-1]
    def is_empty(self):
        return len(self._items) == 0
    def __len__(self):
        return len(self._items)
    def __str__(self):
        return f"Stack({self._items})"
    def __repr__(self):
        return f"Stack(items={self._items!r})"
```
</details>

---

## Assessment Topics Checklist

Before tomorrow's assessment, make sure you can:

- [ ] Define a class with `__init__`, `self`, attributes, and methods
- [ ] Explain the difference between class and instance variables
- [ ] Use `@property` for encapsulation
- [ ] Create a child class that inherits from a parent class
- [ ] Use `super()` correctly
- [ ] Override a method and explain polymorphism
- [ ] Implement `__str__`, `__repr__`, `__len__`, `__eq__`
- [ ] Explain when to use inheritance vs composition
- [ ] Read and trace OOP code written by someone else
- [ ] Identify and fix common OOP bugs
