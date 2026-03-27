# Day 13: Multiple Inheritance & MRO
**Learning Target:** I can use multiple inheritance and understand the Method Resolution Order (MRO) in Python.

### Key Concepts

**Multiple Inheritance:** A class can inherit from more than one parent class, combining attributes and methods from all parents.

**Method Resolution Order (MRO):** The order in which Python looks for methods in a hierarchy of classes. Uses C3 Linearization algorithm.

**Diamond Problem:** A situation where a class inherits from two classes that share a common parent, creating ambiguity in method resolution.

**Mixin Classes:** Classes designed to add specific functionality to other classes through multiple inheritance.

### Code Examples

```python
# Simple multiple inheritance
class Swimmer:
    def swim(self):
        print("Swimming...")

class Runner:
    def run(self):
        print("Running...")

class Athlete(Swimmer, Runner):
    def practice(self):
        print("Practicing...")

athlete = Athlete()
athlete.swim()      # Swimming...
athlete.run()       # Running...
athlete.practice()  # Practicing...

# MRO example
class A:
    def method(self):
        print("A's method")

class B(A):
    def method(self):
        print("B's method")

class C(A):
    def method(self):
        print("C's method")

class D(B, C):
    def method(self):
        print("D's method")

d = D()
d.method()  # D's method

# Check MRO
print(D.__mro__)
# (<class 'D'>, <class 'B'>, <class 'C'>, <class 'A'>, <class 'object'>)

# Practical multiple inheritance example
class Flier:
    def fly(self):
        print("Flying...")

class Walker:
    def walk(self):
        print("Walking...")

class Swimmer:
    def swim(self):
        print("Swimming...")

class Duck(Flier, Walker, Swimmer):
    def quack(self):
        print("Quack!")

duck = Duck()
duck.fly()    # Flying...
duck.walk()   # Walking...
duck.swim()   # Swimming...
duck.quack()  # Quack!

# Mixin classes for functionality
class Serializable:
    def to_dict(self):
        return self.__dict__

    def to_json(self):
        import json
        return json.dumps(self.to_dict())

class Printable:
    def pretty_print(self):
        for key, value in self.__dict__.items():
            print(f"{key}: {value}")

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

class Employee(Person, Serializable, Printable):
    def __init__(self, name, age, employee_id):
        super().__init__(name, age)
        self.employee_id = employee_id

emp = Employee("Alice", 30, "E001")
emp.pretty_print()
# name: Alice
# age: 30
# employee_id: E001

print(emp.to_dict())
# {'name': 'Alice', 'age': 30, 'employee_id': 'E001'}

# Vehicle example with multiple inheritance
class Electric:
    def __init__(self, battery_capacity):
        self.battery_capacity = battery_capacity

    def charge(self):
        print(f"Charging {self.battery_capacity} kWh battery...")

class Gasoline:
    def __init__(self, fuel_capacity):
        self.fuel_capacity = fuel_capacity

    def refuel(self):
        print(f"Refueling {self.fuel_capacity} gallons...")

class HybridCar(Electric, Gasoline):
    def __init__(self, name, battery_capacity, fuel_capacity):
        Electric.__init__(self, battery_capacity)
        Gasoline.__init__(self, fuel_capacity)
        self.name = name

    def display_info(self):
        print(f"{self.name}: {self.battery_capacity} kWh, {self.fuel_capacity} gallons")

hybrid = HybridCar("Toyota Prius", 50, 11.5)
hybrid.display_info()
hybrid.charge()
hybrid.refuel()

# Mixin with super() pattern
class Logger:
    def log(self, message):
        print(f"[LOG] {message}")

class Database:
    def save(self):
        print("[DB] Saving to database...")

class User(Logger, Database):
    def __init__(self, username):
        self.username = username

    def create_account(self):
        self.log(f"Creating account for {self.username}")
        self.save()

user = User("john")
user.create_account()
# [LOG] Creating account for john
# [DB] Saving to database...

# Diamond inheritance with super()
class A:
    def __init__(self):
        print("A init")
        super().__init__()

class B(A):
    def __init__(self):
        print("B init")
        super().__init__()

class C(A):
    def __init__(self):
        print("C init")
        super().__init__()

class D(B, C):
    def __init__(self):
        print("D init")
        super().__init__()

d = D()
# D init
# B init
# C init
# A init

# Checking MRO
print(D.__mro__)

# Stackable functionality with multiple inheritance
class TimestampMixin:
    def get_timestamp(self):
        from datetime import datetime
        return datetime.now().strftime("%Y-%m-%d %H:%M:%S")

class DataMixin:
    def validate_data(self):
        return True

class Document(TimestampMixin, DataMixin):
    def __init__(self, content):
        self.content = content
        self.created = self.get_timestamp()

    def save(self):
        if self.validate_data():
            print(f"Saved at {self.created}")

doc = Document("Important data")
doc.save()

# Permission mixins
class CanRead:
    def read(self):
        print("Reading...")

class CanWrite:
    def write(self):
        print("Writing...")

class CanDelete:
    def delete(self):
        print("Deleting...")

class User(CanRead, CanWrite):
    pass

class Admin(CanRead, CanWrite, CanDelete):
    pass

user = User()
user.read()
user.write()

admin = Admin()
admin.read()
admin.write()
admin.delete()
```

