# Unit 2: Object-Oriented Programming — Quick Reference Guide

## Class Definition Syntax

```python
class ClassName:
    """Docstring describing the class."""

    # Class variable (shared by all instances)
    class_variable = default_value

    def __init__(self, param1, param2):
        """Constructor - called when creating a new instance."""
        # Instance variables (unique to each object)
        self.attribute1 = param1
        self.attribute2 = param2

    def method_name(self, other_param):
        """Instance method - has access to self."""
        return self.attribute1 + other_param

    @classmethod
    def class_method(cls, param):
        """Class method - receives class, not instance."""
        return cls.class_variable + param

    @staticmethod
    def static_method(param):
        """Static method - no access to instance or class."""
        return param * 2

    @property
    def property_name(self):
        """Property - accessed like an attribute, acts like a method."""
        return self._private_attribute

    @property_name.setter
    def property_name(self, value):
        """Setter for property - validates before storing."""
        if value < 0:
            raise ValueError("Must be positive")
        self._private_attribute = value
```

---

## `__init__` and `self` Explained

### `self`
- Represents the **current instance** of the class
- Always the first parameter in instance methods
- Allows you to access and modify instance-specific data
- Not actually a keyword — it's just a convention (though always use it!)

### `__init__` Constructor
- Called automatically when you create a new object
- Initializes instance variables
- Can accept parameters beyond `self`
- Does NOT return anything (implicitly returns the new object)

```python
class Dog:
    def __init__(self, name, age):
        self.name = name      # Instance variable
        self.age = age        # Instance variable

    def bark(self):
        print(f"{self.name} says woof!")

# Creating instances
dog1 = Dog("Buddy", 3)
dog2 = Dog("Lucy", 5)

dog1.bark()  # Output: Buddy says woof!
dog2.bark()  # Output: Lucy says woof!
```

---

## Inheritance Syntax with `super()`

### Basic Inheritance
```python
class Animal:
    """Parent class."""
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "Some sound"

class Dog(Animal):
    """Child class inherits from Animal."""
    def __init__(self, name, breed):
        super().__init__(name)  # Call parent's __init__
        self.breed = breed

    def speak(self):
        return f"{self.name} barks!"

dog = Dog("Rex", "Labrador")
print(dog.name)    # "Rex"
print(dog.breed)   # "Labrador"
print(dog.speak()) # "Rex barks!"
```

### `super()` Function
- Calls the parent class's method
- Essential for extending parent behavior without copying code
- Syntax: `super().__init__(...)` or `super().method_name(...)`

```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand

    def start(self):
        return f"{self.brand} engine started"

class Car(Vehicle):
    def __init__(self, brand, doors):
        super().__init__(brand)  # Call parent constructor
        self.doors = doors

    def start(self):
        parent_behavior = super().start()  # Call parent method
        return parent_behavior + " with 4 wheels"

car = Car("Toyota", 4)
print(car.start())
# Output: Toyota engine started with 4 wheels
```

---

## Decorators

### `@property` — Getters Without Parentheses

```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance  # Convention: _ prefix for "private"

    @property
    def balance(self):
        """Access like an attribute: account.balance"""
        return self._balance

    @balance.setter
    def balance(self, amount):
        """Set with validation: account.balance = 5000"""
        if amount < 0:
            raise ValueError("Balance cannot be negative")
        self._balance = amount

    @balance.deleter
    def balance(self):
        """Allow deletion: del account.balance"""
        del self._balance

account = BankAccount(1000)
print(account.balance)      # Calls getter: 1000
account.balance = 2000      # Calls setter
print(account.balance)      # 2000
```

### `@classmethod` — Methods That Receive the Class

```python
class Person:
    population = 0

    def __init__(self, name):
        self.name = name
        Person.population += 1

    @classmethod
    def from_birth_year(cls, name, birth_year):
        """Alternative constructor using a class method."""
        age = 2026 - birth_year
        return cls(name)  # Returns new instance

    @classmethod
    def get_population(cls):
        """Access class variable."""
        return f"Population: {cls.population}"

p1 = Person("Alice")
p2 = Person.from_birth_year("Bob", 1995)
print(Person.get_population())  # Output: Population: 2
```

