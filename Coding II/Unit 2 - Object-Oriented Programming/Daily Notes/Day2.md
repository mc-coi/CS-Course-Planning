# Day 2: Defining Classes & __init__
**Learning Target:** I can define constructors and initialize objects with attributes.

### Key Concepts
The `__init__` method (constructor) initializes objects when created. The first parameter is always `self`, referring to the object being created.

`self` allows methods to access and modify the object's data.

### Code Examples
```python
class Car:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year
        self.odometer = 0

    def drive(self, distance):
        self.odometer += distance
        print(f"Drove {distance} miles. Total: {self.odometer}")

car = Car("Toyota", "Camry", 2020)
print(car.make)  # "Toyota"
car.drive(50)    # Drove 50 miles. Total: 50
```

### Guided Practice
Create a Movie class that initializes title, director, and year released. Add a method to display movie info.

### Practice Problems
**Problem 1 — Beginner:** Create a Rectangle class with width and height. Initialize in __init__.

**Problem 2 — Intermediate:** Create a Person class that tracks name, birth_year. Add a method to calculate age.

**Problem 3 — Challenge:** Create a VideoGame class tracking title, genre, release_year, and playtime_hours. Add methods to update playtime.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

# Problem 2
class Person:
    def __init__(self, name, birth_year):
        self.name = name
        self.birth_year = birth_year

    def age(self):
        return 2024 - self.birth_year
```
</details>

---
