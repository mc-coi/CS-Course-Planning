# Day 24: Practice Day — OOP Challenges
**Learning Target:** I can solve complex OOP problems and create well-designed systems.

### Challenge 1: E-Commerce System

**Requirements:**
- Products with categories
- Shopping cart with tax calculation
- Multiple payment methods (credit card, PayPal, Bitcoin)
- Order tracking
- Inventory management

**Key Classes:**
```python
from abc import ABC, abstractmethod
from datetime import datetime

class Product:
    def __init__(self, product_id, name, price, quantity):
        self.product_id = product_id
        self.name = name
        self.price = price
        self.quantity = quantity

    def __eq__(self, other):
        return self.product_id == other.product_id

    def __str__(self):
        return f"{self.name}: ${self.price:.2f}"

class CartItem:
    def __init__(self, product, quantity):
        self.product = product
        self.quantity = quantity

    def get_total(self):
        return self.product.price * self.quantity

class ShoppingCart:
    def __init__(self):
        self.items = []

    def add_item(self, product, quantity):
        for item in self.items:
            if item.product == product:
                item.quantity += quantity
                return
        self.items.append(CartItem(product, quantity))

    def get_subtotal(self):
        return sum(item.get_total() for item in self.items)

    def get_total(self, tax_rate=0.08):
        subtotal = self.get_subtotal()
        tax = subtotal * tax_rate
        return subtotal + tax

class PaymentMethod(ABC):
    @abstractmethod
    def process(self, amount):
        pass

class CreditCardPayment(PaymentMethod):
    def __init__(self, card_number):
        self.card_number = card_number

    def process(self, amount):
        print(f"Processing ${amount:.2f} on card {self.card_number[-4:]}")
        return True

class Order:
    def __init__(self, order_id, items, total):
        self.order_id = order_id
        self.items = items
        self.total = total
        self.status = "pending"
        self.created_at = datetime.now()

    def __str__(self):
        return f"Order {self.order_id}: ${self.total:.2f} ({self.status})"

# Usage
products = [
    Product("P001", "Laptop", 999.99, 5),
    Product("P002", "Mouse", 29.99, 50),
    Product("P003", "Keyboard", 79.99, 30)
]

cart = ShoppingCart()
cart.add_item(products[0], 1)
cart.add_item(products[1], 2)
cart.add_item(products[2], 1)

print(f"Subtotal: ${cart.get_subtotal():.2f}")
print(f"Total with tax: ${cart.get_total():.2f}")

payment = CreditCardPayment("1234567890123456")
payment.process(cart.get_total())

order = Order("ORD001", cart.items, cart.get_total())
print(order)
```

### Challenge 2: University Management System

**Requirements:**
- Students and instructors
- Courses with enrollments
- Grade management
- Department organization

**Design:**
```python
class Person:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def __str__(self):
        return f"{self.name} ({self.email})"

class Student(Person):
    def __init__(self, name, email, student_id):
        super().__init__(name, email)
        self.student_id = student_id
        self.courses = []
        self.grades = {}

    def enroll(self, course):
        if course not in self.courses:
            self.courses.append(course)
            course.add_student(self)

    def get_gpa(self):
        if not self.grades:
            return 0
        return sum(self.grades.values()) / len(self.grades)

class Instructor(Person):
    def __init__(self, name, email, employee_id):
        super().__init__(name, email)
        self.employee_id = employee_id
        self.courses = []

    def teach(self, course):
        if course not in self.courses:
            self.courses.append(course)

class Course:
    def __init__(self, course_id, name, instructor):
        self.course_id = course_id
        self.name = name
        self.instructor = instructor
        self.students = []
        self.capacity = 30

    def add_student(self, student):
        if len(self.students) < self.capacity:
            if student not in self.students:
                self.students.append(student)
                return True
        return False

    def __str__(self):
        return f"{self.name} (Taught by {self.instructor.name})"

# Usage
instructor = Instructor("Dr. Smith", "smith@university.edu", "I001")
course = Course("CS101", "Introduction to Python", instructor)
instructor.teach(course)

students = [
    Student("Alice", "alice@university.edu", "S001"),
    Student("Bob", "bob@university.edu", "S002")
]

for student in students:
    student.enroll(course)

print(f"Course: {course}")
print(f"Enrolled: {len(course.students)} students")
```

