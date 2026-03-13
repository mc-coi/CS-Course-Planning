# Unit 3: Conditionals
> Master decision-making in code by using if/else/elif statements and logical operators.

## Unit Overview
- **Duration:** 9 days / 3 weeks
- **Key Concepts:** Boolean expressions, if/else/elif statements, logical operators (and/or/not), nested conditionals, input validation, and debugging logic
- **Big Idea:** Programs make decisions based on conditions—this is what makes them interactive and intelligent

## Learning Targets
- I can evaluate Boolean expressions and understand comparison operators
- I can write if statements that execute code conditionally
- I can use if/else to choose between two paths
- I can use elif for multiple conditions
- I can combine conditions using logical operators (and, or, not)
- I can write nested conditionals for complex decisions
- I can validate user input with conditionals
- I can debug logic errors in conditional statements
- I can build a complete interactive program using conditionals

---

# Day 1: Boolean Expressions
**Learning Target:** I can evaluate Boolean expressions and understand comparison operators.

### Key Concepts
A **Boolean expression** is any expression that evaluates to True or False. Comparison operators create Boolean results:
- `==` equal to
- `!=` not equal to
- `>` greater than
- `<` less than
- `>=` greater than or equal to
- `<=` less than or equal to

Strings are compared **alphabetically** (lexicographically): "apple" < "banana" is True because "a" comes before "b".

### Code Examples
```python
# Numeric comparisons
print(5 > 3)        # True
print(5 < 3)        # False
print(5 == 5)       # True
print(5 != 3)       # True
print(10 >= 10)     # True
print(10 <= 9)      # False

# String comparisons
print("apple" < "banana")   # True (alphabetical)
print("zebra" > "apple")    # True
print("hello" == "hello")   # True

# Variable comparisons
age = 17
print(age >= 16)    # True (can vote)

score = 85
print(score > 90)   # False (not an A)

# Type of comparison
is_student = (age < 18)  # True
print(type(is_student))  # <class 'bool'>
```

### Guided Practice
Write expressions that check:
1. Is 100 greater than 50?
2. Is "python" equal to "Python"?
3. Is 3.14 less than or equal to 3.14?
4. Is a given age greater than or equal to 18?

### Practice Problems
**Problem 1 — Beginner:** Write 5 comparison expressions and predict their output before running.

```python
# Starter code
print()
print()
print()
print()
print()
```

**Problem 2 — Intermediate:** Compare strings: "apple", "banana", "apricot". Which is largest? Which is smallest?

**Problem 3 — Challenge:** Predict the output of each: `5 > 3 == True`, `"5" > "3"`, `len("hi") > 1`

<details>
<summary>💡 Hints</summary>

- Problem 1: Mix numbers and strings
- Problem 2: Remember alphabetical comparison
- Problem 3: String "5" and "3" compare alphabetically, not numerically
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
print(10 > 5)              # True
print("cat" < "dog")       # True
print(3.5 <= 3.5)          # True
print(100 != 99)           # True
print("hello" == "hello")  # True
```
</details>

---

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

# Day 4: elif
**Learning Target:** I can use elif for multiple conditions.

### Key Concepts
**elif** (else if) tests additional conditions if the first if is False. Conditions are checked top-to-bottom and **stops at the first True**.

Order matters! Put more specific conditions first.

Syntax: `if ... elif ... elif ... else ...`

### Code Examples
```python
# Grade classifier with elif
score = 85
if score >= 90:
    print("A")
elif score >= 80:
    print("B")  # This runs
elif score >= 70:
    print("C")
else:
    print("F")

# Time of day
hour = 14  # 2 PM
if hour < 12:
    print("Good morning!")
elif hour < 17:
    print("Good afternoon!")  # This runs
elif hour < 21:
    print("Good evening!")
else:
    print("Good night!")

# Multiple elif's — order matters!
age = 25
if age < 13:
    print("Child")
elif age < 18:
    print("Teenager")
elif age < 65:
    print("Adult")  # This runs
else:
    print("Senior")
