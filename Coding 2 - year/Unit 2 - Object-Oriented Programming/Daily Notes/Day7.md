# Day 7: Properties, Getters & Setters
**Learning Target:** I can use property decorators and getters/setters to control access to attributes with validation.

### Key Concepts

**Getter:** A method that returns the value of a private attribute. Allows reading data in a controlled way.

**Setter:** A method that sets the value of a private attribute. Allows writing data with validation or side effects.

**Property Decorator (@property):** Python's mechanism to make methods look like attributes, allowing `obj.attr` instead of `obj.get_attr()`.

**Validation:** Checking that new values meet requirements before storing them (e.g., age must be positive).

### Code Examples

```python
# Without properties (verbose)
class Person:
    def __init__(self, name, age):
        self._name = name
        self._age = age

    def get_name(self):
        return self._name

    def set_name(self, name):
        if len(name) > 0:
            self._name = name

    def get_age(self):
        return self._age

    def set_age(self, age):
        if age >= 0:
            self._age = age

person = Person("Alice", 25)
print(person.get_name())  # Must use get_name()
person.set_age(26)  # Must use set_age()

# With properties (cleaner)
class Person:
    def __init__(self, name, age):
        self._name = name
        self._age = age

    @property
    def name(self):
        return self._name

    @name.setter
    def name(self, value):
        if len(value) > 0:
            self._name = value

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        if value >= 0:
            self._age = value

person = Person("Alice", 25)
print(person.name)  # Can use like attribute
person.age = 26  # Looks like normal assignment
person.name = "Alicia"

# Temperature class with validation
class Temperature:
    def __init__(self, celsius):
        self._celsius = 0
        self.celsius = celsius  # Uses setter

    @property
    def celsius(self):
        return self._celsius

    @celsius.setter
    def celsius(self, value):
        if -273.15 <= value <= 1000:  # Valid range
            self._celsius = value
        else:
            raise ValueError("Temperature out of valid range!")

    @property
    def fahrenheit(self):
        return (self._celsius * 9/5) + 32

    @fahrenheit.setter
    def fahrenheit(self, value):
        self.celsius = (value - 32) * 5/9  # Convert and validate

temp = Temperature(25)
print(f"Celsius: {temp.celsius}")  # 25
print(f"Fahrenheit: {temp.fahrenheit}")  # 77.0

temp.fahrenheit = 86  # Can set via Fahrenheit
print(f"Celsius: {temp.celsius}")  # 30

# BankAccount with properties
class BankAccount:
    def __init__(self, holder, balance):
        self._holder = holder
        self._balance = balance

    @property
    def holder(self):
        return self._holder

    @property
    def balance(self):
        return self._balance

    @balance.setter
    def balance(self, value):
        if value >= 0:
            self._balance = value
        else:
            raise ValueError("Balance cannot be negative!")

    def deposit(self, amount):
        if amount > 0:
            self._balance = self._balance + amount

    def withdraw(self, amount):
        if 0 < amount <= self._balance:
            self._balance = self._balance - amount

account = BankAccount("Alice", 1000)
print(f"{account.holder}: ${account.balance}")  # Alice: $1000
account.deposit(500)
print(f"{account.holder}: ${account.balance}")  # Alice: $1500
account.balance = 2000  # Direct setter
print(f"{account.holder}: ${account.balance}")  # Alice: $2000

# Student with GPA property
class Student:
    def __init__(self, name, gpa):
        self._name = name
        self._gpa = gpa
        self._grades = []

    @property
    def name(self):
        return self._name

    @property
    def gpa(self):
        return self._gpa

    @gpa.setter
    def gpa(self, value):
        if 0 <= value <= 4.0:
            self._gpa = value
        else:
            raise ValueError("GPA must be between 0 and 4.0")

    @property
    def grades(self):
        return self._grades.copy()  # Return copy for protection

    def add_grade(self, grade):
        if 0 <= grade <= 100:
            self._grades.append(grade)
            self._update_gpa()

    def _update_gpa(self):
        if len(self._grades) > 0:
            avg = sum(self._grades) / len(self._grades)
            self._gpa = (avg / 100) * 4.0

student = Student("Bob", 3.5)
student.add_grade(95)
student.add_grade(88)
student.add_grade(92)
print(f"{student.name}: GPA {student.gpa:.2f}")  # Bob: GPA 3.70

# Rectangle with read-only properties
class Rectangle:
    def __init__(self, width, height):
        self._width = width
        self._height = height

    @property
    def width(self):
        return self._width

    @width.setter
    def width(self, value):
        if value > 0:
            self._width = value

    @property
    def height(self):
        return self._height

    @height.setter
    def height(self, value):
        if value > 0:
            self._height = value

    @property
    def area(self):
        # Read-only property
        return self._width * self._height

    @property
    def perimeter(self):
        # Read-only property
        return 2 * (self._width + self._height)

rect = Rectangle(5, 3)
print(f"Area: {rect.area}")  # Area: 15
print(f"Perimeter: {rect.perimeter}")  # Perimeter: 16
rect.width = 10
print(f"Area: {rect.area}")  # Area: 30

# Game character with health property
class Character:
    def __init__(self, name, max_health):
        self._name = name
        self._max_health = max_health
        self._health = max_health

    @property
    def health(self):
        return self._health

    @health.setter
    def health(self, value):
        self._health = max(0, min(value, self._max_health))

    @property
    def health_percent(self):
        return (self._health / self._max_health) * 100

    def take_damage(self, amount):
        self.health = self._health - amount

    def heal(self, amount):
        self.health = self._health + amount

hero = Character("Aragorn", 100)
print(f"Health: {hero.health} ({hero.health_percent:.0f}%)")
hero.take_damage(25)
print(f"Health: {hero.health} ({hero.health_percent:.0f}%)")
hero.heal(15)
print(f"Health: {hero.health} ({hero.health_percent:.0f}%)")
```

