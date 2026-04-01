# Unit 2 - Object-Oriented Programming: Teacher Misconception & Callout Guide

## Overview

Unit 2 is where Coding 2 truly gets challenging. OOP is conceptually slippery—students will confuse `self` with global state, think classes are just "fancy functions," misunderstand when to use `self` vs. class variables, and struggle deeply with inheritance and `super()`. The biggest risk: students will write syntactically correct OOP code without understanding *why* objects separate concerns. They'll create classes they could have written as functions. Watch for shallow understanding: they memorize `__init__` and `def method(self)` but don't grasp encapsulation, message passing, or polymorphism. This unit makes or breaks everything downstream (Unit 3's recursion, Unit 6's APIs with libraries that use OOP patterns).

---

## Misconceptions by Topic

### Classes, Objects, and `self` (Days 1–2)

**⚠️ Misconception:** "`self` is a global variable. I can use `self` anywhere in my program."

**What it looks like in code:**
```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print(self.name + " barks!")

# Student then tries:
print(self.name)  # NameError: name 'self' is not defined
```

**Why students think this:** The word "self" sounds global. They don't understand that `self` only exists *inside* method calls as a parameter.

**How to address it:** Explain: "**`self` is a parameter.** Every method receives it automatically. Outside a method, there's no `self`. It's like a function parameter—it only exists inside the function." Draw the flow:
```
dog1.bark()
    ↓
    Python calls: Dog.bark(dog1)  # dog1 becomes self
    ↓
    Inside bark(): self = dog1
```

---

**⚠️ Misconception:** "I create a class, but I don't need `__init__`. I can set attributes directly whenever."

**What it looks like in code:**
```python
class Dog:
    def bark(self):
        print(f"{self.name} barks!")

dog1 = Dog()
dog1.name = "Buddy"  # Setting attribute without __init__
dog1.bark()  # Works, but bad practice
```

**Why students think this:** Python allows it. They don't see why initialization matters.

**How to address it:** Show the danger:
```python
dog1 = Dog()
dog2 = Dog()
dog1.name = "Buddy"
# dog2.name is undefined — crash when dog2 tries to bark()
```
Explain: "`__init__` ensures every object starts in a valid state. It's a contract: 'every Dog has a name.' Without it, you'll have bugs."

---

**⚠️ Misconception:** "Instance variables and class variables are the same. `self.x = 5` and `ClassName.x = 5` do the same thing."

**What it looks like in code:**
```python
class Student:
    school = "Lincoln"  # Class variable

    def __init__(self, name):
        self.name = name  # Instance variable
        # Student doesn't realize school and name are fundamentally different
        self.school = "Lincoln"  # Instance variable shadowing class variable

s1 = Student("Alice")
s2 = Student("Bob")
print(s1.school)  # "Lincoln"
print(s2.school)  # "Lincoln"
s1.school = "Central"
print(s1.school)  # "Central"
print(s2.school)  # "Lincoln" — student is confused
```

**Why students think this:** Both use dot notation. The difference feels subtle.

**How to address it:** Use a shared counter example:
```python
class Student:
    total = 0  # CLASS variable — shared by ALL students

    def __init__(self, name):
        self.name = name  # INSTANCE variable — unique to each student
        Student.total += 1  # Increment the shared counter

s1 = Student("Alice")
s2 = Student("Bob")
print(s1.name)   # "Alice" — only s1 has this name
print(s2.name)   # "Bob" — s2 has a different name
print(Student.total)  # 2 — both students share this
```
Teach: "Instance variables = unique to each object. Class variables = shared by all objects."

---

**⚠️ Misconception:** "I don't need `__init__`. I can call a `setup()` method instead."

**What it looks like in code:**
```python
class Dog:
    def setup(self, name):
        self.name = name

dog = Dog()
# Student forgets to call setup()
dog.bark()  # AttributeError: 'Dog' object has no attribute 'name'
```

**Why students think this:** Method names are arbitrary, so why not?

**How to address it:** Explain: "`__init__` is **special**. Python calls it automatically when you create an object. A custom method like `setup()` you have to remember to call—which you'll forget. Always use `__init__`."

---

### Methods and Interactions Between Objects (Day 3)

**⚠️ Misconception:** "Methods are just functions. I can call them without an object."

