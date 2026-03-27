# Day 12: Method Overriding
**Learning Target:** I can override parent methods in child classes to provide specialized behavior.

### Key Concepts

**Method Overriding:** Defining a method in a child class that has the same name as a method in the parent class, replacing the parent's implementation.

**Polymorphism in Action:** Using the same method name on different objects, where each object responds according to its class.

**@override Convention:** Using the `@override` annotation (or comment) to make it clear a method is overridden.

**Signature Compatibility:** Child method should have the same parameters as parent method (or compatible parameters).

### Code Examples

```python
# Simple override example
class Animal:
    def speak(self):
        print("Animal makes a sound")

class Dog(Animal):
    def speak(self):  # Override
        print("Dog barks: Woof!")

class Cat(Animal):
    def speak(self):  # Override
        print("Cat meows: Meow!")

dog = Dog()
dog.speak()  # Dog barks: Woof!

cat = Cat()
cat.speak()  # Cat meows: Meow!

# Polymorphism: same method, different behaviors
animals = [Dog(), Cat(), Animal()]
for animal in animals:
    animal.speak()
# Dog barks: Woof!
# Cat meows: Meow!
# Animal makes a sound

# Shape example
class Shape:
    def area(self):
        return 0

    def describe(self):
        print(f"This is a shape with area {self.area()}")

class Circle:
    import math

    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

    def describe(self):  # Override
        print(f"Circle with radius {self.radius}, area {self.area():.2f}")

class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def describe(self):  # Override
        print(f"Rectangle {self.width}x{self.height}, area {self.area()}")

circle = Circle(5)
circle.describe()  # Circle with radius 5, area 78.54

rect = Rectangle(4, 6)
rect.describe()  # Rectangle 4x6, area 24

# Employee salary calculation with override
class Employee:
    def __init__(self, name, base_salary):
        self.name = name
        self.base_salary = base_salary

    def calculate_pay(self):
        return self.base_salary

    def display_pay(self):
        pay = self.calculate_pay()
        print(f"{self.name}: ${pay}")

class Manager(Employee):
    def __init__(self, name, base_salary, bonus_percent):
        super().__init__(name, base_salary)
        self.bonus_percent = bonus_percent

    def calculate_pay(self):  # Override
        base = super().calculate_pay()
        bonus = base * (self.bonus_percent / 100)
        return base + bonus

class HourlyWorker(Employee):
    def __init__(self, name, hourly_rate, hours_worked):
        super().__init__(name, hourly_rate * hours_worked)
        self.hourly_rate = hourly_rate
        self.hours_worked = hours_worked

    def calculate_pay(self):  # Override
        if self.hours_worked > 40:
            overtime_pay = (self.hours_worked - 40) * self.hourly_rate * 1.5
            regular_pay = 40 * self.hourly_rate
            return regular_pay + overtime_pay
        return self.base_salary

emp = Employee("Alice", 50000)
emp.display_pay()  # Alice: $50000

mgr = Manager("Bob", 60000, 10)
mgr.display_pay()  # Bob: $66000

worker = HourlyWorker("Charlie", 20, 45)
worker.display_pay()  # Charlie: $950

# Game character override example
class Character:
    def __init__(self, name, health):
        self.name = name
        self.health = health

    def take_damage(self, damage):
        self.health = max(0, self.health - damage)
        print(f"{self.name} takes {damage} damage!")

    def get_status(self):
        return f"{self.name}: {self.health} HP"

class Warrior(Character):
    def take_damage(self, damage):  # Override with armor
        reduced_damage = damage // 2  # Armor reduces damage
        super().take_damage(reduced_damage)  # Call parent with reduced damage

class Mage(Character):
    def take_damage(self, damage):  # Override with shield
        if self.health > 50:
            damage = damage - 20  # Shield absorbs 20 damage
        super().take_damage(damage)

class Rogue(Character):
    def take_damage(self, damage):  # Override with dodge
        import random
        if random.random() < 0.3:  # 30% chance to dodge
            print(f"{self.name} dodges!")
            return
        super().take_damage(damage)

warrior = Warrior("Barbarian", 100)
warrior.take_damage(50)  # Takes 25 damage (armor reduction)
print(warrior.get_status())  # Barbarian: 75 HP
print()

mage = Mage("Wizard", 60)
mage.take_damage(50)  # Takes 30 damage (shield absorption)
print(mage.get_status())  # Wizard: 30 HP
print()

rogue = Rogue("Assassin", 80)
rogue.take_damage(40)  # Might dodge or take damage
print(rogue.get_status())

# Vehicle speed calculation
class Vehicle:
    def __init__(self, name, max_speed):
        self.name = name
        self.max_speed = max_speed

    def get_speed(self, throttle):
        # throttle: 0 to 1 (0% to 100%)
        return self.max_speed * throttle

    def accelerate(self, throttle):
        speed = self.get_speed(throttle)
        print(f"{self.name} accelerates to {speed:.1f} mph")

class ElectricCar(Vehicle):
    def get_speed(self, throttle):  # Override
        # Electric cars have instant torque
        speed = super().get_speed(throttle)
        return speed * 1.2  # 20% boost

class Truck(Vehicle):
    def get_speed(self, throttle):  # Override
        # Trucks are slower when fully loaded
        speed = super().get_speed(throttle)
        return speed * 0.8  # 20% reduction

car = Vehicle("Normal Car", 120)
car.accelerate(0.75)  # 90.0 mph

ecar = ElectricCar("Tesla", 120)
ecar.accelerate(0.75)  # 108.0 mph (20% faster)

truck = Truck("Heavy Truck", 120)
truck.accelerate(0.75)  # 72.0 mph (20% slower)

# String representation override
class Product:
    def __init__(self, name, price):
        self.name = name
        self.price = price

    def get_info(self):
        return f"{self.name}: ${self.price}"

class DiscountedProduct(Product):
    def __init__(self, name, price, discount):
        super().__init__(name, price)
        self.discount = discount

    def get_info(self):  # Override to show discount
        base_info = super().get_info()
        original = self.price / (1 - self.discount)
        return f"{base_info} (was ${original:.2f}, {int(self.discount*100)}% off)"

prod = Product("Book", 15)
print(prod.get_info())  # Book: $15

dprod = DiscountedProduct("Book", 12, 0.2)
print(dprod.get_info())  # Book: $12 (was $15.00, 20% off)
```

