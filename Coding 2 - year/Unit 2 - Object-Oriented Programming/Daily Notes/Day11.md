# Day 11: The super() Function
**Learning Target:** I can use super() to call parent class methods and constructors from child classes.

### Key Concepts

**super():** A built-in function that returns a temporary object of the parent class, allowing you to call parent methods from a child class.

**Method Overriding:** When a child class provides its own version of a method from the parent class.

**Calling Parent Constructor:** Using `super().__init__()` to initialize parent attributes in child class constructor.

**Extending Parent Behavior:** Using `super().method()` to call parent method and then add extra behavior.

### Code Examples

```python
# Simple example: super().__init__()
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age = age

class Dog(Animal):
    def __init__(self, name, age, breed):
        super().__init__(name, age)  # Call parent constructor
        self.breed = breed

dog = Dog("Buddy", 3, "Golden Retriever")
print(f"{dog.name} is a {dog.breed}")

# Calling parent method while extending behavior
class Vehicle:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def start(self):
        print(f"{self.brand} {self.model} is starting...")

class Car(Vehicle):
    def __init__(self, brand, model, num_doors):
        super().__init__(brand, model)
        self.num_doors = num_doors

    def start(self):
        super().start()  # Call parent method
        print(f"Checking {self.num_doors} doors...")
        print("Car is ready to drive!")

car = Car("Toyota", "Camry", 4)
car.start()
# Toyota Camry is starting...
# Checking 4 doors...
# Car is ready to drive!

# Shape example with super()
class Shape:
    def __init__(self, color):
        self.color = color

    def describe(self):
        print(f"Color: {self.color}")

class Circle(Shape):
    def __init__(self, color, radius):
        super().__init__(color)
        self.radius = radius

    def describe(self):
        super().describe()  # Call parent describe
        print(f"Radius: {self.radius}")

circle = Circle("red", 5)
circle.describe()
# Color: red
# Radius: 5

# Employee hierarchy with super()
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self._salary = salary

    def get_info(self):
        return f"{self.name}: ${self._salary}"

    def give_raise(self, amount):
        self._salary = self._salary + amount

class Manager(Employee):
    def __init__(self, name, salary, team_size):
        super().__init__(name, salary)
        self.team_size = team_size

    def get_info(self):
        base_info = super().get_info()
        return f"{base_info}, manages {self.team_size} people"

    def give_raise(self, amount):
        super().give_raise(amount * 1.5)  # Managers get 1.5x raise

emp = Employee("Alice", 50000)
print(emp.get_info())  # Alice: $50000
emp.give_raise(5000)
print(emp.get_info())  # Alice: $55000

mgr = Manager("Bob", 80000, 5)
print(mgr.get_info())  # Bob: $80000, manages 5 people
mgr.give_raise(5000)
print(mgr.get_info())  # Bob: $87500, manages 5 people

# Complex hierarchy
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def introduce(self):
        return f"I am {self.name}"

class Student(Person):
    def __init__(self, name, age, student_id):
        super().__init__(name, age)
        self.student_id = student_id

    def introduce(self):
        base = super().introduce()
        return f"{base}, a {self.age}-year-old student (ID: {self.student_id})"

class GraduateStudent(Student):
    def __init__(self, name, age, student_id, thesis_topic):
        super().__init__(name, age, student_id)
        self.thesis_topic = thesis_topic

    def introduce(self):
        base = super().introduce()
        return f"{base} working on: {self.thesis_topic}"

grad = GraduateStudent("Charlie", 26, "G001", "Machine Learning Applications")
print(grad.introduce())
# I am Charlie, a 26-year-old student (ID: G001) working on: Machine Learning Applications

# Method resolution order (MRO) with super()
class A:
    def method(self):
        print("A's method")

class B(A):
    def method(self):
        print("B's method")
        super().method()

class C(A):
    def method(self):
        print("C's method")
        super().method()

class D(B, C):
    def method(self):
        print("D's method")
        super().method()

d = D()
d.method()
# D's method
# B's method
# C's method
# A's method

# GradeBook example
class GradeBook:
    def __init__(self, student_name):
        self.student_name = student_name
        self._grades = []

    def add_grade(self, grade):
        if 0 <= grade <= 100:
            self._grades.append(grade)

    def get_average(self):
        if len(self._grades) == 0:
            return 0
        return sum(self._grades) / len(self._grades)

class WeightedGradeBook(GradeBook):
    def __init__(self, student_name):
        super().__init__(student_name)
        self._weights = {}

    def add_grade(self, grade, weight=1):
        super().add_grade(grade)
        if weight not in self._weights:
            self._weights[weight] = 0
        self._weights[weight] = self._weights[weight] + 1

    def get_weighted_average(self):
        if len(self._grades) == 0:
            return 0
        weighted_sum = 0
        total_weight = 0
        for grade in self._grades:
            weighted_sum = weighted_sum + grade
            total_weight = total_weight + 1
        return weighted_sum / total_weight

book = GradeBook("Alice")
book.add_grade(90)
book.add_grade(85)
book.add_grade(95)
print(f"Average: {book.get_average():.2f}")

wbook = WeightedGradeBook("Bob")
wbook.add_grade(90, 2)
wbook.add_grade(85, 1)
wbook.add_grade(95, 2)
print(f"Weighted average: {wbook.get_weighted_average():.2f}")
```

