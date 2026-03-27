# Day 2: Methods & the self Parameter
**Learning Target:** I can write methods for classes and use the self parameter to access object attributes.

### Key Concepts

**Method:** A function that belongs to a class and defines behavior for objects of that class. Methods operate on the data stored in objects.

**self Parameter:** A special parameter that represents the instance (object) that the method is being called on. It's the first parameter of every instance method and allows the method to access the object's attributes.

**Instance Method:** A method that belongs to individual objects and can access and modify that object's attributes using `self`.

**Method Call:** Invoking a method on an object using dot notation: `object.method()`

### Code Examples

```python
# Define a class with methods
class Dog:
    def bark(self):
        print("Woof!")

    def introduce(self):
        print("I am a dog!")

# Create an object and call methods
my_dog = Dog()
my_dog.bark()          # Woof!
my_dog.introduce()     # I am a dog!

# Methods can access and use attributes
class Person:
    def introduce(self):
        print(f"Hello, my name is {self.name}")

    def have_birthday(self):
        self.age = self.age + 1
        print(f"{self.name} is now {self.age} years old")

person1 = Person()
person1.name = "Alice"
person1.age = 25

person1.introduce()          # Hello, my name is Alice
person1.have_birthday()      # Alice is now 26 years old

# More practical example: Student with methods
class Student:
    def print_info(self):
        print(f"Name: {self.name}, Grade: {self.grade}, GPA: {self.gpa}")

    def add_gpa(self, points):
        self.gpa = self.gpa + points

    def study_hours(self, hours):
        print(f"{self.name} studied for {hours} hours")

student1 = Student()
student1.name = "Bob"
student1.grade = 10
student1.gpa = 3.5

student1.print_info()        # Name: Bob, Grade: 10, GPA: 3.5
student1.study_hours(3)      # Bob studied for 3 hours
student1.add_gpa(0.2)
student1.print_info()        # Name: Bob, Grade: 10, GPA: 3.7

# Rectangle class with methods
class Rectangle:
    def calculate_area(self):
        return self.width * self.height

    def calculate_perimeter(self):
        return 2 * (self.width + self.height)

    def display_info(self):
        area = self.calculate_area()
        perimeter = self.calculate_perimeter()
        print(f"Width: {self.width}, Height: {self.height}")
        print(f"Area: {area}, Perimeter: {perimeter}")

    def scale(self, factor):
        self.width = self.width * factor
        self.height = self.height * factor

rect = Rectangle()
rect.width = 5
rect.height = 3

rect.display_info()
# Width: 5, Height: 3
# Area: 15, Perimeter: 16

rect.scale(2)
rect.display_info()
# Width: 10, Height: 6
# Area: 60, Perimeter: 32

# Bank Account example
class BankAccount:
    def deposit(self, amount):
        self.balance = self.balance + amount
        print(f"Deposited ${amount}. New balance: ${self.balance}")

    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance = self.balance - amount
            print(f"Withdrew ${amount}. New balance: ${self.balance}")
        else:
            print("Insufficient funds!")

    def check_balance(self):
        print(f"Current balance: ${self.balance}")

account = BankAccount()
account.balance = 1000
account.check_balance()      # Current balance: $1000
account.deposit(500)         # Deposited $500. New balance: $1500
account.withdraw(200)        # Withdrew $200. New balance: $1300
account.withdraw(2000)       # Insufficient funds!

# Important: understanding self
class Car:
    def honk(self):
        print(f"The {self.color} car goes HONK!")

car1 = Car()
car1.color = "red"

car2 = Car()
car2.color = "blue"

car1.honk()  # The red car goes HONK!
car2.honk()  # The blue car goes HONK!
# Notice how each object has its own color!
```

### Guided Practice

**Activity: Create a BankAccount Class with Methods**

Follow these steps:

1. Create a class called `BankAccount`
2. Add a method called `deposit` that adds money to the balance
3. Add a method called `withdraw` that removes money (check for sufficient funds)
4. Add a method called `display_balance` that prints the current balance
5. Create two account objects, perform deposits and withdrawals, and display balances

