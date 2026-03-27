# Unit 2: Object-Oriented Programming

> Master the principles of object-oriented design: classes, objects, inheritance, and polymorphism. Write scalable, maintainable code.

## Unit Overview

- **Duration:** 30 days / 6 weeks
- **Key Concepts:** Classes and objects, encapsulation, inheritance, polymorphism, special methods, abstract classes, design patterns
- **Big Idea:** Objects combine data and behavior — a powerful way to model real-world entities and build complex programs
- **TN Standard:** 9-12.CCI.1 — Use an object-oriented programming language with classes and objects

## Learning Targets

By the end of this unit, you will be able to:

- I can define classes with attributes and methods using `__init__` and `self`
- I can distinguish between instance variables and class variables
- I can implement encapsulation using private attributes and `@property`
- I can create inheritance hierarchies and use `super()`
- I can override methods and demonstrate polymorphism
- I can implement dunder/special methods (`__str__`, `__add__`, `__iter__`, etc.)
- I can use abstract classes and interfaces with the `abc` module
- I can choose between composition and inheritance appropriately
- I can apply basic design patterns (singleton, factory)
- I can build a complete multi-class OOP application

---

# Day 1: Introduction to OOP — Classes and Objects

## Learning Target
I can define classes with attributes and methods using `__init__` and `self`

## Key Concepts

### What is Object-Oriented Programming?

**Object-Oriented Programming (OOP)** is a paradigm that models programs as collections of **objects** that interact with each other. Each object combines:
- **Data** (attributes/properties) — information the object holds
- **Behavior** (methods) — actions the object can perform

### Real-World Analogy

Think of a **Dog**:
- **Attributes:** name, age, breed, color
- **Methods:** bark(), eat(), sleep()

In OOP, we create a "blueprint" (class) and then create individual dogs (objects/instances) from that blueprint.

### Class vs Object

- **Class:** A template or blueprint (like a cookie cutter)
- **Object/Instance:** A specific realization of that blueprint (like a cookie made from the cutter)

## Basic Class Syntax

```python
class Dog:
    """A class representing a dog."""

    def __init__(self, name, age):
        """Constructor - initializes a new dog object."""
        self.name = name  # Instance variable
        self.age = age    # Instance variable

    def bark(self):
        """Instance method - describes what the dog does."""
        return f"{self.name} says: Woof!"

    def birthday(self):
        """Instance method - modifies the dog's state."""
        self.age += 1

# Creating instances (objects)
dog1 = Dog("Buddy", 3)
dog2 = Dog("Lucy", 5)

# Accessing attributes
print(dog1.name)  # Output: Buddy
print(dog2.age)   # Output: 5

# Calling methods
print(dog1.bark())  # Output: Buddy says: Woof!
dog2.birthday()
print(dog2.age)     # Output: 6
```

## Understanding `self`

**`self`** represents the **current instance** of the class. It allows each object to track its own data.

```python
class Person:
    def __init__(self, name):
        self.name = name  # "self" stores data unique to THIS person

p1 = Person("Alice")
p2 = Person("Bob")

print(p1.name)  # Alice - self refers to p1's data
print(p2.name)  # Bob - self refers to p2's data
```

Without `self`, Python wouldn't know whether you're talking about Alice or Bob!

## Understanding `__init__`

**`__init__`** (constructor) is a special method that:
1. Is called automatically when you create a new object
2. Initializes instance variables
3. Doesn't return anything (returns the new object automatically)

```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand  # Store what was passed in
        self.color = color

car = Car("Toyota", "red")  # __init__ is called automatically!
```

## Guided Practice

Create a `Rectangle` class:

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        """Returns the area of the rectangle."""
        return self.width * self.height

    def perimeter(self):
        """Returns the perimeter of the rectangle."""
        return 2 * (self.width + self.height)

# Create two rectangles
rect1 = Rectangle(5, 10)
rect2 = Rectangle(3, 7)

print(f"Rectangle 1 area: {rect1.area()}")        # 50
print(f"Rectangle 1 perimeter: {rect1.perimeter()}")  # 30
print(f"Rectangle 2 area: {rect2.area()}")        # 21
```

## Practice Problems

### Beginner: Book Class
Create a `Book` class with:
- `__init__`: takes `title`, `author`, `pages`
- Method: `describe()` returns formatted string with all info

```python
book = Book("1984", "George Orwell", 328)
print(book.describe())
# Expected: "1984" by George Orwell (328 pages)
```

<details>
<summary>Answer</summary>

```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages

    def describe(self):
        return f'"{self.title}" by {self.author} ({self.pages} pages)'

book = Book("1984", "George Orwell", 328)
print(book.describe())
```

</details>

### Intermediate: Point Class
Create a `Point` class that represents a 2D coordinate:
- `__init__`: takes `x`, `y`
- Method: `distance_from_origin()` returns distance from (0,0)
- Method: `move(dx, dy)` updates position

```python
p = Point(3, 4)
print(p.distance_from_origin())  # 5.0
p.move(1, 2)
print(p.distance_from_origin())  # ~5.39
```

<details>
<summary>Hint</summary>
Use the distance formula: √(x² + y²)
</details>

<details>
<summary>Answer</summary>

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def distance_from_origin(self):
        return (self.x**2 + self.y**2)**0.5

    def move(self, dx, dy):
        self.x += dx
        self.y += dy

p = Point(3, 4)
print(p.distance_from_origin())  # 5.0
p.move(1, 2)
print(f"{p.distance_from_origin():.2f}")  # 5.39
```

</details>

### Challenge: Account Class
Create an `Account` class (bank-like):
- `__init__`: takes `owner`, `balance` (default 0)
- Method: `deposit(amount)` adds money
- Method: `withdraw(amount)` removes money (if sufficient funds exist)
- Method: `get_balance()` returns current balance
- Method: `__str__()` returns `"[owner]'s account: $[balance]"`

```python
acc = Account("Alice", 1000)
acc.deposit(500)
acc.withdraw(200)
print(acc)  # Alice's account: $1300
```

<details>
<summary>Answer</summary>

```python
class Account:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance -= amount

    def get_balance(self):
        return self.balance

    def __str__(self):
        return f"{self.owner}'s account: ${self.balance}"

acc = Account("Alice", 1000)
acc.deposit(500)
acc.withdraw(200)
print(acc)  # Alice's account: $1300
```

</details>

---

# Day 2: Attributes, Methods, and the __init__ Method

## Learning Target
I can distinguish between instance variables and class variables

## Key Concepts

### Instance Variables vs Class Variables

**Instance Variables:**
- Unique to each object
- Defined in `__init__`
- Created using `self.attribute = value`
- Each object has its own copy

**Class Variables:**
- Shared by all instances
- Defined outside any method, directly in the class
- Created using `ClassName.attribute = value`
- All objects see the same value (unless overridden)

### Example

```python
class Student:
    school = "Lincoln High"  # CLASS VARIABLE - shared by all students
    total_students = 0       # CLASS VARIABLE - track count

    def __init__(self, name, gpa):
        self.name = name     # INSTANCE VARIABLE - unique to each student
        self.gpa = gpa       # INSTANCE VARIABLE - unique to each student
        Student.total_students += 1

# Create students
s1 = Student("Alice", 3.9)
s2 = Student("Bob", 3.5)

# Instance variables are different
print(s1.name)  # Alice
print(s2.name)  # Bob

# Class variables are the same
print(s1.school)  # Lincoln High
print(s2.school)  # Lincoln High (same for all)
print(Student.total_students)  # 2
```

### When to Use Each

| Use Instance Variables When | Use Class Variables When |
|----|-----|
| Data is unique to each object | Data is shared across all objects |
| Example: person's name, age | Example: total count, constant values |
| Modified per object | Same for all objects |

## Methods Overview

### Instance Methods
Called on an object, have access to `self`:

```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):  # Instance method
        return f"{self.name} barks!"

dog = Dog("Rex")
print(dog.bark())  # Calls instance method
```

### Constructor Method
The `__init__` method is called automatically:

```python
class Car:
    def __init__(self, brand, year):
        self.brand = brand
        self.year = year
        print(f"{self.brand} {self.year} created!")

car = Car("Toyota", 2020)  # Constructor called automatically
# Output: Toyota 2020 created!
```

## Guided Practice: Traffic Light Class