### Guided Practice

**Activity: Create a Bank Account Override System**

Follow these steps:

1. Create `BankAccount` with `calculate_interest()` method (5% default)
2. Create `PremiumAccount(BankAccount)` that overrides to 7% interest
3. Create `StudentAccount(BankAccount)` that overrides to 0% interest (no fees)
4. Create 3 accounts and apply interest to each

**Expected Output:**
```
Regular account: $1000 + $50 interest = $1050
Premium account: $1000 + $70 interest = $1070
Student account: $1000 + $0 interest = $1000
```

**Solution:**
```python
class BankAccount:
    def __init__(self, holder, balance):
        self.holder = holder
        self._balance = balance

    def calculate_interest(self):
        return self._balance * 0.05

    def apply_interest(self):
        interest = self.calculate_interest()
        self._balance = self._balance + interest
        return interest

    def display(self):
        print(f"{self.holder} account: ${self._balance}")

class PremiumAccount(BankAccount):
    def calculate_interest(self):
        return self._balance * 0.07

class StudentAccount(BankAccount):
    def calculate_interest(self):
        return 0  # No interest

regular = BankAccount("Regular", 1000)
premium = PremiumAccount("Premium", 1000)
student = StudentAccount("Student", 1000)

r_interest = regular.apply_interest()
print(f"Regular account: $1000 + ${r_interest} interest = ${regular._balance}")

p_interest = premium.apply_interest()
print(f"Premium account: $1000 + ${p_interest} interest = ${premium._balance}")

s_interest = student.apply_interest()
print(f"Student account: $1000 + ${s_interest} interest = ${student._balance}")
```

### Practice Problems

**Problem 1 — Beginner:** Create a `Drink` class with `get_calories()` returning 0. Override in `Coffee` (5), `Soda` (150), and `Water` (0). Create an array of drinks and calculate total calories.

**Problem 2 — Intermediate:** Create `Weapon` with `get_damage()`. Override in `Sword` (50), `Bow` (35), `Magic Staff` (60). Override in `Enchanted` version of each to add 20 bonus damage.

**Problem 3 — Challenge:** Create `Animal` with `move()`. Override appropriately for `Fish` (swim), `Bird` (fly), `Dog` (run). Create a mixed array and call move on each.

<details>
<summary>💡 Hints</summary>

**Hint 1:** When overriding, the method name must be identical to the parent method.

**Hint 2:** You can call the parent method using `super()` and then add extra logic.

**Hint 3:** For Problem 2, create a base Weapon class, then inherit Enchanted versions.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Drink:
    def get_calories(self):
        return 0

class Coffee(Drink):
    def get_calories(self):
        return 5

class Soda(Drink):
    def get_calories(self):
        return 150

class Water(Drink):
    def get_calories(self):
        return 0

drinks = [Coffee(), Soda(), Water(), Coffee()]
total = sum(drink.get_calories() for drink in drinks)
print(f"Total calories: {total}")

# Problem 2
class Weapon:
    def get_damage(self):
        return 0

class Sword(Weapon):
    def get_damage(self):
        return 50

class Bow(Weapon):
    def get_damage(self):
        return 35

class Staff(Weapon):
    def get_damage(self):
        return 60

class EnchantedWeapon(Weapon):
    def __init__(self, base_weapon):
        self.base = base_weapon

    def get_damage(self):
        return self.base.get_damage() + 20

sword = Sword()
enchanted_sword = EnchantedWeapon(sword)
print(f"Sword: {sword.get_damage()}")
print(f"Enchanted Sword: {enchanted_sword.get_damage()}")

# Problem 3
class Animal:
    def move(self):
        print("Moving...")

class Fish(Animal):
    def move(self):
        print("Swimming...")

class Bird(Animal):
    def move(self):
        print("Flying...")

class Dog(Animal):
    def move(self):
        print("Running...")

animals = [Fish(), Bird(), Dog(), Fish()]
for animal in animals:
    animal.move()
```

</details>