### `@staticmethod` — Methods Independent of Instance/Class

```python
class MathUtils:
    @staticmethod
    def add(a, b):
        """No access to self or cls — just utility."""
        return a + b

    @staticmethod
    def celsius_to_fahrenheit(celsius):
        return (celsius * 9/5) + 32

# Call without creating an instance
print(MathUtils.add(5, 3))                    # 8
print(MathUtils.celsius_to_fahrenheit(0))    # 32.0
```

---

## Special/Dunder Methods

Special methods (double underscore) allow objects to interact with Python syntax.

| Method | Purpose | Example |
|--------|---------|---------|
| `__init__` | Constructor | Called when object created |
| `__str__` | User-friendly string | `print(obj)` or `str(obj)` |
| `__repr__` | Official representation | `repr(obj)`, debugging |
| `__len__` | Length | `len(obj)` |
| `__eq__` | Equality | `obj1 == obj2` |
| `__lt__`, `__le__`, `__gt__`, `__ge__` | Comparison | `obj1 < obj2`, etc. |
| `__add__` | Addition | `obj1 + obj2` |
| `__sub__`, `__mul__`, `__truediv__` | Operators | `-`, `*`, `/` |
| `__iter__` | Make iterable | `for item in obj:` |
| `__next__` | Iterator protocol | `next(iterator)` |
| `__enter__`, `__exit__` | Context manager | `with statement:` |
| `__getitem__`, `__setitem__` | Indexing | `obj[key]` |
| `__call__` | Make callable | `obj()` |

### Examples

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        """Called by print() and str()"""
        return f"Vector({self.x}, {self.y})"

    def __repr__(self):
        """Official representation for debugging"""
        return f"Vector(x={self.x}, y={self.y})"

    def __eq__(self, other):
        """Equality comparison: v1 == v2"""
        return self.x == other.x and self.y == other.y

    def __add__(self, other):
        """Addition: v1 + v2"""
        return Vector(self.x + other.x, self.y + other.y)

    def __len__(self):
        """Length: len(obj)"""
        return int((self.x**2 + self.y**2)**0.5)

v1 = Vector(3, 4)
v2 = Vector(1, 2)

print(v1)           # __str__: Vector(3, 4)
print(repr(v1))     # __repr__: Vector(x=3, y=4)
print(v1 == v2)     # __eq__: False
print(v1 + v2)      # __add__: Vector(4, 6)
print(len(v1))      # __len__: 5
```

### Iterator Protocol

```python
class CountUp:
    def __init__(self, max):
        self.max = max
        self.current = 1

    def __iter__(self):
        """Return iterator object (usually self)"""
        self.current = 1
        return self

    def __next__(self):
        """Return next item or raise StopIteration"""
        if self.current > self.max:
            raise StopIteration
        result = self.current
        self.current += 1
        return result

counter = CountUp(3)
for num in counter:
    print(num)  # Prints 1, 2, 3
```

### Context Manager Protocol

```python
class FileManager:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None

    def __enter__(self):
        """Called when entering 'with' block"""
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_val, exc_tb):
        """Called when exiting 'with' block (cleanup)"""
        if self.file:
            self.file.close()
        return False  # Don't suppress exceptions

with FileManager("test.txt", "w") as f:
    f.write("Hello!")