### Guided Practice

**Activity: Create a Multimedia Player**

Follow these steps:

1. Create `AudioPlayer` with `play_audio()` method
2. Create `VideoPlayer` with `play_video()` method
3. Create `MediaPlayer(AudioPlayer, VideoPlayer)` that uses both
4. Understand the MRO

**Solution:**
```python
class AudioPlayer:
    def play_audio(self):
        print("Playing audio file...")

class VideoPlayer:
    def play_video(self):
        print("Playing video file...")

class MediaPlayer(AudioPlayer, VideoPlayer):
    def play(self, file_type):
        if file_type == "audio":
            self.play_audio()
        elif file_type == "video":
            self.play_video()

player = MediaPlayer()
player.play("audio")
player.play("video")

print("MRO:", MediaPlayer.__mro__)
```

### Practice Problems

**Problem 1 — Beginner:** Create `Reader` and `Writer` classes with their methods. Create `Editor(Reader, Writer)` that inherits both. Demonstrate both methods work.

**Problem 2 — Intermediate:** Create `Comparable` with comparison methods and `Displayable` with display methods. Create `Person` class that inherits from both.

**Problem 3 — Challenge:** Create a 4-level hierarchy with Diamond inheritance pattern. Verify MRO is correct and super() works properly.

<details>
<summary>💡 Hints</summary>

**Hint 1:** Use `ClassName.__mro__` to see the method resolution order.

**Hint 2:** When calling `__init__` with multiple parents, you may need to call each parent explicitly or use cooperative `super()`.

**Hint 3:** For Problem 3, create a diamond by having two branches meet at a common parent.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Reader:
    def read(self):
        print("Reading file...")

class Writer:
    def write(self):
        print("Writing file...")

class Editor(Reader, Writer):
    def edit(self):
        print("Editing file...")

editor = Editor()
editor.read()
editor.write()
editor.edit()

# Problem 2
class Comparable:
    def is_equal(self, other):
        return False

    def is_greater(self, other):
        return False

class Displayable:
    def display(self):
        print(self)

class Person(Comparable, Displayable):
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def is_equal(self, other):
        return self.age == other.age

    def __str__(self):
        return f"{self.name}, {self.age}"

p1 = Person("Alice", 30)
p1.display()
p2 = Person("Bob", 30)
print(p1.is_equal(p2))

# Problem 3
class A:
    def method(self):
        print("A")

class B(A):
    def method(self):
        print("B")

class C(A):
    def method(self):
        print("C")

class D(B, C):
    def method(self):
        print("D")

d = D()
d.method()
print(D.__mro__)
```

</details>