```

### Guided Practice
Create a program that asks for a test score and prints:
- A (90+), B (80-89), C (70-79), D (60-69), F (<60)

### Practice Problems
**Problem 1 — Beginner:** Use elif to classify a number as "Small", "Medium", or "Large".

```python
num = int(input("Number: "))
if num < 50:
    print()
elif :
    print()
else:
    print()
```

**Problem 2 — Intermediate:** Ask for a month number (1-12) and print the season.

**Problem 3 — Challenge:** Build a simple quiz—ask a question, check answer, print custom message based on correctness and other factors.

<details>
<summary>💡 Hints</summary>

- Problem 1: Split range into 3 categories
- Problem 2: Winter (12,1,2), Spring (3,4,5), Summer (6,7,8), Fall (9,10,11)
- Problem 3: Can add extra elif for "partially correct" or check string length
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num = int(input("Number: "))
if num < 50:
    print("Small")
elif num < 100:
    print("Medium")
else:
    print("Large")

# Problem 2 Example
month = int(input("Month (1-12): "))
if month in [12, 1, 2]:
    print("Winter")
elif month in [3, 4, 5]:
    print("Spring")
elif month in [6, 7, 8]:
    print("Summer")
else:
    print("Fall")
```
</details>

---

# Day 5: Logical Operators
**Learning Target:** I can combine conditions using logical operators (and, or, not).

### Key Concepts
**Logical operators** combine Boolean expressions:
- **and:** Both conditions must be True
- **or:** At least one condition must be True
- **not:** Reverses the Boolean (True becomes False, False becomes True)

**Short-circuit evaluation:** With `and`, if first condition is False, the second isn't checked. With `or`, if first is True, second isn't checked.

### Code Examples
```python
# and operator — both must be True
age = 17
has_license = True
if age >= 16 and has_license:
    print("Can drive!")  # Runs

# or operator — at least one True
day = "Sunday"
has_homework = False
if day == "Saturday" or day == "Sunday" or has_homework == False:
    print("No school!")  # Runs

# not operator — reverses
is_raining = False
if not is_raining:
    print("Let's go outside!")  # Runs (not False = True)

# Complex expression
score = 85
attendance = 0.9
if score >= 80 and attendance >= 0.8:
    print("Passing grade")  # Runs

# Combining all three
age = 20
has_id = True
is_member = False
if (age >= 18 and has_id) or is_member:
    print("Access granted")  # Runs
```

### Guided Practice
Write conditions for:
1. "You can apply for college" if age >= 18 AND you have a diploma
2. "Discount applies" if age < 13 OR age > 65
3. "Not allowed" if you're NOT an adult (age < 18)

### Practice Problems
**Problem 1 — Beginner:** Create a condition with `and`: check if a number is between 1 and 10.

```python
num = int(input("Number: "))
if :
    print("In range")
else:
    print("Out of range")
```

**Problem 2 — Intermediate:** Check if a password is strong (8+ chars AND contains a digit and uppercase).

**Problem 3 — Challenge:** Create a "can borrow a book" checker: student AND not overdue AND not maxed out books.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `num >= 1 and num <= 10`
- Problem 2: Use `.isdigit()` and `.isupper()` on strings, or check characters
- Problem 3: Use multiple conditions with `and`
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num = int(input("Number: "))
if num >= 1 and num <= 10:
    print("In range")
else:
    print("Out of range")

# Pythonic way with chained comparison
if 1 <= num <= 10:
    print("In range")
```
</details>

---

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

# Day 7: Conditional Applications
**Learning Target:** I can validate input and handle complex conditions.

### Key Concepts
**Input validation** ensures user input is safe and correct before using it. Validate with if statements.

**Chained comparisons** (Pythonic): `1 <= x <= 10` instead of `x >= 1 and x <= 10`

### Code Examples
```python
# Input validation — loop until valid
while True:
    try:
        age = int(input("Age (0-150): "))
        if 0 <= age <= 150:
            break
        else:
            print("Age must be 0-150")
    except ValueError:
        print("Please enter a number")

# Chained comparison (Pythonic)
score = 85
if 80 <= score <= 90:
    print("In the 80s range")

# Range check
x = 50
if 1 <= x <= 100:
    print("In valid range")