**What it looks like in code:**
```python
class Dog:
    def bark(self):
        return "Woof!"

bark()  # NameError: name 'bark' is not defined
Dog.bark()  # TypeError: bark() missing 1 required positional argument: 'self'
```

**Why students think this:** In procedural code, they call functions directly.

**How to address it:** Emphasize: "Methods live *inside* the object. To call a method, you need an object. `dog.bark()` means 'ask dog to bark.' The dog is passed as `self` automatically."

---

**⚠️ Misconception:** "If two objects have the same method, they'll interfere with each other."

**What it looks like in code:**
```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        return f"{self.name} barks!"

dog1 = Dog("Buddy")
dog2 = Dog("Lucy")

print(dog1.bark())  # "Buddy barks!"
print(dog2.bark())  # "Lucy barks!"
# Student expects them to interfere, but they don't
```

**Why students think this:** They don't understand that each object has its own `self`.

**How to address it:** Show that `self` **changes**:
```
dog1.bark() → Dog.bark(dog1) → self = dog1
dog2.bark() → Dog.bark(dog2) → self = dog2
# Each call has its own self!
```

---

### Instance vs Class Variables (Day 2)

**⚠️ Misconception:** "I should use class variables to store counts because they're 'global' and easier."

**What it looks like in code:**
```python
class Player:
    total_players = 0

    def __init__(self, name):
        self.name = name
        Player.total_players += 1

p1 = Player("Alice")
p2 = Player("Bob")
print(Player.total_players)  # 2 — okay

# But then student does:
class Enemy:
    total_count = 0  # Another count

    def __init__(self):
        Enemy.total_count += 1

# And confuses the two counts or thinks they share the same class variable
```

**Why students think this:** Class variables feel like global variables, which are simpler.

**How to address it:** Teach: "Class variables are for data **shared by all objects of that class**. Use them for counts, constants, or shared config. Don't use them as a substitute for globals—it's still messy."

---

### Special Methods / Dunder Methods (Day 4–5)

**⚠️ Misconception:** "`__str__` and `__repr__` do the same thing."

**What it looks like in code:**
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"({self.x}, {self.y})"

    # Student forgets __repr__ or thinks they're identical
p = Point(3, 4)
print(p)  # __str__: (3, 4)
print(repr(p))  # __repr__: <Point object at 0x...> (default)
```

**Why students think this:** Both return strings representing the object.

**How to address it:** Teach the distinction:
- **`__str__`** is for **users**. Make it friendly: `"Point(3, 4)"`.
- **`__repr__`** is for **developers/debugging**. Make it official/reproducible: `"Point(x=3, y=4)"` or even code you could paste.

Show:
```python
def __repr__(self):
    return f"Point({self.x}, {self.y})"
```

---

**⚠️ Misconception:** "I don't know which dunder methods to implement. I'll implement all of them."

**What it looks like in code:**
```python
class MyClass:
    def __init__(self):
        pass

    def __str__(self): pass
    def __repr__(self): pass
    def __len__(self): pass
    def __eq__(self): pass
    def __add__(self): pass
    def __iter__(self): pass
    # ... implementing everything out of cargo-cult instinct
```

**Why students think this:** They're unsure, so they over-implement.

**How to address it:** Guide: "Implement dunder methods **as needed** based on how you'll use the object. Does it need to be printed? `__str__`. Will you compare two objects? `__eq__`. Will you add them? `__add__`. Start minimal."

---

### Inheritance and `super()` (Days 6–8)

**⚠️ Misconception:** "`super()` means 'call the parent class.' I should use it whenever I override a method."

**What it looks like in code:**
```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)  # Good
        self.breed = breed

# But then in another method:
class Animal:
    def speak(self):
        return "Some sound"

class Dog(Animal):
    def speak(self):
        return super().speak() + " WOOF!"  # Unnecessary?
```

**Why students think this:** They learn `super()` and apply it everywhere.

**How to address it:** Teach: "`super()` is for **reusing parent code**. Use it when the parent does something you want to keep. In `__init__`, almost always use `super().__init__()`. In other methods, only if you want to extend parent behavior."

---

**⚠️ Misconception:** "I can override a method and completely change what it does. The parent version doesn't matter."

**What it looks like in code:**
```python
class Shape:
    def area(self):
        """Returns the area."""
        return 0

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        """Returns the area."""
        return self.width * self.height

