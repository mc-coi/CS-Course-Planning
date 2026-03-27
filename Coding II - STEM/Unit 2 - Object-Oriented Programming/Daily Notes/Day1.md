# Day 1: Introduction to OOP
**Learning Target:** I can define classes and create objects with attributes and methods.

### Key Concepts
**Object-oriented programming (OOP)** organizes code around objects that combine data (attributes) and behavior (methods).

**Class:** A blueprint defining the structure of objects.
**Object (instance):** An individual example of a class.
**Attribute:** A variable that belongs to an object.
**Method:** A function that belongs to an object.

Think of a class like a blueprint for a car, and each car you build from that blueprint is an object.

### Code Examples
```python
# Define a class
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def bark(self):
        print(f"{self.name} says woof!")

    def age_in_dog_years(self):
        return self.age * 7

# Create objects (instances)
dog1 = Dog("Buddy", 3)
dog2 = Dog("Max", 5)

# Access attributes
print(dog1.name)  # "Buddy"

# Call methods
dog1.bark()  # "Buddy says woof!"
print(dog2.age_in_dog_years())  # 35
```

### Guided Practice
Create a Student class with name and grade attributes. Add a method that prints a greeting.

### Practice Problems
**Problem 1 — Beginner:** Create a simple Circle class with a radius attribute and a method to calculate area.

**Problem 2 — Intermediate:** Create a BankAccount class with balance, deposit(), and withdraw() methods.

**Problem 3 — Challenge:** Create a Book class with title, author, and pages. Add methods for a summary and reading progress.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

# Problem 2
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount
```
</details>

---
