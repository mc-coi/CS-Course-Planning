# Day 2: if Statements
**Learning Target:** I can write if statements that execute code conditionally.

### Key Concepts
An **if statement** executes code only if a condition is True. The syntax requires:
- The keyword `if`
- A Boolean condition
- A colon `:`
- An **indented block** (4 spaces, not tabs)

If the condition is False, the indented code is skipped.

**Indentation is critical in Python.** It defines which code belongs to the if statement.

### Code Examples
```python
# Basic if statement
age = 17
if age >= 16:
    print("You can get a driver's permit!")

# The indentation matters
x = 5
if x > 3:
    print("x is big")    # indented — part of if
print("Done")            # NOT indented — always runs

# If with False condition
score = 50
if score >= 90:
    print("A!")          # This doesn't run

print("Score was", score)  # This always runs

# Multiple statements in if
name = "Alex"
if name == "Alex":
    print("Hello, Alex!")
    print("Welcome back!")

# Using variables in conditions
min_age = 18
user_age = 17
if user_age >= min_age:
    print("Can enter")
```

### Guided Practice
Write a program that asks for a temperature in Fahrenheit and prints different messages:
- If >= 80: "It's hot!"
- If >= 60: "It's pleasant"
- Always print "Temperature check complete"

### Practice Problems
**Problem 1 — Beginner:** Write an if statement that checks if a number is even (divisible by 2).

```python
num =
if :
    print()
```

**Problem 2 — Intermediate:** Ask the user for their age and print "You can vote" if age >= 18.

**Problem 3 — Challenge:** Write an if statement that checks if a word contains the letter 'e'.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use modulus: num % 2 == 0
- Problem 2: Get age with input(), convert to int, check if >= 18
- Problem 3: Use `in` operator: `if 'e' in word:`
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num = int(input("Number: "))
if num % 2 == 0:
    print("Even number!")

# Problem 2 Example
age = int(input("Age: "))
if age >= 18:
    print("You can vote")
```
</details>

---