```python
class TrafficLight:
    """A traffic light with three colors."""
    colors = ["red", "yellow", "green"]  # Class variable

    def __init__(self, current_color):
        self.current_color = current_color  # Instance variable
        self.cycle_count = 0                # Instance variable

    def change(self):
        """Cycle to next color."""
        idx = self.colors.index(self.current_color)
        self.current_color = self.colors[(idx + 1) % 3]
        self.cycle_count += 1

    def status(self):
        """Return current state."""
        return f"Light is {self.current_color} (cycled {self.cycle_count} times)"

# Create lights at different intersections
light1 = TrafficLight("red")
light2 = TrafficLight("green")

print(light1.status())  # Light is red (cycled 0 times)
light1.change()
print(light1.status())  # Light is yellow (cycled 1 times)
print(light2.status())  # Light is green (cycled 0 times) - separate instance
```

## Practice Problems

### Beginner: Counter Class
Create a `Counter` class:
- `__init__`: starts with `count = 0`
- Method: `increment()` adds 1
- Method: `decrement()` subtracts 1
- Method: `get_count()` returns current value

```python
c = Counter()
c.increment()
c.increment()
c.decrement()
print(c.get_count())  # 1
```

<details>
<summary>Answer</summary>

```python
class Counter:
    def __init__(self):
        self.count = 0

    def increment(self):
        self.count += 1

    def decrement(self):
        self.count -= 1

    def get_count(self):
        return self.count

c = Counter()
c.increment()
c.increment()
c.decrement()
print(c.get_count())  # 1
```

</details>

### Intermediate: Player Class
Create a `Player` class for a game:
- `__init__`: takes `name`, starts with `level = 1`, `experience = 0`
- Class variable: `total_players` (count all created)
- Method: `gain_experience(amount)` adds exp
- Method: `level_up()` if exp >= 100, reset exp and increase level

```python
p1 = Player("Alice")
p1.gain_experience(60)
p1.gain_experience(50)  # Now at 110 exp
print(p1.level)  # 2
print(p1.experience)  # 10
```

<details>
<summary>Answer</summary>

```python
class Player:
    total_players = 0

    def __init__(self, name):
        self.name = name
        self.level = 1
        self.experience = 0
        Player.total_players += 1

    def gain_experience(self, amount):
        self.experience += amount
        if self.experience >= 100:
            self.level += 1
            self.experience -= 100

p1 = Player("Alice")
p1.gain_experience(60)
p1.gain_experience(50)
print(p1.level)       # 2
print(p1.experience)  # 10
print(Player.total_players)  # 1
```

</details>

### Challenge: Inventory Class
Create an `Inventory` class:
- `__init__`: takes `capacity` (max items)
- Instance variable: `items` (dictionary: item_name -> quantity)
- Class variable: `total_inventories` (count created)
- Method: `add_item(name, quantity)` adds items if space
- Method: `remove_item(name, quantity)` removes items
- Method: `get_item_count(name)` returns quantity of item

```python
inv = Inventory(10)
inv.add_item("sword", 1)
inv.add_item("potion", 5)
print(inv.get_item_count("potion"))  # 5
inv.remove_item("potion", 2)
print(inv.get_item_count("potion"))  # 3
```

<details>
<summary>Answer</summary>

```python
class Inventory:
    total_inventories = 0

    def __init__(self, capacity):
        self.capacity = capacity
        self.items = {}
        self.current_count = 0
        Inventory.total_inventories += 1

    def add_item(self, name, quantity):
        if self.current_count + quantity <= self.capacity:
            if name in self.items:
                self.items[name] += quantity
            else:
                self.items[name] = quantity
            self.current_count += quantity

    def remove_item(self, name, quantity):
        if name in self.items and self.items[name] >= quantity:
            self.items[name] -= quantity
            self.current_count -= quantity
            if self.items[name] == 0:
                del self.items[name]

    def get_item_count(self, name):
        return self.items.get(name, 0)

inv = Inventory(10)
inv.add_item("sword", 1)
inv.add_item("potion", 5)
print(inv.get_item_count("potion"))  # 5
inv.remove_item("potion", 2)
print(inv.get_item_count("potion"))  # 3
```

</details>

---

# Day 3: Working with Multiple Objects and Object Interactions

## Learning Target
I can understand how objects interact and communicate with each other

## Key Concepts

### Objects Talking to Objects

Objects often work together. One object can:
- Call methods on another object
- Access another object's attributes
- Store references to other objects

### Example: Game Characters

```python
class Character:
    def __init__(self, name, health):
        self.name = name
        self.health = health

    def take_damage(self, amount):
        self.health -= amount
        return f"{self.name} takes {amount} damage!"

    def is_alive(self):
        return self.health > 0

class Game:
    def __init__(self):
        self.characters = []

    def add_character(self, character):
        self.characters.append(character)

    def battle(self, char1, char2):
        """One character attacks another."""
        damage = 10
        result = char2.take_damage(damage)
        print(result)
        if not char2.is_alive():
            print(f"{char2.name} has been defeated!")
        return result

# Create game and characters
game = Game()
hero = Character("Hero", 100)
villain = Character("Villain", 50)

game.add_character(hero)
game.add_character(villain)

game.battle(hero, villain)  # Villain takes 10 damage
game.battle(hero, villain)  # Villain takes 10 damage
game.battle(hero, villain)  # Villain takes 10 damage
game.battle(hero, villain)  # Villain takes 10 damage
game.battle(hero, villain)  # Villain defeated
```

## Guided Practice: Team System

```python
class Player:
    def __init__(self, name, role):
        self.name = name
        self.role = role

    def __str__(self):
        return f"{self.name} ({self.role})"

class Team:
    def __init__(self, team_name):
        self.team_name = team_name
        self.players = []

    def add_player(self, player):
        self.players.append(player)

    def remove_player(self, name):
        self.players = [p for p in self.players if p.name != name]

    def list_players(self):
        print(f"\n{self.team_name}:")
        for player in self.players:
            print(f"  - {player}")

    def get_roles(self):
        return [p.role for p in self.players]

# Create teams and players
team1 = Team("Team A")
team1.add_player(Player("Alice", "Striker"))
team1.add_player(Player("Bob", "Goalkeeper"))
team1.add_player(Player("Charlie", "Defender"))

team1.list_players()  # Shows all players
print(team1.get_roles())  # ['Striker', 'Goalkeeper', 'Defender']
```

## Practice Problems

### Beginner: School System
Create `Teacher` and `Classroom` classes:
- `Teacher`: `__init__(name, subject)`
- `Classroom`: `__init__(name)`, `add_teacher(teacher)`, `get_teacher_info()`

```python
class_1 = Classroom("Room 101")
teacher = Teacher("Mrs. Smith", "Math")
class_1.add_teacher(teacher)
print(class_1.get_teacher_info())  # Mrs. Smith teaches Math
```

<details>
<summary>Answer</summary>

```python
class Teacher:
    def __init__(self, name, subject):
        self.name = name
        self.subject = subject

class Classroom:
    def __init__(self, name):
        self.name = name
        self.teacher = None

    def add_teacher(self, teacher):
        self.teacher = teacher

    def get_teacher_info(self):
        if self.teacher:
            return f"{self.teacher.name} teaches {self.teacher.subject}"
        return "No teacher assigned"

class_1 = Classroom("Room 101")
teacher = Teacher("Mrs. Smith", "Math")
class_1.add_teacher(teacher)
print(class_1.get_teacher_info())  # Mrs. Smith teaches Math
```

</details>

### Intermediate: Restaurant System
Create `MenuItem` and `Order` classes:
- `MenuItem`: `name`, `price`
- `Order`: list of items, methods: `add_item()`, `remove_item()`, `total_cost()`, `__str__()`

```python
order = Order()
item1 = MenuItem("Pizza", 10.99)
item2 = MenuItem("Soda", 2.99)
order.add_item(item1)
order.add_item(item2)
print(order.total_cost())  # 13.98
```

<details>
<summary>Answer</summary>

```python
class MenuItem:
    def __init__(self, name, price):
        self.name = name
        self.price = price

    def __str__(self):
        return f"{self.name}: ${self.price:.2f}"

class Order:
    def __init__(self):
        self.items = []

    def add_item(self, menu_item):
        self.items.append(menu_item)

    def remove_item(self, name):
        self.items = [i for i in self.items if i.name != name]

    def total_cost(self):
        return sum(item.price for item in self.items)

    def __str__(self):
        return "\n".join(str(item) for item in self.items)

order = Order()
item1 = MenuItem("Pizza", 10.99)
item2 = MenuItem("Soda", 2.99)
order.add_item(item1)
order.add_item(item2)
print(f"Total: ${order.total_cost():.2f}")  # Total: $13.98
```

</details>

### Challenge: Pet Shop
Create `Pet` and `PetShop` classes:
- `Pet`: `name`, `species`, `price`, `age`
- `PetShop`: `inventory` (list of pets), `add_pet()`, `sell_pet(name)`, `get_pets_by_species()`, `get_average_price()`

