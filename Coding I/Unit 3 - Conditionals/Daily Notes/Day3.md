# Day 3: if/else
**Learning Target:** I can use if/else to choose between two paths.

### Key Concepts
An **else statement** catches everything where the if condition is False. It provides an alternative path.

Only ONE branch executes—if the condition is True, the if block runs and else is skipped. If False, else runs.

### Code Examples
```python
# Basic if/else
number = 7
if number % 2 == 0:
    print("Even")
else:
    print("Odd")  # This runs because 7 is odd

# Login check
password = input("Password: ")
if password == "secret":
    print("Access granted!")
else:
    print("Access denied!")

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
```

### Guided Practice
Create a simple login program. Ask for a username and password. If both match stored values, print "Welcome!" Otherwise, print "Invalid credentials."

### Practice Problems
**Problem 1 — Beginner:** Ask for a number and print "Positive" if > 0, else "Not positive".

```python
num = int(input("Number: "))
if :
    print()
else:
    print()
```

**Problem 2 — Intermediate:** Ask for a number and print "Even" or "Odd".

**Problem 3 — Challenge:** Write a simple game: pick a random number 1-10, ask user to guess, print "Correct!" or "Wrong! It was [number]".

<details>
<summary>💡 Hints</summary>

- Problem 1: Check if num > 0
- Problem 2: Use modulus operator %
- Problem 3: Use `import random; random.randint(1, 10)`
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num = int(input("Number: "))
if num > 0:
    print("Positive")
else:
    print("Not positive")

# Problem 3 Example
import random
secret = random.randint(1, 10)
guess = int(input("Guess (1-10): "))
if guess == secret:
    print("Correct!")
else:
    print(f"Wrong! It was {secret}")
```
</details>

---