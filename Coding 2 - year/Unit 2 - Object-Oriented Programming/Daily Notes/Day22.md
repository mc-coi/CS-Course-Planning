# Day 22: Composition vs Inheritance
**Learning Target:** I can choose between composition and inheritance when designing classes.

### Key Concepts

**Inheritance (Is-A):** "A dog IS-A animal"—child class is a type of parent class.

**Composition (Has-A):** "A dog HAS-A tail"—object contains another object as a part.

**When to Use Inheritance:** When there's a true is-A relationship and behavior is shared.

**When to Use Composition:** For flexibility and avoiding tight coupling.

**"Favor Composition Over Inheritance":** A design principle that composition is often more flexible than inheritance.

### Code Examples

```python
# Inheritance example
class Animal:
    def eat(self):
        print("Eating...")

class Dog(Animal):
    def bark(self):
        print("Woof!")

dog = Dog()
dog.eat()   # From parent
dog.bark()  # Own method

# Problem: What if we have a class that's not an animal?
# class Robot(Animal):  # Wrong! Robot IS-A Animal? No!

# Composition example
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()

car = Car()
car.start()  # Car HAS-A engine

# Better design: Animal behavior as composition
class Running:
    def run(self):
        print("Running...")

class Swimming:
    def swim(self):
        print("Swimming...")

class Flying:
    def fly(self):
        print("Flying...")

class Dog:
    def __init__(self):
        self.runner = Running()
        self.swimmer = Swimming()

    def run(self):
        self.runner.run()

    def swim(self):
        self.swimmer.swim()

class Bird:
    def __init__(self):
        self.flyer = Flying()
        self.runner = Running()

    def fly(self):
        self.flyer.fly()

    def run(self):
        self.runner.run()

dog = Dog()
dog.run()
dog.swim()

bird = Bird()
bird.fly()
bird.run()

# Multiple inheritance problems (The Diamond Problem)
class Athlete:
    def train(self):
        print("Training...")

class Swimmer:
    def train(self):
        print("Swimming training...")

class RunningAthlete:
    def train(self):
        print("Running training...")

# Bad: What if class Triathlete(Swimmer, RunningAthlete)?
# Which train() method should it use?

# Better with composition:
class Triathlete:
    def __init__(self):
        self.swim_training = SwimmingCoach()
        self.run_training = RunningCoach()

    def train_swimming(self):
        self.swim_training.coach()

    def train_running(self):
        self.run_training.coach()

# Personnel system
# Bad inheritance design:
class Employee:
    def work(self):
        print("Working...")

class Manager(Employee):
    def manage(self):
        print("Managing team...")

class Developer(Employee):
    def code(self):
        print("Coding...")

# Problem: What if someone is both manager and developer?
# class TechLead(Manager, Developer):  # Awkward!

# Better with composition:
class Employee:
    def __init__(self, name):
        self.name = name
        self.roles = []

    def add_role(self, role):
        self.roles.append(role)

    def perform_duties(self):
        for role in self.roles:
            role.perform_duty()

class ManagerRole:
    def perform_duty(self):
        print("Managing team...")

class DeveloperRole:
    def perform_duty(self):
        print("Writing code...")

employee = Employee("Alice")
employee.add_role(DeveloperRole())
employee.add_role(ManagerRole())
employee.perform_duties()

# Game character system
# Bad: Deep inheritance
class Character:
    pass

class Fighter(Character):
    pass

class Archer(Fighter):
    pass

class MageArcher(Archer):
    pass

# Good: Composition approach
class Ability:
    @abstractmethod
    def use(self):
        pass

class MagicAbility(Ability):
    def use(self):
        print("Using magic...")

class ArcheryAbility(Ability):
    def use(self):
        print("Using bow...")

class FightingAbility(Ability):
    def use(self):
        print("Using sword...")

class Character:
    def __init__(self, name):
        self.name = name
        self.abilities = []

    def add_ability(self, ability):
        self.abilities.append(ability)

    def use_abilities(self):
        for ability in self.abilities:
            ability.use()

character = Character("Hero")
character.add_ability(FightingAbility())
character.add_ability(ArcheryAbility())
character.add_ability(MagicAbility())
character.use_abilities()

# Vehicle example
# Problem with inheritance
class Vehicle:
    def move(self):
        pass

class Car(Vehicle):
    def move(self):
        print("Driving...")

class Plane(Vehicle):
    def move(self):
        print("Flying...")

class AmphibiousCar(Car, Plane):  # Problem: which move()?
    pass

# Better with composition
class GroundTransport:
    def move(self):
        print("Driving...")

class AirTransport:
    def move(self):
        print("Flying...")

class AmphibiousCar:
    def __init__(self):
        self.ground = GroundTransport()
        self.air = AirTransport()

    def drive(self):
        self.ground.move()

    def fly(self):
        self.air.move()

# When inheritance IS appropriate
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "Some sound"

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

# This IS inheritance done right:
# - Dog IS-A Animal (true is-A relationship)
# - Share common attributes (name)
# - Override specific behavior (speak)
# - Polymorphic collection

animals = [Dog("Buddy"), Cat("Whiskers"), Animal("Thing")]
for animal in animals:
    print(f"{animal.name}: {animal.speak()}")

# Composition with shared behavior
class Shape:
    def __init__(self, color):
        self._color = color

    @property
    def color(self):
        return self._color

class Drawable:
    def draw(self):
        print("Drawing...")

class Circle:
    def __init__(self, radius, color):
        self.radius = radius
        self.shape = Shape(color)
        self.drawable = Drawable()

    def draw(self):
        self.drawable.draw()

    @property
    def color(self):
        return self.shape.color

# Refactoring from inheritance to composition
# Original (bad):
class Button:
    def click(self):
        pass

class BlueButton(Button):
    pass

class RedButton(Button):
    pass

# Better:
class Button:
    def __init__(self, color):
        self.color = color

    def click(self):
        print(f"Clicked {self.color} button")

# Or even better with strategy pattern:
class Color:
    def describe(self):
        pass

class BlueColor(Color):
    def describe(self):
        return "blue"

class Button:
    def __init__(self, color: Color):
        self.color = color

    def click(self):
        print(f"Clicked {self.color.describe()} button")
```

