# Day 21: OOP Design — Planning Classes
**Learning Target:** I can plan well-designed class hierarchies using OOP principles.

### Key Concepts

**Design Principles:** SOLID principles guide good OOP design.
- **S**ingle Responsibility: Each class should have one reason to change
- **O**pen/Closed: Open for extension, closed for modification
- **L**iskov Substitution: Subclasses should be substitutable for parents
- **I**nterface Segregation: Many specific interfaces better than one general
- **D**ependency Inversion: Depend on abstractions, not concrete classes

**Class Hierarchy:** Organize classes using inheritance and composition.

**Cohesion:** Methods and data should be closely related.

**Coupling:** Minimize dependencies between classes.

### Design Process

**1. Identify Requirements**
- What problem are we solving?
- What are the key entities?
- What behaviors do they need?

**2. Identify Classes**
- Nouns in requirements become classes
- Verbs in requirements become methods
- Adjectives describe attributes

**3. Define Relationships**
- Is-A relationships (inheritance)
- Has-A relationships (composition)
- Uses relationships (dependencies)

**4. Design Methods**
- What operations should each class support?
- What are the inputs and outputs?
- What validation is needed?

**5. Plan Attributes**
- What data does each class need?
- Should attributes be public or private?
- Are there constraints on values?

### Case Study Examples

**Example 1: School Management System**

**Requirements:**
- Manage students, teachers, and courses
- Track grades and attendance
- Generate reports

**Class Design:**
```python
class Person:
    def __init__(self, name, email):
        self.name = name
        self.email = email

class Student(Person):
    def __init__(self, name, email, student_id):
        super().__init__(name, email)
        self.student_id = student_id
        self.grades = {}
        self.attendance = {}

class Teacher(Person):
    def __init__(self, name, email, employee_id, subject):
        super().__init__(name, email)
        self.employee_id = employee_id
        self.subject = subject
        self.classes = []

class Course:
    def __init__(self, course_id, name, teacher):
        self.course_id = course_id
        self.name = name
        self.teacher = teacher
        self.students = []

class Grade:
    def __init__(self, student, course, score):
        self.student = student
        self.course = course
        self.score = score
```

**Example 2: Library Management System**

**Requirements:**
- Manage books, members, and loans
- Track borrowing and returns
- Handle overdue books

**Class Design:**
```python
class Book:
    def __init__(self, isbn, title, author, quantity):
        self.isbn = isbn
        self.title = title
        self.author = author
        self.quantity = quantity

class Member:
    def __init__(self, member_id, name, email):
        self.member_id = member_id
        self.name = name
        self.email = email
        self.borrowed_books = []

class Loan:
    def __init__(self, book, member, borrow_date, due_date):
        self.book = book
        self.member = member
        self.borrow_date = borrow_date
        self.due_date = due_date
        self.return_date = None

class Library:
    def __init__(self, name):
        self.name = name
        self.books = {}
        self.members = {}
        self.loans = []
```

**Example 3: E-Commerce System**

**Requirements:**
- Manage products, shopping carts, and orders
- Support different payment methods
- Track inventory

**Class Design:**
```python
class Product:
    def __init__(self, product_id, name, price, quantity):
        self.product_id = product_id
        self.name = name
        self.price = price
        self.quantity = quantity

class CartItem:
    def __init__(self, product, quantity):
        self.product = product
        self.quantity = quantity

class ShoppingCart:
    def __init__(self):
        self.items = []

    def add_item(self, product, quantity):
        self.items.append(CartItem(product, quantity))

    def get_total(self):
        return sum(item.product.price * item.quantity for item in self.items)

class Order:
    def __init__(self, order_id, customer, items, total):
        self.order_id = order_id
        self.customer = customer
        self.items = items
        self.total = total
        self.status = "pending"

class Customer:
    def __init__(self, customer_id, name, email):
        self.customer_id = customer_id
        self.name = name
        self.email = email
        self.orders = []
```

### Design Guidelines