### Guided Practice

**Activity: Create a Banking System with super()**

Follow these steps:

1. Create a `BankAccount` class with:
   - `__init__` taking holder and balance
   - `deposit(amount)` and `withdraw(amount)` methods
   - `get_balance()` method

2. Create a `SavingsAccount(BankAccount)` class with:
   - `__init__` calling `super().__init__()` and adding interest_rate
   - Override `deposit()` to call parent and add interest bonus
   - Override `withdraw()` to apply a fee

3. Test with multiple accounts

**Solution:**
```python
class BankAccount:
    def __init__(self, holder, balance):
        self.holder = holder
        self._balance = balance

    def deposit(self, amount):
        if amount > 0:
            self._balance = self._balance + amount
            print(f"Deposited ${amount}")

    def withdraw(self, amount):
        if 0 < amount <= self._balance:
            self._balance = self._balance - amount
            print(f"Withdrew ${amount}")
        else:
            print("Insufficient funds!")

    def get_balance(self):
        return self._balance

class SavingsAccount(BankAccount):
    def __init__(self, holder, balance, interest_rate):
        super().__init__(holder, balance)
        self.interest_rate = interest_rate

    def deposit(self, amount):
        super().deposit(amount)
        bonus = amount * self.interest_rate
        self._balance = self._balance + bonus
        print(f"Interest bonus: ${bonus:.2f}")

    def withdraw(self, amount):
        fee = 0.5
        total = amount + fee
        if total <= self._balance:
            super().withdraw(amount)
            self._balance = self._balance - fee
            print(f"Withdrawal fee: ${fee:.2f}")
        else:
            print("Insufficient funds (including fee)!")

account = BankAccount("Alice", 1000)
account.deposit(500)
print(f"Balance: ${account.get_balance()}\n")

savings = SavingsAccount("Bob", 1000, 0.05)
savings.deposit(500)
print(f"Balance: ${savings.get_balance():.2f}\n")

savings.withdraw(100)
print(f"Balance: ${savings.get_balance():.2f}")
```

### Practice Problems

**Problem 1 — Beginner:** Create a `Transport` parent class with `travel()` method. Create `Car` and `Bicycle` child classes that call `super().travel()` but add their own behavior.

**Problem 2 — Intermediate:** Create a `Shape` parent with `__init__` and `area()`. Create `Triangle`, `Square`, and `Circle` children that call `super().__init__()` and override `area()`.

**Problem 3 — Challenge:** Create a 3-level hierarchy: `Vehicle` → `Car` → `ElectricCar` with super() calls at each level to initialize and extend functionality.

<details>
<summary>💡 Hints</summary>

**Hint 1:** Always call `super().__init__()` early in the child constructor to initialize parent attributes.

**Hint 2:** You can call `super().method()` multiple times in a single method.

**Hint 3:** For Problem 3, each class should add one additional attribute and use super() to pass responsibility up the chain.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Transport:
    def travel(self):
        print("Traveling...")

class Car(Transport):
    def travel(self):
        super().travel()
        print("by car on the road")

class Bicycle(Transport):
    def travel(self):
        super().travel()
        print("by bicycle using pedals")

car = Car()
car.travel()

bicycle = Bicycle()
bicycle.travel()

# Problem 2
import math

class Shape:
    def __init__(self, color):
        self.color = color

    def area(self):
        return 0

class Triangle(Shape):
    def __init__(self, color, base, height):
        super().__init__(color)
        self.base = base
        self.height = height

    def area(self):
        return (self.base * self.height) / 2

class Square(Shape):
    def __init__(self, color, side):
        super().__init__(color)
        self.side = side

    def area(self):
        return self.side ** 2

class Circle(Shape):
    def __init__(self, color, radius):
        super().__init__(color)
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

triangle = Triangle("red", 4, 3)
print(f"Triangle area: {triangle.area()}")

square = Square("blue", 5)
print(f"Square area: {square.area()}")

circle = Circle("green", 3)
print(f"Circle area: {circle.area():.2f}")

# Problem 3
class Vehicle:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def describe(self):
        print(f"{self.brand} {self.model}")

class Car(Vehicle):
    def __init__(self, brand, model, num_doors):
        super().__init__(brand, model)
        self.num_doors = num_doors

    def describe(self):
        super().describe()
        print(f"Doors: {self.num_doors}")

class ElectricCar(Car):
    def __init__(self, brand, model, num_doors, battery_capacity):
        super().__init__(brand, model, num_doors)
        self.battery_capacity = battery_capacity

    def describe(self):
        super().describe()
        print(f"Battery: {self.battery_capacity} kWh")

electric = ElectricCar("Tesla", "Model 3", 4, 75)
electric.describe()
# Tesla Model 3
# Doors: 4
# Battery: 75 kWh
```

</details>
