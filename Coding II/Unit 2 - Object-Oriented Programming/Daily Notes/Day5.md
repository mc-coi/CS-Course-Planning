# Day 5: Encapsulation & Properties
**Learning Target:** I can implement encapsulation using private attributes and @property decorator.

### Key Concepts
**Encapsulation** hides internal details and exposes only what's necessary.

**Private attributes** (prefix with _) are intended for internal use only.
**Properties** provide controlled access to attributes using getters and setters via @property.

### Code Examples
```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance  # Private attribute

    @property
    def balance(self):
        return self._balance

    @balance.setter
    def balance(self, amount):
        if amount < 0:
            print("Error: Balance cannot be negative")
            return
        self._balance = amount

    def deposit(self, amount):
        if amount > 0:
            self._balance += amount

account = BankAccount(1000)
print(account.balance)  # 1000
account.deposit(500)
print(account.balance)  # 1500
account.balance = -100  # "Error: Balance cannot be negative"
```

### Guided Practice
Create a Temperature class that stores temperature in Celsius but provides properties to get/set in Fahrenheit.

### Practice Problems
**Problem 1 — Beginner:** Create a Student class with a private _gpa that only accepts values 0-4.0.

**Problem 2 — Intermediate:** Create a Box class with height, width, depth properties that validate positive numbers.

**Problem 3 — Challenge:** Create a User class with private password that validates strength (length, characters).

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Student:
    def __init__(self, name, gpa):
        self._gpa = gpa

    @property
    def gpa(self):
        return self._gpa

    @gpa.setter
    def gpa(self, value):
        if 0 <= value <= 4.0:
            self._gpa = value
```
</details>

---
