# Day 4: Class Variables vs Instance Variables
**Learning Target:** I can distinguish between class variables (shared across all objects) and instance variables (unique to each object).

### Key Concepts

**Instance Variable:** A variable that belongs to a specific object. Each object has its own independent copy of instance variables. Created using `self.variable_name` inside `__init__` or methods.

**Class Variable:** A variable that belongs to the class itself and is shared by all objects of that class. Defined directly in the class body (outside methods). All instances share the same value unless it's reassigned at the instance level.

**Shared State:** Data that all objects of a class access and potentially modify together (class variables).

**Unique State:** Data that each object maintains independently (instance variables).

### Code Examples

```python
# Simple example: Class vs Instance variables
class Counter:
    count = 0  # Class variable - shared by all instances

    def __init__(self, name):
        self.name = name  # Instance variable - unique to each object
        Counter.count = Counter.count + 1

counter1 = Counter("First")
counter2 = Counter("Second")
counter3 = Counter("Third")

print(Counter.count)  # 3 (all objects share this)
print(counter1.name)  # First (unique to counter1)
print(counter2.name)  # Second (unique to counter2)

# Student class with both types
class Student:
    school = "Central High"  # Class variable - all students go to same school
    student_count = 0

    def __init__(self, name, grade):
        self.name = name  # Instance variable
        self.grade = grade  # Instance variable
        Student.student_count = Student.student_count + 1

    def display_info(self):
        print(f"{self.name} in grade {self.grade} at {Student.school}")

alice = Student("Alice", 10)
bob = Student("Bob", 11)
charlie = Student("Charlie", 10)

alice.display_info()  # Alice in grade 10 at Central High
bob.display_info()    # Bob in grade 11 at Central High
charlie.display_info()  # Charlie in grade 10 at Central High

print(f"Total students: {Student.student_count}")  # Total students: 3
print(f"School: {Student.school}")  # School: Central High

# Bank Account example
class BankAccount:
    interest_rate = 0.02  # Class variable - all accounts share the same rate
    total_accounts = 0

    def __init__(self, holder, balance):
        self.holder = holder  # Instance variable
        self.balance = balance  # Instance variable
        BankAccount.total_accounts = BankAccount.total_accounts + 1

    def apply_interest(self):
        interest = self.balance * BankAccount.interest_rate
        self.balance = self.balance + interest
        print(f"Interest of ${interest:.2f} applied")

    def display(self):
        print(f"{self.holder}: ${self.balance:.2f}")

account1 = BankAccount("Alice", 1000)
account2 = BankAccount("Bob", 500)

print(f"Interest rate: {BankAccount.interest_rate}")  # 0.02
print(f"Total accounts: {BankAccount.total_accounts}")  # 2

account1.apply_interest()
account2.apply_interest()

account1.display()  # Alice: $1020.00
account2.display()  # Bob: $510.00

# Accessing class variable through instance
print(account1.interest_rate)  # 0.02 (can access through instance)
print(BankAccount.interest_rate)  # 0.02 (access through class)

# Car example showing the difference
class Car:
    wheels = 4  # Class variable - all cars have 4 wheels

    def __init__(self, brand, color):
        self.brand = brand  # Instance variable
        self.color = color  # Instance variable
        self.mileage = 0  # Instance variable

car1 = Car("Toyota", "red")
car2 = Car("Honda", "blue")

# Instance variables are different
print(car1.brand)  # Toyota
print(car2.brand)  # Honda

# Class variable is shared
print(car1.wheels)  # 4
print(car2.wheels)  # 4
print(Car.wheels)  # 4

# Important: Be careful when modifying class variables
class Product:
    tax_rate = 0.08  # Class variable
    total_products = 0

    def __init__(self, name, price):
        self.name = name  # Instance variable
        self.price = price  # Instance variable
        Product.total_products = Product.total_products + 1

    def get_total_price(self):
        return self.price * (1 + Product.tax_rate)

product1 = Product("Laptop", 1000)
product2 = Product("Phone", 500)

print(product1.get_total_price())  # 1080.0
print(f"Total products: {Product.total_products}")  # 2

# Changing class variable affects all instances
Product.tax_rate = 0.10
print(product1.get_total_price())  # 1100.0 (affected by change)
print(product2.get_total_price())  # 550.0 (affected by change)

# Game character example
class Character:
    max_level = 100  # Class variable - game setting
    character_count = 0

    def __init__(self, name, level=1):
        self.name = name  # Instance variable
        self.level = level  # Instance variable
        self.experience = 0  # Instance variable
        Character.character_count = Character.character_count + 1

    def gain_experience(self, amount):
        self.experience = self.experience + amount
        if self.experience >= 100:
            if self.level < Character.max_level:
                self.level = self.level + 1
                self.experience = 0

    def display(self):
        print(f"{self.name}: Level {self.level}, XP {self.experience}")

hero1 = Character("Aragorn", 50)
hero2 = Character("Legolas", 50)
hero3 = Character("Gimli", 50)

hero1.gain_experience(100)
hero1.display()  # Aragorn: Level 51, XP 0

print(f"Total characters: {Character.character_count}")  # 3
print(f"Max level: {Character.max_level}")  # 100
```