```python
shop = PetShop()
shop.add_pet(Pet("Fluffy", "Cat", 50, 2))
shop.add_pet(Pet("Rex", "Dog", 200, 1))
shop.add_pet(Pet("Whiskers", "Cat", 45, 3))
print(shop.get_average_price())  # 98.33
print(len(shop.get_pets_by_species("Cat")))  # 2
```

<details>
<summary>Answer</summary>

```python
class Pet:
    def __init__(self, name, species, price, age):
        self.name = name
        self.species = species
        self.price = price
        self.age = age

    def __str__(self):
        return f"{self.name} ({self.species})"

class PetShop:
    def __init__(self):
        self.inventory = []

    def add_pet(self, pet):
        self.inventory.append(pet)

    def sell_pet(self, name):
        self.inventory = [p for p in self.inventory if p.name != name]

    def get_pets_by_species(self, species):
        return [p for p in self.inventory if p.species == species]

    def get_average_price(self):
        if not self.inventory:
            return 0
        return sum(p.price for p in self.inventory) / len(self.inventory)

shop = PetShop()
shop.add_pet(Pet("Fluffy", "Cat", 50, 2))
shop.add_pet(Pet("Rex", "Dog", 200, 1))
shop.add_pet(Pet("Whiskers", "Cat", 45, 3))
print(f"{shop.get_average_price():.2f}")  # 98.33
print(len(shop.get_pets_by_species("Cat")))  # 2
```

</details>

---

# Day 4: Instance Variables vs Class Variables

## Learning Target
I can demonstrate proper use of instance and class variables in context

## Key Concepts

### Modifying Class Variables

```python
class Bank:
    interest_rate = 0.02  # Class variable - same for all accounts
    total_accounts = 0    # Class variable - tracks total

    def __init__(self, owner, balance):
        self.owner = owner       # Instance - unique per account
        self.balance = balance   # Instance - unique per account
        Bank.total_accounts += 1  # Modify class variable

    def apply_interest(self):
        self.balance *= (1 + Bank.interest_rate)

# All accounts share the same interest rate
acc1 = Account("Alice", 1000)
acc2 = Account("Bob", 2000)

print(Bank.total_accounts)  # 2
print(Bank.interest_rate)   # 0.02

acc1.apply_interest()
print(acc1.balance)  # 1020.0
```

### Beware: Unintended Instance Variables

```python
class Counter:
    count = 0  # Class variable

    def __init__(self):
        self.count = 0  # Creates INSTANCE variable!

c1 = Counter()
c2 = Counter()

c1.count = 5
print(c2.count)  # Still 0 (separate instance variable)
print(Counter.count)  # Still 0 (class variable unchanged)
```

## Guided Practice: Banking System

```python
class Bank:
    total_deposits = 0  # Class variable - track all money in bank

    def __init__(self, name, initial_balance):
        self.name = name              # Instance variable
        self.balance = initial_balance  # Instance variable
        Bank.total_deposits += initial_balance

    def deposit(self, amount):
        self.balance += amount
        Bank.total_deposits += amount

    def report(self):
        return f"{self.name}: ${self.balance} (Bank Total: ${Bank.total_deposits})"

acc1 = Bank("Alice", 1000)
acc2 = Bank("Bob", 2000)

print(acc1.report())  # Alice: $1000 (Bank Total: $3000)
acc1.deposit(500)
print(acc1.report())  # Alice: $1500 (Bank Total: $3500)
print(acc2.report())  # Bob: $2000 (Bank Total: $3500)
```

## Practice Problems

### Beginner: Company Employee Count
Create an `Employee` class:
- Instance: `name`, `salary`
- Class: `total_employees` (increments on creation)
- Method: `report()` shows name, salary, and total employee count

```python
e1 = Employee("Alice", 50000)
e2 = Employee("Bob", 55000)
print(e1.report())  # Alice earns $50000. Total employees: 2
```

<details>
<summary>Answer</summary>

```python
class Employee:
    total_employees = 0

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
        Employee.total_employees += 1

    def report(self):
        return f"{self.name} earns ${self.salary}. Total employees: {Employee.total_employees}"

e1 = Employee("Alice", 50000)
e2 = Employee("Bob", 55000)
print(e1.report())  # Alice earns $50000. Total employees: 2
```

</details>

### Intermediate: School Grade Tracking
Create a `School` class:
- Class variable: `average_gpa` (updated as students change)
- Instance (via students): individual GPAs
- Method: `add_student(gpa)`, `calculate_average_gpa()`

```python
school = School()
school.add_student(3.5)
school.add_student(3.8)
school.add_student(3.2)
print(f"Average GPA: {school.calculate_average_gpa():.2f}")  # 3.50
```

<details>
<summary>Answer</summary>

```python
class School:
    def __init__(self):
        self.students_gpas = []

    def add_student(self, gpa):
        self.students_gpas.append(gpa)

    def calculate_average_gpa(self):
        if not self.students_gpas:
            return 0
        return sum(self.students_gpas) / len(self.students_gpas)

school = School()
school.add_student(3.5)
school.add_student(3.8)
school.add_student(3.2)
print(f"Average GPA: {school.calculate_average_gpa():.2f}")  # 3.50
```

</details>

### Challenge: Game Economy
Create a `Game` class with a currency system:
- Class variable: `total_currency_in_game` (tracks economy)
- Instance (players): individual gold amounts
- Methods: `create_player(starting_gold)`, `transfer(from_player, to_player, amount)`, `get_economy_status()`

```python
game = Game()
p1 = game.create_player(100)
p2 = game.create_player(50)
game.transfer(p1, p2, 30)  # p1 loses 30, p2 gains 30
print(game.get_economy_status())  # Total: $150, distributed as [70, 80]
```

<details>
<summary>Answer</summary>

```python
class Player:
    def __init__(self, player_id, gold):
        self.player_id = player_id
        self.gold = gold

class Game:
    total_currency = 0

    def __init__(self):
        self.players = []
        self.player_count = 0

    def create_player(self, starting_gold):
        player = Player(len(self.players), starting_gold)
        self.players.append(player)
        Game.total_currency += starting_gold
        return player

    def transfer(self, from_player, to_player, amount):
        if from_player.gold >= amount:
            from_player.gold -= amount
            to_player.gold += amount

    def get_economy_status(self):
        golds = [p.gold for p in self.players]
        return f"Total: ${Game.total_currency}, distributed as {golds}"

game = Game()
p1 = game.create_player(100)
p2 = game.create_player(50)
game.transfer(p1, p2, 30)
print(game.get_economy_status())  # Total: $150, distributed as [70, 80]
```

</details>

---

# Day 5: Class Methods and Static Methods

## Learning Target
I can implement and use `@classmethod` and `@staticmethod` decorators appropriately

## Key Concepts

### `@classmethod` — Methods That Work with the Class

**`@classmethod`** receives the class itself (`cls`) instead of an instance (`self`):

```python
class Person:
    population = 0

    def __init__(self, name):
        self.name = name
        Person.population += 1

    @classmethod
    def get_population(cls):
        """Access class variable through cls."""
        return cls.population

    @classmethod
    def from_birth_year(cls, name, birth_year):
        """Alternative constructor."""
        age = 2026 - birth_year
        person = cls(name)  # Create instance
        person.age = age
        return person

p1 = Person("Alice")
p2 = Person("Bob")
print(Person.get_population())  # 2

p3 = Person.from_birth_year("Charlie", 1995)
print(p3.age)  # 31
```

### `@staticmethod` — Utility Methods

**`@staticmethod`** is just a regular function inside a class (no `self`, no `cls`):

```python
class Math:
    @staticmethod
    def add(a, b):
        return a + b

    @staticmethod
    def multiply(a, b):
        return a * b

# No need to create an instance
print(Math.add(5, 3))      # 8
print(Math.multiply(4, 7))  # 28
```

## When to Use Each

| Method Type | Receives | Use When |
|---|---|---|
| Instance method | `self` | Working with instance data |
| `@classmethod` | `cls` | Need to access/modify class data or create alternative constructors |
| `@staticmethod` | nothing | Pure utility that doesn't need instance or class data |

## Guided Practice: Temperature Converter

