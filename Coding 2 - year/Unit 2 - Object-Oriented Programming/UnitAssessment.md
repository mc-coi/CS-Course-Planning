# Unit 2: Object-Oriented Programming — Unit Assessment

**Student Name:** _____________________ **Date:** _________

**Total Points:** 100

---

## Part 1: Multiple Choice (30 points, 3 points each)

Select the best answer for each question.

**1.** What is the primary purpose of the `__init__` method?
- A) To delete an object when done
- B) To initialize instance variables when an object is created
- C) To define class variables
- D) To return the object to its caller

<details>
<summary>Answer</summary>
B) To initialize instance variables when an object is created
</details>

---

**2.** What does `self` represent in a class method?
- A) The class itself
- B) The current instance of the class
- C) A static reference to the module
- D) A required keyword with no special meaning

<details>
<summary>Answer</summary>
B) The current instance of the class
</details>

---

**3.** What is the difference between a class variable and an instance variable?
- A) Class variables are larger in memory
- B) Instance variables are created in `__init__` and unique to each object; class variables are shared by all instances
- C) They are the same thing with different names
- D) Class variables only exist in parent classes

<details>
<summary>Answer</summary>
B) Instance variables are created in `__init__` and unique to each object; class variables are shared by all instances
</details>

---

**4.** Which decorator is used to create a method that doesn't have access to `self` or `cls`?
- A) `@property`
- B) `@classmethod`
- C) `@staticmethod`
- D) `@abstractmethod`

<details>
<summary>Answer</summary>
C) `@staticmethod`
</details>

---

**5.** What is the purpose of `super()`?
- A) To create a new object
- B) To call a parent class's method
- C) To make a method static
- D) To define an abstract method

<details>
<summary>Answer</summary>
B) To call a parent class's method
</details>

---

**6.** What is polymorphism?
- A) Multiple classes with the same name
- B) The ability to use objects of different types with the same interface
- C) The process of copying code from one class to another
- D) Creating objects inside other objects

<details>
<summary>Answer</summary>
B) The ability to use objects of different types with the same interface
</details>

---

**7.** Which special method allows an object to be used in a `for` loop?
- A) `__len__`
- B) `__str__`
- C) `__iter__`
- D) `__eq__`

<details>
<summary>Answer</summary>
C) `__iter__`
</details>

---

**8.** What does the `@property` decorator allow you to do?
- A) Define static methods
- B) Access a method like an attribute (without parentheses)
- C) Define class methods
- D) Create abstract classes

<details>
<summary>Answer</summary>
B) Access a method like an attribute (without parentheses)
</details>

---

**9.** When should you use composition instead of inheritance?
- A) When you need to add functionality from multiple unrelated classes
- B) Always use inheritance
- C) Never use composition
- D) Only when inheritance is not allowed

<details>
<summary>Answer</summary>
A) When you need to add functionality from multiple unrelated classes
</details>

---

**10.** What does `__str__` return?
- A) The type of the object
- B) A user-friendly string representation of the object
- C) A unique identifier for the object
- D) The memory address of the object

<details>
<summary>Answer</summary>
B) A user-friendly string representation of the object
</details>

---

## Part 2: Short Answer (20 points, 4 points each)

**1.** Explain the difference between `__str__` and `__repr__`.

<details>
<summary>Answer</summary>
`__str__` returns a user-friendly, readable string representation of an object (used by `print()` and `str()`). `__repr__` returns an official representation that is more technical/debugging-oriented and ideally shows how to recreate the object (used by `repr()` and in the interactive shell).
</details>

---

**2.** Write a brief explanation of when you would use a `@classmethod` instead of a regular instance method.

<details>
<summary>Answer</summary>
A `@classmethod` is used when you need to access or modify class-level data, or when you need to create an alternative constructor (like a factory method). It receives the class (`cls`) as the first parameter instead of an instance (`self`). Example: `from_string()` or `get_total_count()` for a class variable.
</details>

---

**3.** What is name mangling in Python, and why would you use it?

