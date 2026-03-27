# Day 19: Special Methods Lab
**Learning Target:** I can implement comprehensive special methods to create objects that behave like built-in types.

### Lab Activities

#### Activity 1: Build a Money/Currency Class

**Objective:** Create a Money class with arithmetic and comparison special methods.

**Requirements:**
- Attributes: amount, currency (e.g., "USD")
- Methods: __add__(), __sub__(), __mul__(), __truediv__()
- Comparisons: __eq__(), __lt__(), __le__(), __gt__(), __ge__()
- String: __str__(), __repr__()

**Starter Code:**
```python
class Money:
    def __init__(self, amount, currency="USD"):
        self.amount = amount
        self.currency = currency

    def __str__(self):
        return f"${self.amount:.2f} {self.currency}"

    def __repr__(self):
        return f"Money({self.amount}, '{self.currency}')"

    def __add__(self, other):
        # YOUR CODE: add amounts
        pass

    def __sub__(self, other):
        # YOUR CODE: subtract amounts
        pass

    def __mul__(self, factor):
        # YOUR CODE: multiply by scalar
        pass

    def __truediv__(self, divisor):
        # YOUR CODE: divide by scalar
        pass

    def __eq__(self, other):
        # YOUR CODE: compare
        pass

    def __lt__(self, other):
        # YOUR CODE: less than
        pass

    def __le__(self, other):
        return self < other or self == other

    def __gt__(self, other):
        return not (self <= other)

    def __ge__(self, other):
        return not (self < other)

# Test
m1 = Money(100)
m2 = Money(50)
m3 = Money(100)

print(m1 + m2)  # $150.00 USD
print(m1 - m2)  # $50.00 USD
print(m1 * 2)   # $200.00 USD
print(m1 / 2)   # $50.00 USD

print(m1 == m3)  # True
print(m1 > m2)   # True
print(m1 < m2)   # False

# Sorting
amounts = [m1, m2, m3, Money(75)]
sorted_amounts = sorted(amounts)
for m in sorted_amounts:
    print(m)
```

**Solution:**
```python
class Money:
    def __init__(self, amount, currency="USD"):
        self.amount = amount
        self.currency = currency

    def __str__(self):
        return f"${self.amount:.2f} {self.currency}"

    def __repr__(self):
        return f"Money({self.amount}, '{self.currency}')"

    def __add__(self, other):
        if not isinstance(other, Money):
            return NotImplemented
        if self.currency != other.currency:
            raise ValueError("Cannot add different currencies")
        return Money(self.amount + other.amount, self.currency)

    def __sub__(self, other):
        if not isinstance(other, Money):
            return NotImplemented
        if self.currency != other.currency:
            raise ValueError("Cannot subtract different currencies")
        return Money(self.amount - other.amount, self.currency)

    def __mul__(self, factor):
        return Money(self.amount * factor, self.currency)

    def __rmul__(self, factor):
        return self * factor

    def __truediv__(self, divisor):
        if divisor == 0:
            raise ValueError("Cannot divide by zero")
        return Money(self.amount / divisor, self.currency)

    def __eq__(self, other):
        if not isinstance(other, Money):
            return False
        return self.amount == other.amount and self.currency == other.currency

    def __lt__(self, other):
        if not isinstance(other, Money):
            return NotImplemented
        if self.currency != other.currency:
            raise ValueError("Cannot compare different currencies")
        return self.amount < other.amount

    def __le__(self, other):
        return self < other or self == other

    def __gt__(self, other):
        return not (self <= other)

    def __ge__(self, other):
        return not (self < other)

m1 = Money(100)
m2 = Money(50)
m3 = Money(100)

print(m1 + m2)
print(m1 - m2)
print(m1 * 2)
print(2 * m1)  # Uses __rmul__
print(m1 / 2)

print(m1 == m3)
print(m1 > m2)
print(m1 < m2)

amounts = [m1, m2, m3, Money(75)]
sorted_amounts = sorted(amounts)
for m in sorted_amounts:
    print(m)
```

---

#### Activity 2: Build a Rational Number Class

**Objective:** Create a Rational number (fraction) class with full arithmetic support.

**Requirements:**
- Attributes: numerator, denominator
- Simplify fractions automatically
- Arithmetic: __add__(), __sub__(), __mul__(), __truediv__()
- Comparisons: __eq__(), __lt__()
- String: __str__(), __repr__()
- Length: __len__() returns gcd

**Starter Code:**
```python
import math

class Rational:
    def __init__(self, numerator, denominator):
        if denominator == 0:
            raise ValueError("Denominator cannot be zero")

        gcd = math.gcd(abs(numerator), abs(denominator))
        self.numerator = numerator // gcd
        self.denominator = denominator // gcd

    def __str__(self):
        if self.denominator == 1:
            return str(self.numerator)
        return f"{self.numerator}/{self.denominator}"

    def __repr__(self):
        return f"Rational({self.numerator}, {self.denominator})"

    def __len__(self):
        return math.gcd(self.numerator, self.denominator)

    def __add__(self, other):
        # YOUR CODE
        pass

    def __sub__(self, other):
        # YOUR CODE
        pass

    def __mul__(self, other):
        # YOUR CODE
        pass

    def __truediv__(self, other):
        # YOUR CODE
        pass

    def __eq__(self, other):
        # YOUR CODE
        pass

    def __lt__(self, other):
        # YOUR CODE
        pass

# Test
r1 = Rational(1, 2)
r2 = Rational(1, 3)
r3 = Rational(2, 4)  # Simplifies to 1/2

print(r1 + r2)  # 5/6
print(r1 - r2)  # 1/6
print(r1 * r2)  # 1/6
print(r1 / r2)  # 3/2
print(r1 == r3)  # True
print(r1 < r2)  # False
```