**Expected Output:**
```
Account holder: Alice
Current balance: $1000
Deposited $500
Current balance: $1500
Withdrew $200
Current balance: $1300

Account holder: Bob
Current balance: $500
Deposited $1000
Current balance: $1500
Withdrew $800
Current balance: $700
```

**Solution:**
```python
class BankAccount:
    def deposit(self, amount):
        self.balance = self.balance + amount
        print(f"Deposited ${amount}")

    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance = self.balance - amount
            print(f"Withdrew ${amount}")
        else:
            print("Cannot withdraw - insufficient funds!")

    def display_balance(self):
        print(f"Current balance: ${self.balance}")

account1 = BankAccount()
account1.holder = "Alice"
account1.balance = 1000
print(f"Account holder: {account1.holder}")
account1.display_balance()
account1.deposit(500)
account1.display_balance()
account1.withdraw(200)
account1.display_balance()

print()

account2 = BankAccount()
account2.holder = "Bob"
account2.balance = 500
print(f"Account holder: {account2.holder}")
account2.display_balance()
account2.deposit(1000)
account2.display_balance()
account2.withdraw(800)
account2.display_balance()
```

### Practice Problems

**Problem 1 — Beginner:** Create a class called `Animal` with two methods: `eat()` that prints "[animal name] is eating" and `sleep()` that prints "[animal name] is sleeping". Create two animal objects, set their names, and call both methods on each.

**Problem 2 — Intermediate:** Create a class called `GradeTracker` with methods: `add_grade(grade)` to add a grade to a list, `calculate_average()` to compute the average, and `display_stats()` to print the count of grades and the average. Create a student object and add 5 grades.

**Problem 3 — Challenge:** Create a class called `Shape` with a method `describe()` that prints information about the shape. Create subclasses for `Circle` and `Square` with attributes like `radius` or `side`, and methods to calculate `area()`. Override `describe()` to show specific information for each shape.

<details>
<summary>💡 Hints</summary>

**Hint 1:** Remember to use `self.` when accessing object attributes inside methods.

**Hint 2:** For Problem 2, you'll need to use a list to store grades. Use `append()` to add to the list and `sum()` / `len()` to calculate average.

**Hint 3:** For Problem 3, you'll learn more about subclasses soon, but try to understand the concept of multiple classes working together.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Animal:
    def eat(self):
        print(f"{self.name} is eating")

    def sleep(self):
        print(f"{self.name} is sleeping")

animal1 = Animal()
animal1.name = "Lion"
animal1.eat()
animal1.sleep()

animal2 = Animal()
animal2.name = "Elephant"
animal2.eat()
animal2.sleep()

# Problem 2
class GradeTracker:
    def __init__(self):
        self.grades = []

    def add_grade(self, grade):
        self.grades.append(grade)

    def calculate_average(self):
        if len(self.grades) == 0:
            return 0
        return sum(self.grades) / len(self.grades)

    def display_stats(self):
        avg = self.calculate_average()
        print(f"Number of grades: {len(self.grades)}")
        print(f"Average grade: {avg:.2f}")

tracker = GradeTracker()
tracker.add_grade(90)
tracker.add_grade(85)
tracker.add_grade(92)
tracker.add_grade(88)
tracker.add_grade(95)
tracker.display_stats()

# Problem 3
import math

class Shape:
    def describe(self):
        print("I am a shape")

class Circle(Shape):
    def area(self):
        return math.pi * self.radius ** 2

    def describe(self):
        print(f"Circle with radius {self.radius}")
        print(f"Area: {self.area():.2f}")

class Square(Shape):
    def area(self):
        return self.side ** 2

    def describe(self):
        print(f"Square with side {self.side}")
        print(f"Area: {self.area():.2f}")

circle = Circle()
circle.radius = 5
circle.describe()

square = Square()
square.side = 4
square.describe()
```

</details>
