# Day 6: Inheritance
**Learning Target:** I can create class hierarchies using inheritance and call parent methods with super().

### Key Concepts
**Inheritance** allows a child class to inherit attributes and methods from a parent class.

Use `super()` to call parent methods.

### Code Examples
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        print(f"{self.name} makes a sound")

class Dog(Animal):
    def speak(self):
        print(f"{self.name} barks")

class Cat(Animal):
    def speak(self):
        print(f"{self.name} meows")

dog = Dog("Rex")
dog.speak()  # "Rex barks"

cat = Cat("Whiskers")
cat.speak()  # "Whiskers meows"
```

### Guided Practice
Create a Shape parent class and Rectangle/Circle child classes with area() methods.

### Practice Problems
**Problem 1 — Beginner:** Create a Vehicle class and Car/Motorcycle child classes.

**Problem 2 — Intermediate:** Create an Employee parent and Manager/Developer child classes.

**Problem 3 — Challenge:** Create a multi-level inheritance: Animal > Mammal > Dog.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Vehicle:
    def __init__(self, make):
        self.make = make

class Car(Vehicle):
    def __init__(self, make, doors):
        super().__init__(make)
        self.doors = doors

# Problem 2
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def get_info(self):
        return f"{self.name}: ${self.salary}"

class Manager(Employee):
    def __init__(self, name, salary, team_size):
        super().__init__(name, salary)
        self.team_size = team_size
```
</details>

---