```python
class Temperature:
    def __init__(self, celsius):
        self.celsius = celsius

    @classmethod
    def from_fahrenheit(cls, fahrenheit):
        """Create instance from Fahrenheit."""
        celsius = (fahrenheit - 32) * 5/9
        return cls(celsius)

    @classmethod
    def from_kelvin(cls, kelvin):
        """Create instance from Kelvin."""
        celsius = kelvin - 273.15
        return cls(celsius)

    @staticmethod
    def celsius_to_fahrenheit(celsius):
        """Static utility - no instance needed."""
        return (celsius * 9/5) + 32

    def to_fahrenheit(self):
        """Instance method - uses self."""
        return Temperature.celsius_to_fahrenheit(self.celsius)

# Create from different units
t1 = Temperature(0)
t2 = Temperature.from_fahrenheit(32)
t3 = Temperature.from_kelvin(273.15)

print(t1.to_fahrenheit())  # 32.0
print(Temperature.celsius_to_fahrenheit(10))  # 50.0
```

## Practice Problems

### Beginner: Currency Converter
Create a `Currency` class:
- Instance: `amount`
- `@staticmethod`: `convert(amount, rate)` (utility)
- `@classmethod`: `from_dollars(cls, dollars)` with rate 1.2

```python
c = Currency.from_dollars(100)  # 100 * 1.2 = 120
print(c.amount)  # 120
print(Currency.convert(100, 0.85))  # 85
```

<details>
<summary>Answer</summary>

```python
class Currency:
    def __init__(self, amount):
        self.amount = amount

    @staticmethod
    def convert(amount, rate):
        return amount * rate

    @classmethod
    def from_dollars(cls, dollars):
        converted = cls.convert(dollars, 1.2)
        return cls(converted)

c = Currency.from_dollars(100)
print(c.amount)  # 120
print(Currency.convert(100, 0.85))  # 85.0
```

</details>

### Intermediate: Logger Class
Create a `Logger` class:
- Class variable: `logs` (list)
- `@classmethod`: `log(message)` adds to logs
- `@classmethod`: `get_logs()` returns all logs
- `@staticmethod`: `format_message(level, msg)` returns "[LEVEL] msg"

```python
Logger.log(Logger.format_message("INFO", "App started"))
Logger.log(Logger.format_message("ERROR", "File not found"))
print(Logger.get_logs())  # ['[INFO] App started', '[ERROR] File not found']
```

<details>
<summary>Answer</summary>

```python
class Logger:
    logs = []

    @staticmethod
    def format_message(level, msg):
        return f"[{level}] {msg}"

    @classmethod
    def log(cls, message):
        cls.logs.append(message)

    @classmethod
    def get_logs(cls):
        return cls.logs

Logger.log(Logger.format_message("INFO", "App started"))
Logger.log(Logger.format_message("ERROR", "File not found"))
print(Logger.get_logs())  # ['[INFO] App started', '[ERROR] File not found']
```

</details>

### Challenge: Factory Pattern with Alternative Constructors
Create a `Rectangle` class:
- Instance: `width`, `height`
- `@classmethod`: `square(cls, side)` creates square
- `@classmethod`: `from_area(cls, area, width)` calculates height
- `@staticmethod`: `is_valid_dimensions(w, h)` checks if positive

```python
rect = Rectangle.square(5)
print(rect.width, rect.height)  # 5 5

rect2 = Rectangle.from_area(20, 4)
print(rect2.height)  # 5

print(Rectangle.is_valid_dimensions(5, -3))  # False
```

<details>
<summary>Answer</summary>

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    @classmethod
    def square(cls, side):
        return cls(side, side)

    @classmethod
    def from_area(cls, area, width):
        height = area / width
        return cls(width, height)

    @staticmethod
    def is_valid_dimensions(w, h):
        return w > 0 and h > 0

rect = Rectangle.square(5)
print(rect.width, rect.height)  # 5 5

rect2 = Rectangle.from_area(20, 4)
print(rect2.height)  # 5.0

print(Rectangle.is_valid_dimensions(5, -3))  # False
```

</details>

---

# Day 6: Encapsulation — Private Attributes and Naming Conventions

## Learning Target
I can implement encapsulation using private attributes and naming conventions

## Key Concepts

### Access Modifiers by Convention

Python doesn't enforce privacy, but uses naming conventions:

```python
class BankAccount:
    def __init__(self, balance):
        self.public_data = "anyone can see"      # Public
        self._protected = balance                # Protected (discourage external access)
        self.__private = balance                 # Name-mangled (strong privacy signal)

account = BankAccount(1000)
print(account.public_data)      # OK
print(account._protected)       # Works, but discouraged
# print(account.__private)      # AttributeError - name-mangled!
```

### How Name Mangling Works

Python automatically renames `__private` to `_ClassName__private`:

```python
class Secret:
    def __init__(self):
        self.__secret = "hidden"

obj = Secret()
print(obj._Secret__secret)  # Works but DON'T DO THIS!
```

### Why Use Private Attributes?

1. **Encapsulation:** Hide internal details
2. **Control:** Force access through methods (can add validation)
3. **Flexibility:** Change internals without breaking external code

```python
class Person:
    def __init__(self, age):
        self.__age = age  # Private

    def get_age(self):
        """Public interface to access age."""
        return self.__age

    def set_age(self, age):
        """Public interface to set age (with validation)."""
        if age >= 0:
            self.__age = age
        else:
            print("Age must be positive!")

p = Person(25)
print(p.get_age())  # 25
p.set_age(30)
print(p.get_age())  # 30
p.set_age(-5)  # Rejected with message
```

## Guided Practice: Secure Bank Account

```python
class BankAccount:
    def __init__(self, owner, initial_balance):
        self.owner = owner              # Public
        self._transaction_history = []  # Protected - internal tracking
        self.__balance = initial_balance  # Private - hide from outside

    def deposit(self, amount):
        """Public method - safe way to modify balance."""
        if amount > 0:
            self.__balance += amount
            self._transaction_history.append(f"Deposit: +{amount}")
            return True
        return False

    def withdraw(self, amount):
        """Public method - with safety checks."""
        if 0 < amount <= self.__balance:
            self.__balance -= amount
            self._transaction_history.append(f"Withdraw: -{amount}")
            return True
        return False

    def get_balance(self):
        """Public method - read-only access to balance."""
        return self.__balance

    def get_history(self):
        """Protected method - shows transaction history."""
        return self._transaction_history

account = BankAccount("Alice", 1000)
account.deposit(500)
account.withdraw(200)
print(account.get_balance())   # 1300
print(account.get_history())   # ['Deposit: +500', 'Withdraw: -200']
# account.__balance = 0  # Blocked by name mangling
```

## Practice Problems

### Beginner: Grading System
Create a `Grade` class:
- Private: `__score` (0-100)
- Public methods: `set_score(score)` with validation, `get_score()`, `get_letter_grade()`

```python
grade = Grade()
grade.set_score(85)
print(grade.get_letter_grade())  # B
grade.set_score(101)  # Invalid
print(grade.get_score())  # Still 85
```

<details>
<summary>Answer</summary>

```python
class Grade:
    def __init__(self):
        self.__score = 0

    def set_score(self, score):
        if 0 <= score <= 100:
            self.__score = score

    def get_score(self):
        return self.__score

    def get_letter_grade(self):
        if self.__score >= 90:
            return 'A'
        elif self.__score >= 80:
            return 'B'
        elif self.__score >= 70:
            return 'C'
        return 'F'

grade = Grade()
grade.set_score(85)
print(grade.get_letter_grade())  # B
```

</details>

### Intermediate: Password-Protected Account
Create an `Account` class:
- Private: `__password`, `__balance`
- Public: `verify_password(pwd)`, `check_balance(pwd)`, `deposit(pwd, amount)`

```python
acc = Account("secret123", 1000)
print(acc.check_balance("wrong"))  # None (wrong password)
print(acc.check_balance("secret123"))  # 1000 (correct)
```

<details>
<summary>Answer</summary>

```python
class Account:
    def __init__(self, password, balance):
        self.__password = password
        self.__balance = balance

    def verify_password(self, pwd):
        return pwd == self.__password

    def check_balance(self, pwd):
        if self.verify_password(pwd):
            return self.__balance
        return None

    def deposit(self, pwd, amount):
        if self.verify_password(pwd) and amount > 0:
            self.__balance += amount
            return True
        return False

