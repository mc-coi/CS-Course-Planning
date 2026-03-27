# Day 15: Polymorphism — Duck Typing
**Learning Target:** I can apply polymorphism and understand duck typing in Python for flexible, extensible code.

### Key Concepts

**Polymorphism:** The ability of objects of different types to respond to the same method call in their own way. "Many forms."

**Duck Typing:** "If it walks like a duck and quacks like a duck, it's a duck." In Python, we focus on what an object can do rather than what it is.

**Protocol:** An informal interface—if an object has certain methods, it's treated as if it implements that protocol, regardless of inheritance.

**Interface Compatibility:** Objects don't need to inherit from the same class to work together; they just need to have compatible methods.

### Code Examples

```python
# Simple polymorphism with inheritance
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

class Bird(Animal):
    def speak(self):
        return "Tweet!"

# Polymorphic behavior
animals = [Dog(), Cat(), Bird(), Dog()]
for animal in animals:
    print(animal.speak())
# Woof!
# Meow!
# Tweet!
# Woof!

# Duck typing - no inheritance needed
class Person:
    def speak(self):
        return "Hello!"

class Robot:
    def speak(self):
        return "Beep boop!"

def make_speak(entity):
    print(entity.speak())

make_speak(Dog())        # Woof!
make_speak(Person())     # Hello!
make_speak(Robot())      # Beep boop!
# Works even though Person and Robot don't inherit from Animal!

# Shape polymorphism
class Shape:
    def area(self):
        return 0

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        import math
        return math.pi * self.radius ** 2

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Triangle(Shape):
    def __init__(self, base, height):
        self.base = base
        self.height = height

    def area(self):
        return (self.base * self.height) / 2

shapes = [Circle(5), Rectangle(4, 6), Triangle(3, 4)]
total_area = 0
for shape in shapes:
    area = shape.area()
    total_area = total_area + area
    print(f"Area: {area:.2f}")

print(f"Total area: {total_area:.2f}")

# Payment processing polymorphism
class PaymentMethod:
    def process_payment(self, amount):
        pass

class CreditCard(PaymentMethod):
    def __init__(self, card_number):
        self.card_number = card_number

    def process_payment(self, amount):
        print(f"Processing ${amount} via credit card {self.card_number[-4:]}")
        return True

class PayPal(PaymentMethod):
    def __init__(self, email):
        self.email = email

    def process_payment(self, amount):
        print(f"Processing ${amount} via PayPal ({self.email})")
        return True

class Cryptocurrency(PaymentMethod):
    def __init__(self, wallet_address):
        self.wallet_address = wallet_address

    def process_payment(self, amount):
        print(f"Processing {amount} Bitcoin via {self.wallet_address}")
        return True

def checkout(payment_method, amount):
    if payment_method.process_payment(amount):
        print(f"Payment successful!\n")
    else:
        print(f"Payment failed!\n")

checkout(CreditCard("1234567890123456"), 99.99)
checkout(PayPal("user@example.com"), 49.99)
checkout(Cryptocurrency("1A1z7agoat"), 0.002)

# Iterator-like protocol (duck typing)
class CountUp:
    def __init__(self, max_value):
        self.current = 0
        self.max = max_value

    def __iter__(self):
        return self

    def __next__(self):
        if self.current < self.max:
            self.current = self.current + 1
            return self.current
        else:
            raise StopIteration

for num in CountUp(3):
    print(num)
# 1
# 2
# 3

# Logger duck typing example
class ConsoleLogger:
    def log(self, message):
        print(f"[CONSOLE] {message}")

class FileLogger:
    def __init__(self, filename):
        self.filename = filename

    def log(self, message):
        with open(self.filename, 'a') as f:
            f.write(f"[FILE] {message}\n")

class EmailLogger:
    def __init__(self, email):
        self.email = email

    def log(self, message):
        print(f"[EMAIL to {self.email}] {message}")

def send_alert(logger, message):
    logger.log(message)

console = ConsoleLogger()
send_alert(console, "System started")

# All objects with a log() method work the same way!
loggers = [ConsoleLogger(), FileLogger("app.log"), EmailLogger("admin@example.com")]
for logger in loggers:
    send_alert(logger, "Alert message")

# Drawable protocol
class Circle:
    def __init__(self, x, y, radius):
        self.x = x
        self.y = y
        self.radius = radius

    def draw(self):
        print(f"Drawing circle at ({self.x}, {self.y}) with radius {self.radius}")

class Square:
    def __init__(self, x, y, size):
        self.x = x
        self.y = y
        self.size = size

    def draw(self):
        print(f"Drawing square at ({self.x}, {self.y}) with size {self.size}")

class Line:
    def __init__(self, x1, y1, x2, y2):
        self.x1 = x1
        self.y1 = y1
        self.x2 = x2
        self.y2 = y2

    def draw(self):
        print(f"Drawing line from ({self.x1}, {self.y1}) to ({self.x2}, {self.y2})")

# All objects with draw() method can be treated the same
def render_all(shapes):
    for shape in shapes:
        shape.draw()

shapes = [Circle(0, 0, 5), Square(10, 10, 20), Line(0, 0, 100, 100)]
render_all(shapes)

# Worker interface (duck typing)
class Programmer:
    def code(self):
        return "Writing code..."

class Designer:
    def design(self):
        return "Creating designs..."

class Manager:
    def code(self):
        return "Writing management code..."

# Polymorphic work assignment
def assign_work(worker, work_type):
    if work_type == "coding" and hasattr(worker, 'code'):
        print(worker.code())
    elif work_type == "design" and hasattr(worker, 'design'):
        print(worker.design())

programmer = Programmer()
designer = Designer()
manager = Manager()

assign_work(programmer, "coding")  # Writing code...
assign_work(designer, "design")    # Creating designs...
assign_work(manager, "coding")     # Writing management code...

# Bank account polymorphism
class BankAccount:
    def __init__(self, balance):
        self._balance = balance

    @property
    def balance(self):
        return self._balance

    def deposit(self, amount):
        self._balance = self._balance + amount

    def withdraw(self, amount):
        if amount <= self._balance:
            self._balance = self._balance - amount
            return True
        return False

class CheckingAccount(BankAccount):
    def withdraw(self, amount):
        fee = 1
        return super().withdraw(amount + fee)

class SavingsAccount(BankAccount):
    def __init__(self, balance, interest_rate):
        super().__init__(balance)
        self.interest_rate = interest_rate

    def apply_interest(self):
        interest = self._balance * self.interest_rate
        self._balance = self._balance + interest

# Process accounts polymorphically
accounts = [
    CheckingAccount(1000),
    SavingsAccount(5000, 0.05),
    BankAccount(2000)
]

for account in accounts:
    print(f"Balance: ${account.balance}")
    account.deposit(100)
    print(f"After deposit: ${account.balance}\n")
```

