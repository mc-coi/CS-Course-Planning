# Day 12: Built-in Decorators (@property, @staticmethod, @classmethod)

**Learning Target:** I can use built-in decorators to create properties, static methods, and class methods in classes.

---

## Key Concepts

**@property** — Turns a method into a read-only attribute. Allows computed properties without visible method call syntax.

**@staticmethod** — A method that doesn't access the instance or class. Acts like a regular function but grouped with the class.

**@classmethod** — A method that receives the class itself (not an instance) as the first parameter. Useful for factory methods and class-wide operations.

**When to use each:**
- `@property` — For computed attributes or controlled access
- `@staticmethod` — For utility functions related to a class
- `@classmethod` — For alternative constructors or class-level operations

**Descriptor Protocol** — `@property` implements a protocol that intercepts attribute access, enabling powerful customization.

---

## Code Examples

```python
# Example 1: @property - simple computed property
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius
    
    @property
    def fahrenheit(self):
        """Computed property: converts Celsius to Fahrenheit"""
        return self._celsius * 9/5 + 32
    
    @property
    def celsius(self):
        """Read the internal value"""
        return self._celsius

temp = Temperature(0)
print(temp.fahrenheit)  # Output: 32.0
print(temp.celsius)     # Output: 0

# Example 2: @property with setter
class Circle:
    def __init__(self, radius):
        self._radius = radius
    
    @property
    def radius(self):
        return self._radius
    
    @radius.setter
    def radius(self, value):
        if value <= 0:
            raise ValueError("Radius must be positive")
        self._radius = value
    
    @property
    def area(self):
        return 3.14159 * self._radius ** 2

circle = Circle(5)
print(circle.area)      # Output: 78.53975
circle.radius = 10      # Uses the setter
print(circle.area)      # Output: 314.159
# circle.radius = -5    # Would raise ValueError

# Example 3: @staticmethod - utility function in a class
class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b
    
    @staticmethod
    def is_even(n):
        return n % 2 == 0

# Can call without creating an instance
print(MathUtils.add(5, 3))        # Output: 8
print(MathUtils.is_even(4))       # Output: True

# Can also call on instance (but doesn't need it)
utils = MathUtils()
print(utils.add(5, 3))            # Output: 8

# Example 4: @classmethod - factory method
class Student:
    school = "Central High"  # Class variable
    
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade
    
    @classmethod
    def from_string(cls, student_string):
        """Alternative constructor from 'Name,Grade' string"""
        name, grade = student_string.split(",")
        return cls(name, int(grade))
    
    @classmethod
    def set_school(cls, school_name):
        """Update school for all students"""
        cls.school = school_name

# Normal constructor
student1 = Student("Alice", 11)
print(f"{student1.name} - {student1.school}")  # Alice - Central High

# Alternative constructor
student2 = Student.from_string("Bob,10")
print(f"{student2.name}, grade {student2.grade}")  # Bob, grade 10

# Class method modifies class variable
Student.set_school("Lincoln High")
print(student1.school)  # Lincoln High (affected all instances)

# Example 5: All three decorators together
class BankAccount:
    interest_rate = 0.05  # Class variable
    
    def __init__(self, name, balance):
        self.name = name
        self._balance = balance
    
    @property
    def balance(self):
        """Read-only balance property"""
        return self._balance
    
    @property
    def balance_with_interest(self):
        """Computed property"""
        return self._balance * (1 + self.interest_rate)
    
    def deposit(self, amount):
        self._balance += amount
    
    @staticmethod
    def validate_amount(amount):
        """Utility method - doesn't need instance"""
        return amount > 0
    
    @classmethod
    def update_interest_rate(cls, new_rate):
        """Update interest for all accounts"""
        cls.interest_rate = new_rate

# Usage
account = BankAccount("Alice", 1000)
print(account.balance)                    # 1000
print(account.balance_with_interest)      # 1050.0
print(BankAccount.validate_amount(100))   # True
BankAccount.update_interest_rate(0.10)
print(account.balance_with_interest)      # 1100.0

# Example 6: @property for validation
class Person:
    def __init__(self, name, age):
        self.name = name
        self._age = age
    
    @property
    def age(self):
        return self._age
    
    @age.setter
    def age(self, value):
        if not isinstance(value, int) or value < 0:
            raise ValueError("Age must be a non-negative integer")
        self._age = value

person = Person("Alice", 25)
print(person.age)  # 25
person.age = 26    # Uses setter for validation
# person.age = -5  # Would raise ValueError

# Example 7: @classmethod for counting instances
class Product:
    count = 0
    
    def __init__(self, name, price):
        self.name = name
        self.price = price
        Product.count += 1
    
    @classmethod
    def total_products(cls):
        return cls.count

p1 = Product("Laptop", 1200)
p2 = Product("Mouse", 25)
p3 = Product("Keyboard", 75)
print(Product.total_products())  # Output: 3
```

---

## Guided Practice

**Step 1:** Create a class with a @property that computes a value.
```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    @property
    def area(self):
        return self.width * self.height

rect = Rectangle(5, 10)
print(rect.area)  # Should print: 50
```

**Step 2:** Add a @property setter to validate input.
```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance
    
    @property
    def balance(self):
        return self._balance
    
    @balance.setter
    def balance(self, amount):
        if amount < 0:
            raise ValueError("Balance cannot be negative")
        self._balance = amount

account = BankAccount(100)
print(account.balance)  # Should print: 100
account.balance = 200   # Should work
# account.balance = -50  # Should raise error
```

**Step 3:** Create a @staticmethod that doesn't need instance data.
```python
class Converter:
    @staticmethod
    def celsius_to_fahrenheit(c):
        return c * 9/5 + 32

print(Converter.celsius_to_fahrenheit(0))   # Should print: 32.0
```

**Step 4:** Create a @classmethod factory method.
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    @classmethod
    def from_tuple(cls, point_tuple):
        return cls(point_tuple[0], point_tuple[1])

p = Point.from_tuple((3, 4))
print(f"({p.x}, {p.y})")  # Should print: (3, 4)
```

---

## Practice Problems

**Beginner:** Create a class with a @property that returns the square of an internal value.

**Intermediate:** Create a class with @property, @staticmethod, and @classmethod, each serving a different purpose.

**Challenge:** Create a class that uses @property with setter to maintain invariants (like keeping total money constant when transferring between accounts).

<details>
<summary>💡 Hints</summary>
- For Beginner: Store value in _value, return value ** 2 in property
- For Intermediate: Think about what each decorator is good for
- For Challenge: Update both accounts atomically in the setter
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
class Number:
    def __init__(self, value):
        self._value = value
    
    @property
    def squared(self):
        return self._value ** 2

num = Number(5)
print(num.squared)  # Output: 25

# Intermediate
class Library:
    total_books = 0
    
    def __init__(self, title, author):
        self.title = title
        self.author = author
        Library.total_books += 1
    
    @property
    def full_title(self):
        return f"{self.title} by {self.author}"
    
    @staticmethod
    def is_valid_year(year):
        return 0 < year <= 2026
    
    @classmethod
    def book_count(cls):
        return cls.total_books

# Challenge (simplified)
class Account:
    def __init__(self, balance):
        self._balance = balance
    
    @property
    def balance(self):
        return self._balance
    
    @balance.setter
    def balance(self, amount):
        if amount < 0:
            raise ValueError("Balance cannot be negative")
        self._balance = amount
```
</details>