# Okay so far, but then:
class Circle(Shape):
    def area(self):
        """Returns the circumference instead."""
        return 2 * 3.14 * self.radius
        # Wait, this returns circumference, not area!
```

**Why students think this:** Overriding feels like "I can do whatever I want."

**How to address it:** Teach: "**Override only when the method's purpose stays the same.** If `area()` means 'return the area,' all subclasses must return the area. If you need to return circumference, create a new method `circumference()`. Violating the parent's contract breaks polymorphism."

---

**⚠️ Misconception:** "I have to call `super().__init__()`. If I don't, the program crashes."

**What it looks like in code:**
```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        # Forgot super().__init__(name)
        self.breed = breed

dog = Dog("Buddy", "Labrador")
print(dog.name)  # AttributeError: 'Dog' object has no attribute 'name'
```

**Why students think this:** They're told "always call `super().__init__()`" and assume it's a hard rule.

**How to address it:** Clarify: "Call `super().__init__()` **if the parent needs to set up state**. If the parent does nothing, you don't need to call it. But usually, yes, call it."

---

**⚠️ Misconception:** "`self` in a child class points to the parent class."

**What it looks like in code:**
```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed

    def info(self):
        # self still points to the Dog object, not the Animal
        return f"{self.name} ({self.breed})"
```

**Why students think this:** They conflate inheritance with `self` changing.

**How to address it:** Emphasize: "`self` **always** points to the object you called the method on. If you call a method on a Dog, `self` is a Dog. The parent's `__init__` receives the same `self`."

---

### Encapsulation and Access Control (Days 9–10)

**⚠️ Misconception:** "Using `_private` or `__private` actually prevents access. It's like `private` in Java."

**What it looks like in code:**
```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

account = BankAccount(1000)
print(account.__balance)  # AttributeError — okay
print(account._BankAccount__balance)  # Works! Student is shocked.
```

**Why students think this:** Python has the syntax, so it must be enforcing privacy.

**How to address it:** Explain: "Python **doesn't enforce privacy**. `__private` is just a *signal* and name-mangling trick. It says 'don't use this from outside.' But Python won't stop you. It's about **convention and trust**, not security."

---

**⚠️ Misconception:** "Properties (`@property`) are just a shortcut for getter methods. I can use `.get_balance()` just as well."

**What it looks like in code:**
```python
class Account:
    def __init__(self, balance):
        self._balance = balance

    # Student avoids property:
    def get_balance(self):
        return self._balance

account = Account(1000)
balance = account.get_balance()  # Works, but not Pythonic

# Instead of:
class Account:
    def __init__(self, balance):
        self._balance = balance

    @property
    def balance(self):
        return self._balance

account = Account(1000)
balance = account.balance  # Cleaner!
```

**Why students think this:** Methods and properties both do the same thing.

**How to address it:** Teach: "Properties let you access data like an attribute (`account.balance`) but run code behind the scenes (validation, computation). It's **Pythonic**. Use properties when you want validation or computed values."

---

### Composition vs Inheritance (Days 11–12)

**⚠️ Misconception:** "Inheritance is always the right choice. I should make a hierarchy for everything."

**What it looks like in code:**
```python
# Student creates a deep hierarchy:
class Entity:
    pass

class LivingThing(Entity):
    pass

class Animal(LivingThing):
    pass

class Dog(Animal):
    pass

# This is silly. Should just be class Dog or use composition.
```

**Why students think this:** They learned inheritance first and think it's the only tool.

**How to address it:** Teach the decision:
- **Inheritance:** "Is-a" relationships. A Dog *is-an* Animal. Makes sense.
- **Composition:** "Has-a" relationships. A Car *has-an* Engine. Combine objects with different jobs.

Show:
```python
# Bad inheritance hierarchy:
class Game:
    pass

class Chess(Game):
    pass

class Checkers(Game):
    pass

# Better with composition:
class Game:
    def __init__(self, rules):
        self.rules = rules

class ChessRules:
    pass

chess = Game(ChessRules())
```

---

**⚠️ Misconception:** "If I use inheritance, the child automatically has all the parent's methods and I don't need to override anything."

**What it looks like in code:**
```python
class Animal:
    def speak(self):
        return "Some sound"

class Dog(Animal):
    pass

dog = Dog()
print(dog.speak())  # "Some sound" — works, but generic

