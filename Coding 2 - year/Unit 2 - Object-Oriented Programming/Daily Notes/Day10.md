# Day 10: Inheritance — Parent & Child Classes
**Learning Target:** I can create parent and child classes and use inheritance to share code between related classes.

### Key Concepts

**Inheritance:** A mechanism where a child class inherits attributes and methods from a parent class, allowing code reuse and hierarchical organization.

**Parent Class (Base Class):** The class that is inherited from. It contains common attributes and methods shared by multiple child classes.

**Child Class (Derived Class):** A class that inherits from a parent class. It can use parent's methods and add its own.

**Class Hierarchy:** An organization of classes where more specific classes inherit from more general ones.

**Code Reuse:** Avoiding duplicate code by having related classes share a common parent.

### Code Examples

```python
# Parent class - general category
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def speak(self):
        print(f"{self.name} makes a sound")

    def info(self):
        print(f"{self.name} is {self.age} years old")

# Child class - specific type of animal
class Dog(Animal):
    def __init__(self, name, age, breed):
        super().__init__(name, age)  # Call parent constructor
        self.breed = breed

    def speak(self):  # Override parent method
        print(f"{self.name} barks: Woof!")

# Child class - another specific type
class Cat(Animal):
    def __init__(self, name, age, color):
        super().__init__(name, age)
        self.color = color

    def speak(self):
        print(f"{self.name} meows: Meow!")

# Using inheritance
dog = Dog("Buddy", 3, "Golden Retriever")
dog.info()  # Buddy is 3 years old
dog.speak()  # Buddy barks: Woof!

cat = Cat("Whiskers", 2, "orange")
cat.info()  # Whiskers is 2 years old
cat.speak()  # Whiskers meows: Meow!

# Vehicle hierarchy
class Vehicle:
    def __init__(self, brand, model, year):
        self.brand = brand
        self.model = model
        self.year = year

    def describe(self):
        print(f"{self.year} {self.brand} {self.model}")

class Car(Vehicle):
    def __init__(self, brand, model, year, num_doors):
        super().__init__(brand, model, year)
        self.num_doors = num_doors

    def describe(self):
        super().describe()  # Call parent method
        print(f"Doors: {self.num_doors}")

class Motorcycle(Vehicle):
    def __init__(self, brand, model, year, has_sidecar):
        super().__init__(brand, model, year)
        self.has_sidecar = has_sidecar

    def describe(self):
        super().describe()
        print(f"Has sidecar: {self.has_sidecar}")

car = Car("Toyota", "Camry", 2022, 4)
car.describe()
# 2022 Toyota Camry
# Doors: 4

bike = Motorcycle("Harley-Davidson", "Street 750", 2023, False)
bike.describe()
# 2023 Harley-Davidson Street 750
# Has sidecar: False

# Employee hierarchy
class Employee:
    def __init__(self, name, employee_id, salary):
        self.name = name
        self.employee_id = employee_id
        self._salary = salary

    def calculate_bonus(self):
        return self._salary * 0.05  # 5% base bonus

    def display_info(self):
        print(f"Name: {self.name}, ID: {self.employee_id}, Salary: ${self._salary}")

class Manager(Employee):
    def __init__(self, name, employee_id, salary, team_size):
        super().__init__(name, employee_id, salary)
        self.team_size = team_size

    def calculate_bonus(self):
        return self._salary * 0.10  # 10% bonus for managers

    def display_info(self):
        super().display_info()
        print(f"Team size: {self.team_size}")

class Developer(Employee):
    def __init__(self, name, employee_id, salary, language):
        super().__init__(name, employee_id, salary)
        self.language = language

    def calculate_bonus(self):
        return self._salary * 0.08  # 8% bonus for developers

    def display_info(self):
        super().display_info()
        print(f"Primary language: {self.language}")

emp = Employee("Alice", "E001", 50000)
emp.display_info()
print(f"Bonus: ${emp.calculate_bonus()}")
print()

mgr = Manager("Bob", "M001", 80000, 5)
mgr.display_info()
print(f"Bonus: ${mgr.calculate_bonus()}")
print()

dev = Developer("Charlie", "D001", 75000, "Python")
dev.display_info()
print(f"Bonus: ${dev.calculate_bonus()}")

# Shape hierarchy
class Shape:
    def __init__(self, color):
        self.color = color

    def area(self):
        return 0

    def describe(self):
        print(f"A {self.color} shape")

class Circle(Shape):
    def __init__(self, color, radius):
        super().__init__(color)
        self.radius = radius

    def area(self):
        import math
        return math.pi * self.radius ** 2

    def describe(self):
        super().describe()
        print(f"Circle with radius {self.radius}")

class Rectangle(Shape):
    def __init__(self, color, width, height):
        super().__init__(color)
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def describe(self):
        super().describe()
        print(f"Rectangle {self.width}x{self.height}")

circle = Circle("red", 5)
circle.describe()
print(f"Area: {circle.area():.2f}")
print()

rect = Rectangle("blue", 4, 6)
rect.describe()
print(f"Area: {rect.area()}")

# Checking inheritance with isinstance()
print(isinstance(circle, Circle))  # True
print(isinstance(circle, Shape))   # True
print(isinstance(rect, Circle))    # False

# Getting the parent class
print(Circle.__bases__)  # (<class '__main__.Shape'>,)
```

### Guided Practice

**Activity: Create a Student and Teacher Hierarchy**

