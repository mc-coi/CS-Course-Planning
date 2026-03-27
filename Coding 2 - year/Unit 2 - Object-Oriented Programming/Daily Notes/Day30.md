# Day 30: Unit 2 Assessment — Object-Oriented Programming

**Learning Target:** I can demonstrate mastery of object-oriented programming concepts including classes, inheritance, polymorphism, encapsulation, and special methods.

---

## Assessment Overview

**Format:** Written assessment (paper or digital)
**Time:** 55 minutes
**Total Points:** 100

| Part | Topic | Points |
|------|-------|--------|
| Part 1 | Multiple Choice | 30 pts (3 pts each) |
| Part 2 | Short Answer | 20 pts (4 pts each) |
| Part 3 | Code Tracing | 20 pts |
| Part 4 | Coding Challenges | 30 pts |

---

## Part 1: Multiple Choice (30 points)

Circle the best answer.

**1.** Which keyword is used to create a class in Python?
- a) `object`
- b) `class`
- c) `def`
- d) `new`

**2.** In Python, `self` refers to:
- a) The parent class
- b) The current module
- c) The current instance of the class
- d) The class itself

**3.** Which of the following creates an instance of a class called `Dog`?
- a) `Dog.create("Buddy")`
- b) `new Dog("Buddy")`
- c) `Dog("Buddy")`
- d) `instance Dog("Buddy")`

**4.** What is the purpose of `__init__`?
- a) To destroy an object
- b) To initialize an object's attributes when it's created
- c) To print the object
- d) To compare two objects

**5.** A class variable is:
- a) A variable defined inside a method
- b) Shared by all instances of the class
- c) Only accessible through `self`
- d) The same as a local variable

**6.** What does `super()` do in a child class?
- a) Calls the current class's method
- b) Calls the parent class's method or `__init__`
- c) Deletes the parent class
- d) Creates a copy of the parent object

**7.** Polymorphism in Python means:
- a) A class can only have one method with a given name
- b) Different classes can have methods with the same name that behave differently
- c) All objects must be the same type
- d) A class cannot inherit from another class

**8.** The `@property` decorator is used to:
- a) Create class methods
- b) Make a method behave like an attribute (getter)
- c) Delete an attribute
- d) Create a static method

**9.** Which dunder method is called when you use `str(obj)` or `print(obj)`?
- a) `__repr__`
- b) `__str__`
- c) `__print__`
- d) `__format__`

**10.** An abstract class:
- a) Cannot be inherited from
- b) Cannot be instantiated directly and may contain abstract methods
- c) Has no attributes or methods
- d) Is the same as a regular class

---

## Part 2: Short Answer (20 points)

Answer each question in 2–4 sentences or with brief code examples.

**11.** Explain the difference between a class variable and an instance variable. Give an example of when you would use each.

**12.** What is encapsulation? How does Python's naming convention (single underscore `_`) support it, and how does `@property` enhance it?

**13.** Describe method overriding. Write a two-class example (parent and child) where the child overrides a parent method.

**14.** What is the difference between inheritance and composition? Give a real-world example of when you would choose composition over inheritance.

**15.** Name and explain three dunder (special) methods other than `__init__`. For each, describe what Python operation triggers it.

---

## Part 3: Code Tracing (20 points)

**16.** (10 pts) Trace this code and write the exact output:

```python
class Animal:
    def __init__(self, name, sound):
        self.name = name
        self.sound = sound

    def speak(self):
        return f"{self.name} says {self.sound}"

    def __str__(self):
        return f"Animal: {self.name}"

class Dog(Animal):
    def __init__(self, name):
        super().__init__(name, "Woof")
        self.tricks = []

    def learn(self, trick):
        self.tricks.append(trick)

    def speak(self):
        base = super().speak()
        return f"{base}! (trained: {len(self.tricks)} tricks)"

a = Animal("Cat", "Meow")
d = Dog("Rex")
d.learn("sit")
d.learn("shake")

print(a.speak())
print(d.speak())
print(str(a))
print(d.name)
print(len(d.tricks))
```

**17.** (10 pts) What is the output of this code? If any line causes an error, write the error type and explain why.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

    def describe(self):
        return f"I am a shape with area {self.area():.2f}"

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

class Square(Shape):
    def __init__(self, side):
        self.side = side

shapes = [Circle(5), Square(4)]

for s in shapes:
    print(s.describe())

blank = Shape()
```

---

## Part 4: Coding Challenges (30 points)

**18.** (10 pts) Create a `Student` class with:
- Attributes: `name`, `_gpa` (private), `courses` (list)
- `@property` for `gpa` with a setter that validates (0.0–4.0 only)
- `add_course(course)` method
- `__str__` that displays name and GPA
- `__repr__` for debugging

```python
# Starter code
class Student:
    def __init__(self, name, gpa):
        pass  # your code here
