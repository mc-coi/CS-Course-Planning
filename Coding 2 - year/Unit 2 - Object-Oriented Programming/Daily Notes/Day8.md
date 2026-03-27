# Day 8: Encapsulation Lab
**Learning Target:** I can apply encapsulation principles to build secure, well-designed classes with proper data protection.

### Lab Activities

#### Activity 1: Build a Secure User Account System

**Objective:** Create a `User` class that securely manages user information with encapsulation.

**Requirements:**
- Private attributes: `_username`, `_password`, `_email`, `_created_date`
- Class variable: `user_count` (track total users)
- Properties (with validation):
  - `username` (read-only after creation)
  - `email` (can be changed, must contain @)
  - `password` (write-only, minimum 8 characters)
- Methods:
  - `verify_password(password)` — checks if given password matches
  - `change_password(old_password, new_password)` — change with verification
  - `display_info()` — shows username and email (not password!)

**Starter Code:**
```python
from datetime import datetime

class User:
    user_count = 0

    def __init__(self, username, password, email):
        # YOUR CODE HERE
        pass

    @property
    def username(self):
        # YOUR CODE HERE
        pass

    @property
    def email(self):
        # YOUR CODE HERE
        pass

    @email.setter
    def email(self, value):
        # YOUR CODE HERE
        pass

    @property
    def password(self):
        # Password is write-only, no getter
        pass

    @password.setter
    def password(self, value):
        # YOUR CODE HERE
        pass

    def verify_password(self, password):
        # YOUR CODE HERE
        pass

    def change_password(self, old_password, new_password):
        # YOUR CODE HERE
        pass

    def display_info(self):
        # YOUR CODE HERE
        pass

# Test your code
user1 = User("alice", "securepass123", "alice@example.com")
user1.display_info()

user2 = User("bob", "password456", "bob@example.com")
user2.display_info()

print(f"Total users: {User.user_count}")

# Try to change password
print(user1.verify_password("securepass123"))  # True
user1.change_password("securepass123", "newpass789")
print(user1.verify_password("newpass789"))  # True

# Try invalid operations
user1.email = "alice@newdomain.com"
print(user1.email)  # alice@newdomain.com
```

**Expected Output:**
```
Username: alice
Email: alice@example.com

Username: bob
Email: bob@example.com

Total users: 2
True
True
alice@newdomain.com
```

**Solution:**
```python
from datetime import datetime

class User:
    user_count = 0

    def __init__(self, username, password, email):
        self._username = username
        self._password = password
        self._email = email
        self._created_date = datetime.now()
        User.user_count = User.user_count + 1

    @property
    def username(self):
        return self._username

    @property
    def email(self):
        return self._email

    @email.setter
    def email(self, value):
        if "@" in value and len(value) > 3:
            self._email = value
        else:
            print("Invalid email address!")

    @property
    def password(self):
        raise AttributeError("Password cannot be read")

    @password.setter
    def password(self, value):
        if len(value) >= 8:
            self._password = value
        else:
            print("Password must be at least 8 characters!")

    def verify_password(self, password):
        return password == self._password

    def change_password(self, old_password, new_password):
        if self.verify_password(old_password):
            self.password = new_password
            return True
        else:
            print("Old password incorrect!")
            return False

    def display_info(self):
        print(f"Username: {self._username}")
        print(f"Email: {self._email}")
        print()

user1 = User("alice", "securepass123", "alice@example.com")
user1.display_info()

user2 = User("bob", "password456", "bob@example.com")
user2.display_info()

print(f"Total users: {User.user_count}")

print(user1.verify_password("securepass123"))
user1.change_password("securepass123", "newpass789")
print(user1.verify_password("newpass789"))

user1.email = "alice@newdomain.com"
print(user1.email)
```

---

#### Activity 2: Build a Credit Card Class with Data Protection

**Objective:** Create a `CreditCard` class that safely manages sensitive financial data.

**Requirements:**
- Private attributes: `_card_number`, `_cvv`, `_expiration`, `_balance`
- Properties:
  - `card_number` (read-only, masked when displayed)
  - `cvv` (write-only)
  - `balance` (read-only)
  - `expiration` (read-only)
- Methods:
  - `charge(amount, cvv)` — verify CVV before charging
  - `pay(amount)` — add payment to balance
  - `display_card()` — shows masked card info

**Starter Code:**
```python
class CreditCard:
    def __init__(self, card_number, cvv, expiration, balance):
        # YOUR CODE HERE
        pass

    @property
    def card_number(self):
        # Return masked number for security
        # Should show only last 4 digits
        pass

    @property
    def cvv(self):
        # Write-only, no getter
        pass

    @cvv.setter
    def cvv(self, value):
        # YOUR CODE HERE
        pass

    @property
    def balance(self):
        # YOUR CODE HERE
        pass

    @property
    def expiration(self):
        # YOUR CODE HERE
        pass

    def charge(self, amount, cvv):
        # YOUR CODE HERE
        pass

    def pay(self, amount):
        # YOUR CODE HERE
        pass

    def display_card(self):
        # YOUR CODE HERE
        pass

# Test your code
card = CreditCard("1234567890123456", "123", "12/25", 5000)
card.display_card()

card.charge(100, "123")  # Valid CVV
print(f"Balance after charge: ${card.balance}")

card.charge(50, "999")  # Invalid CVV
print(f"Balance after invalid charge: ${card.balance}")

card.pay(150)
print(f"Balance after payment: ${card.balance}")
```