acc = Account("secret123", 1000)
print(acc.check_balance("wrong"))  # None
print(acc.check_balance("secret123"))  # 1000
```

</details>

### Challenge: Secure Player Profile
Create a `Player` class:
- Private: `__health` (0-100), `__experience` (0-1000)
- Public: `take_damage(amount)`, `heal(amount)`, `gain_exp(amount)`, `get_level()` (based on exp)
- Protected: `_is_valid_health(h)`, `_is_valid_exp(e)`

```python
p = Player(100, 0)
p.take_damage(30)
print(p.get_health())  # 70
p.gain_exp(500)
print(p.get_level())  # Level 5 or similar
```

<details>
<summary>Answer</summary>

```python
class Player:
    def __init__(self, health, experience):
        self.__health = health
        self.__experience = experience

    def _is_valid_health(self, h):
        return 0 <= h <= 100

    def _is_valid_exp(self, e):
        return 0 <= e <= 1000

    def take_damage(self, amount):
        new_health = self.__health - amount
        if self._is_valid_health(new_health):
            self.__health = new_health

    def heal(self, amount):
        new_health = self.__health + amount
        if self._is_valid_health(new_health):
            self.__health = new_health

    def gain_exp(self, amount):
        new_exp = self.__experience + amount
        if self._is_valid_exp(new_exp):
            self.__experience = new_exp

    def get_health(self):
        return self.__health

    def get_level(self):
        return 1 + self.__experience // 200

p = Player(100, 0)
p.take_damage(30)
print(p.get_health())  # 70
p.gain_exp(500)
print(p.get_level())  # 3
```

</details>

---

# Day 7: The @property Decorator — Getters and Setters

## Learning Target
I can use `@property` to create getters and setters with validation

## Key Concepts

### What is `@property`?

`@property` allows you to access a method like an attribute (without parentheses):

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def area(self):
        """Access like attribute: circle.area"""
        return 3.14159 * self._radius**2

    def area_method(self):
        """Traditional method: circle.area_method()"""
        return 3.14159 * self._radius**2

circle = Circle(5)
print(circle.area)          # 78.5 (property - no parentheses)
print(circle.area_method()) # 78.5 (method - with parentheses)
```

### Setters with Validation

```python
class Age:
    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        """Getter - read the age."""
        return self._age

    @age.setter
    def age(self, value):
        """Setter - validate before setting."""
        if 0 <= value <= 150:
            self._age = value
        else:
            print("Invalid age!")

person = Age(25)
print(person.age)  # 25 (uses getter)
person.age = 30    # Uses setter
print(person.age)  # 30
person.age = -5    # Setter rejects it
```

### Property with Deletion

```python
class Account:
    def __init__(self, balance):
        self._balance = balance

    @property
    def balance(self):
        return self._balance

    @balance.setter
    def balance(self, amount):
        if amount >= 0:
            self._balance = amount

    @balance.deleter
    def balance(self):
        """Allow deletion if needed."""
        del self._balance

acc = Account(1000)
del acc.balance  # Calls deleter
```

## Guided Practice: Temperature with Properties

```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius

    @property
    def celsius(self):
        """Get temperature in Celsius."""
        return self._celsius

    @celsius.setter
    def celsius(self, value):
        """Set temperature in Celsius with validation."""
        if value >= -273.15:  # Absolute zero
            self._celsius = value
        else:
            raise ValueError("Temperature cannot be below absolute zero")

    @property
    def fahrenheit(self):
        """Get temperature in Fahrenheit."""
        return (self._celsius * 9/5) + 32

    @fahrenheit.setter
    def fahrenheit(self, value):
        """Set temperature in Fahrenheit."""
        self.celsius = (value - 32) * 5/9

    def __str__(self):
        return f"{self._celsius}°C / {self.fahrenheit}°F"

temp = Temperature(0)
print(temp)  # 0°C / 32.0°F

temp.celsius = 100
print(temp)  # 100°C / 212.0°F

temp.fahrenheit = 68
print(temp)  # 20.0°C / 68.0°F
```

## Practice Problems

### Beginner: Score Limiter
Create a `Score` class:
- Property: `score` (0-100)
- Getter returns current, setter validates range

```python
score = Score(50)
print(score.score)  # 50
score.score = 95
print(score.score)  # 95
score.score = 150  # Invalid
print(score.score)  # Still 95
```

<details>
<summary>Answer</summary>

```python
class Score:
    def __init__(self, initial_score):
        self._score = initial_score

    @property
    def score(self):
        return self._score

    @score.setter
    def score(self, value):
        if 0 <= value <= 100:
            self._score = value
        else:
            print(f"Invalid score: {value}. Must be 0-100")

score = Score(50)
print(score.score)  # 50
score.score = 95
print(score.score)  # 95
score.score = 150
print(score.score)  # Still 95
```

</details>

### Intermediate: Volume with Read-Only Property
Create a `Box` class:
- Attributes: `length`, `width`, `height` (with setters)
- Property: `volume` (read-only)

```python
box = Box(2, 3, 4)
print(box.volume)  # 24
box.length = 5
print(box.volume)  # 60
```

<details>
<summary>Answer</summary>

```python
class Box:
    def __init__(self, length, width, height):
        self._length = length
        self._width = width
        self._height = height

    @property
    def length(self):
        return self._length

    @length.setter
    def length(self, value):
        if value > 0:
            self._length = value

    @property
    def width(self):
        return self._width

    @width.setter
    def width(self, value):
        if value > 0:
            self._width = value

    @property
    def height(self):
        return self._height

    @height.setter
    def height(self, value):
        if value > 0:
            self._height = value

    @property
    def volume(self):
        return self._length * self._width * self._height

box = Box(2, 3, 4)
print(box.volume)  # 24
box.length = 5
print(box.volume)  # 60
```

</details>

### Challenge: Computed Property
Create a `Rectangle` class:
- Private: `_width`, `_height`
- Properties with setters: `width`, `height` (must be > 0)
- Computed property: `aspect_ratio` (read-only, width/height)
- Computed property: `diagonal` (read-only, √(w²+h²))

```python
rect = Rectangle(3, 4)
print(rect.diagonal)  # 5.0
print(rect.aspect_ratio)  # 0.75
```

<details>
<summary>Answer</summary>

```python
class Rectangle:
    def __init__(self, width, height):
        self._width = width
        self._height = height

    @property
    def width(self):
        return self._width

    @width.setter
    def width(self, value):
        if value > 0:
            self._width = value

    @property
    def height(self):
        return self._height

    @height.setter
    def height(self, value):
        if value > 0:
            self._height = value

    @property
    def aspect_ratio(self):
        return self._width / self._height

    @property
    def diagonal(self):
        return (self._width**2 + self._height**2)**0.5

rect = Rectangle(3, 4)
print(rect.diagonal)  # 5.0
print(rect.aspect_ratio)  # 0.75
```

</details>

---

# Day 8: Encapsulation Lab — Building a Secure BankAccount

## Project: Complete BankAccount Class

Create a comprehensive `BankAccount` class that demonstrates all encapsulation concepts:

### Requirements

1. **Private Attributes:**
   - `__balance` (starting balance)
   - `__pin` (security pin)
   - `__transaction_history` (list of transactions)

2. **Public Methods:**
   - `authenticate(pin)` — verify PIN
   - `deposit(pin, amount)` — add funds
   - `withdraw(pin, amount)` — remove funds
   - `get_balance(pin)` — check balance (requires auth)
   - `get_transaction_history(pin)` — view history

3. **Protected Methods:**
   - `_record_transaction(transaction_type, amount)` — internal tracking
   - `_is_valid_amount(amount)` — validation

4. **Properties:**
   - `account_holder` (getter only)

### Starter Code

```python
class BankAccount:
    def __init__(self, account_holder, initial_balance, pin):
        # Your code here
        pass

    def authenticate(self, pin):
        # Your code here
        pass

    def deposit(self, pin, amount):
        # Your code here
        pass

    def withdraw(self, pin, amount):
        # Your code here
        pass

    def get_balance(self, pin):
        # Your code here
        pass

    def get_transaction_history(self, pin):
        # Your code here
        pass

    def _record_transaction(self, trans_type, amount):
        # Your code here
        pass

    def _is_valid_amount(self, amount):
        # Your code here
        pass

    @property
    def account_holder(self):
        # Your code here
        pass

# Test
account = BankAccount("Alice", 1000, "1234")
account.deposit("1234", 500)
print(account.get_balance("1234"))  # 1500
account.withdraw("1234", 200)
print(account.get_balance("1234"))  # 1300
print(account.account_holder)  # Alice
```

<details>
<summary>Answer</summary>

