# Day 74: Input Validation Loops — Defensive Programming

**Learning Target:** I can write loops that repeatedly ask for input until the user provides valid data.

### Key Concepts

**Input validation** means checking that user input is acceptable before using it. Rather than crashing or producing wrong results when given bad input, a program should ask the user to try again.

**Input Validation Loop Pattern:**
```python
while True:
    value = input("Enter a value: ")
    if is_valid(value):
        break  # Valid input, exit loop
    else:
        print("Invalid input. Please try again.")
# value is now guaranteed to be valid
```

**Types of validation:**
- **Range check:** Is the value within acceptable bounds? (age 0–120, score 0–100)
- **Type check:** Can the string be converted to the right type? (is it a valid integer?)
- **Pattern check:** Does it match a required pattern? (email format, phone number)
- **List check:** Is it one of a set of options? (choice from 1–3, day of week)

**Benefits:**
- Program doesn't crash on bad input
- User gets immediate feedback
- Loop guarantees valid input for the rest of the program

### Code Examples

```python
# Example 1: Age validation (range check)
while True:
    age = int(input("Enter age (1-120): "))
    if 1 <= age <= 120:
        break
    print("Invalid. Age must be 1-120.")
print(f"Your age: {age}\n")

# Example 2: Menu choice (list check)
while True:
    print("1. Start game")
    print("2. Load game")
    print("3. Exit")
    choice = input("Choose (1-3): ")
    if choice in ["1", "2", "3"]:
        break
    print("Invalid choice. Try again.\n")
print(f"You chose: {choice}\n")

# Example 3: Password strength (pattern check)
while True:
    password = input("Enter password (8+ chars, with number): ")
    has_number = any(char.isdigit() for char in password)
    if len(password) >= 8 and has_number:
        break
    print("Password must be 8+ characters and include a number.\n")
print("Password accepted!\n")

# Example 4: Non-negative number
while True:
    try:
        value = float(input("Enter a positive number: "))
        if value > 0:
            break
        print("Must be positive (greater than 0).")
    except ValueError:
        print("That's not a valid number.")
print(f"You entered: {value}\n")

# Example 5: Yes/no decision
while True:
    answer = input("Do you want to continue? (yes/no): ").lower()
    if answer in ["yes", "no", "y", "n"]:
        break
    print("Please enter 'yes' or 'no'.")
if answer.startswith("y"):
    print("Great! Let's continue.")
else:
    print("Goodbye!")
```

### Guided Practice

Write a program that:
1. Asks for a number between 10 and 50
2. Keeps asking if the input is out of range
3. Once valid, prints "You entered: [number]"

Then, extend it to also validate that the input is actually a number (not text).

### Practice Problems

**Problem 1 — Beginner:** Write a validation loop that asks for a grade (A, B, C, D, F) and keeps asking until one of these is entered.

```python
# Starter code
while True:
    grade = input("Enter grade (A-F): ").upper()
    # Your code here
```

**Problem 2 — Intermediate:** Write a validation loop that asks for a quantity (must be 1–100) and a price per item (must be positive). Accept both, then calculate and print the total cost.

**Problem 3 — Challenge:** Write a program that validates three pieces of information:
- Name (non-empty string)
- Age (1–120)
- Email (must contain "@" and ".")

Ask for each with validation, then print a summary.

<details>
<summary>💡 Hints</summary>

- Problem 1: Check if grade is in the list ["A", "B", "C", "D", "F"]
- Problem 2: Validate quantity is in range, validate price > 0. You might need two nested validation loops.
- Problem 3: For name, check `len(name) > 0`. For email, check `"@" in email and "." in email`

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
while True:
    grade = input("Enter grade (A-F): ").upper()
    if grade in ["A", "B", "C", "D", "F"]:
        break
    print("Invalid grade. Try again.")
print(f"Grade: {grade}\n")

# Problem 2 Example
while True:
    quantity = int(input("Quantity (1-100): "))
    if 1 <= quantity <= 100:
        break
    print("Must be 1-100.")

while True:
    price = float(input("Price per item: $"))
    if price > 0:
        break
    print("Price must be positive.")

total = quantity * price
print(f"Total: ${total:.2f}\n")

# Problem 3 Example
while True:
    name = input("Name: ")
    if len(name) > 0:
        break
    print("Name cannot be empty.")

while True:
    age = int(input("Age: "))
    if 1 <= age <= 120:
        break
    print("Age must be 1-120.")

while True:
    email = input("Email: ")
    if "@" in email and "." in email:
        break
    print("Invalid email format.")

print(f"\nName: {name}")
print(f"Age: {age}")
print(f"Email: {email}")
```

</details>

---