<details>
<summary>Answer</summary>
Name mangling is a Python convention using double underscores (`__attribute`) at the start of a name, which causes Python to rename the attribute to `_ClassName__attribute`. This is used to signal "private" attributes and prevent accidental access from outside the class. However, it's not true privacy—the attribute can still be accessed if you know the mangled name.
</details>

---

**4.** Describe the abstract class pattern and give one example of when you would use it.

<details>
<summary>Answer</summary>
An abstract class is a class that cannot be instantiated directly and serves as a template for subclasses. It defines abstract methods that subclasses MUST implement. You would use this when you want to enforce that all subclasses have certain methods. Example: An `Animal` abstract class with abstract method `make_sound()` ensures that `Dog`, `Cat`, and `Bird` all implement their own `make_sound()`.
</details>

---

**5.** Explain the Singleton design pattern in one or two sentences.

<details>
<summary>Answer</summary>
The Singleton pattern ensures that a class has only one instance throughout the program's lifetime. All calls to create a new instance return the same object. This is useful for resources that should only exist once, like a database connection or configuration manager.
</details>

---

## Part 3: Coding Challenges (50 points)

### Challenge 1: Basic Class (15 points)

Write a `Student` class that:
- Takes `name` and `student_id` in `__init__`
- Has a method `add_grade(grade)` that stores grades in a list
- Has a method `calculate_average()` that returns the average of all grades
- Has a `__str__()` method that returns `"Name: [name], ID: [id], Average: [avg]"`

**Test Code:**
```python
s = Student("Alice", "S001")
s.add_grade(90)
s.add_grade(85)
s.add_grade(92)
print(s)  # Output: Name: Alice, ID: S001, Average: 89.0
print(f"Average: {s.calculate_average()}")  # Output: Average: 89.0
```

<details>
<summary>Answer</summary>

```python
class Student:
    def __init__(self, name, student_id):
        self.name = name
        self.student_id = student_id
        self.grades = []

    def add_grade(self, grade):
        self.grades.append(grade)

    def calculate_average(self):
        if not self.grades:
            return 0
        return sum(self.grades) / len(self.grades)

    def __str__(self):
        avg = self.calculate_average()
        return f"Name: {self.name}, ID: {self.student_id}, Average: {avg}"

# Test
s = Student("Alice", "S001")
s.add_grade(90)
s.add_grade(85)
s.add_grade(92)
print(s)  # Name: Alice, ID: S001, Average: 89.0
print(f"Average: {s.calculate_average()}")  # Average: 89.0
```

</details>

---

### Challenge 2: Inheritance Hierarchy (20 points)

Create a parent class `Employee` and child classes `Manager` and `Intern`:

**Employee** (parent):
- `__init__`: `name`, `salary`
- Method: `get_info()` returns `"[name] earns $[salary]"`
- Method: `give_raise(amount)` increases salary

**Manager(Employee)**:
- `__init__`: `name`, `salary`, `team_size`
- Override `get_info()` to also include team size: `"[name] earns $[salary] and manages [team_size] people"`

**Intern(Employee)**:
- `__init__`: `name`, `salary`, `university`
- Override `get_info()` to also include university: `"[name] earns $[salary] and studies at [university]"`

**Test Code:**
```python
m = Manager("Bob", 80000, 5)
i = Intern("Charlie", 15000, "MIT")
print(m.get_info())
print(i.get_info())
m.give_raise(5000)
print(m.get_info())
```

Expected Output:
```
Bob earns $80000 and manages 5 people
Charlie earns $15000 and studies at MIT
Bob earns $85000 and manages 5 people
```

<details>
<summary>Answer</summary>

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def get_info(self):
        return f"{self.name} earns ${self.salary}"

    def give_raise(self, amount):
        self.salary += amount

class Manager(Employee):
    def __init__(self, name, salary, team_size):
        super().__init__(name, salary)
        self.team_size = team_size

    def get_info(self):
        return f"{self.name} earns ${self.salary} and manages {self.team_size} people"

