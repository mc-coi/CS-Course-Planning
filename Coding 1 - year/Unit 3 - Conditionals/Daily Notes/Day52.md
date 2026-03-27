# Day 52: if/else Statements

**Learning Target:** I can use if/else to implement two-path decisions where only one branch executes.

---

## Key Concepts

An **else statement** provides an alternative path when the if condition is False. Exactly ONE branch executes:
- If condition is True → if block runs, else block is skipped
- If condition is False → if block is skipped, else block runs

Syntax:
```python
if condition:
    # code runs if True
else:
    # code runs if False
```

**Key point:** else has no condition. It catches everything the if doesn't.

---

## Code Examples

```python
# Basic if/else
number = 7
if number % 2 == 0:
    print("Even")
else:
    print("Odd")  # Runs because 7 is odd

# Login check
password = input("Password: ")
if password == "secret":
    print("Access granted!")
else:
    print("Access denied!")  # Runs if password is wrong

# Age check
age = int(input("Your age: "))
if age >= 18:
    print("You are an adult")
else:
    print("You are a minor")

# Grade classifier
score = 75
if score >= 90:
    print("Grade: A")
else:
    print("Grade: Not A")  # Runs if score < 90

# String comparison
user_input = input("Enter 'yes' or 'no': ")
if user_input == "yes":
    print("You chose yes")
else:
    print("You chose something else")

# Using 'in' operator
fruit = input("Is it a fruit? apple, banana, orange: ")
if fruit in ["apple", "banana", "orange"]:
    print("That's a fruit!")
else:
    print("That's not in my list")

# Integer comparison
score = int(input("What's your score? "))
if score > 50:
    print("You passed!")
else:
    print("You failed. Try again.")

# Checking truthiness
value = input("Enter something: ")
if value:
    print(f"You entered: {value}")
else:
    print("You didn't enter anything")
```

---

## Control Flow Visualization

```
        Check condition
             |
             v
        condition True?
           /    \
          /      \
       YES       NO
        |         |
        v         v
    Run if     Run else
      block      block
        |         |
        v         v
    Continue program
```

---

## Guided Practice (15 minutes)

**Activity:** Traffic Light Simulator

```python
light = input("Enter traffic light color (red/yellow/green): ")

if light == "red":
    print("STOP")
else:
    print("GO")

# What prints for each input?
# - Input: "red" → Prints: "STOP"
# - Input: "green" → Prints: "GO"
# - Input: "yellow" → Prints: "GO"
```

**Modify the program:** What if we want yellow to print "CAUTION"? (Hint: You'll need elif, coming tomorrow!)

**Partner Activity:** Create an if/else program together. One partner writes the condition, the other writes the blocks.

---

## Practice Problems

### Problem 1 — Beginner
Ask the user for a number and print "Positive" if > 0, else "Not positive".

```python
num = int(input("Enter a number: "))
if :
    print("Positive")
else:
    print("Not positive")
```

---

### Problem 2 — Intermediate
Ask for a number and print "Even" or "Odd".

```python
num = int(input("Enter a number: "))
if :
    print("Even")
else:
    print("Odd")
```

---

### Problem 3 — Challenge
Create a simple number guessing game:
1. Pick a random number 1-10
2. Ask user to guess
3. Print "Correct!" or "Wrong! It was [number]"

```python
import random

secret = random.randint(1, 10)
guess = int(input("Guess a number (1-10): "))

if :
    print("Correct!")
else:
    print(f"Wrong! It was {secret}")
```

---

## Hints

- **Problem 1:** Check `if num > 0:`
- **Problem 2:** Use modulus: `if num % 2 == 0:` (even) else (odd)
- **Problem 3:** Compare `guess == secret`

---

## Sample Answers

### Problem 1 Example
```python
num = int(input("Enter a number: "))
if num > 0:
    print("Positive")
else:
    print("Not positive")
```

### Problem 2 Example
```python
num = int(input("Enter a number: "))
if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

### Problem 3 Example
```python
import random

secret = random.randint(1, 10)
guess = int(input("Guess a number (1-10): "))

if guess == secret:
    print("Correct!")
else:
    print(f"Wrong! It was {secret}")
```

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Using if twice instead of if/else | Both blocks might seem to run | Use else for alternate path |
| Forgetting indentation in else | IndentationError | Indent else block same as if block |
| Using `=` instead of `==` | SyntaxError | Use comparison: `==` |
| Else at wrong indentation | else doesn't match its if | Align else with its if |
| Condition always True/False | Only one branch runs (by design, but check logic) | Review your condition |

---

## Key Takeaway

if/else gives your program two choices. One path ALWAYS executes—either the if block or the else block, never both, never neither. This is fundamental to decision-making in programs!