### Challenge 3: Game Character System

**Requirements:**
- Multiple character types with different abilities
- Equipment and inventory system
- Combat with damage calculation
- Leveling and experience
- Special abilities

**Key Features:**
```python
from abc import ABC, abstractmethod

class Ability:
    def __init__(self, name, damage, cost):
        self.name = name
        self.damage = damage
        self.cost = cost  # mana/stamina cost

class Character(ABC):
    def __init__(self, name, health, mana):
        self.name = name
        self.health = health
        self.max_health = health
        self.mana = mana
        self.max_mana = mana
        self.level = 1
        self.experience = 0
        self.abilities = []
        self.inventory = []

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
        self.max_health += 20
        self.health = self.max_health
        self.max_mana += 10
        self.mana = self.max_mana

class Warrior(Character):
    def __init__(self, name):
        super().__init__(name, 100, 20)
        self.strength = 10

    def attack(self, target):
        damage = self.strength * 2
        target.take_damage(damage)
        return damage

class Mage(Character):
    def __init__(self, name):
        super().__init__(name, 60, 100)
        self.intelligence = 12

    def attack(self, target):
        if self.mana >= 20:
            damage = self.intelligence * 3
            self.mana -= 20
            target.take_damage(damage)
            return damage
        return 0

# Simulate combat
warrior = Warrior("Conan")
mage = Mage("Merlin")

print(f"{warrior.name} (Health: {warrior.health})")
print(f"{mage.name} (Health: {mage.health})")
print()

damage = warrior.attack(mage)
print(f"{warrior.name} attacks for {damage} damage")
print(f"{mage.name} now has {mage.health} health\n")

damage = mage.attack(warrior)
print(f"{mage.name} casts spell for {damage} damage")
print(f"{warrior.name} now has {warrior.health} health")
```

### Challenge 4: Library Management

```python
class Book:
    def __init__(self, isbn, title, author):
        self.isbn = isbn
        self.title = title
        self.author = author
        self.available = True

    def __eq__(self, other):
        return self.isbn == other.isbn

class Member:
    def __init__(self, member_id, name):
        self.member_id = member_id
        self.name = name
        self.borrowed = []

class Loan:
    def __init__(self, book, member, due_days=14):
        self.book = book
        self.member = member
        self.borrowed_date = datetime.now()
        self.due_date = datetime.now() + timedelta(days=due_days)
        self.returned_date = None
        self.is_active = True

    def return_book(self):
        self.returned_date = datetime.now()
        self.is_active = False
        self.book.available = True

class Library:
    def __init__(self, name):
        self.name = name
        self.books = []
        self.members = []
        self.loans = []

    def add_book(self, book):
        self.books.append(book)

    def register_member(self, member):
        self.members.append(member)

    def borrow_book(self, book, member):
        if book.available:
            book.available = False
            loan = Loan(book, member)
            self.loans.append(loan)
            member.borrowed.append(loan)
            return True
        return False
```

### Practice Assignments

**Assignment 1:** Implement complete e-commerce system with multiple features.

**Assignment 2:** Design a school management system with students, teachers, courses, grades.

**Assignment 3:** Create a game with combat, inventory, leveling system.

**Assignment 4:** Build a library system with book management and borrowing.

Each assignment should include:
- Proper class design
- Encapsulation with private attributes
- Inheritance where appropriate
- Polymorphism where needed
- Special methods for comparison/display
- Error handling and validation
- Clear public interfaces