# Complex validation
password = input("Password: ")
if len(password) >= 8:
    print("Password long enough")
else:
    print("Too short (min 8 chars)")
```

### Guided Practice
Create an age checker that asks for age and prints:
- If < 13: "Child"
- If 13-19: "Teenager"
- If 20-64: "Adult"
- If 65+: "Senior"

### Practice Problems
**Problem 1 — Beginner:** Ask for test score, validate it's 0-100, print "Valid" or "Invalid".

**Problem 2 — Intermediate:** Ask for password, validate it's 8+ chars, has uppercase, has digit.

**Problem 3 — Challenge:** Ask for height and weight, calculate BMI, classify (underweight/normal/overweight/obese).

<details>
<summary>💡 Hints</summary>

- Problem 1: Check `0 <= score <= 100`
- Problem 2: Use string methods like `.isupper()` or loop to check
- Problem 3: BMI = weight(lb) / height(in)² × 703
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
score = int(input("Score (0-100): "))
if 0 <= score <= 100:
    print("Valid")
else:
    print("Invalid")

# Problem 2 Example
pw = input("Password: ")
if len(pw) >= 8 and any(c.isupper() for c in pw) and any(c.isdigit() for c in pw):
    print("Strong password")
else:
    print("Weak password")
```
</details>

---

# Day 8: Review & Debugging
**Learning Target:** I can debug logic errors in conditional statements.

### Key Concepts
Common logic errors in conditionals:
- **Using = instead of ==:** `if x = 5:` (should be `if x == 5:`)
- **Off-by-one errors:** Using > instead of >=, or vice versa
- **Wrong operator:** Using and instead of or, or vice versa
- **Missing else:** Forgetting that you need to handle False condition
- **Fall-through:** elif not stopping execution

### Code Examples
```python
# WRONG: using = instead of ==
# if score = 90:
#     print("A")

# CORRECT
if score == 90:
    print("A")

# WRONG: >= vs >
# if score > 90:
#     print("A")  # 90 doesn't print!

# CORRECT (if 90 should be A)
if score >= 90:
    print("A")

# WRONG: not stopping at right place
if grade == "A":
    print("Excellent")
elif grade == "B":
    print("Good")
# Falls through and also prints "Done"
print("Done")  # Always runs—that's correct!

# WRONG: and instead of or
# if day == "Sat" and day == "Sun":  # NEVER true!
#     print("Weekend")

# CORRECT
if day == "Sat" or day == "Sun":
    print("Weekend")
```

### Guided Practice
Debug three faulty programs with conditional errors.

### Practice Problems
**Problem 1 — Beginner:** Fix: `if age = 18: print("Adult")`

**Problem 2 — Intermediate:** Fix: grade check that should print "A" for 90+, but doesn't work correctly.

**Problem 3 — Challenge:** Trace through complex nested conditions and identify what will print.

---

# Day 9: Unit 3 Project
**Learning Target:** I can build a complete interactive program using conditionals.

### Project: Arcade Access Control System

Create a program that controls access to an arcade based on age, membership status, and behavior rating. Your program must include:

**Requirements:**
- At least 3 inputs (age, membership status, behavior rating)
- At least 5 if/elif/else branches
- At least 1 nested conditional
- At least 1 logical operator (and/or/not)
- Input validation (ensure inputs are valid ranges)
- Clear output messages
- At least 4 comments

**Example Logic:**
- If age < 13: children only section
- If age 13-17: teen section
- If age 18+: adult section
- If member: discount applied
- If behavior rating poor: access denied

---

## Unit Practice Bank

