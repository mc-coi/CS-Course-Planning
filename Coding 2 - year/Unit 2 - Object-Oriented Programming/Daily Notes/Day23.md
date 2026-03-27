# Day 23: OOP Review Day
**Learning Target:** I can demonstrate mastery of all OOP concepts and apply them to solve problems.

### Comprehensive OOP Concepts Review

**Classes and Objects**
- Classes are blueprints, objects are instances
- Use constructors to initialize state
- Methods represent behavior

**Encapsulation**
- Private attributes with _ prefix
- Properties with @property decorator
- Validation in setters
- Public interface hides implementation

**Inheritance**
- Child classes inherit from parents
- Use super() to call parent methods
- Override methods to customize behavior
- Design hierarchies carefully

**Polymorphism**
- Same method name, different implementations
- Duck typing: objects with same methods work together
- Enables flexible, extensible code

**Special Methods**
- __init__: constructor
- __str__, __repr__: string representation
- __len__, __eq__, __lt__, __add__: operator overloading
- Make objects behave like built-in types

**Abstract Classes**
- Define interfaces with ABC
- Force subclasses to implement methods
- Prevent instantiation of base classes

**Composition vs Inheritance**
- Favor composition for flexibility
- Use inheritance only for true is-A relationships
- Avoid deep hierarchies

### Practice Problems

**Problem 1: Banking System Design**

Create classes for:
- BankAccount (base class)
- CheckingAccount (with monthly fee)
- SavingsAccount (with interest)
- SpecialAccount (has-a bonus system)

Requirements:
- Private balance, public operations
- Polymorphic withdraw() with different rules
- Special methods for comparison and arithmetic

**Solution:**
```python
from abc import ABC, abstractmethod

class BankAccount(ABC):
    def __init__(self, holder, balance):
        self.holder = holder
        self._balance = balance

    @property
    def balance(self):
        return self._balance

    @abstractmethod
    def withdraw(self, amount):
        pass

    def deposit(self, amount):
        if amount > 0:
            self._balance += amount

    def __str__(self):
        return f"{self.holder}: ${self._balance:.2f}"

    def __eq__(self, other):
        return self.balance == other.balance

    def __lt__(self, other):
        return self.balance < other.balance

class CheckingAccount(BankAccount):
    MONTHLY_FEE = 10

    def withdraw(self, amount):
        total = amount + self.MONTHLY_FEE
        if total <= self._balance:
            self._balance -= total
            return True
        return False

class SavingsAccount(BankAccount):
    def __init__(self, holder, balance, interest_rate=0.05):
        super().__init__(holder, balance)
        self.interest_rate = interest_rate

    def withdraw(self, amount):
        if amount <= self._balance:
            self._balance -= amount
            return True
        return False

    def apply_interest(self):
        interest = self._balance * self.interest_rate
        self._balance += interest

class BonusSystem:
    def __init__(self, bonus_percent):
        self.bonus_percent = bonus_percent

    def calculate_bonus(self, amount):
        return amount * self.bonus_percent

class SpecialAccount(SavingsAccount):
    def __init__(self, holder, balance, interest_rate):
        super().__init__(holder, balance, interest_rate)
        self.bonus = BonusSystem(0.02)

    def deposit(self, amount):
        super().deposit(amount)
        bonus = self.bonus.calculate_bonus(amount)
        self._balance += bonus

# Usage
accounts = [
    CheckingAccount("Alice", 1000),
    SavingsAccount("Bob", 5000, 0.07),
    SpecialAccount("Charlie", 2000, 0.05)
]

for account in accounts:
    print(account)

accounts[0].withdraw(100)
accounts[1].apply_interest()
accounts[2].deposit(500)

sorted_accounts = sorted(accounts)
for account in sorted_accounts:
    print(f"{account} (after operations)")
```

**Problem 2: Game System**

Create a game with:
- Abstract Character class
- Concrete character types (Warrior, Mage, Rogue)
- Equipment system (composition)
- Combat mechanics (polymorphism)
- Inventory management

**Problem 3: Data Processing Pipeline**

Create classes for:
- Abstract DataProcessor
- Concrete processors (FilterProcessor, TransformProcessor, AggregateProcessor)
- Pipeline class that chains processors
- Support for adding/removing processors

### Review Checklist

Check your understanding:

**Fundamentals:**
- [ ] Can define a class with __init__
- [ ] Can create and use instances
- [ ] Understand self parameter

**Encapsulation:**
- [ ] Can use private attributes
- [ ] Can implement properties with @property
- [ ] Can validate data in setters

**Inheritance:**
- [ ] Can create parent and child classes
- [ ] Use super() correctly
- [ ] Override methods
- [ ] Design class hierarchies

**Polymorphism:**
- [ ] Multiple classes with same method
- [ ] Use polymorphic behavior
- [ ] Duck typing

**Special Methods:**
- [ ] __str__ and __repr__
- [ ] __len__, __eq__, __lt__
- [ ] __add__ and other operators

**Advanced:**
- [ ] Abstract classes with ABC
- [ ] Choose composition vs inheritance
- [ ] Design classes with SOLID principles

### Common Mistakes to Avoid

1. **Mutable default arguments**
   ```python
   # Bad
   def __init__(self, items=[]):
       self.items = items  # Shared across instances!

   # Good
   def __init__(self, items=None):
       self.items = items if items else []
   ```

2. **Not using super()**
   ```python
   # Bad
   class Child(Parent):
       def __init__(self, x, y):
           Parent.__init__(self, x)  # Fragile
           self.y = y

   # Good
   class Child(Parent):
       def __init__(self, x, y):
           super().__init__(x)
           self.y = y
   ```

3. **Violating Liskov Substitution Principle**
   ```python
   # Bad: Child not substitutable for Parent
   class Parent:
       def withdraw(self, amount):
           return amount <= balance

   class Child(Parent):
       def withdraw(self, amount):
           raise NotImplementedError()  # Breaks contracts!

   # Good: Child maintains parent's contracts
   ```

4. **Inheritance for code reuse only**
   ```python
   # Bad: Not a true is-A relationship
   class Utility(Base):
       @staticmethod
       def helper():
           pass

   # Good: Use composition or stand-alone functions
   class UtilityHelper:
       @staticmethod
       def helper():
           pass
   ```

### Real-World Design Exercise

Design a simple music streaming system:

**Requirements:**
- Users can create playlists
- Playlists contain songs
- Users can play songs, pause, skip
- Track listening history
- Support different audio formats

**Classes needed:**
- User
- Playlist
- Song
- Player
- AudioFormat (abstract)
- MP3Format, WAVFormat (concrete)
- ListeningHistory

**Hints:**
- Use composition for User has-a Playlist
- Use composition for Playlist has-a Songs
- Use inheritance for different audio formats
- Use special methods for Song equality
- Use properties for Player state

This exercise tests:
- Identifying classes from requirements
- Choosing appropriate relationships
- Designing methods and attributes
- Applying OOP principles
- Creating usable public interfaces