Follow these steps:

1. Create a `Person` class with: `name`, `age`, `email`
2. Create a `Student` class that inherits from Person with: `student_id`, `gpa`
3. Create a `Teacher` class that inherits from Person with: `employee_id`, `subject`
4. Add methods to each class
5. Create 2 students and 1 teacher, call their methods

**Expected Output:**
```
Name: Alice, Age: 16, Email: alice@school.edu
Student ID: S001, GPA: 3.8
Studying for Biology test

Name: Bob, Age: 17, Email: bob@school.edu
Student ID: S002, GPA: 3.5
Studying for Math test

Name: Dr. Johnson, Age: 45, Email: johnson@school.edu
Employee ID: T001, Subject: History
Preparing lesson for History class
```

**Solution:**
```python
class Person:
    def __init__(self, name, age, email):
        self.name = name
        self.age = age
        self.email = email

    def display_info(self):
        print(f"Name: {self.name}, Age: {self.age}, Email: {self.email}")

class Student(Person):
    def __init__(self, name, age, email, student_id, gpa):
        super().__init__(name, age, email)
        self.student_id = student_id
        self.gpa = gpa

    def display_info(self):
        super().display_info()
        print(f"Student ID: {self.student_id}, GPA: {self.gpa}")

    def study(self, subject):
        print(f"Studying for {subject} test")

class Teacher(Person):
    def __init__(self, name, age, email, employee_id, subject):
        super().__init__(name, age, email)
        self.employee_id = employee_id
        self.subject = subject

    def display_info(self):
        super().display_info()
        print(f"Employee ID: {self.employee_id}, Subject: {self.subject}")

    def prepare_lesson(self):
        print(f"Preparing lesson for {self.subject} class")

student1 = Student("Alice", 16, "alice@school.edu", "S001", 3.8)
student1.display_info()
student1.study("Biology")
print()

student2 = Student("Bob", 17, "bob@school.edu", "S002", 3.5)
student2.display_info()
student2.study("Math")
print()

teacher = Teacher("Dr. Johnson", 45, "johnson@school.edu", "T001", "History")
teacher.display_info()
teacher.prepare_lesson()
```

### Practice Problems

**Problem 1 — Beginner:** Create a `Bird` parent class with a `fly()` method. Create `Parrot` and `Penguin` child classes that override `fly()` — Parrot prints "I can fly!", Penguin prints "I cannot fly".

**Problem 2 — Intermediate:** Create a `BankAccount` parent with `deposit()` and `withdraw()`. Create `SavingsAccount` (limited withdrawals) and `CheckingAccount` (unlimited) child classes that override `withdraw()` appropriately.

**Problem 3 — Challenge:** Create a `Weapon` parent class with `damage()` and `cost()` methods. Create `Sword`, `Bow`, and `Staff` child classes with different damage values and costs. Create a list of weapons and calculate total damage and cost.

<details>
<summary>💡 Hints</summary>

**Hint 1:** Use `super().__init__()` in child class constructors to call parent constructor.

**Hint 2:** Use `super().method_name()` to call parent methods from child methods.

**Hint 3:** For Problem 3, store weapons in a list and loop through them to calculate totals.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Bird:
    def fly(self):
        print("I can fly!")

class Parrot(Bird):
    pass  # Inherits fly() from Bird

class Penguin(Bird):
    def fly(self):
        print("I cannot fly")

parrot = Parrot()
parrot.fly()  # I can fly!

penguin = Penguin()
penguin.fly()  # I cannot fly

# Problem 2
class BankAccount:
    def __init__(self, balance):
        self._balance = balance

    def deposit(self, amount):
        if amount > 0:
            self._balance = self._balance + amount

    def withdraw(self, amount):
        if 0 < amount <= self._balance:
            self._balance = self._balance - amount

    def get_balance(self):
        return self._balance

class SavingsAccount(BankAccount):
    def __init__(self, balance):
        super().__init__(balance)
        self._withdrawals = 0

    def withdraw(self, amount):
        if self._withdrawals < 3:  # Limited to 3 withdrawals
            super().withdraw(amount)
            self._withdrawals = self._withdrawals + 1
        else:
            print("Withdrawal limit reached!")

class CheckingAccount(BankAccount):
    pass  # No limit, uses parent withdraw()

savings = SavingsAccount(1000)
savings.withdraw(100)
savings.withdraw(100)
savings.withdraw(100)
savings.withdraw(100)  # Withdrawal limit reached!

checking = CheckingAccount(1000)
checking.withdraw(200)  # Works fine

# Problem 3
class Weapon:
    def __init__(self, name, damage, cost):
        self.name = name
        self.damage = damage
        self.cost = cost

    def get_info(self):
        return f"{self.name}: Damage {self.damage}, Cost ${self.cost}"

class Sword(Weapon):
    def __init__(self):
        super().__init__("Sword", 50, 100)

class Bow(Weapon):
    def __init__(self):
        super().__init__("Bow", 30, 75)

class Staff(Weapon):
    def __init__(self):
        super().__init__("Staff", 40, 120)

weapons = [Sword(), Bow(), Staff()]
total_damage = 0
total_cost = 0

for weapon in weapons:
    print(weapon.get_info())
    total_damage = total_damage + weapon.damage
    total_cost = total_cost + weapon.cost

print(f"Total damage: {total_damage}")
print(f"Total cost: ${total_cost}")
```

</details>