**Use Composition Over Inheritance:**
```python
# Bad: Too many inheritance levels
class Vehicle:
    pass

class Car(Vehicle):
    pass

class ElectricCar(Car):
    pass

class TeslaModelS(ElectricCar):
    pass

# Better: Composition
class Engine:
    pass

class ElectricEngine(Engine):
    pass

class Car:
    def __init__(self, engine):
        self.engine = engine
```

**Single Responsibility:**
```python
# Bad: User class does too much
class User:
    def __init__(self, name):
        self.name = name

    def save_to_database(self):
        # Shouldn't be here
        pass

    def send_email(self):
        # Shouldn't be here
        pass

# Better: Separate concerns
class User:
    def __init__(self, name):
        self.name = name

class UserRepository:
    def save(self, user):
        # Database logic
        pass

class EmailService:
    def send_email(self, user):
        # Email logic
        pass
```

**Depend on Abstractions:**
```python
# Bad: Depends on concrete class
class PaymentProcessor:
    def __init__(self):
        self.payment_method = CreditCardProcessor()  # Concrete!

# Better: Depends on abstraction
class PaymentProcessor:
    def __init__(self, payment_method):
        self.payment_method = payment_method  # Any PaymentMethod works
```

### Practical Exercise: Design a Game System

**Requirements:**
1. Multiple character types (Warrior, Mage, Rogue)
2. Combat system
3. Inventory system
4. Experience and leveling
5. Save/load functionality

**Solution Design:**
```python
from abc import ABC, abstractmethod

# Abstract base class
class Character(ABC):
    def __init__(self, name, health, level=1):
        self.name = name
        self.health = health
        self.level = level
        self.experience = 0
        self.inventory = Inventory()

    @abstractmethod
    def attack(self, target):
        pass

    def take_damage(self, damage):
        self.health = max(0, self.health - damage)

    def gain_experience(self, amount):
        self.experience += amount
        if self.experience >= 100:
            self.level_up()

    def level_up(self):
        self.level += 1
        self.experience = 0
        self.health += 20

# Concrete implementations
class Warrior(Character):
    def __init__(self, name):
        super().__init__(name, 100)
        self.strength = 10

    def attack(self, target):
        damage = self.strength * 2
        target.take_damage(damage)
        return damage

class Mage(Character):
    def __init__(self, name):
        super().__init__(name, 60)
        self.intelligence = 12
        self.mana = 100

    def attack(self, target):
        if self.mana >= 20:
            damage = self.intelligence * 3
            self.mana -= 20
            target.take_damage(damage)
            return damage
        return 0

# Supporting classes
class Item:
    def __init__(self, name, item_type, value):
        self.name = name
        self.item_type = item_type
        self.value = value

class Inventory:
    def __init__(self):
        self.items = []

    def add_item(self, item):
        self.items.append(item)

    def get_total_value(self):
        return sum(item.value for item in self.items)

class Game:
    def __init__(self):
        self.characters = []
        self.current_level = 1

    def add_character(self, character):
        self.characters.append(character)

    def simulate_combat(self, char1, char2):
        while char1.health > 0 and char2.health > 0:
            damage = char1.attack(char2)
            if char2.health <= 0:
                char1.gain_experience(50)
                return char1
            # char2 attacks back...

# Usage
game = Game()
warrior = Warrior("Conan")
mage = Mage("Merlin")

game.add_character(warrior)
game.add_character(mage)

# Play...
```

### Design Checklist

When designing a class:
- [ ] Single Responsibility: Does it have one reason to change?
- [ ] Clear Interface: Are methods well-named and purposeful?
- [ ] Proper Encapsulation: Are private details hidden?
- [ ] Cohesion: Are related data and methods grouped?
- [ ] Coupling: Are dependencies minimal?
- [ ] Extensibility: Can new types be added without modifying existing code?
- [ ] Documentation: Are methods and classes well-documented?

### Summary

Good OOP design:
1. Identifies clear responsibilities for each class
2. Uses inheritance for is-A relationships
3. Uses composition for has-A relationships
4. Depends on abstractions, not concrete classes
5. Minimizes coupling between classes
6. Maximizes cohesion within classes
7. Follows the principle of least surprise
8. Makes code easy to test, maintain, and extend