**Solution:**
```python
import math

class Rational:
    def __init__(self, numerator, denominator):
        if denominator == 0:
            raise ValueError("Denominator cannot be zero")

        gcd = math.gcd(abs(numerator), abs(denominator))
        self.numerator = numerator // gcd
        self.denominator = denominator // gcd

        if self.denominator < 0:
            self.numerator = -self.numerator
            self.denominator = -self.denominator

    def __str__(self):
        if self.denominator == 1:
            return str(self.numerator)
        return f"{self.numerator}/{self.denominator}"

    def __repr__(self):
        return f"Rational({self.numerator}, {self.denominator})"

    def __add__(self, other):
        if isinstance(other, int):
            other = Rational(other, 1)
        num = self.numerator * other.denominator + other.numerator * self.denominator
        denom = self.denominator * other.denominator
        return Rational(num, denom)

    def __sub__(self, other):
        if isinstance(other, int):
            other = Rational(other, 1)
        num = self.numerator * other.denominator - other.numerator * self.denominator
        denom = self.denominator * other.denominator
        return Rational(num, denom)

    def __mul__(self, other):
        if isinstance(other, int):
            other = Rational(other, 1)
        return Rational(self.numerator * other.numerator,
                       self.denominator * other.denominator)

    def __truediv__(self, other):
        if isinstance(other, int):
            other = Rational(other, 1)
        return Rational(self.numerator * other.denominator,
                       self.denominator * other.numerator)

    def __eq__(self, other):
        if isinstance(other, int):
            other = Rational(other, 1)
        return (self.numerator == other.numerator and
                self.denominator == other.denominator)

    def __lt__(self, other):
        if isinstance(other, int):
            other = Rational(other, 1)
        return (self.numerator * other.denominator <
                other.numerator * self.denominator)

r1 = Rational(1, 2)
r2 = Rational(1, 3)
r3 = Rational(2, 4)

print(r1 + r2)
print(r1 - r2)
print(r1 * r2)
print(r1 / r2)
print(r1 == r3)
print(r1 < r2)
```

---

#### Activity 3: Build a Rectangle Class with Full Features

**Objective:** Create a Rectangle class with multiple special methods.

**Requirements:**
- Attributes: width, height
- __len__(): perimeter
- __mul__(): scale rectangle
- __add__(): combine rectangles (not overlap, just larger rectangle)
- __eq__(): compare area
- __lt__(): compare by area
- __str__() and __repr__()

**Starter Code:**
```python
class Rectangle:
    def __init__(self, width, height):
        if width <= 0 or height <= 0:
            raise ValueError("Width and height must be positive")
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

    def __str__(self):
        return f"Rectangle {self.width}x{self.height}"

    def __repr__(self):
        return f"Rectangle(width={self.width}, height={self.height})"

    def __len__(self):
        return self.perimeter()

    def __mul__(self, factor):
        return Rectangle(self.width * factor, self.height * factor)

    def __add__(self, other):
        # Combine into larger rectangle
        # YOUR CODE
        pass

    def __eq__(self, other):
        # Compare by area
        return self.area() == other.area()

    def __lt__(self, other):
        return self.area() < other.area()

# Test
r1 = Rectangle(5, 3)
r2 = Rectangle(4, 4)
r3 = Rectangle(6, 2.5)  # Same area as r1

print(r1)
print(r1.area())
print(len(r1))

print(r1 * 2)
print(r1 + r2)

print(r1 == r3)  # True (same area)
print(r1 < r2)   # True (15 < 16)

rects = [r1, r2, r3, Rectangle(3, 3)]
sorted_rects = sorted(rects)
for r in sorted_rects:
    print(f"{r}: area {r.area()}")
```

**Solution:**
```python
class Rectangle:
    def __init__(self, width, height):
        if width <= 0 or height <= 0:
            raise ValueError("Width and height must be positive")
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

    def __str__(self):
        return f"Rectangle {self.width}x{self.height}"

    def __repr__(self):
        return f"Rectangle(width={self.width}, height={self.height})"

    def __len__(self):
        return int(self.perimeter())

    def __mul__(self, factor):
        return Rectangle(self.width * factor, self.height * factor)

    def __add__(self, other):
        # Combine width and height
        new_width = max(self.width, other.width)
        new_height = self.height + other.height
        return Rectangle(new_width, new_height)

    def __eq__(self, other):
        return abs(self.area() - other.area()) < 0.001

    def __lt__(self, other):
        return self.area() < other.area()

    def __le__(self, other):
        return self.area() <= other.area()

    def __gt__(self, other):
        return self.area() > other.area()

    def __ge__(self, other):
        return self.area() >= other.area()

r1 = Rectangle(5, 3)
r2 = Rectangle(4, 4)
r3 = Rectangle(6, 2.5)

print(r1)
print(f"Area: {r1.area()}")
print(f"Perimeter (len): {len(r1)}")

print(r1 * 2)
print(r1 + r2)

print(r1 == r3)
print(r1 < r2)

rects = [r1, r2, r3, Rectangle(3, 3)]
sorted_rects = sorted(rects)
for r in sorted_rects:
    print(f"{r}: area {r.area()}")
```

### Reflection Questions

1. **How do special methods make objects more "Pythonic"?**
2. **Which special method was most useful in your design?**
3. **How did simplification help in the Rational class?**
4. **What validation was important in these classes?**

### Extension Challenges

**Challenge 1:** Add __bool__() to Money to check if amount is positive.

**Challenge 2:** Add __hash__() to Money to use as dictionary keys.

**Challenge 3:** Create a Vector2D class with full arithmetic support and cross product.
