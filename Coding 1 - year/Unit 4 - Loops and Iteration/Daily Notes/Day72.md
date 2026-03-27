# Day 72: Sentinel Loops — User-Controlled Exit

**Learning Target:** I can write sentinel loops where a special value signals loop termination, and use break to exit loops conditionally.

### Key Concepts

A **sentinel loop** uses a special value (the sentinel) to signal when the loop should stop. Instead of a counter, the loop depends on user input to determine when to exit.

**Sentinel Pattern:**
```python
while True:
    value = input("Enter value (or 'quit' to exit): ")
    if value == "quit":
        break  # Exit the loop
    # Process value
```

This structure:
1. Loops "forever" (`while True` always true)
2. Gets user input
3. Checks if the sentinel value was entered
4. **break** immediately exits the loop (stops all iterations)

The sentinel is a value that means "stop now." Common sentinels:
- `"quit"`, `"done"`, `"exit"` (strings)
- `-1`, `0` (numbers when negative/zero is not valid input)
- `"no"` (for yes/no decisions)

**break Statement:** Immediately stops the loop, skipping any remaining iterations.
```python
for i in range(10):
    if i == 5:
        break  # Loop stops immediately
    print(i)  # Prints 0, 1, 2, 3, 4
```

### Code Examples

```python
# Example 1: Sum numbers until user enters 0
print("Enter numbers (0 to stop):")
total = 0
while True:
    num = int(input("Number: "))
    if num == 0:
        break  # Sentinel: 0 means stop
    total += num
print(f"Sum: {total}\n")

# Example 2: Menu loop
while True:
    print("\n1. Say hello")
    print("2. Say goodbye")
    print("3. Quit")
    choice = input("Pick (1-3): ")

    if choice == "3":
        break  # Exit loop
    elif choice == "1":
        print("Hello!")
    elif choice == "2":
        print("Goodbye!")
    else:
        print("Invalid choice")

# Example 3: Input validation with break
while True:
    password = input("Enter password: ")
    if len(password) >= 8:
        break  # Valid password, exit loop
    else:
        print("Too short. Must be 8+ characters.\n")
print("Password accepted!")

# Example 4: break in a for loop
numbers = [5, 2, 8, 1, 9, 3]
for num in numbers:
    if num > 7:
        print(f"Found large number: {num}")
        break  # Stop searching
```

### Guided Practice

Write a program that:
1. Asks the user for a word repeatedly
2. Stops when they type "stop"
3. Prints how many words they entered (not counting "stop")

Use a sentinel loop with break.

### Practice Problems

**Problem 1 — Beginner:** Write a sentinel loop that asks for names until the user enters "done", then prints how many names were collected.

```python
# Starter code
count = 0
while True:
    name = input("Enter a name ('done' to stop): ")
    # Your code here
```

**Problem 2 — Intermediate:** Write a sentinel loop that asks for test scores until the user enters -1. Calculate and print the average of all scores entered.

**Problem 3 — Challenge:** Write a number-guessing game: computer has a secret number (you can hardcode it, like 42). User guesses repeatedly. After each guess, tell them "too high," "too low," or "correct!" Stop when they guess correctly.

<details>
<summary>💡 Hints</summary>

- Problem 1: Count each name (not "done"), use break when "done" is entered
- Problem 2: Add all scores, count them, divide at the end. -1 is sentinel (not a score).
- Problem 3: Use a loop with break when guess is correct. Compare guess to secret number each iteration.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
count = 0
while True:
    name = input("Enter a name ('done' to stop): ")
    if name == "done":
        break
    count += 1
print(f"You entered {count} names")

# Problem 2 Example
total = 0
num_scores = 0
while True:
    score = int(input("Enter score (-1 to stop): "))
    if score == -1:
        break
    total += score
    num_scores += 1
if num_scores > 0:
    average = total / num_scores
    print(f"Average: {average:.2f}")

# Problem 3 Example
secret = 42
while True:
    guess = int(input("Guess the number: "))
    if guess == secret:
        print("Correct!")
        break
    elif guess < secret:
        print("Too low!")
    else:
        print("Too high!")
```

</details>

---
