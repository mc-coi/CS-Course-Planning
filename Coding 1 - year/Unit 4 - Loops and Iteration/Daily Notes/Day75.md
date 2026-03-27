# Day 75: Practice Lab — While Loop Programs

**Learning Target:** I can design, code, and test complete while loop programs using counter, sentinel, accumulator, and validation patterns.

### Key Concepts

This lab consolidates Week 15 (Days 71–74). You'll apply all four while loop patterns:
1. **Counter pattern:** Loop a fixed number of times
2. **Sentinel pattern:** Exit when a special value is entered
3. **Accumulator pattern:** Collect/combine values
4. **Validation pattern:** Ensure valid input

A complete program often combines multiple patterns.

### Guided Practice

**Option A: Number Statistics Program**
Ask the user for numbers until they enter 0. Calculate and display:
- Sum (accumulator)
- Count (accumulator)
- Average
- Highest (accumulator with comparison)
- Lowest (accumulator with comparison)

Validate that the sum/average are meaningful (count > 0).

**Option B: Quiz Game**
Define 3 quiz questions and answers. Ask each question repeatedly until the user gets it right. Display:
- Question number
- Number of attempts for each question
- Total attempts across all questions

Use sentinel (exit when answer correct) and accumulator (count attempts).

**Option C: Savings Calculator**
Ask user for:
- Monthly savings amount (validate > 0)
- Target amount (validate > 0)

Then loop: calculate running total, display month and total, until target is reached. Print how many months it took.

### Practice Problems

**Problem 1 — Beginner:** Create a program that asks for 5 test scores, then prints the sum and average.

```python
# Starter code
total = 0
for i in range(5):
    score = float(input(f"Score {i+1}: "))
    total += score
average = total / 5
print(f"Sum: {total}, Average: {average:.2f}")
```

Modify this to use a **while loop with a counter** instead of for loop.

**Problem 2 — Intermediate:** Create a program that simulates a bank ATM:
- Ask for a PIN (validate it's 4 digits)
- Menu: withdraw, deposit, check balance, quit
- Use a sentinel loop; balance starts at $1000

**Problem 3 — Challenge:** Create a "Guess the Number" game:
- Computer picks a random number (1–100)
- User guesses repeatedly
- Track number of attempts
- After correct guess: display "You got it in N attempts!"
- Offer to play again (sentinel loop)

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `while count < 5:` instead of `for i in range(5):`
- Problem 2: Nested loops: outer sentinel (menu), inner validation (PIN). Use if/elif for menu choices.
- Problem 3: Use `import random` and `random.randint(1, 100)` to pick the number

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example (while loop version)
total = 0
count = 0
while count < 5:
    score = float(input(f"Score {count+1}: "))
    total += score
    count += 1
average = total / 5
print(f"Sum: {total}, Average: {average:.2f}")

# Problem 2 Example
while True:
    pin = input("Enter PIN (4 digits): ")
    if len(pin) == 4 and pin.isdigit():
        break
    print("Invalid PIN. Must be 4 digits.\n")

balance = 1000.0
while True:
    print(f"\nBalance: ${balance:.2f}")
    print("1. Withdraw")
    print("2. Deposit")
    print("3. Check Balance")
    print("4. Quit")
    choice = input("Choose (1-4): ")

    if choice == "1":
        amount = float(input("Withdraw amount: $"))
        if amount <= balance:
            balance -= amount
            print(f"Withdrew ${amount:.2f}")
        else:
            print("Insufficient funds.")
    elif choice == "2":
        amount = float(input("Deposit amount: $"))
        balance += amount
        print(f"Deposited ${amount:.2f}")
    elif choice == "3":
        print(f"Your balance: ${balance:.2f}")
    elif choice == "4":
        break
    else:
        print("Invalid choice.")

print("Thank you! Goodbye.")

# Problem 3 Example
import random
while True:
    secret = random.randint(1, 100)
    attempts = 0
    while True:
        guess = int(input("Guess (1-100): "))
        attempts += 1
        if guess == secret:
            print(f"You got it in {attempts} attempts!")
            break
        elif guess < secret:
            print("Too low.")
        else:
            print("Too high.")

    again = input("Play again? (yes/no): ").lower()
    if again != "yes":
        break
print("Thanks for playing!")
```

</details>

---

## Week 15 Reflection

**What you've learned:**
- While loops and conditions
- Counter, sentinel, accumulator, and validation patterns
- The break statement for early exit
- Nested while loops for complex control flow

**Key takeaway:** While loops are flexible—they can repeat a fixed number of times (counter), until a user signals to stop (sentinel), while building a result (accumulator), or while validating input. Master these four patterns, and you can handle most iteration needs!

---
