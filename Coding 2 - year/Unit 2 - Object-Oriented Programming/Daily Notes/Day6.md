# Day 6: Encapsulation — Public vs Private Attributes
**Learning Target:** I can protect object data using private attributes and understand encapsulation principles.

### Key Concepts

**Encapsulation:** The bundling of data and methods together, and hiding internal implementation details from the outside. This protects data integrity.

**Public Attribute:** An attribute that can be accessed and modified from outside the class. Convention: regular names like `name`, `age`.

**Private Attribute:** An attribute that should only be accessed within the class itself. Convention: prefixed with underscore like `_balance`, `_password`.

**Data Protection:** Using private attributes to prevent external code from directly modifying sensitive or critical data.

**Convention vs Enforcement:** Python uses naming conventions (_variable) rather than language-level enforcement for privacy (unlike Java or C++).

### Code Examples

```python
# Without encapsulation (problematic)
class BankAccount:
    def __init__(self, holder, balance):
        self.holder = holder
        self.balance = balance

account = BankAccount("Alice", 1000)
account.balance = account.balance + 5000  # Anyone can modify!
print(account.balance)  # 6000 (shouldn't be this easy!)

# With encapsulation (better)
class BankAccount:
    def __init__(self, holder, balance):
        self.holder = holder
        self._balance = balance  # Private attribute

    def deposit(self, amount):
        if amount > 0:
            self._balance = self._balance + amount
            return True
        return False

    def withdraw(self, amount):
        if 0 < amount <= self._balance:
            self._balance = self._balance - amount
            return True
        return False

    def get_balance(self):
        return self._balance

account = BankAccount("Alice", 1000)
account.deposit(500)  # Controlled access
print(account.get_balance())  # 1500

# Incorrect usage now requires calling methods
account.withdraw(200)
print(account.get_balance())  # 1300

# Student class with private attributes
class Student:
    def __init__(self, name, gpa):
        self.name = name  # Public
        self._gpa = gpa  # Private
        self._grades = []  # Private

    def add_grade(self, grade):
        if 0 <= grade <= 100:
            self._grades.append(grade)
            self._update_gpa()
            return True
        return False

    def _update_gpa(self):
        # Private method - only called internally
        if len(self._grades) > 0:
            self._gpa = sum(self._grades) / len(self._grades) / 100 * 4.0

    def get_gpa(self):
        return self._gpa

    def get_grades(self):
        return self._grades.copy()  # Return a copy, not the original

student = Student("Bob", 3.5)
student.add_grade(95)
student.add_grade(88)
student.add_grade(92)
print(f"GPA: {student.get_gpa():.2f}")  # GPA: 3.75

# Cannot directly access private attributes (but can if you really try)
print(student._grades)  # Still possible, but bad practice
print(student.get_grades())  # Better way

# Employee class
class Employee:
    def __init__(self, name, salary, ssn):
        self.name = name  # Public
        self._salary = salary  # Private
        self._ssn = ssn  # Private

    def give_raise(self, amount):
        if amount > 0:
            self._salary = self._salary + amount
            print(f"Raise granted: ${amount}")

    def get_salary(self):
        return self._salary

    def get_ssn(self):
        # Return masked SSN for privacy
        return f"***-**-{self._ssn[-4:]}"

emp = Employee("Charlie", 50000, "123-45-6789")
emp.give_raise(5000)
print(f"Salary: ${emp.get_salary()}")  # Salary: $55000
print(f"SSN: {emp.get_ssn()}")  # SSN: ***-**-6789

# Game character with private stats
class Character:
    def __init__(self, name, max_health):
        self.name = name
        self._health = max_health
        self._max_health = max_health
        self._level = 1
        self._experience = 0

    def take_damage(self, amount):
        self._health = max(0, self._health - amount)
        return self._health

    def heal(self, amount):
        self._health = min(self._max_health, self._health + amount)
        return self._health

    def gain_experience(self, amount):
        self._experience = self._experience + amount
        if self._experience >= 100:
            self._level = self._level + 1
            self._experience = 0

    def get_health(self):
        return self._health

    def get_status(self):
        health_percent = (self._health / self._max_health) * 100
        return f"{self.name} - Level {self._level}, HP {self._health}/{self._max_health} ({health_percent:.0f}%)"

hero = Character("Aragorn", 100)
hero.take_damage(25)
hero.gain_experience(50)
hero.gain_experience(60)
print(hero.get_status())  # Aragorn - Level 2, HP 75/100 (75%)

# Password-protected account
class Account:
    def __init__(self, username, password):
        self.username = username
        self._password = password  # Never store as plain text in real apps!
        self._login_attempts = 0

    def verify_password(self, password):
        if password == self._password:
            self._login_attempts = 0
            return True
        else:
            self._login_attempts = self._login_attempts + 1
            if self._login_attempts >= 3:
                print("Account locked!")
            return False

    def is_locked(self):
        return self._login_attempts >= 3

account = Account("alice", "secret123")
print(account.verify_password("wrong"))  # False
print(account.verify_password("wrong"))  # False
print(account.verify_password("wrong"))  # False, Account locked!
print(account.verify_password("secret123"))  # Still False (locked)
```