```

**19.** (10 pts) Create an inheritance hierarchy:
- `Employee` base class: `name`, `salary`, `give_raise(amount)` method, `__str__`
- `Manager(Employee)`: adds `department`, overrides `__str__` to include department, adds `hire(employee)` that adds to a `reports` list
- `Engineer(Employee)`: adds `language` (programming language), overrides `__str__`

Create two engineers and one manager; have the manager hire both engineers; print all three.

**20.** (10 pts) Implement a `Fraction` class that represents a mathematical fraction (numerator/denominator):
- `__init__(self, numerator, denominator)` — raise `ValueError` if denominator is 0
- `__str__` returns `"3/4"` format
- `__add__` adds two fractions (use cross-multiplication: `a/b + c/d = (a*d + b*c) / (b*d)`)
- `__eq__` checks equality (cross-multiply to compare: `a/b == c/d` if `a*d == b*c`)
- `simplify()` reduces to lowest terms (use GCD)

```python
# Test your class with:
f1 = Fraction(1, 2)
f2 = Fraction(1, 3)
f3 = f1 + f2
print(f3)         # should print 5/6
print(f1 == Fraction(2, 4))  # should print True
```

---

## Answer Key

### Part 1 Answers
1. b) `class`
2. c) The current instance of the class
3. c) `Dog("Buddy")`
4. b) To initialize an object's attributes when it's created
5. b) Shared by all instances of the class
6. b) Calls the parent class's method or `__init__`
7. b) Different classes can have methods with the same name that behave differently
8. b) Make a method behave like an attribute (getter)
9. b) `__str__`
10. b) Cannot be instantiated directly and may contain abstract methods

### Part 2 Sample Answers
11. A class variable is defined directly in the class body (outside methods) and is shared across all instances. An instance variable is defined inside `__init__` using `self.` and is unique to each object. Use class variable for shared data (e.g., species = "Canis familiaris"); use instance variable for per-object data (e.g., self.name).

12. Encapsulation hides internal state and requires access through defined methods. The `_` prefix signals "treat as private by convention." `@property` enforces this by letting you run validation code whenever the attribute is read or set.

13. Method overriding means a child class provides its own version of a method defined in the parent. The child version replaces the parent version for that class.
```python
class Animal:
    def speak(self): return "..."
class Dog(Animal):
    def speak(self): return "Woof!"
```

14. Inheritance: "is-a" relationship (Dog is an Animal). Composition: "has-a" relationship (Car has an Engine). Use composition when the relationship is ownership/delegation rather than type-hierarchy; e.g., a `Library` has a list of `Book` objects rather than inheriting from `Book`.

15. Any three from: `__str__` (triggered by str() / print), `__repr__` (triggered by repr() or REPL), `__len__` (triggered by len()), `__eq__` (triggered by ==), `__add__` (triggered by +), `__iter__` (triggered by for loops), `__getitem__` (triggered by []).

### Part 3 Answers

**16.**
```
Cat says Meow
Rex says Woof! (trained: 2 tricks)
Animal: Cat
Rex
2
```

**17.**
```
I am a shape with area 78.54
```
Then: `TypeError: Can't instantiate abstract class Shape with abstract method area`
(Square never defines `area()` so `shapes[1].describe()` would also error — but it's not reached because the list only gets to index 1 after Circle prints successfully. Wait: `Square` never defines `area()` either, so `shapes = [Circle(5), Square(4)]` would raise a TypeError at `Square(4)` since Square is still abstract. Correct answer: `Square(4)` raises `TypeError: Can't instantiate abstract class Square with abstract method area` before any printing occurs.)

Actually: Circle prints `I am a shape with area 78.54`, then Square(4) fails with TypeError on instantiation. Then `Shape()` would also raise TypeError.

### Part 4 Sample Answers

```python
# Problem 18
import math

class Student:
    def __init__(self, name, gpa):
        self.name = name
        self._gpa = 0.0
        self.courses = []
        self.gpa = gpa   # use setter for validation

    @property
    def gpa(self):
        return self._gpa

    @gpa.setter
    def gpa(self, value):
        if not 0.0 <= value <= 4.0:
            raise ValueError(f"GPA must be between 0.0 and 4.0, got {value}")
        self._gpa = value

    def add_course(self, course):
        self.courses.append(course)

    def __str__(self):
        return f"{self.name} (GPA: {self._gpa:.2f})"

    def __repr__(self):
        return f"Student(name={self.name!r}, gpa={self._gpa}, courses={self.courses})"

# Problem 19
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def give_raise(self, amount):
        self.salary += amount

    def __str__(self):
        return f"{self.name} (${self.salary:,})"

class Manager(Employee):
    def __init__(self, name, salary, department):
        super().__init__(name, salary)
        self.department = department
        self.reports = []

    def hire(self, employee):
        self.reports.append(employee)

    def __str__(self):
        return f"{self.name} — Manager of {self.department} (${self.salary:,})"

class Engineer(Employee):
    def __init__(self, name, salary, language):
        super().__init__(name, salary)
        self.language = language

    def __str__(self):
        return f"{self.name} — {self.language} Engineer (${self.salary:,})"

eng1 = Engineer("Alice", 95000, "Python")
eng2 = Engineer("Bob", 90000, "JavaScript")
mgr = Manager("Carol", 120000, "Engineering")
mgr.hire(eng1)
mgr.hire(eng2)
print(mgr)
print(eng1)
print(eng2)

# Problem 20
from math import gcd

class Fraction:
    def __init__(self, numerator, denominator):
        if denominator == 0:
            raise ValueError("Denominator cannot be zero")
        self.numerator = numerator
        self.denominator = denominator

    def simplify(self):
        common = gcd(abs(self.numerator), abs(self.denominator))
        return Fraction(self.numerator // common, self.denominator // common)

    def __add__(self, other):
        new_num = self.numerator * other.denominator + other.numerator * self.denominator
        new_den = self.denominator * other.denominator
        return Fraction(new_num, new_den).simplify()

    def __eq__(self, other):
        return self.numerator * other.denominator == other.numerator * self.denominator

    def __str__(self):
        simple = self.simplify()
        return f"{simple.numerator}/{simple.denominator}"
```
