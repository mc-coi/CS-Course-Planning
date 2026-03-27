# Day 51: if Statements

**Learning Target:** I can write if statements that execute code conditionally based on Boolean conditions.

---

## Key Concepts

An **if statement** executes code only if a condition is True. The syntax requires:
- The keyword `if`
- A Boolean condition
- A colon `:` (required!)
- An **indented block** of code (exactly 4 spaces per indentation level)

If the condition is False, the indented code is skipped entirely.

**Critical:** Indentation in Python defines code blocks. Incorrect indentation causes IndentationError or wrong program behavior.

---

## Code Examples

```python
# Basic if statement
age = 17
if age >= 16:
    print("You can get a driver's permit!")  # Runs if age >= 16

# Indentation matters
x = 5
if x > 3:
    print("x is big")      # Indented — part of if block
print("Done")              # NOT indented — always runs

# If with False condition
score = 50
if score >= 90:
    print("A!")            # This doesn't run (score is not 90+)

print("Score was", score)  # This always runs

# Multiple statements in if block
name = "Alex"
if name == "Alex":
    print("Hello, Alex!")
    print("Welcome back!")
    print("Great to see you!")

# Using variables in conditions
min_age = 18
user_age = 17
if user_age >= min_age:
    print("Can enter")
else:
    print("Too young")

# Checking membership with 'in'
favorite_color = input("Your favorite color: ")
if favorite_color in ["red", "blue", "green"]:
    print("Primary color!")

# Checking if character is in string
word = "python"
if 'y' in word:
    print("Contains 'y'")  # Runs

# Using modulus to check even
number = 8
if number % 2 == 0:
    print("Even number")   # Runs

# Nested if (coming later, but valid here)
age = 20
if age >= 18:
    if age < 65:
        print("Can vote")
```

---

## Indentation Deep Dive

Python uses indentation to define code blocks. Always use **4 spaces** (not tabs, not 2 spaces, not 3).

```python
# CORRECT indentation
if True:
    print("This is indented 4 spaces")

# WRONG - uses tab (may look like spaces but isn't)
# if True:
# 	print("This causes IndentationError")

# WRONG - mixes indentation levels
# if True:
#   print("Only 2 spaces")
```

---

## Guided Practice (15 minutes)

**Activity:** Condition Checker

For each scenario, decide if the if block runs or is skipped:

1. **Scenario:** `age = 16`, `if age >= 16:`
   - Condition: `16 >= 16` = **True**
   - Code block: **RUNS**

2. **Scenario:** `score = 85`, `if score > 90:`
   - Condition: `85 > 90` = **False**
   - Code block: **SKIPPED**

3. **Scenario:** `name = "Alice"`, `if name == "alice":`
   - Condition: `"Alice" == "alice"` = **False** (case matters!)
   - Code block: **SKIPPED**

**Write your own:** Create three if statements with different conditions and predict which ones run.

---

## Practice Problems

### Problem 1 — Beginner
Write an if statement that checks if a number is even (divisible by 2).

```python
num = int(input("Enter a number: "))
if :
    print("This is an even number")
```

**Requirement:** Use the modulus operator `%`.

---

### Problem 2 — Intermediate
Ask the user for their age and print a message if they can vote (age >= 18).

```python
age = int(input("What is your age? "))
if :
    print("You can vote!")
```

**Requirement:** Use input() and convert to int.

---

### Problem 3 — Challenge
Check if a word contains the letter 'e'. If it does, print the word and a message. If not, print "No 'e' found".

```python
word = input("Enter a word: ")
if :
    print(f"The word '{word}' contains 'e'")
else:
    print("No 'e' found")
```

**Hint:** Use the `in` operator.

---

## Hints

- **Problem 1:** Use `if num % 2 == 0:` to check if remainder is 0
- **Problem 2:** Compare age to 18 with `>=`
- **Problem 3:** Use `if 'e' in word:` (case matters!)

---

## Sample Answers

### Problem 1 Example
```python
num = int(input("Enter a number: "))
if num % 2 == 0:
    print("This is an even number")
```

### Problem 2 Example
```python
age = int(input("What is your age? "))
if age >= 18:
    print("You can vote!")
```

### Problem 3 Example
```python
word = input("Enter a word: ")
if 'e' in word:
    print(f"The word '{word}' contains 'e'")
else:
    print("No 'e' found")
```

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Forgetting colon | `if x > 5` | Add `:` → `if x > 5:` |
| Wrong indentation | Code part of if when it shouldn't be | Use exactly 4 spaces |
| Using `=` instead of `==` | `if x = 5:` causes error | Use `==` for comparison |
| Forgetting `int()` | `"18" >= 18` compares string to number (error) | Convert: `int(input(...))` |

---

## Key Takeaway

if statements let your programs make decisions. A condition is either True (run the block) or False (skip it). Proper indentation is absolutely critical in Python!