# File automatically closed
```

---

## Abstract Classes with `abc` Module

Abstract classes define an interface that subclasses **must** implement.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    """Abstract base class - cannot be instantiated directly."""

    @abstractmethod
    def area(self):
        """Subclasses MUST implement this."""
        pass

    @abstractmethod
    def perimeter(self):
        """Subclasses MUST implement this."""
        pass

    def describe(self):
        """Concrete method - subclasses inherit it."""
        return f"I am a shape with area {self.area()}"

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius**2

    def perimeter(self):
        return 2 * 3.14159 * self.radius

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

# shape = Shape()  # TypeError: Can't instantiate abstract class
circle = Circle(5)
rect = Rectangle(4, 6)

print(circle.area())      # 78.54975
print(rect.describe())    # I am a shape with area 24
```

---

## Composition vs Inheritance

### Inheritance ("is-a")
Use when there's a **true hierarchical relationship**.

```python
class Animal:
    def eat(self):
        return "Eating..."

class Dog(Animal):  # Dog IS-A Animal
    def bark(self):
        return "Woof!"

dog = Dog()
print(dog.eat())    # Inherited from Animal
print(dog.bark())   # Own method
```

### Composition ("has-a")
Use to **combine objects with different responsibilities**.

```python
class Engine:
    def start(self):
        return "Engine started"

class Car:  # Car HAS-A Engine (not is-an engine)
    def __init__(self):
        self.engine = Engine()  # Composition

    def start(self):
        return self.engine.start()

car = Car()
print(car.start())  # "Engine started"
```

### When to Use Which

| Situation | Use |
|-----------|-----|
| Natural "is-a" relationship | Inheritance |
| Need shared behavior among related objects | Inheritance |
| Object needs components from different classes | Composition |
| Avoiding deep hierarchies (3+ levels) | Composition |
| Flexibility to swap components | Composition |

---

## Access Modifiers by Convention

Python doesn't enforce privacy, but uses naming conventions:

```python
class BankAccount:
    def __init__(self, balance):
        self.public_account = "12345"      # Public - use freely
        self._protected = balance          # Protected - internal use
        self.__private = balance           # Name-mangled (private intent)

    def get_balance(self):
        """Access private data through public method."""
        return self.__private

account = BankAccount(1000)
print(account.public_account)          # OK
print(account._protected)              # Accessible but discouraged
# print(account.__private)             # AttributeError (name-mangled)
print(account._BankAccount__private)   # Mangled name (accessible but don't do this)
```

### Summary

| Prefix | Meaning | Usage |
|--------|---------|-------|
| `public` | No prefix | Free to use anywhere |
| `_protected` | Single underscore | Internal API, discourage external access |
| `__private` | Double underscore | Name-mangled, strong privacy signal |

---

## Quick Syntax Checklist

- [ ] `class ClassName:` — Define class
- [ ] `def __init__(self, ...)` — Constructor
- [ ] `self.attribute = value` — Instance variable
- [ ] `ClassName.class_var = value` — Class variable
- [ ] `def method(self):` — Instance method
- [ ] `@classmethod` + `cls` — Class method
- [ ] `@staticmethod` — Utility method
- [ ] `@property` — Getter (no parentheses)
- [ ] `@property.setter` — Setter with validation
- [ ] `super().__init__(...)` — Call parent constructor
- [ ] `class Child(Parent):` — Inheritance
- [ ] `@abstractmethod` — Force subclass implementation
- [ ] `__str__`, `__repr__`, `__eq__`, `__add__`, etc. — Special methods
- [ ] `with statement:` + `__enter__/__exit__` — Context manager

---

## Common Error Messages and Fixes

| Error | Cause | Fix |
|-------|-------|-----|
| `TypeError: __init__() missing required positional argument` | Forgot `self` | Add `self` as first parameter |
| `AttributeError: type object has no attribute` | Accessing instance var on class | Use instance: `obj.attribute` not `Class.attribute` |
| `TypeError: 'ClassName' object is not callable` | Forgot `__init__` or `()` | Add `()` when creating object |
| `TypeError: Can't instantiate abstract class` | Didn't implement @abstractmethod | Implement all abstract methods in child class |
| `NameError: name 'super' is not defined` | Wrong Python 2 syntax | Use `super().__init__()` not `super(ClassName, self).__init__()` |