# Student then overrides it correctly in practice, but doesn't *understand* that inheritance passes down behavior
```

**Why students think this:** They understand inheritance works, but not *why*.

**How to address it:** Explain: "Inheritance **passes down behavior**. The child can use it as-is or override it. This is powerful for code reuse. But each child should adapt behavior to its own needs—a Dog speaks differently than a Cat."

---

### Abstract Classes (Days 13–14)

**⚠️ Misconception:** "Abstract classes are too advanced. I'll just use regular classes and document what subclasses should do."

**What it looks like in code:**
```python
# Bad:
class Shape:
    def area(self):
        """Subclasses should override this."""
        pass

# Student creates Circle without implementing area()
class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    # Forgot to implement area()!

circle = Circle(5)
print(circle.area())  # None — bug!
```

**Why students think this:** Abstract classes feel like "advanced OOP" and they don't see the point.

**How to address it:** Show the power:
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    # Forgot to implement area()
    pass

circle = Circle(5)  # TypeError: Can't instantiate abstract class Circle
# Python catches the error at object creation!
```

Teach: "Abstract classes **force** subclasses to implement required methods. It's like a contract. Without it, you'll forget and find bugs later."

---

## Whole-Class Warning Signs

- **Students are writing classes that read like procedural code with no `self` usage** — they created a class that should be functions. Pause and ask: "What is the purpose of your class? What state does each object hold?"
- **Students create classes but always access them via `ClassName.method()` instead of `obj.method()`** — they don't understand instantiation. Show: "Create objects first: `obj = ClassName()`. Then call methods on the object."
- **Students are avoiding `super()` or not calling it in `__init__`** — their child classes don't inherit parent state. Pair program one example using `super().__init__()`.
- **Students aren't using `@property` for validation** — they write getter/setter methods manually. Show one `@property` example; they'll see the elegance.
- **Students are using double-underscore `__private` to "hide" data, thinking it's secure** — explain name-mangling and convention. Use single underscore `_protected` as the Pythonic way.
- **Students are creating deep inheritance hierarchies (3+ levels) without a good reason** — suggest composition instead. Do a refactoring exercise.
- **Students override methods but change their meaning** — e.g., `area()` returns circumference. Teach polymorphism: override to *extend* or *specialize*, not to *change the contract*.

---

## Questions That Reveal Understanding

1. **"Create a `Dog` class. A dog has a name. Write the class definition, then create two dog objects with different names."**
   - If they can do this, they understand `__init__`, `self`, and instantiation.
   - If they don't use `__init__` or set attributes correctly: they don't grasp initialization.

2. **"You have a `BankAccount` class with a `balance` attribute. Write a method to deposit money. How do you make sure the balance is never negative?"**
   - If they use validation in the method or `@property`: they understand encapsulation.
   - If they just modify `self.balance` directly: they don't see the need to protect data.

3. **"Why would you use a class variable instead of an instance variable?"**
   - If they can give an example (count of objects, shared constant): they understand the difference.
   - If they don't answer or are confused: reteach with a concrete counter example.

4. **"You have an `Animal` class with a `speak()` method. A `Dog` class inherits from `Animal`. When you call `dog.speak()`, which method runs?"**
   - If they say `Dog.speak()` (if it exists), else `Animal.speak()`: polymorphism is understood.
   - If they're confused about the order or think both run: clarify method resolution order (MRO).

5. **"What does `super().__init__(name)` do in a child class?"**
   - If they say "calls the parent's constructor to set up inherited state": correct.
   - If they don't know or say "calls something else": reteach with a visual diagram.

6. **"You create a `Vector` class with `x` and `y`. How would you make `v1 + v2` work (add two vectors)?"**
   - If they write `__add__`: correct.
   - If they don't know: show the dunder method and explain Python uses these for operators.

7. **"When is composition better than inheritance?"**
   - If they give an example like "a Car has-an Engine, not is-an Engine": they grasp the distinction.
   - If they always pick inheritance: they haven't internalized the trade-off.

---

## Common Student Questions & How to Answer Them

**Q: "Why do I need `self`? Why can't I just use the variable name directly?"**
A: "Great question. Without `self`, Python wouldn't know which object you're talking about. If you have two Dogs named Buddy and Lucy, and you call `.bark()`, which one barks? Python uses `self` to track which object you're working with. `self` means 'this specific dog.'"

---

