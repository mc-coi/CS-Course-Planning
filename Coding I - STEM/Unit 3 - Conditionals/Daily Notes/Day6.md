# Day 6: Nested Conditionals
**Learning Target:** I can write nested conditionals for complex decisions.

### Key Concepts
A **nested conditional** is an if statement inside another if statement. Indentation determines nesting level.

Use nested conditionals for dependent decisions. Sometimes logical operators (`and`/`or`) are cleaner than nesting.

### Code Examples
```python
# Nested if/else
age = 17
if age >= 18:
    print("You can vote")
    if age >= 65:
        print("Senior voting benefits apply")
else:
    print("You cannot vote yet")

# Access control — nested example
is_admin = True
if is_admin:
    action = input("Admin action: ")
    if action == "delete":
        print("Deleting...")
    elif action == "edit":
        print("Editing...")
    else:
        print("Unknown action")
else:
    print("Not authorized")

# Restaurant reservation
party_size = 8
reservation = True
if reservation:
    print("Reservation confirmed")
    if party_size > 6:
        print("Large party—reserved back room")
    else:
        print("Standard table")
else:
    print("No reservation—may have wait")

# Same logic with and/or (cleaner!)
is_admin = True
action = "delete"
if is_admin and action == "delete":
    print("Deleting...")
```

### Guided Practice
Create a game where:
- If player has sword, check if they have armor
- If they have both, they can fight
- Otherwise, they must buy equipment

### Practice Problems
**Problem 1 — Beginner:** Nested if to check: is a number positive? If yes, is it even?

```python
num = int(input("Number: "))
if num > 0:
    if :
        print()
    else:
        print()
else:
    print()
```

**Problem 2 — Intermediate:** Login system: check username, then password, with different messages for each failure.

**Problem 3 — Challenge:** Game: check if player has enough gold for sword. If yes, check inventory space. If space, complete purchase.

<details>
<summary>💡 Hints</summary>

- Problem 1: Check num % 2 == 0 inside the positive check
- Problem 2: Nested if for password check inside username check
- Problem 3: Nested checks for gold, then space, then purchase
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num = int(input("Number: "))
if num > 0:
    if num % 2 == 0:
        print("Positive and even")
    else:
        print("Positive and odd")
else:
    print("Not positive")
```
</details>

---
