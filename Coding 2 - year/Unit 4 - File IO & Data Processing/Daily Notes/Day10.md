# Day 10: Custom Exceptions — Creating Your Own
**Learning Target:** I can create custom exception classes that inherit from Exception and use them in my programs.

### Key Concepts

**Custom exceptions:** Classes that inherit from Exception to represent specific error conditions in your program.

**Inheritance:** Custom exceptions extend the Exception class using `class MyException(Exception):`.

**Why create custom exceptions:** Makes code more readable and allows you to distinguish between different types of errors.

**__init__() method:** Optionally define to customize the exception initialization and message.

**raise custom exception:** Use `raise YourCustomException("message")` just like built-in exceptions.

**Catching custom exceptions:** Use except blocks with your custom exception class.

### Code Examples

```python
# Example 1: Simple custom exception
class InvalidScoreError(Exception):
    pass

def validate_score(score):
    if score < 0 or score > 100:
        raise InvalidScoreError("Score must be between 0 and 100")
    return score

try:
    validate_score(150)
except InvalidScoreError as e:
    print(f"Error: {e}")

# Example 2: Custom exception with __init__
class InsufficientFundsError(Exception):
    def __init__(self, amount, balance):
        self.amount = amount
        self.balance = balance
        message = f"Cannot withdraw ${amount}. Balance: ${balance}"
        super().__init__(message)

def withdraw(amount, balance):
    if amount > balance:
        raise InsufficientFundsError(amount, balance)
    return balance - amount

try:
    new_balance = withdraw(100, 50)
except InsufficientFundsError as e:
    print(f"Transaction failed: {e}")

# Example 3: Multiple custom exceptions
class EmptyFieldError(Exception):
    pass

class InvalidEmailError(Exception):
    pass

class InvalidAgeError(Exception):
    pass

def register_user(name, email, age):
    if not name:
        raise EmptyFieldError("Name cannot be empty")
    if "@" not in email:
        raise InvalidEmailError(f"Invalid email: {email}")
    if age < 13:
        raise InvalidAgeError(f"User must be 13+, got {age}")
    return f"User registered: {name}"

data = [
    ("Alice", "alice@example.com", 25),
    ("", "bob@example.com", 30),
    ("Carol", "invalid-email", 20)
]

for name, email, age in data:
    try:
        print(register_user(name, email, age))
    except EmptyFieldError as e:
        print(f"Form error: {e}")
    except InvalidEmailError as e:
        print(f"Email error: {e}")
    except InvalidAgeError as e:
        print(f"Age error: {e}")

# Example 4: Exception hierarchy
class ValidationError(Exception):
    pass

class DataFormatError(ValidationError):
    pass

class RangeError(ValidationError):
    pass

def parse_temperature(temp_str):
    try:
        temp = float(temp_str)
    except ValueError:
        raise DataFormatError(f"Temperature must be a number, got {temp_str}")

    if temp < -50 or temp > 150:
        raise RangeError(f"Temperature {temp} is unrealistic")

    return temp

temps = ["25.5", "abc", "200"]
for temp in temps:
    try:
        result = parse_temperature(temp)
        print(f"Temperature: {result}°C")
    except DataFormatError as e:
        print(f"Format error: {e}")
    except RangeError as e:
        print(f"Range error: {e}")

# Example 5: Custom exception with context
class FileProcessingError(Exception):
    def __init__(self, filename, message):
        self.filename = filename
        self.message = message
        super().__init__(f"Error processing {filename}: {message}")

def process_file(filename):
    if not filename.endswith('.txt'):
        raise FileProcessingError(filename, "Only .txt files supported")
    return f"Processing {filename}"

try:
    process_file("data.csv")
except FileProcessingError as e:
    print(f"Processing failed: {e}")

# Example 6: Catching parent and child exceptions
class PaymentError(Exception):
    pass

class InsufficientBalance(PaymentError):
    pass

class InvalidCard(PaymentError):
    pass

def process_payment(card_valid, balance, amount):
    if not card_valid:
        raise InvalidCard("Card is invalid")
    if amount > balance:
        raise InsufficientBalance(f"Need ${amount}, have ${balance}")
    return True

try:
    process_payment(True, 50, 100)
except InsufficientBalance as e:
    print(f"Balance error: {e}")
except InvalidCard as e:
    print(f"Card error: {e}")
except PaymentError as e:
    print(f"General payment error: {e}")

# Example 7: Chaining exceptions (showing context)
class DatabaseError(Exception):
    pass

def connect_database(host):
    try:
        # Simulate connection failure
        if not host:
            raise ValueError("Host cannot be empty")
    except ValueError as e:
        raise DatabaseError(f"Failed to connect: {e}") from e

try:
    connect_database("")
except DatabaseError as e:
    print(f"Error: {e}")
```

### Guided Practice

**Activity: Custom Exception System**

1. Create three custom exceptions:
   - `InvalidPasswordError`: For password validation failures
   - `UserAlreadyExistsError`: When trying to create duplicate user
   - `IncompleteProfileError`: When required fields are missing

2. Create a `register_user()` function that uses these exceptions
3. Test with various inputs that trigger each exception

**Step-by-step code:**
```python
class InvalidPasswordError(Exception):
    pass

class UserAlreadyExistsError(Exception):
    pass

class IncompleteProfileError(Exception):
    pass

def register_user(username, password, email, existing_users):
    if not username or not password or not email:
        raise IncompleteProfileError("All fields required")

    if len(password) < 8:
        raise InvalidPasswordError("Password must be 8+ characters")

    if username in existing_users:
        raise UserAlreadyExistsError(f"User {username} already exists")

    return True

existing = ["alice", "bob"]
users_to_register = [
    ("charlie", "secure123", "charlie@example.com"),
    ("alice", "password", "alice2@example.com"),
    ("dave", "short", "dave@example.com")
]

for username, password, email in users_to_register:
    try:
        register_user(username, password, email, existing)
        print(f"✓ {username} registered successfully")
    except IncompleteProfileError as e:
        print(f"✗ {username}: {e}")
    except InvalidPasswordError as e:
        print(f"✗ {username}: {e}")
    except UserAlreadyExistsError as e:
        print(f"✗ {username}: {e}")
```

