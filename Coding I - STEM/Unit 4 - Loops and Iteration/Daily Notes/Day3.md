# Day 3: Loops with User Input
**Learning Target:** I can use loops with user input and validation.

### Key Concepts
Loops are perfect for repeated user interaction: getting input, validating, prompting again if invalid, etc.

**Sentinel value pattern:** Keep looping until user enters a specific value (like -1 or "quit").

### Code Examples
```python
# Validation loop
while True:
    try:
        age = int(input("Age (0-120): "))
        if 0 <= age <= 120:
            break
        print("Please enter 0-120")
    except ValueError:
        print("Please enter a number")

# Accumulate user scores
total = 0
count = 0
while True:
    score = int(input("Score (-1 to quit): "))
    if score == -1:
        break
    total += score
    count += 1
average = total / count if count > 0 else 0
print(f"Average: {average:.2f}")

# Keep asking until correct
password = "secret"
while True:
    guess = input("Password: ")
    if guess == password:
        print("Correct!")
        break
    print("Wrong, try again")
```

### Guided Practice
Create a program that asks for test scores (stop on -1), calculates average, and validates all entries are 0-100.

### Practice Problems
**Problem 1 — Beginner:** Ask the user for 5 numbers and print the sum.

**Problem 2 — Intermediate:** Ask for scores until -1 is entered, print highest and lowest score.

**Problem 3 — Challenge:** Ask for a password with retry limit (3 attempts, then lock out).

---