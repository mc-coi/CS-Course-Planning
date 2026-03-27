# Day 56: Nested Conditionals

**Learning Target:** I can write nested if statements (decisions inside decisions) for hierarchical decision-making.

---

## Key Concepts

A **nested conditional** is an if statement inside another if statement. Nesting allows you to make dependent decisions: "If X is true, then check Y."

**Structure:**
```python
if condition1:
    # Outer block
    if condition2:
        # Inner block (nested)
        # Code here runs only if BOTH conditions are true
```

**Indentation defines nesting:** Each level adds 4 spaces.

**When to use nesting:**
- When a decision depends on a previous decision
- When you need hierarchical logic
- Sometimes you can replace with logical operators (and/or)

---

## Code Examples

```python
# Basic nested if
age = 17
if age >= 16:
    print("Old enough to drive")
    if age >= 18:
        print("Can vote too!")

# Without nesting (using and)
age = 17
if age >= 16 and age >= 18:
    print("Can drive and vote")

# Access control system
is_admin = True
if is_admin:
    print("Welcome, admin")
    action = input("Action (delete/edit): ")
    if action == "delete":
        print("Deleting...")
    elif action == "edit":
        print("Editing...")
    else:
        print("Unknown")
else:
    print("Not authorized")

# Game inventory
has_key = True
if has_key:
    print("You have the key")
    locked_door = True
    if locked_door:
        print("You unlock the door")
        print("You enter the room")
    else:
        print("Door already open")
else:
    print("You need the key first")

# Nested with multiple levels
score = 85
if score >= 60:
    print("Passing")
    if score >= 80:
        print("Above average")
        if score >= 90:
            print("Excellent!")

# Real-world: Bank ATM
pin_correct = True
if pin_correct:
    print("Pin accepted")
    action = input("Withdraw or Check balance? ")
    if action == "Withdraw":
        amount = float(input("Amount: "))
        balance = 500
        if amount <= balance:
            print(f"Withdrawn: ${amount}")
        else:
            print("Insufficient funds")
    elif action == "Check balance":
        print(f"Balance: ${balance}")
else:
    print("Incorrect PIN")
```

---

## Indentation Deep Dive

```python
# CORRECT - properly nested
if x > 5:              # 0 spaces
    print("x > 5")     # 4 spaces
    if y > 10:         # 4 spaces
        print("y > 10")    # 8 spaces
    print("Still inside x check")  # 4 spaces
print("Outside all ifs")  # 0 spaces

# WRONG - indentation error
# if x > 5:
# print("Not indented")  # IndentationError!
```

---

## Guided Practice (15 minutes)

**Activity: Game Logic**

```python
# Simplified RPG combat system
has_sword = True
has_shield = True
health = 100

if has_sword:
    print("You have a sword!")
    if has_shield:
        print("You have armor! You're ready for battle!")
        if health > 50:
            print("You attack!")
        else:
            print("You're wounded. Retreat!")
    else:
        print("You need armor for protection")
else:
    print("Find a weapon first")
```

**Trace through:** What prints for:
1. has_sword=True, has_shield=True, health=75?
2. has_sword=True, has_shield=False?
3. has_sword=False?

---

## Practice Problems

### Problem 1 — Beginner
Nested if to check: is a number positive? If yes, is it even?

```python
num = int(input("Number: "))
if num > 0:
    if :
        print("Positive and even")
    else:
        print("Positive and odd")
else:
    print("Not positive")
```

---

### Problem 2 — Intermediate
Login system:
1. Check username
2. If correct, check password
3. If both correct, show options
4. Different messages for each failure

```python
correct_user = "alice"
correct_pass = "secret123"

username = input("Username: ")
if username == correct_user:
    password = input("Password: ")
    if password == correct_pass:
        print("✓ Login successful!")
        print("Options: View, Edit, Delete")
    else:
        print("✗ Wrong password")
else:
    print("✗ User not found")
```

---

### Problem 3 — Challenge
Game: Player has items and wants to purchase equipment.
1. Check if player has enough gold
2. If yes, check inventory space
3. If space available, complete purchase

```python
player_gold = 150
player_inventory = 3
max_inventory = 5

sword_cost = 100

if player_gold >= sword_cost:
    print(f"You can afford the sword")
    if :
        print("You have space!")
        print("✓ Sword purchased!")
        player_gold -= sword_cost
        player_inventory += 1
        print(f"Gold: {player_gold}, Items: {player_inventory}")
    else:
        print("Inventory full!")
else:
    print("Not enough gold")
```

---

## Hints

- **Problem 1:** Check `if num % 2 == 0:` inside the positive check
- **Problem 2:** Nested if for password after username matches
- **Problem 3:** Check `player_inventory < max_inventory`

---

## Sample Answers

### Problem 1 Example
```python
num = int(input("Number: "))
if num > 0:
    if num % 2 == 0:
        print("Positive and even")
    else:
        print("Positive and odd")
else:
    print("Not positive")
```

### Problem 2 Example
```python
correct_user = "alice"
correct_pass = "secret123"

username = input("Username: ")
if username == correct_user:
    password = input("Password: ")
    if password == correct_pass:
        print("✓ Login successful!")
    else:
        print("✗ Wrong password")
else:
    print("✗ User not found")
```

### Problem 3 Example
```python
player_gold = 150
player_inventory = 3
max_inventory = 5
sword_cost = 100

if player_gold >= sword_cost:
    print("You can afford the sword")
    if player_inventory < max_inventory:
        print("You have space!")
        print("✓ Sword purchased!")
        player_gold -= sword_cost
        player_inventory += 1
    else:
        print("Inventory full!")
else:
    print("Not enough gold")
```

---

## When to Use Nesting vs. Logical Operators

**Use nesting when:**
- Logic is hierarchical (dependent decisions)
- You need to execute multiple statements in inner block
- Different outcomes based on both conditions

**Use logical operators when:**
- You just need to check if conditions are true
- Simpler, more readable
- No inner block needed

Both work; choose for readability!

---

## Key Takeaway

Nested conditionals handle complex, hierarchical logic. Each indentation level represents a deeper decision. Structure your logic clearly so others can follow it!