### Guided Practice

**Activity: Create a Vehicle Rental System**

Follow these steps:

1. Create `Vehicle` base class with `rent_daily()` method
2. Create `Car`, `Truck`, `Motorcycle` that override with different rates
3. Create a `Rental` function that accepts any vehicle and calculates cost
4. Demonstrate polymorphism by renting different vehicles

**Solution:**
```python
class Vehicle:
    def __init__(self, name):
        self.name = name

    def rent_daily(self):
        return 0

class Car(Vehicle):
    def rent_daily(self):
        return 50

class Truck(Vehicle):
    def rent_daily(self):
        return 80

class Motorcycle(Vehicle):
    def rent_daily(self):
        return 30

def calculate_rental_cost(vehicle, days):
    daily_rate = vehicle.rent_daily()
    total = daily_rate * days
    print(f"{vehicle.name}: ${daily_rate}/day x {days} days = ${total}")
    return total

# Polymorphism in action
vehicles = [Car("Sedan"), Truck("Ford F-150"), Motorcycle("Harley")]
total_cost = 0

for vehicle in vehicles:
    total_cost = total_cost + calculate_rental_cost(vehicle, 3)

print(f"\nTotal rental cost: ${total_cost}")
```

### Practice Problems

**Problem 1 — Beginner:** Create `Shape` classes (Circle, Square) with `perimeter()` method. Show polymorphic behavior by calculating perimeter for a list of shapes.

**Problem 2 — Intermediate:** Create a list of different objects (with no common parent) that all have `get_info()` method. Loop through and call `get_info()` on each (duck typing).

**Problem 3 — Challenge:** Create a plugin system where different classes can be "registered" and used polymorphically without explicitly inheriting from a common base.

<details>
<summary>💡 Hints</summary>

**Hint 1:** Polymorphism works because Python looks for methods on objects dynamically, not at compile time.

**Hint 2:** Duck typing doesn't require inheritance—any object with the right method will work.

**Hint 3:** Use `hasattr()` to check if an object has a method before calling it.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
import math

class Shape:
    def perimeter(self):
        return 0

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def perimeter(self):
        return 2 * math.pi * self.radius

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def perimeter(self):
        return 4 * self.side

shapes = [Circle(5), Square(4), Circle(3), Square(2)]
for shape in shapes:
    print(f"Perimeter: {shape.perimeter():.2f}")

# Problem 2
class Dog:
    def get_info(self):
        return "I'm a dog"

class Car:
    def get_info(self):
        return "I'm a car"

class Book:
    def get_info(self):
        return "I'm a book"

objects = [Dog(), Car(), Book(), Dog()]
for obj in objects:
    print(obj.get_info())

# Problem 3
class PluginSystem:
    plugins = []

    @classmethod
    def register(cls, plugin):
        cls.plugins.append(plugin)

    @classmethod
    def execute_all(cls, method_name):
        for plugin in cls.plugins:
            if hasattr(plugin, method_name):
                getattr(plugin, method_name)()

class Plugin1:
    def run(self):
        print("Plugin 1 running...")

class Plugin2:
    def run(self):
        print("Plugin 2 running...")

PluginSystem.register(Plugin1())
PluginSystem.register(Plugin2())
PluginSystem.execute_all('run')
```

</details>