### Guided Practice

**Activity: Create a Product Class with Property Validation**

Follow these steps:

1. Create a `Product` class with private attributes: `_name`, `_price`, `_quantity`
2. Create properties for all three:
   - `name` (read-write, must be non-empty)
   - `price` (read-write, must be positive)
   - `quantity` (read-write, must be non-negative)
3. Add a read-only property `total_value` that returns price × quantity
4. Create several products and test setting and getting values

**Expected Output:**
```
Product: Laptop, Price: $999.99, Qty: 2, Total: $1999.98
Price updated to $899.99
New total: $1799.98
```

**Solution:**
```python
class Product:
    def __init__(self, name, price, quantity):
        self._name = name
        self._price = price
        self._quantity = quantity

    @property
    def name(self):
        return self._name

    @name.setter
    def name(self, value):
        if len(value) > 0:
            self._name = value

    @property
    def price(self):
        return self._price

    @price.setter
    def price(self, value):
        if value > 0:
            self._price = value

    @property
    def quantity(self):
        return self._quantity

    @quantity.setter
    def quantity(self, value):
        if value >= 0:
            self._quantity = value

    @property
    def total_value(self):
        return self._price * self._quantity

product = Product("Laptop", 999.99, 2)
print(f"Product: {product.name}, Price: ${product.price:.2f}, Qty: {product.quantity}, Total: ${product.total_value:.2f}")
product.price = 899.99
print(f"Price updated to ${product.price:.2f}")
print(f"New total: ${product.total_value:.2f}")
```

### Practice Problems

**Problem 1 — Beginner:** Create an `Email` class with a private `_address` attribute. Use a property to get the email and a setter that validates the email contains "@". If invalid, keep the old value and print an error.

**Problem 2 — Intermediate:** Create a `Volume` class that stores volume in milliliters (private). Provide properties to get/set in milliliters, liters, and gallons. All conversions should be automatic and consistent.

**Problem 3 — Challenge:** Create a `BankAccount` class with properties for `balance` (read-only to public, can be modified through deposit/withdraw), `account_number`, and `interest_rate`. Implement a compound interest calculation method that updates balance using the property setter.

<details>
<summary>💡 Hints</summary>

**Hint 1:** To create a read-only property, just use `@property` without a setter.

**Hint 2:** Validation in setters should raise exceptions or silently reject invalid values. Choose one approach and be consistent.

**Hint 3:** For Problem 3, remember that property setters can call other methods to update dependent values.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Email:
    def __init__(self, address):
        self._address = ""
        self.address = address  # Use setter

    @property
    def address(self):
        return self._address

    @address.setter
    def address(self, value):
        if "@" in value and len(value) > 3:
            self._address = value
        else:
            print("Invalid email address!")

email = Email("alice@example.com")
print(email.address)  # alice@example.com
email.address = "invalid"  # Invalid email address!
print(email.address)  # alice@example.com (unchanged)

# Problem 2
class Volume:
    def __init__(self, milliliters):
        self._ml = milliliters

    @property
    def milliliters(self):
        return self._ml

    @milliliters.setter
    def milliliters(self, value):
        if value >= 0:
            self._ml = value

    @property
    def liters(self):
        return self._ml / 1000

    @liters.setter
    def liters(self, value):
        self._ml = value * 1000

    @property
    def gallons(self):
        return self._ml / 3785.41

    @gallons.setter
    def gallons(self, value):
        self._ml = value * 3785.41

vol = Volume(1000)
print(f"Milliliters: {vol.milliliters}")  # 1000
print(f"Liters: {vol.liters}")  # 1.0
print(f"Gallons: {vol.gallons:.3f}")  # 0.264

vol.liters = 2
print(f"Milliliters: {vol.milliliters}")  # 2000

# Problem 3
class BankAccount:
    def __init__(self, account_number, initial_balance, interest_rate):
        self._account_number = account_number
        self._balance = initial_balance
        self._interest_rate = interest_rate

    @property
    def account_number(self):
        return self._account_number

    @property
    def balance(self):
        return self._balance

    @property
    def interest_rate(self):
        return self._interest_rate

    @interest_rate.setter
    def interest_rate(self, value):
        if 0 <= value <= 1:
            self._interest_rate = value

    def apply_interest(self):
        self._balance = self._balance * (1 + self._interest_rate)

    def deposit(self, amount):
        if amount > 0:
            self._balance = self._balance + amount

    def withdraw(self, amount):
        if 0 < amount <= self._balance:
            self._balance = self._balance - amount

account = BankAccount("A001", 1000, 0.02)
print(f"Balance: ${account.balance:.2f}")
account.apply_interest()
print(f"After interest: ${account.balance:.2f}")
account.deposit(500)
print(f"After deposit: ${account.balance:.2f}")
```

</details>