### Guided Practice

**Activity: Refactor from Inheritance to Composition**

Start with this problematic design:

```python
class Weapon:
    def attack(self):
        pass

class Sword(Weapon):
    def attack(self):
        print("Slash!")

class Bow(Weapon):
    def attack(self):
        print("Arrow!")

class Character(Weapon):  # Problem! Character IS-A Weapon?
    def attack(self):
        pass
```

Refactor using composition:

```python
class Weapon:
    def attack(self):
        pass

class Sword(Weapon):
    def attack(self):
        print("Slash!")

class Bow(Weapon):
    def attack(self):
        print("Arrow!")

class Character:
    def __init__(self, name, weapon):
        self.name = name
        self.weapon = weapon

    def attack(self):
        self.weapon.attack()

character = Character("Archer", Bow())
character.attack()

character.weapon = Sword()
character.attack()
```

### Decision Matrix

Use **Inheritance** when:
- True is-A relationship exists
- You want to enforce a common interface
- Child classes override some methods but share others
- You need polymorphic behavior

Use **Composition** when:
- Has-A relationship is more accurate
- You want flexibility to change behavior at runtime
- You need to avoid deep inheritance hierarchies
- An object needs multiple behaviors
- You want to reduce coupling

### Practice Problems

**Problem 1:** Identify whether each relationship should use inheritance or composition:
- Dog and Animal
- Car and Engine
- Employee and Salary
- Student and Course

**Problem 2:** Refactor a class hierarchy with 4+ levels into composition.

**Problem 3:** Design a flexible weapon system using composition instead of inheritance.

### Key Takeaways

1. Inheritance creates tight coupling between parent and child
2. Composition is more flexible and easier to change
3. Inheritance should only be used for true is-A relationships
4. Deep inheritance hierarchies are often a sign of bad design
5. Modern OOP favors composition over inheritance for flexibility