1. **Beginner:** Predict: `x=15; if x>10: print("Big") elif x>5: print("Medium") else: print("Small")`
2. **Beginner:** What does `not (5 > 3 and 2 < 1)` evaluate to? Show each step.
3. **Intermediate:** Write a speed limit checker: prints Fine if 10+ over, Warning if 1-9 over, Clear if at/under.
4. **Intermediate:** Write a season finder: asks month number, prints Spring/Summer/Fall/Winter.
5. **Intermediate:** Fix the logic error: `if score > 90: print("A") if score > 80: print("B")` (why both print?)
6. **Intermediate:** Triangle classifier: asks for 3 angles, checks if valid (sum=180), classifies type.
7. **Intermediate:** Rewrite using chained comparison: `if x >= 0: if x <= 100:`
8. **Intermediate:** What's wrong? `if x = 5: print("five")`
9. **Challenge:** Write a leap year checker (divisible by 4, but not 100, unless also by 400).
10. **Challenge:** Write a BMI calculator with classification (underweight/normal/overweight/obese).
11. **Challenge:** Predict: `a=5; b=0; if a and not b: print("yes") else: print("no")`
12. **Challenge:** Simple login: username AND password both must match specific values.
13. **Challenge:** Rock-paper-scissors outcome checker: given two players' choices, print who wins.
14. **Challenge:** Shipping cost calculator: weight determines base rate, express fee if requested, international fee if outside US.
15. **Challenge:** Debug: `grade=75; if grade>=90: letter="A" elif grade>=80: letter="B" elif grade>=70 letter="C" print(letter)`

---

## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Using `=` instead of `==`: `if x = 5:` | SyntaxError | Use `==` for comparison: `if x == 5:` |
| Forgetting colon: `if x > 5` | SyntaxError: expected ':' | Add colon: `if x > 5:` |
| Wrong indentation | IndentationError or logic error | Indent exactly 4 spaces after `if` |
| Using `and` instead of `or`: `if day == "Sat" and day == "Sun":` | Condition never True | Use `or`: one variable can't be two values |
| Forgetting `elif`/`else` paths execute | One True condition prints multiple times | Use `elif` or `else` to make conditions mutually exclusive |
| Off-by-one: `if score > 90:` but should include 90 | Score of 90 doesn't qualify | Use `>=` instead of `>` |
| Testing conditions in wrong order | Earlier True condition runs | Put most specific conditions first in elif |

---

## Unit Assessment Prep

**Review Questions:**

1. What is the difference between `=` and `==`?
2. When should you use `if` vs `elif` vs `else`?
3. Explain `and`, `or`, and `not` operators.
4. What does a nested conditional look like?
5. Why is indentation important in Python?
6. Write an if statement with 3+ branches (if/elif/elif/else).
7. Explain short-circuit evaluation in `and`/`or`.
8. What does `1 <= x <= 10` do?
9. Write a chained comparison.
10. Describe input validation.

**Answers:**
1. `=` assigns; `==` compares
2. `if` tests condition; `elif` tests another if first was False; `else` catches all remaining
3. `and` = both True; `or` = at least one True; `not` = reverses Boolean
4. An if inside another if, requiring nested indentation
5. Python uses indentation to define code blocks; incorrect indentation causes errors
6. Example: if/elif/elif/else with different age ranges
7. With `and`, if first False, second not checked; with `or`, if first True, second not checked
8. Checks if x is >= 1 AND <= 10 in one condition
9. Example: `80 <= score <= 100`
10. Checking that user input meets requirements before using it

---

## Vocabulary & Quick Reference

**Key Terms:**
- **Condition:** Expression that evaluates to True or False
- **Boolean:** Data type with values True or False
- **Logical operator:** and, or, not
- **Nested:** One structure inside another (if inside if)
- **Indentation:** Spacing that defines code blocks in Python
- **Mutually exclusive:** Only one path can execute

**Key Syntax:**
```python
if condition:
    # code runs if True

if condition:
    # runs if True
else:
    # runs if False

if condition1:
    # if True
elif condition2:
    # else if condition2 True
elif condition3:
    # else if condition3 True
else:
    # catch all remaining

# Logical operators
condition1 and condition2    # both True
condition1 or condition2     # at least one True
not condition               # reverse

# Chained comparison
1 <= x <= 100              # x is between 1 and 100

# Common patterns
if value in [1, 2, 3]:     # check if in list
if "substring" in "text":  # check if substring exists
if not is_valid:           # check if False
```

**Boolean Truth Table:**
| and | T | F |     | or | T | F |     | not |  |
|-----|---|---|     |----|---|---|     |-----|--|
| T   | T | F |     | T  | T | T |     | T   | F |
| F   | F | F |     | F  | T | F |     | F   | T |
