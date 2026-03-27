# Day 20: Abstract Classes & Interfaces
**Learning Target:** I can create abstract base classes to enforce a common interface across multiple implementations.

### Key Concepts

**Abstract Class:** A class that cannot be instantiated directly; it defines methods that subclasses must implement.

**Abstract Method:** A method defined in an abstract class without implementation; subclasses must override it.

**Interface:** A contract that specifies what methods an object must have (in Python, often implemented with abstract classes).

**abc Module:** Python's Abstract Base Class module for creating abstract classes.

**Method Not Implemented:** Ensures child classes provide their own implementation.

### Code Examples

```python
# Without abstract class (bad)
class Animal:
    def speak(self):
        print("Animal makes a sound")

# Problem: You can instantiate Animal directly
animal = Animal()  # Shouldn't be allowed
animal.speak()  # Generic sound, not meaningful

# With abstract class (good)
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

# Now you can't create Animal directly
# animal = Animal()  # TypeError: Can't instantiate abstract class

class Dog(Animal):
    def speak(self):
        print("Woof!")

class Cat(Animal):
    def speak(self):
        print("Meow!")

dog = Dog()
dog.speak()  # Woof!

cat = Cat()
cat.speak()  # Meow!

# Vehicle abstract class
from abc import ABC, abstractmethod

class Vehicle(ABC):
    def __init__(self, brand):
        self.brand = brand

    @abstractmethod
    def start_engine(self):
        pass

    @abstractmethod
    def stop_engine(self):
        pass

class Car(Vehicle):
    def start_engine(self):
        print(f"{self.brand} car engine started")

    def stop_engine(self):
        print(f"{self.brand} car engine stopped")

class Motorcycle(Vehicle):
    def start_engine(self):
        print(f"{self.brand} motorcycle engine started")

    def stop_engine(self):
        print(f"{self.brand} motorcycle engine stopped")

car = Car("Toyota")
car.start_engine()  # Toyota car engine started

bike = Motorcycle("Harley")
bike.start_engine()  # Harley motorcycle engine started

# Shape abstract class
from abc import ABC, abstractmethod
import math

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

    def perimeter(self):
        return 2 * math.pi * self.radius

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

# Calculate total area
shapes = [Circle(5), Rectangle(4, 6), Circle(3)]
total_area = sum(shape.area() for shape in shapes)
print(f"Total area: {total_area:.2f}")

# Database abstract class
from abc import ABC, abstractmethod

class Database(ABC):
    @abstractmethod
    def connect(self):
        pass

    @abstractmethod
    def query(self, sql):
        pass

    @abstractmethod
    def disconnect(self):
        pass

class MySQLDatabase(Database):
    def connect(self):
        print("Connected to MySQL")

    def query(self, sql):
        print(f"Executing MySQL: {sql}")

    def disconnect(self):
        print("Disconnected from MySQL")

class PostgresDatabase(Database):
    def connect(self):
        print("Connected to PostgreSQL")

    def query(self, sql):
        print(f"Executing PostgreSQL: {sql}")

    def disconnect(self):
        print("Disconnected from PostgreSQL")

db = MySQLDatabase()
db.connect()
db.query("SELECT * FROM users")
db.disconnect()

# Worker abstract class
from abc import ABC, abstractmethod

class Worker(ABC):
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    @abstractmethod
    def do_work(self):
        pass

    @abstractmethod
    def get_pay(self):
        pass

class Engineer(Worker):
    def do_work(self):
        print(f"{self.name} is coding")

    def get_pay(self):
        return self.salary

class Manager(Worker):
    def __init__(self, name, salary, bonus):
        super().__init__(name, salary)
        self.bonus = bonus

    def do_work(self):
        print(f"{self.name} is managing")

    def get_pay(self):
        return self.salary + self.bonus

workers = [
    Engineer("Alice", 80000),
    Manager("Bob", 100000, 20000)
]

for worker in workers:
    worker.do_work()
    print(f"Pay: ${worker.get_pay()}")

# Authentication abstract class
from abc import ABC, abstractmethod

class AuthMethod(ABC):
    @abstractmethod
    def authenticate(self, credentials):
        pass

class UsernamePasswordAuth(AuthMethod):
    def authenticate(self, credentials):
        if credentials.get("username") == "admin":
            print("Authenticated with username/password")
            return True
        return False

class TokenAuth(AuthMethod):
    def authenticate(self, credentials):
        if credentials.get("token") == "secret123":
            print("Authenticated with token")
            return True
        return False

# Processor abstract class with concrete method
from abc import ABC, abstractmethod

class DataProcessor(ABC):
    @abstractmethod
    def process(self, data):
        pass

    def validate(self, data):
        # Concrete method used by all subclasses
        return len(data) > 0

class JSONProcessor(DataProcessor):
    def process(self, data):
        print(f"Processing JSON: {data}")

class XMLProcessor(DataProcessor):
    def process(self, data):
        print(f"Processing XML: {data}")

json_proc = JSONProcessor()
if json_proc.validate("data"):
    json_proc.process("data")

# Multiple abstract methods in hierarchy
from abc import ABC, abstractmethod

class BaseEntity(ABC):
    @abstractmethod
    def save(self):
        pass

class DataModel(BaseEntity):
    @abstractmethod
    def validate(self):
        pass

class User(DataModel):
    def __init__(self, name):
        self.name = name

    def save(self):
        print(f"Saving user {self.name}")

    def validate(self):
        return len(self.name) > 0

user = User("Alice")
if user.validate():
    user.save()

# Cannot instantiate intermediate abstract class
# dm = DataModel()  # TypeError
# Can instantiate concrete class
u = User("Bob")
u.save()
```