class Intern(Employee):
    def __init__(self, name, salary, university):
        super().__init__(name, salary)
        self.university = university

    def get_info(self):
        return f"{self.name} earns ${self.salary} and studies at {self.university}"

# Test
m = Manager("Bob", 80000, 5)
i = Intern("Charlie", 15000, "MIT")
print(m.get_info())
print(i.get_info())
m.give_raise(5000)
print(m.get_info())
```

</details>

---

### Challenge 3: Special Methods and Composition (15 points)

Create a `BankAccount` class with:
- `__init__`: `account_holder`, `balance`
- `__add__`: merges two accounts (returns new account with combined balance)
- `__eq__`: two accounts are equal if same holder name
- `__lt__`: compare by balance
- `__str__`: formatted account info

Create an `ATM` class (composition) that:
- Holds a list of `BankAccount` objects
- Method: `add_account(account)`
- Method: `find_account(name)` returns account or None
- Method: `__len__`: returns number of accounts

**Test Code:**
```python
atm = ATM()
acc1 = BankAccount("Alice", 1000)
acc2 = BankAccount("Bob", 500)
atm.add_account(acc1)
atm.add_account(acc2)

print(atm.find_account("Alice"))  # Alice's account
print(len(atm))  # 2
print(acc1 > acc2)  # True (1000 > 500)

merged = acc1 + acc2
print(merged)  # Combined account
```

<details>
<summary>Answer</summary>

```python
class BankAccount:
    def __init__(self, account_holder, balance):
        self.account_holder = account_holder
        self.balance = balance

    def __add__(self, other):
        new_balance = self.balance + other.balance
        return BankAccount(f"{self.account_holder} & {other.account_holder}", new_balance)

    def __eq__(self, other):
        return self.account_holder == other.account_holder

    def __lt__(self, other):
        return self.balance < other.balance

    def __gt__(self, other):
        return self.balance > other.balance

    def __str__(self):
        return f"{self.account_holder}: ${self.balance}"

class ATM:
    def __init__(self):
        self.accounts = []

    def add_account(self, account):
        self.accounts.append(account)

    def find_account(self, name):
        for account in self.accounts:
            if account.account_holder == name:
                return account
        return None

    def __len__(self):
        return len(self.accounts)

# Test
atm = ATM()
acc1 = BankAccount("Alice", 1000)
acc2 = BankAccount("Bob", 500)
atm.add_account(acc1)
atm.add_account(acc2)

print(atm.find_account("Alice"))  # Alice: $1000
print(len(atm))  # 2
print(acc1 > acc2)  # True
merged = acc1 + acc2
print(merged)  # Alice & Bob: $1500
```

</details>

---

## Answer Key Summary

| Section | Total Points |
|---------|--------------|
| Part 1: Multiple Choice (10 × 3) | 30 |
| Part 2: Short Answer (5 × 4) | 20 |
| Part 3: Coding Challenges | 50 |
| **TOTAL** | **100** |

### Grading Rubric for Coding Challenges

**Challenge 1: Basic Class (15 points)**
- Constructor correctly initializes attributes (3 pts)
- `add_grade()` method works (3 pts)
- `calculate_average()` returns correct value (4 pts)
- `__str__()` returns properly formatted string (3 pts)
- Code runs without errors (2 pts)

**Challenge 2: Inheritance (20 points)**
- `Employee` class correctly defined (5 pts)
- `Manager` class inherits and overrides correctly (7 pts)
- `Intern` class inherits and overrides correctly (5 pts)
- `give_raise()` works correctly (2 pts)
- Output matches expected (1 pt)

**Challenge 3: Special Methods & Composition (15 points)**
- `BankAccount` class with all special methods (7 pts)
- `__add__`, `__eq__`, `__lt__`, `__gt__` work correctly (5 pts)
- `ATM` class with composition (2 pts)
- All test code runs and produces correct output (1 pt)

---

## Passing Score: 70/100 (70%)

**Excellent:** 90-100
**Proficient:** 80-89
**Developing:** 70-79
**Below Standard:** Below 70