```python
class BankAccount:
    def __init__(self, account_holder, initial_balance, pin):
        self._account_holder = account_holder
        self.__balance = initial_balance
        self.__pin = pin
        self.__transaction_history = [f"Account opened with ${initial_balance}"]

    def authenticate(self, pin):
        """Verify the PIN."""
        return pin == self.__pin

    def _is_valid_amount(self, amount):
        """Check if amount is positive."""
        return amount > 0

    def _record_transaction(self, trans_type, amount):
        """Record a transaction."""
        self.__transaction_history.append(f"{trans_type}: ${amount}")

    def deposit(self, pin, amount):
        """Deposit funds."""
        if not self.authenticate(pin):
            return "Invalid PIN"
        if not self._is_valid_amount(amount):
            return "Amount must be positive"

        self.__balance += amount
        self._record_transaction("Deposit", amount)
        return f"Deposited ${amount}. New balance: ${self.__balance}"

    def withdraw(self, pin, amount):
        """Withdraw funds."""
        if not self.authenticate(pin):
            return "Invalid PIN"
        if not self._is_valid_amount(amount):
            return "Amount must be positive"
        if amount > self.__balance:
            return "Insufficient funds"

        self.__balance -= amount
        self._record_transaction("Withdraw", amount)
        return f"Withdrew ${amount}. New balance: ${self.__balance}"

    def get_balance(self, pin):
        """Get account balance (requires authentication)."""
        if not self.authenticate(pin):
            return "Invalid PIN"
        return self.__balance

    def get_transaction_history(self, pin):
        """Get transaction history (requires authentication)."""
        if not self.authenticate(pin):
            return "Invalid PIN"
        return self.__transaction_history

    @property
    def account_holder(self):
        return self._account_holder

# Test
account = BankAccount("Alice", 1000, "1234")
print(account.deposit("1234", 500))  # Deposited $500. New balance: $1500
print(account.get_balance("1234"))  # 1500
print(account.withdraw("1234", 200))  # Withdrew $200. New balance: $1300
print(account.get_balance("1234"))  # 1300
print(account.account_holder)  # Alice
```

</details>

---

# Day 9: Inheritance Basics — Parent and Child Classes

## Learning Target
I can create inheritance hierarchies using parent and child classes

## Key Concepts

### What is Inheritance?

**Inheritance** allows a child class to inherit attributes and methods from a parent class. Use it when there's an "is-a" relationship.

```python
class Animal:
    """Parent class (base class)."""
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "Some sound"

class Dog(Animal):
    """Child class (derived class) - inherits from Animal."""
    def speak(self):
        return "Woof!"

# Dog is-an Animal
dog = Dog("Rex")
print(dog.name)      # Inherited from Animal
print(dog.speak())   # Overridden in Dog
```

### Benefits of Inheritance

1. **Code Reuse:** Write code once, use in many places
2. **Logical Organization:** Group related classes
3. **Polymorphism:** Different classes, same interface

### Inheritance Syntax

```python
class Parent:
    def method(self):
        return "parent"

class Child(Parent):  # "Child inherits from Parent"
    pass

c = Child()
print(c.method())  # "parent" - inherited from Parent
```

## Guided Practice: Animal Hierarchy

```python
class Animal:
    """Base class for all animals."""
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def eat(self):
        return f"{self.name} is eating"

    def sleep(self):
        return f"{self.name} is sleeping"

    def birthday(self):
        self.age += 1

class Dog(Animal):
    """Dog is-an Animal."""
    def speak(self):
        return f"{self.name} barks: Woof!"

class Cat(Animal):
    """Cat is-an Animal."""
    def speak(self):
        return f"{self.name} meows: Meow!"

class Bird(Animal):
    """Bird is-an Animal."""
    def speak(self):
        return f"{self.name} chirps: Tweet!"

# All inherit eat(), sleep(), birthday()
dog = Dog("Buddy", 3)
cat = Cat("Whiskers", 2)
bird = Bird("Tweety", 1)

print(dog.eat())      # Buddy is eating (inherited)
print(cat.sleep())    # Whiskers is sleeping (inherited)
print(bird.speak())   # Tweety chirps: Tweet! (child method)
```

## Practice Problems

### Beginner: Vehicle Hierarchy
Create a parent `Vehicle` class and children `Car` and `Motorcycle`:
- `Vehicle.__init__`: `brand`, `color`
- `Vehicle.describe()`: returns brand and color
- `Car.describe()`: adds "4 wheels"
- `Motorcycle.describe()`: adds "2 wheels"

```python
car = Car("Toyota", "red")
print(car.describe())  # Red Toyota with 4 wheels

bike = Motorcycle("Harley", "black")
print(bike.describe())  # Black Harley with 2 wheels
```

<details>
<summary>Answer</summary>

```python
class Vehicle:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color

    def describe(self):
        return f"{self.color.capitalize()} {self.brand}"

class Car(Vehicle):
    def describe(self):
        return super().describe() + " with 4 wheels"

class Motorcycle(Vehicle):
    def describe(self):
        return super().describe() + " with 2 wheels"

car = Car("Toyota", "red")
print(car.describe())  # Red Toyota with 4 wheels

bike = Motorcycle("Harley", "black")
print(bike.describe())  # Black Harley with 2 wheels
```

</details>

### Intermediate: Shape Hierarchy
Create parent `Shape` with children `Circle`, `Square`:
- `Shape.__init__`: takes parameters for shape
- `Shape.area()`: abstract method (or returns 0)
- Each child implements `area()`
- Each child implements `__str__()`

```python
circle = Circle(5)
print(circle.area())  # 78.5
print(circle)  # Circle with radius 5

square = Square(4)
print(square.area())  # 16
print(square)  # Square with side 4
```

<details>
<summary>Answer</summary>

```python
class Shape:
    def area(self):
        return 0

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius**2

    def __str__(self):
        return f"Circle with radius {self.radius}"

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side**2

    def __str__(self):
        return f"Square with side {self.side}"

circle = Circle(5)
print(f"{circle.area():.2f}")  # 78.50
print(circle)  # Circle with radius 5

square = Square(4)
print(square.area())  # 16
print(square)  # Square with side 4
```

</details>

### Challenge: Employee Hierarchy
Create parent `Employee` and children `Manager`, `Programmer`, `Intern`:
- All have: `name`, `salary`, `get_info()`
- Manager: adds `team_size` to info
- Programmer: adds `language` to info
- Intern: adds `university` to info

```python
emp = Programmer("Alice", 80000, "Python")
print(emp.get_info())  # Alice earns $80000 and programs in Python
```

<details>
<summary>Answer</summary>

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def get_info(self):
        return f"{self.name} earns ${self.salary}"

class Manager(Employee):
    def __init__(self, name, salary, team_size):
        super().__init__(name, salary)
        self.team_size = team_size

    def get_info(self):
        return super().get_info() + f" and manages {self.team_size} people"

class Programmer(Employee):
    def __init__(self, name, salary, language):
        super().__init__(name, salary)
        self.language = language

    def get_info(self):
        return super().get_info() + f" and programs in {self.language}"

class Intern(Employee):
    def __init__(self, name, salary, university):
        super().__init__(name, salary)
        self.university = university

    def get_info(self):
        return super().get_info() + f" and studies at {self.university}"

emp = Programmer("Alice", 80000, "Python")
print(emp.get_info())  # Alice earns $80000 and programs in Python
```

</details>

---

# Day 10: The super() Function

## Learning Target
I can use `super()` to call parent class methods

## Key Concepts

### What is `super()`?

`super()` allows a child class to call methods from its parent class. Essential for:
1. Extending parent behavior (not replacing it)
2. Avoiding code duplication
3. Proper initialization chains in inheritance

### Basic super() Usage

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def describe(self):
        return f"I am {self.name}"

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)  # Call parent's __init__
        self.breed = breed

    def describe(self):
        parent_desc = super().describe()  # Call parent's method
        return parent_desc + f" and I'm a {self.breed}"

dog = Dog("Rex", "Labrador")
print(dog.describe())
# Output: I am Rex and I'm a Labrador
```

### super() vs Directly Calling Parent

```python
class Parent:
    def greet(self):
        return "Hello from Parent"

class Child(Parent):
    def greet(self):
        # Option 1: Using super() (PREFERRED)
        return super().greet() + " and Child"

        # Option 2: Calling directly (NOT recommended)
        # return Parent.greet(self) + " and Child"

child = Child()
print(child.greet())  # Hello from Parent and Child
```

Why is `super()` better? It handles multiple inheritance correctly and is more maintainable.

## Guided Practice: Employee with super()

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def get_info(self):
        return f"{self.name} earns ${self.salary}"

    def give_raise(self, amount):
        self.salary += amount

class Manager(Employee):
    def __init__(self, name, salary, department):
        super().__init__(name, salary)  # Initialize parent
        self.department = department

    def get_info(self):
        parent_info = super().get_info()  # Extend parent's method
        return parent_info + f" in {self.department}"

    def give_raise(self, amount):
        super().give_raise(amount * 1.5)  # Managers get 1.5x raise