### Guided Practice

**Activity: Create a School Class with Both Variables**

Follow these steps:

1. Create a `School` class with a class variable `name` and a class variable `student_count`
2. Create an `__init__` method that takes student `name` and `grade`
3. Store `name` and `grade` as instance variables
4. In `__init__`, increment the class variable `student_count`
5. Add a method `enroll()` that prints student info including the school name
6. Create 5 student objects and call `enroll()` on each
7. Print the total student count

**Expected Output:**
```
Enrolling Alice (Grade 10) at Lincoln High
Enrolling Bob (Grade 11) at Lincoln High
Total students at Lincoln High: 5
```

**Solution:**
```python
class School:
    name = "Lincoln High"
    student_count = 0

    def __init__(self, student_name, grade):
        self.student_name = student_name
        self.grade = grade
        School.student_count = School.student_count + 1

    def enroll(self):
        print(f"Enrolling {self.student_name} (Grade {self.grade}) at {School.name}")

s1 = School("Alice", 10)
s2 = School("Bob", 11)
s3 = School("Charlie", 10)
s4 = School("Diana", 12)
s5 = School("Eve", 9)

s1.enroll()
s2.enroll()
s3.enroll()
s4.enroll()
s5.enroll()

print(f"Total students at {School.name}: {School.student_count}")
```

### Practice Problems

**Problem 1 — Beginner:** Create a `Dog` class with a class variable `species = "Canis lupus"` and instance variables `name` and `age`. Create 3 dog objects and print each dog's name and the species (which should be the same for all).

**Problem 2 — Intermediate:** Create a `Library` class with a class variable `total_books = 0` that tracks total books added to the system. Each book is an instance with a `title` and `author`. When you create a new book, increment the class variable. Create 5 books and print the total.

**Problem 3 — Challenge:** Create a `GameAccount` class with a class variable `server = "North America"` and instance variables `username`, `level`, and `gold`. Add a method that increases gold. Create multiple accounts, check that they share the same server but have different stats, then simulate a "server change" by modifying the class variable.

<details>
<summary>💡 Hints</summary>

**Hint 1:** Class variables are defined directly in the class body, before the `__init__` method. Instance variables are defined inside `__init__` using `self.`.

**Hint 2:** To access a class variable from inside a method, use `ClassName.variable_name` or `self.__class__.variable_name`.

**Hint 3:** For Problem 3, when you change the class variable, all instances will see the change. Try printing the server for each account before and after changing it.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Dog:
    species = "Canis lupus"

    def __init__(self, name, age):
        self.name = name
        self.age = age

dog1 = Dog("Buddy", 5)
dog2 = Dog("Max", 3)
dog3 = Dog("Bella", 7)

print(f"{dog1.name} is a {Dog.species}")
print(f"{dog2.name} is a {Dog.species}")
print(f"{dog3.name} is a {Dog.species}")

# Problem 2
class Book:
    total_books = 0

    def __init__(self, title, author):
        self.title = title
        self.author = author
        Book.total_books = Book.total_books + 1

book1 = Book("To Kill a Mockingbird", "Harper Lee")
book2 = Book("1984", "George Orwell")
book3 = Book("Pride and Prejudice", "Jane Austen")
book4 = Book("The Great Gatsby", "F. Scott Fitzgerald")
book5 = Book("Brave New World", "Aldous Huxley")

print(f"Total books: {Book.total_books}")

# Problem 3
class GameAccount:
    server = "North America"

    def __init__(self, username, level=1, gold=0):
        self.username = username
        self.level = level
        self.gold = gold

    def add_gold(self, amount):
        self.gold = self.gold + amount

    def display(self):
        print(f"{self.username} - Level {self.level}, Gold: {self.gold}, Server: {GameAccount.server}")

account1 = GameAccount("Player1", 10, 500)
account2 = GameAccount("Player2", 5, 200)
account3 = GameAccount("Player3", 15, 1000)

account1.display()
account2.display()
account3.display()

print("\nServer changed to South America")
GameAccount.server = "South America"

account1.display()
account2.display()
account3.display()
```

</details>
