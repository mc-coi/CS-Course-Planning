# Day 6: Custom Exceptions
**Learning Target:** I can create and use custom exception classes.

### Key Concepts
Create custom exceptions by inheriting from `Exception`.

Useful for application-specific errors.

### Code Examples
```python
# Define custom exception
class InsufficientFundsError(Exception):
    pass

class InvalidAgeError(Exception):
    def __init__(self, age):
        self.age = age
        super().__init__(f"Age {age} is invalid")

# Use custom exception
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def withdraw(self, amount):
        if amount > self.balance:
            raise InsufficientFundsError("Not enough money!")
        self.balance -= amount

account = BankAccount(100)
try:
    account.withdraw(200)
except InsufficientFundsError as e:
    print(f"Error: {e}")

# Catching custom exceptions
def validate_age(age):
    if age < 0 or age > 150:
        raise InvalidAgeError(age)

try:
    validate_age(-5)
except InvalidAgeError as e:
    print(f"Error: {e}")
```

### Guided Practice
Create custom exceptions for validation errors.

### Practice Problems
**Problem 1 — Beginner:** Create a simple custom exception class.

**Problem 2 — Intermediate:** Create exceptions for a Student class.

**Problem 3 — Challenge:** Create exception hierarchy with parent/child exceptions.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class CustomError(Exception):
    pass

# Problem 2
class InvalidGPAError(Exception):
    pass

class Student:
    def __init__(self, name, gpa):
        if gpa < 0 or gpa > 4.0:
            raise InvalidGPAError(f"GPA must be 0-4.0, got {gpa}")
        self.gpa = gpa
```
</details>

---

---