**Expected Output:**
```
Card: ****3456
Expiration: 12/25
Balance: $5000.00

Balance after charge: $4900.00
Invalid CVV!
Balance after invalid charge: $4900.00
Balance after payment: $5050.00
```

**Solution:**
```python
class CreditCard:
    def __init__(self, card_number, cvv, expiration, balance):
        self._card_number = card_number
        self._cvv = cvv
        self._expiration = expiration
        self._balance = balance

    @property
    def card_number(self):
        # Mask the card number
        return f"****{self._card_number[-4:]}"

    @property
    def cvv(self):
        raise AttributeError("CVV cannot be read")

    @cvv.setter
    def cvv(self, value):
        self._cvv = value

    @property
    def balance(self):
        return self._balance

    @property
    def expiration(self):
        return self._expiration

    def charge(self, amount, cvv):
        if cvv == self._cvv:
            if amount <= self._balance:
                self._balance = self._balance - amount
                print(f"Charged ${amount}")
                return True
            else:
                print("Insufficient funds!")
                return False
        else:
            print("Invalid CVV!")
            return False

    def pay(self, amount):
        if amount > 0:
            self._balance = self._balance + amount
            print(f"Payment of ${amount} received")

    def display_card(self):
        print(f"Card: {self.card_number}")
        print(f"Expiration: {self._expiration}")
        print(f"Balance: ${self._balance:.2f}")
        print()

card = CreditCard("1234567890123456", "123", "12/25", 5000)
card.display_card()

card.charge(100, "123")
print(f"Balance after charge: ${card.balance}")

card.charge(50, "999")
print(f"Balance after invalid charge: ${card.balance}")

card.pay(150)
print(f"Balance after payment: ${card.balance}")
```

---

#### Activity 3: Build a Gradebook Class with Validation

**Objective:** Create a `GradeBook` class that manages student grades with proper encapsulation.

**Requirements:**
- Private attributes: `_student_name`, `_grades` (list), `_weights` (dict for weighted categories)
- Properties:
  - `student_name` (read-only)
  - `grades` (return copy, not original list)
- Methods:
  - `add_grade(grade, category)` — add grade with validation (0-100)
  - `get_average()` — average of all grades
  - `get_weighted_average()` — weighted average by category
  - `get_letter_grade()` — converts numeric to letter
  - `display_report()` — shows comprehensive grade info

**Starter Code:**
```python
class GradeBook:
    def __init__(self, student_name):
        # YOUR CODE HERE
        pass

    @property
    def student_name(self):
        # YOUR CODE HERE
        pass

    @property
    def grades(self):
        # YOUR CODE HERE (return copy)
        pass

    def add_grade(self, grade, category="General"):
        # Validate grade is 0-100
        # Add to list and track by category
        pass

    def get_average(self):
        # YOUR CODE HERE
        pass

    def get_letter_grade(self):
        # A: 90-100, B: 80-89, C: 70-79, D: 60-69, F: <60
        pass

    def display_report(self):
        # YOUR CODE HERE
        pass

# Test your code
book = GradeBook("Alice")
book.add_grade(95, "Homework")
book.add_grade(88, "Homework")
book.add_grade(92, "Quiz")
book.add_grade(85, "Exam")
book.add_grade(90, "Project")

book.display_report()
```

**Expected Output:**
```
=== Grade Report for Alice ===
Grades: [95, 88, 92, 85, 90]
Average: 90.00
Letter Grade: A
```

**Solution:**
```python
class GradeBook:
    def __init__(self, student_name):
        self._student_name = student_name
        self._grades = []
        self._categories = {}

    @property
    def student_name(self):
        return self._student_name

    @property
    def grades(self):
        return self._grades.copy()

    def add_grade(self, grade, category="General"):
        if 0 <= grade <= 100:
            self._grades.append(grade)
            if category not in self._categories:
                self._categories[category] = []
            self._categories[category].append(grade)
        else:
            print("Grade must be between 0 and 100!")

    def get_average(self):
        if len(self._grades) == 0:
            return 0
        return sum(self._grades) / len(self._grades)

    def get_letter_grade(self):
        avg = self.get_average()
        if avg >= 90:
            return "A"
        elif avg >= 80:
            return "B"
        elif avg >= 70:
            return "C"
        elif avg >= 60:
            return "D"
        else:
            return "F"

    def display_report(self):
        print(f"=== Grade Report for {self._student_name} ===")
        print(f"Grades: {self._grades}")
        print(f"Average: {self.get_average():.2f}")
        print(f"Letter Grade: {self.get_letter_grade()}")
        print()

book = GradeBook("Alice")
book.add_grade(95, "Homework")
book.add_grade(88, "Homework")
book.add_grade(92, "Quiz")
book.add_grade(85, "Exam")
book.add_grade(90, "Project")

book.display_report()
```

---

### Reflection Questions

1. **Why is encapsulation important for security-sensitive classes like User and CreditCard?**
2. **When would you use a property instead of a regular getter/setter method?**
3. **How does validation in setters improve code reliability?**
4. **What happens if you try to access a write-only property for reading?**

### Extension Challenges

**Challenge 1:** Modify the User class to track last login time and enforce password expiration (must change password every 90 days).

**Challenge 2:** Add multi-step verification to CreditCard (CVV + PIN) before allowing a charge.

**Challenge 3:** Create a Teacher class that manages multiple GradeBook objects for different students.