### Guided Practice

**Activity: Create an Abstract Animal Class**

Follow these steps:

1. Create `Animal(ABC)` with abstract methods: `eat()`, `sleep()`, `make_sound()`
2. Create concrete classes: `Dog`, `Cat`, `Bird`
3. Override all abstract methods in each class
4. Create a list of different animals and call methods on each

**Solution:**
```python
from abc import ABC, abstractmethod

class Animal(ABC):
    def __init__(self, name):
        self.name = name

    @abstractmethod
    def eat(self):
        pass

    @abstractmethod
    def sleep(self):
        pass

    @abstractmethod
    def make_sound(self):
        pass

class Dog(Animal):
    def eat(self):
        print(f"{self.name} eats dog food")

    def sleep(self):
        print(f"{self.name} sleeps in a bed")

    def make_sound(self):
        print(f"{self.name} barks: Woof!")

class Cat(Animal):
    def eat(self):
        print(f"{self.name} eats cat food")

    def sleep(self):
        print(f"{self.name} sleeps on a windowsill")

    def make_sound(self):
        print(f"{self.name} meows: Meow!")

class Bird(Animal):
    def eat(self):
        print(f"{self.name} eats seeds")

    def sleep(self):
        print(f"{self.name} sleeps on a perch")

    def make_sound(self):
        print(f"{self.name} chirps: Tweet!")

animals = [Dog("Buddy"), Cat("Whiskers"), Bird("Tweety")]

for animal in animals:
    animal.make_sound()
    animal.eat()
    animal.sleep()
    print()
```

### Practice Problems

**Problem 1 — Beginner:** Create a Shape abstract class with area() method. Implement Circle, Square, and Triangle.

**Problem 2 — Intermediate:** Create a Transport abstract class with multiple abstract methods. Implement Car, Bus, Train.

**Problem 3 — Challenge:** Create a multi-level abstract hierarchy: PaymentMethod (abstract) → OnlinePayment (partial) → CreditCard (concrete).

<details>
<summary>💡 Hints</summary>

**Hint 1:** Use `from abc import ABC, abstractmethod` at the top.

**Hint 2:** Mark methods with `@abstractmethod` decorator.

**Hint 3:** Subclasses MUST override all abstract methods or they're also abstract.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
from abc import ABC, abstractmethod
import math

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side ** 2

class Triangle(Shape):
    def __init__(self, base, height):
        self.base = base
        self.height = height

    def area(self):
        return (self.base * self.height) / 2

# Problem 2
from abc import ABC, abstractmethod

class Transport(ABC):
    @abstractmethod
    def start(self):
        pass

    @abstractmethod
    def stop(self):
        pass

class Car(Transport):
    def start(self):
        print("Car started")

    def stop(self):
        print("Car stopped")

class Bus(Transport):
    def start(self):
        print("Bus started")

    def stop(self):
        print("Bus stopped")

# Problem 3
from abc import ABC, abstractmethod

class PaymentMethod(ABC):
    @abstractmethod
    def process_payment(self, amount):
        pass

class OnlinePayment(PaymentMethod):
    def verify(self):
        print("Verifying payment...")

class CreditCard(OnlinePayment):
    def __init__(self, card_number):
        self.card_number = card_number

    def process_payment(self, amount):
        self.verify()
        print(f"Processing ${amount} with card")

cc = CreditCard("1234567890123456")
cc.process_payment(99.99)
```

</details>