**Q: "Do I have to name it `self`? Can I call it something else?"**
A: "Technically yes, but **don't**. `self` is a universal convention in Python. Any experienced programmer expects it. Use `self` so your code is readable to others."

---

**Q: "What's the difference between `__init__` and other methods?"**
A: "`__init__` is **special**. Python calls it automatically when you create an object. Other methods, you call manually. Think of `__init__` as 'the constructor'—it builds a new object."

---

**Q: "When should I use class variables vs instance variables?"**
A: "Instance variables are unique to each object. Class variables are shared. Use instance variables for data that changes per object (name, age). Use class variables for data that's the same for all objects (school name, total count)."

---

**Q: "Do I have to use `super()` in every child class?"**
A: "Only in `__init__` if the parent has an `__init__`. And only if the parent does something you need to keep. If the parent does nothing, you can skip it. But usually, use it in `__init__` to be safe."

---

## Analogies That Work

**1. Class vs Object:**
"A class is like a blueprint for a house. An object is like an actual house built from the blueprint. You can build many houses from one blueprint, and each house has its own furniture, color, etc., even though they're all built from the same blueprint."

---

**2. `self` in Methods:**
"Imagine you're a teacher and you have a method `grade_student()`. Every time you call it, you need to know which student you're grading. `self` is like the student you're currently grading. When you call `student.grade_exam()`, Python passes the student as `self` automatically."

---

**3. Inheritance:**
"Inheritance is like a family tree. A Dog is a type of Animal, so a Dog inherits traits from Animal (eating, sleeping). But a Dog adds its own traits (barking). The child specializes the parent."

---

**4. Composition:**
"Composition is like combining LEGO bricks. A Car is made of an Engine, Wheels, and Steering. The Car doesn't *inherit* from Engine; it *has* an Engine. They're separate pieces joined together."

---

## Coding 1 Gaps to Watch For

Students enter Unit 2 having written functions but never classes. Watch for:

**Gap 1: Function Definition**
- **What to watch for:** Students understand `def func():` but struggle with `def method(self):`. They forget `self` is a parameter.
- **Quick fix:** When defining the first method, pause and show: "`self` is a parameter, like any function parameter. Every method gets it automatically."

**Gap 2: Variable Scope**
- **What to watch for:** Students create variables inside `__init__` and try to use them elsewhere without `self`.
  ```python
  def __init__(self, name):
      name = name  # Wrong! This is a local variable
  # Should be: self.name = name
  ```
- **Quick fix:** Explain: "To save data in the object, use `self.attribute`. Without `self`, it's a local variable that disappears after `__init__`."

**Gap 3: Dictionaries and Objects**
- **What to watch for:** Students who just finished Unit 1 think classes are like dictionaries: `student["name"]` vs. `student.name`. They sometimes try to use bracket notation.
- **Quick fix:** Show: "Classes use dot notation: `student.name`. Dictionaries use brackets: `student["name"]`. Different tools."

**Gap 4: Return Statements**
- **What to watch for:** Students write methods that modify `self` but don't return anything, then they treat the method call like a return: `x = dog.bark()` expecting a string.
- **Quick fix:** Clarify: "Methods can return values (like functions) or modify state. Decide which. If you want a value, `return` it. If you're modifying the object, you might not return anything."

---

## Quick Troubleshooting Guide

| Error | Most Likely Cause | Fix |
|-------|-------------------|-----|
| `NameError: name 'self' is not defined` | Using `self` outside a method | `self` only exists inside methods |
| `TypeError: __init__() missing required positional argument: 'self'` | Defining method without `self` | Add `self` as first parameter: `def method(self):` |
| `AttributeError: 'ClassName' object has no attribute 'x'` | Attribute not set in `__init__` | Add `self.x = ...` in `__init__` |
| `TypeError: 'ClassName' object is not callable` | Forgot parentheses when creating object | Use `obj = ClassName()` not `obj = ClassName` |
| `TypeError: method() takes 1 positional argument but 2 were given` | Calling method on class instead of instance | Use `obj.method()` not `Class.method()` |
| `AttributeError: type object has no attribute` | Accessing instance variable on class | Use `obj.attribute` not `Class.attribute` |
| `TypeError: Can't instantiate abstract class` | Didn't implement required @abstractmethod | Implement all abstract methods |
| `TypeError: super().__init__() missing required argument` | Parent's `__init__` needs parameter | Pass correct arguments: `super().__init__(param)` |