manager = Manager("Alice", 80000, "Engineering")
print(manager.get_info())  # Alice earns $80000 in Engineering
manager.give_raise(1000)
print(manager.get_info())  # Alice earns $81500 in Engineering
```

## Practice Problems

### Beginner: Vehicle with super()
Create `Vehicle` parent and `Car` child:
- `Vehicle.__init__`: `make`, `year`
- `Car.__init__`: calls `super().__init__`, adds `num_doors`
- Both have `start()` method

```python
car = Car("Honda", 2020, 4)
print(car.start())  # Honda (2020) with 4 doors starts
```

<details>
<summary>Answer</summary>

```python
class Vehicle:
    def __init__(self, make, year):
        self.make = make
        self.year = year

    def start(self):
        return f"{self.make} starts"

class Car(Vehicle):
    def __init__(self, make, year, num_doors):
        super().__init__(make, year)
        self.num_doors = num_doors

    def start(self):
        parent_start = super().start()
        return f"{parent_start} ({self.year}) with {self.num_doors} doors"

car = Car("Honda", 2020, 4)
print(car.start())  # Honda starts (2020) with 4 doors
```

</details>

### Intermediate: Person → Student → GraduateStudent
Create three-level hierarchy:
- `Person`: name, age
- `Student(Person)`: gpa, year
- `GraduateStudent(Student)`: thesis_topic

```python
gs = GraduateStudent("Alice", 24, 3.8, "Senior", "AI in Healthcare")
print(gs.get_info())  # Multi-line info
```

<details>
<summary>Answer</summary>

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def get_info(self):
        return f"Name: {self.name}, Age: {self.age}"

class Student(Person):
    def __init__(self, name, age, gpa, year):
        super().__init__(name, age)
        self.gpa = gpa
        self.year = year

    def get_info(self):
        parent_info = super().get_info()
        return f"{parent_info}, GPA: {self.gpa}, Year: {self.year}"

class GraduateStudent(Student):
    def __init__(self, name, age, gpa, year, thesis_topic):
        super().__init__(name, age, gpa, year)
        self.thesis_topic = thesis_topic

    def get_info(self):
        parent_info = super().get_info()
        return f"{parent_info}, Thesis: {self.thesis_topic}"

gs = GraduateStudent("Alice", 24, 3.8, "Senior", "AI in Healthcare")
print(gs.get_info())
# Name: Alice, Age: 24, GPA: 3.8, Year: Senior, Thesis: AI in Healthcare
```

</details>

### Challenge: Account Hierarchy
Create `Account` → `SavingsAccount` → `HighYieldSavings`:
- Each level adds functionality using `super()`
- Base: `balance`, `deposit()`
- Savings: adds `interest_rate`, overrides `deposit()` to add interest
- HighYield: adds `bonus_rate`, applies both interests

```python
hy = HighYieldSavings(1000, 0.02, 0.01)
hy.deposit(100)  # Deposited, with interest applied
print(hy.balance)  # ~1103
```

<details>
<summary>Answer</summary>

```python
class Account:
    def __init__(self, balance):
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount
        return f"Deposited ${amount}"

class SavingsAccount(Account):
    def __init__(self, balance, interest_rate):
        super().__init__(balance)
        self.interest_rate = interest_rate

    def deposit(self, amount):
        result = super().deposit(amount)
        interest = self.balance * self.interest_rate
        self.balance += interest
        return result + f" (interest: ${interest:.2f})"

class HighYieldSavings(SavingsAccount):
    def __init__(self, balance, interest_rate, bonus_rate):
        super().__init__(balance, interest_rate)
        self.bonus_rate = bonus_rate

    def deposit(self, amount):
        result = super().deposit(amount)
        bonus = self.balance * self.bonus_rate
        self.balance += bonus
        return result + f" (bonus: ${bonus:.2f})"

hy = HighYieldSavings(1000, 0.02, 0.01)
print(hy.deposit(100))
print(f"Balance: ${hy.balance:.2f}")
```

</details>

---

# Day 11: Method Overriding

## Learning Target
I can override parent methods with child implementations

## Key Concepts

### What is Method Overriding?

**Method overriding** occurs when a child class defines a method with the same name as the parent. The child's version "hides" the parent's.

```python
class Parent:
    def speak(self):
        return "Parent speaks"

class Child(Parent):
    def speak(self):  # Override parent's speak()
        return "Child speaks"

p = Parent()
c = Child()

print(p.speak())  # Parent speaks
print(c.speak())  # Child speaks (not parent's)
```

### Override vs Extend

```python
class Parent:
    def greet(self):
        return "Hello"

class ChildReplace(Parent):
    def greet(self):
        return "Hi"  # REPLACES parent's method

class ChildExtend(Parent):
    def greet(self):
        return super().greet() + " and goodbye"  # EXTENDS parent's method

child_r = ChildReplace()
child_e = ChildExtend()

print(child_r.greet())  # Hi (replaced)
print(child_e.greet())  # Hello and goodbye (extended)
```

## Guided Practice: Shapes with Overriding

```python
class Shape:
    def __init__(self, name):
        self.name = name

    def area(self):
        return 0

    def describe(self):
        return f"{self.name}: area = {self.area()}"

class Circle(Shape):
    def __init__(self, radius):
        super().__init__("Circle")
        self.radius = radius

    def area(self):  # Override
        return 3.14159 * self.radius**2

class Rectangle(Shape):
    def __init__(self, width, height):
        super().__init__("Rectangle")
        self.width = width
        self.height = height

    def area(self):  # Override
        return self.width * self.height

shapes = [Circle(5), Rectangle(4, 6)]
for shape in shapes:
    print(shape.describe())
# Output:
# Circle: area = 78.5395
# Rectangle: area = 24
```

## Practice Problems

### Beginner: Payment Methods
Create `PaymentMethod` parent and `CreditCard`, `PayPal` children:
- Parent: `process_payment(amount)` returns "Processing..."
- Children: override to return specific messages

```python
cc = CreditCard("1234-5678-9012-3456")
pp = PayPal("user@example.com")
print(cc.process_payment(100))  # Processing with credit card...
print(pp.process_payment(100))  # Processing with PayPal...
```

<details>
<summary>Answer</summary>

```python
class PaymentMethod:
    def process_payment(self, amount):
        return f"Processing ${amount}..."

class CreditCard(PaymentMethod):
    def __init__(self, card_number):
        self.card_number = card_number

    def process_payment(self, amount):
        return f"Processing ${amount} with credit card {self.card_number[-4:]}..."

class PayPal(PaymentMethod):
    def __init__(self, email):
        self.email = email

    def process_payment(self, amount):
        return f"Processing ${amount} with PayPal ({self.email})..."

cc = CreditCard("1234-5678-9012-3456")
pp = PayPal("user@example.com")
print(cc.process_payment(100))  # Processing $100 with credit card 3456...
print(pp.process_payment(100))  # Processing $100 with PayPal (user@example.com)...
```

</details>

### Intermediate: Worker Types
Create `Worker` parent and `FullTime`, `PartTime` children:
- Parent: `calculate_pay(hours)` returns standard pay
- FullTime: override to add 1.5x for overtime (>40 hours)
- PartTime: override to reduce pay by 10%

```python
ft = FullTime("Alice", 20)
pt = PartTime("Bob", 15)
print(ft.calculate_pay(50))  # 40*20 + 10*20*1.5 = 1100
print(pt.calculate_pay(30))  # 30*15*0.9 = 405
```

<details>
<summary>Answer</summary>

```python
class Worker:
    def __init__(self, name, hourly_rate):
        self.name = name
        self.hourly_rate = hourly_rate

    def calculate_pay(self, hours):
        return hours * self.hourly_rate

class FullTime(Worker):
    def calculate_pay(self, hours):
        if hours > 40:
            regular = 40 * self.hourly_rate
            overtime = (hours - 40) * self.hourly_rate * 1.5
            return regular + overtime
        return super().calculate_pay(hours)

class PartTime(Worker):
    def calculate_pay(self, hours):
        base_pay = super().calculate_pay(hours)
        return base_pay * 0.9  # 10% reduction

ft = FullTime("Alice", 20)
pt = PartTime("Bob", 15)
print(ft.calculate_pay(50))  # 1100
print(pt.calculate_pay(30))  # 405
```

</details>

### Challenge: Game Units
Create `Unit` parent and `Warrior`, `Mage`, `Archer` children:
- Parent: `attack()` returns base damage
- Each child: override `attack()` with different behavior
- Warrior: 20 + strength bonus
- Mage: 10 but 2x for magic damage
- Archer: 15 but +5 if enemy far

```python
warrior = Warrior("Conan", 8)  # strength=8
mage = Mage("Merlin")
print(warrior.attack())  # 28
print(mage.attack())  # 20
```

