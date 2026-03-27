# Day 4: Class vs Instance Variables
**Learning Target:** I can distinguish between class variables and instance variables and use them appropriately.

### Key Concepts
**Instance variables** are unique to each object: `self.name`.
**Class variables** are shared by all instances of a class. Define them outside __init__.

### Code Examples
```python
class Student:
    school = "Lincoln High"  # Class variable—shared by all students

    def __init__(self, name):
        self.name = name  # Instance variable—unique to each student
        self.grade = 9

student1 = Student("Alice")
student2 = Student("Bob")

print(student1.name)      # "Alice"
print(student2.name)      # "Bob"
print(student1.school)    # "Lincoln High"—same for both
print(Student.school)     # Access class variable from class itself

# Modifying class variable
Student.school = "Washington High"
print(student1.school)    # "Washington High"—changes for all
```

### Guided Practice
Create a Car class with a class variable tracking the number of cars created. Update it when each car is created.

### Practice Problems
**Problem 1 — Beginner:** Create a Counter class with a class variable that counts instances created.

**Problem 2 — Intermediate:** Create a Game with a class variable for high score and instance variables for player data.

**Problem 3 — Challenge:** Create an Employee class with salary (class variable), name, and id. Track and display company-wide info.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Counter:
    count = 0

    def __init__(self):
        Counter.count += 1

# Problem 2
class Game:
    high_score = 0

    def __init__(self, player_name):
        self.player_name = player_name
        self.score = 0
```
</details>

---