### Practice Problems

**Problem 1 — Beginner:** Create a custom exception class called `NegativeNumberError` and write a function that raises it when given a negative number.

**Problem 2 — Intermediate:** Create multiple custom exceptions for a simple login system (InvalidUsername, IncorrectPassword, AccountLocked). Write a login function that uses them.

**Problem 3 — Challenge:** Create a custom exception hierarchy with a parent `DataValidationError` and children (RangeError, TypeMismatchError, DuplicateError). Implement a data validation function that uses all three.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Define `class NegativeNumberError(Exception): pass`.
- Check the input in your function.
- Raise the exception with a message.

**Problem 2:**
- Create three separate exception classes.
- In the login function, check username, password, and locked status.
- Raise appropriate exception for each case.

**Problem 3:**
- Create parent class that inherits from Exception.
- Create three child classes that inherit from the parent.
- Implement validation checks for each error type.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class NegativeNumberError(Exception):
    pass

def check_number(num):
    if num < 0:
        raise NegativeNumberError(f"{num} is negative")
    return num

try:
    check_number(-5)
except NegativeNumberError as e:
    print(f"Error: {e}")

# Problem 2
class InvalidUsername(Exception):
    pass

class IncorrectPassword(Exception):
    pass

class AccountLocked(Exception):
    pass

def login(username, password, valid_users, locked_users):
    if username not in valid_users:
        raise InvalidUsername(f"User {username} not found")
    if username in locked_users:
        raise AccountLocked(f"Account {username} is locked")
    if valid_users[username] != password:
        raise IncorrectPassword("Wrong password")
    return True

users = {"alice": "pass123", "bob": "secure"}
locked = ["charlie"]

try:
    login("alice", "pass123", users, locked)
    print("Login successful")
except (InvalidUsername, IncorrectPassword, AccountLocked) as e:
    print(f"Login failed: {e}")

# Problem 3
class DataValidationError(Exception):
    pass

class RangeError(DataValidationError):
    pass

class TypeMismatchError(DataValidationError):
    pass

class DuplicateError(DataValidationError):
    pass

def validate_record(value, expected_type, min_val, max_val, existing_values):
    if not isinstance(value, expected_type):
        raise TypeMismatchError(f"Expected {expected_type.__name__}")
    if value < min_val or value > max_val:
        raise RangeError(f"Must be {min_val}-{max_val}")
    if value in existing_values:
        raise DuplicateError(f"Value {value} already exists")
    return True

existing = [5, 10, 15]
try:
    validate_record(20, int, 0, 100, existing)
    print("Validation passed")
except DataValidationError as e:
    print(f"Validation error: {e}")
```

</details>
    print(students)

# Example 2: Write Python dict to JSON file
data = {
    "name": "Alice",
    "age": 16,
    "grades": [90, 85, 92]
}
with open('student.json', 'w') as f:
    json.dump(data, f, indent=2)

# Example 3: Read, modify, and write back
with open('config.json', 'r') as f:
    config = json.load(f)

# Modify the data
config['theme'] = 'dark'
config['font_size'] = 14

# Write updated data back to file
with open('config.json', 'w') as f:
    json.dump(config, f, indent=2)

# Example 4: Handling file not found errors
import os
json_file = 'data.json'
if os.path.exists(json_file):
    with open(json_file, 'r') as f:
        data = json.load(f)
else:
    print(f"{json_file} not found")
    data = []

# Example 5: Reading a list from JSON file
# Assuming data.json contains: [{"id": 1, "name": "Item1"}, {"id": 2, "name": "Item2"}]
with open('data.json', 'r') as f:
    items = json.load(f)
    for item in items:
        print(f"{item['id']}: {item['name']}")
```

---

## Guided Practice

1. **Create a JSON file** named `books.json` containing at least 2 books with fields: title, author, and year.
2. **Write Python code** that reads this file using `json.load()`.
3. **Access and print** information about each book.
4. **Add a new book** to the data and write it back to the file using `json.dump()`.
5. **Verify** the file was updated correctly by reading it again.

---

## Practice Problems

**Beginner:** Write code that opens a JSON file called `config.json`, reads it, and prints the value of the key `'theme'`.

**Intermediate:** Write code that reads a JSON file containing a list of products (each with name and price), calculates the total cost, and prints it.

**Challenge:** Write code that reads a JSON file, adds a new entry to the main data structure, and writes it back to the same file without losing existing data.

<details>
<summary>💡 Hints</summary>
- Beginner: Use `json.load()` with an open file object, then access the dict key.
- Intermediate: The JSON file contains a list; loop through it, sum the prices.
- Challenge: Read the file, modify the structure (append to a list or add a key), then write back with `json.dump()`.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
import json

# Beginner
with open('config.json', 'r') as f:
    config = json.load(f)
    print(config['theme'])

# Intermediate
with open('products.json', 'r') as f:
    products = json.load(f)
    total = sum(p['price'] for p in products)
    print(f"Total: ${total}")

# Challenge
with open('data.json', 'r') as f:
    data = json.load(f)

# Add new entry
new_entry = {"id": 3, "name": "New Item"}
data.append(new_entry)

# Write back
with open('data.json', 'w') as f:
    json.dump(data, f, indent=2)
```
</details>