<details>
<summary>Answer</summary>

```python
class Unit:
    def __init__(self, name):
        self.name = name

    def attack(self):
        return 10

class Warrior(Unit):
    def __init__(self, name, strength):
        super().__init__(name)
        self.strength = strength

    def attack(self):
        return 20 + (self.strength * 2)

class Mage(Unit):
    def attack(self):
        return 10 * 2  # 2x magic damage

class Archer(Unit):
    def attack(self, far_enemy=False):
        base = 15
        return base + 5 if far_enemy else base

warrior = Warrior("Conan", 8)
mage = Mage("Merlin")
archer = Archer("Robin")
print(warrior.attack())  # 36
print(mage.attack())  # 20
print(archer.attack(True))  # 20
```

</details>

---

# Day 12: Inheritance Lab — Animal Kingdom

## Project: Complete Animal Hierarchy

Create a comprehensive animal classification system demonstrating inheritance:

### Class Hierarchy

```
Animal (parent)
├── Mammal
│   ├── Dog
│   ├── Cat
│   └── Whale
├── Bird
│   ├── Parrot
│   ├── Penguin
│   └── Eagle
└── Reptile
    ├── Snake
    ├── Lizard
    └── Turtle
```

### Requirements

1. **Animal (Parent)**
   - Attributes: `name`, `age`
   - Methods: `birthday()`, `eat(food)`, `sleep()`, `make_sound()`

2. **Mammal**
   - Override `eat()` to show mammals chew
   - Attribute: `fur_color`

3. **Dog(Mammal)**
   - Specific `make_sound()`
   - Method: `fetch(item)`

4. **Bird**
   - Attribute: `can_fly`
   - Override `make_sound()`

5. **Parrot(Bird)**
   - Method: `repeat(phrase)`

6. **Reptile**
   - Attribute: `cold_blooded = True`
   - Override `make_sound()`

### Starter Code

```python
class Animal:
    def __init__(self, name, age):
        # Your code
        pass

    def birthday(self):
        # Your code
        pass

    def eat(self, food):
        # Your code
        pass

    def sleep(self):
        # Your code
        pass

    def make_sound(self):
        # Your code
        pass

# Implement all child classes...

# Test
dog = Dog("Buddy", 3, "brown")
bird = Parrot("Polly", 5, True)
snake = Snake("Sssam", 2)

print(dog.make_sound())  # Woof!
print(dog.eat("kibble"))  # Buddy chews kibble
print(bird.repeat("Hello!"))  # Polly says: Hello!
print(snake.make_sound())  # Hisss!
```

<details>
<summary>Answer</summary>

```python
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def birthday(self):
        self.age += 1
        return f"{self.name} is now {self.age}"

    def eat(self, food):
        return f"{self.name} eats {food}"

    def sleep(self):
        return f"{self.name} sleeps"

    def make_sound(self):
        return "Some sound"

class Mammal(Animal):
    def __init__(self, name, age, fur_color):
        super().__init__(name, age)
        self.fur_color = fur_color

    def eat(self, food):
        return f"{self.name} chews {food}"

class Dog(Mammal):
    def make_sound(self):
        return f"{self.name} says: Woof!"

    def fetch(self, item):
        return f"{self.name} fetches {item}"

class Cat(Mammal):
    def make_sound(self):
        return f"{self.name} says: Meow!"

class Whale(Mammal):
    def make_sound(self):
        return f"{self.name} sings: Whooooo!"

class Bird(Animal):
    def __init__(self, name, age, can_fly):
        super().__init__(name, age)
        self.can_fly = can_fly

    def make_sound(self):
        return "Tweet!"

class Parrot(Bird):
    def make_sound(self):
        return f"{self.name} squawks!"

    def repeat(self, phrase):
        return f"{self.name} says: {phrase}"

class Penguin(Bird):
    def make_sound(self):
        return f"{self.name} squawks: Waak waak!"

class Eagle(Bird):
    def make_sound(self):
        return f"{self.name} screeches!"

class Reptile(Animal):
    def __init__(self, name, age):
        super().__init__(name, age)
        self.cold_blooded = True

class Snake(Reptile):
    def make_sound(self):
        return f"{self.name} hisses: Sssss!"

class Lizard(Reptile):
    def make_sound(self):
        return f"{self.name} chirps!"

class Turtle(Reptile):
    def make_sound(self):
        return "..."

# Test
dog = Dog("Buddy", 3, "brown")
bird = Parrot("Polly", 5, True)
snake = Snake("Sssam", 2)

print(dog.make_sound())  # Buddy says: Woof!
print(dog.eat("kibble"))  # Buddy chews kibble
print(bird.repeat("Hello!"))  # Polly says: Hello!
print(snake.make_sound())  # Sssam hisses: Sssss!
```

</details>

---

[Continue with Days 13-30...]

---

# Unit Practice Bank

See **UnitPractice.md** for 20 comprehensive practice problems at three levels.

---

# Common Mistakes & How to Fix Them

| Mistake | Example | Fix |
|---------|---------|-----|
| Forgetting `self` | `def method():` | Add `self` as first parameter: `def method(self):` |
| Forgetting `self.` | `name = "Alice"` | Use `self.name = "Alice"` for instance variables |
| Confusing `=` and `==` | `if x = 5:` | Use `==` for comparison: `if x == 5:` |
| Class vs instance vars | `self.count = 0` then using `Count` | Use `ClassName.var` for class variables |
| Not calling `super().__init__()` | Child skips parent init | Always call `super().__init__(args)` in child constructor |
| Modifying class var unintentionally | Setting `self.class_var = new` | Be aware this creates instance variable, not modifying class var |
| Private attributes not hidden | `self.__var` accessible from outside | Use `@property` or methods to control access |
| Inheritance without "is-a" relationship | Making Dog inherit from Car | Use composition instead |

---

# Unit Assessment Prep

**Review Questions:**

1. **Q: What's the difference between `__init__` and `__new__`?**
   A: `__new__` creates the object, `__init__` initializes it. You usually only override `__init__`.

2. **Q: Can you have multiple inheritance in Python?**
   A: Yes, but it's complex. Use composition instead when possible.

3. **Q: How do you prevent a method from being overridden?**
   A: Python doesn't enforce this. Use naming conventions (`_protected`) or abstract classes.

4. **Q: What's the difference between `isinstance()` and `type()`?**
   A: `isinstance()` checks if object is instance of class or subclass. `type()` checks exact class.

5. **Q: Can abstract methods have implementations?**
   A: Yes, subclasses still override, but can call parent's version with `super()`.

6. **Q: What's wrong with deeply nested inheritance (5+ levels)?**
   A: Hard to understand, maintain, and debug. Use composition instead.

7. **Q: How do you check if a class has a method?**
   A: Use `hasattr(obj, 'method_name')` or `callable(getattr(obj, 'method_name', None))`.

8. **Q: Can instance methods be called on the class itself?**
   A: No, they need `self`. You must pass instance as first arg: `Class.method(instance)`.

9. **Q: What happens if a child doesn't override a parent method?**
   A: Child inherits and uses parent's version automatically.

10. **Q: How do you make attributes truly private (unhackable)?**
    A: You can't in Python. Use conventions and `@property` for control.

---

# Vocabulary & Quick Reference

## Key Terms

| Term | Definition |
|------|-----------|
| **Class** | Template/blueprint for creating objects |
| **Object/Instance** | Specific realization of a class |
| **Attribute** | Data stored in an object |
| **Method** | Function defined in a class |
| **Constructor** | `__init__` method called when object created |
| **Inheritance** | Child class acquires parent's methods/attributes |
| **Polymorphism** | Different objects respond to same method call differently |
| **Encapsulation** | Hiding internal details, controlling access |
| **Override** | Child class provides its own implementation of parent method |
| **Abstract Class** | Class that can't be instantiated directly |
| **Interface** | Set of methods a class must implement |
| **Composition** | Object contains instances of other classes |
| **Dunder Method** | Special method with double underscores (`__method__`) |

## Decorators Quick Ref

```python
@property          # Make method accessible like attribute
@property.setter   # Create setter for property
@classmethod       # Method receives class, not instance
@staticmethod      # Utility method, no instance/class needed
@abstractmethod    # Method must be implemented by subclass
```

## Method Signatures

```python
def regular_method(self, arg):          # Instance method
def class_method(cls, arg):             # @classmethod
def static_method(arg):                 # @staticmethod
def __init__(self, arg):                # Constructor
def __str__(self):                      # String representation
def __eq__(self, other):                # Equality
def __lt__(self, other):                # Less than
def __add__(self, other):               # Addition
```