### Guided Practice

**Activity: Build a Bank Account with Private Data**

Follow these steps:

1. Create a `BankAccount` class with:
   - Private attributes: `_balance`, `_pin`
   - Public attribute: `holder`
   - Private method: `_verify_pin(pin)` that checks if the PIN is correct
   - Public methods: `deposit()`, `withdraw()`, `check_balance()` (all require PIN verification)

2. Test the class:
   - Create an account
   - Try to deposit and withdraw with correct PIN (should work)
   - Try to withdraw with wrong PIN (should fail)
   - Verify balance can only be checked with correct PIN

**Solution:**
```python
class BankAccount:
    def __init__(self, holder, initial_balance, pin):
        self.holder = holder
        self._balance = initial_balance
        self._pin = pin

    def _verify_pin(self, pin):
        return pin == self._pin

    def deposit(self, amount, pin):
        if not self._verify_pin(pin):
            print("Invalid PIN!")
            return False
        if amount > 0:
            self._balance = self._balance + amount
            print(f"Deposited ${amount}")
            return True
        return False

    def withdraw(self, amount, pin):
        if not self._verify_pin(pin):
            print("Invalid PIN!")
            return False
        if 0 < amount <= self._balance:
            self._balance = self._balance - amount
            print(f"Withdrew ${amount}")
            return True
        else:
            print("Insufficient funds!")
            return False

    def check_balance(self, pin):
        if not self._verify_pin(pin):
            print("Invalid PIN!")
            return None
        return self._balance

account = BankAccount("Alice", 1000, "1234")
account.deposit(500, "1234")  # Deposited $500
account.check_balance("1234")  # 1500
account.withdraw(200, "wrong")  # Invalid PIN!
account.withdraw(200, "1234")  # Withdrew $200
```

### Practice Problems

**Problem 1 — Beginner:** Create a `Temperature` class that stores temperature in Celsius (private). Provide methods to: set temperature with validation (must be between -50 and 50), get temperature in Celsius, and get temperature in Fahrenheit. Prevent direct access to the internal storage.

**Problem 2 — Intermediate:** Create a `SecurePassword` class that validates and stores a password. Require passwords to be at least 8 characters. Provide a method to verify password and another to change password (with old password verification). Track failed login attempts.

**Problem 3 — Challenge:** Create a `Game` class that manages a player's level, health, and experience. Use private attributes and provide public methods for gaining experience, taking damage, and healing. Implement automatic level-up when experience reaches 100, resetting experience to 0.

<details>
<summary>💡 Hints</summary>

**Hint 1:** Private attributes in Python use the `_` prefix by convention. They're not truly private, but it signals "don't touch this from outside."

**Hint 2:** Always provide getter and setter methods to control how data is accessed and modified.

**Hint 3:** For Problem 3, create a method like `_level_up()` that's called internally when conditions are met.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Temperature:
    def __init__(self, celsius):
        self._celsius = None
        self.set_temperature(celsius)

    def set_temperature(self, celsius):
        if -50 <= celsius <= 50:
            self._celsius = celsius
            return True
        else:
            print("Temperature out of valid range!")
            return False

    def get_celsius(self):
        return self._celsius

    def get_fahrenheit(self):
        return (self._celsius * 9/5) + 32

temp = Temperature(25)
print(f"Celsius: {temp.get_celsius()}")
print(f"Fahrenheit: {temp.get_fahrenheit():.1f}")

# Problem 2
class SecurePassword:
    def __init__(self, password):
        self._password = None
        self._failed_attempts = 0
        self.set_password(password)

    def set_password(self, password):
        if len(password) >= 8:
            self._password = password
            return True
        return False

    def verify_password(self, password):
        if password == self._password:
            self._failed_attempts = 0
            return True
        else:
            self._failed_attempts = self._failed_attempts + 1
            return False

    def change_password(self, old_password, new_password):
        if self.verify_password(old_password):
            return self.set_password(new_password)
        return False

pwd = SecurePassword("secure123")
print(pwd.verify_password("secure123"))  # True
print(pwd.verify_password("wrong"))  # False
print(pwd.change_password("secure123", "newsecure456"))  # True

# Problem 3
class Game:
    def __init__(self, player_name):
        self.player_name = player_name
        self._level = 1
        self._health = 100
        self._experience = 0
        self._max_health = 100

    def gain_experience(self, amount):
        self._experience = self._experience + amount
        if self._experience >= 100:
            self._level_up()

    def _level_up(self):
        self._level = self._level + 1
        self._experience = 0
        self._max_health = self._max_health + 10
        self._health = self._max_health
        print(f"Level up! Now level {self._level}")

    def take_damage(self, amount):
        self._health = max(0, self._health - amount)

    def heal(self, amount):
        self._health = min(self._max_health, self._health + amount)

    def get_status(self):
        return f"{self.player_name} - Lvl {self._level}, HP {self._health}/{self._max_health}, XP {self._experience}/100"

game = Game("Hero")
print(game.get_status())
game.gain_experience(60)
game.gain_experience(50)
print(game.get_status())
game.take_damage(30)
print(game.get_status())
```

</details>
