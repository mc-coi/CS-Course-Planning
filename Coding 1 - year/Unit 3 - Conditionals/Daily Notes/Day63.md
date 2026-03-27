# Day 63: Number Guessing Game (Single Guess)

**Learning Target:** I can build a number guessing game that applies conditionals to game logic and provides feedback.

---

## Key Concepts

Number Guessing Game demonstrates:
- Random number generation
- User input and validation
- Conditional comparisons (==, <, >)
- Feedback based on results
- Game state management

**Game Logic:**
1. Pick a random number
2. Ask user to guess
3. Compare guess to target
4. Give feedback (correct, too high, too low)
5. End game

---

## Code Examples

```python
import random

# Basic version
secret = random.randint(1, 10)
guess = int(input("Guess a number (1-10): "))

if guess == secret:
    print("✓ Correct!")
elif guess < secret:
    print("Too low")
else:
    print("Too high")

# Version with hints
secret = random.randint(1, 100)
guess = int(input("Guess (1-100): "))

if guess == secret:
    print("Perfect!")
elif guess < secret:
    distance = secret - guess
    if distance > 20:
        print("Way too low")
    else:
        print("Too low")
else:
    distance = guess - secret
    if distance > 20:
        print("Way too high")
    else:
        print("Too high")

# Version with scoring
import random

secret = random.randint(1, 50)
guess = int(input("Guess (1-50): "))

if guess == secret:
    print(f"Correct! The number was {secret}")
    print("Score: 100 points!")
elif abs(guess - secret) <= 5:
    print(f"Very close! It was {secret}")
    print("Score: 75 points!")
elif abs(guess - secret) <= 10:
    print(f"Close! It was {secret}")
    print("Score: 50 points!")
else:
    print(f"Not even close! It was {secret}")
    print("Score: 0 points")

# Full game with difficulty selection
import random

print("=== Number Guessing Game ===")
difficulty = input("Difficulty (easy/medium/hard): ").lower()

if difficulty == "easy":
    max_num = 10
    points = 100
elif difficulty == "medium":
    max_num = 50
    points = 50
elif difficulty == "hard":
    max_num = 100
    points = 25
else:
    print("Invalid difficulty")
    exit()

secret = random.randint(1, max_num)
guess = int(input(f"Guess (1-{max_num}): "))

if guess == secret:
    print(f"Correct! It was {secret}")
    print(f"Score: {points} points!")
elif guess < secret:
    print(f"Too low! It was {secret}")
    print(f"Score: {points // 2} points")
else:
    print(f"Too high! It was {secret}")
    print(f"Score: {points // 2} points")

# Game with validation
import random

print("=== Number Guessing Game ===")
print("I'm thinking of a number between 1-10")

secret = random.randint(1, 10)

try:
    guess = int(input("Your guess: "))
    if guess < 1 or guess > 10:
        print("Please guess between 1-10")
    elif guess == secret:
        print(f"✓ Correct! It was {secret}")
    elif guess < secret:
        print(f"Too low (it was {secret})")
    else:
        print(f"Too high (it was {secret})")
except ValueError:
    print("Please enter a number")
```

---

## Guided Practice (15 minutes)

**Activity: Basic Game**

```python
import random

# Setup
secret = random.randint(1, 10)
print("I'm thinking of a number between 1 and 10")

# Get guess
guess = int(input("What's your guess? "))

# Give feedback
if guess == secret:
    print("🎉 Correct!")
elif guess < secret:
    print(f"Too low! The number was {secret}")
else:
    print(f"Too high! The number was {secret}")
```

Test multiple times. Each run should pick a new number.

---

## Practice Problems

### Problem 1 — Beginner
Add "hot/cold" feedback:
- Within 5 of target: "Hot!"
- Within 10: "Warm"
- Otherwise: "Cold"

```python
import random

secret = random.randint(1, 20)
guess = int(input("Guess (1-20): "))

distance = abs(guess - secret)

if guess == secret:
    print("✓ Correct!")
elif :
    print("🔥 Hot!")
elif :
    print("🌡 Warm")
else:
    print("❄ Cold")

print(f"The number was {secret}")
```

---

### Problem 2 — Intermediate
Add difficulty selection with range:
- Easy: 1-10
- Medium: 1-50
- Hard: 1-100

```python
import random

difficulty = input("Difficulty (easy/medium/hard)? ").lower()

if difficulty == "easy":
    max_num = 10
elif difficulty == "medium":
    max_num = 50
elif difficulty == "hard":
    max_num = 100
else:
    print("Invalid difficulty")
    exit()

secret = random.randint(1, max_num)
guess = int(input(f"Guess (1-{max_num}): "))

if guess == secret:
    print("✓ Correct!")
elif guess < secret:
    print("Too low")
else:
    print("Too high")
```

---

### Problem 3 — Challenge
Score based on accuracy:
- Exact: 100 points
- Within 5: 75 points
- Within 10: 50 points
- Within 20: 25 points
- Otherwise: 0 points

```python
import random

secret = random.randint(1, 100)
guess = int(input("Guess (1-100): "))

distance = abs(guess - secret)

if distance == 0:
    score = 100
    message = "Perfect!"
elif distance <= 5:
    score = 75
    message = "Very close!"
elif :
    score = 50
    message = "Close"
elif :
    score = 25
    message = "Not far off"
else:
    score = 0
    message = "Not close"

print(f"{message} It was {secret}")
print(f"Score: {score}")
```

---

## Hints

- **Problem 1:** Use `abs()` to get absolute distance, compare with 5 and 10
- **Problem 2:** Store max range in variable, use in message and random.randint()
- **Problem 3:** Check distance ranges: 0, <=5, <=10, <=20, otherwise

---

## Sample Answers

### Problem 1 Example
```python
import random

secret = random.randint(1, 20)
guess = int(input("Guess (1-20): "))

distance = abs(guess - secret)

if guess == secret:
    print("✓ Correct!")
elif distance <= 5:
    print("🔥 Hot!")
elif distance <= 10:
    print("🌡 Warm")
else:
    print("❄ Cold")

print(f"The number was {secret}")
```

### Problem 3 Example
```python
import random

secret = random.randint(1, 100)
guess = int(input("Guess (1-100): "))

distance = abs(guess - secret)

if distance == 0:
    score = 100
    message = "Perfect!"
elif distance <= 5:
    score = 75
    message = "Very close!"
elif distance <= 10:
    score = 50
    message = "Close"
elif distance <= 20:
    score = 25
    message = "Not far off"
else:
    score = 0
    message = "Not close"

print(f"{message} It was {secret}")
print(f"Score: {score}")
```

---

## Extension Ideas

1. **Multiple rounds:** Play N guesses, best score wins
2. **Attempts counter:** Limit to 3 guesses
3. **Hints system:** Provide random hints if asked
4. **Replay option:** Ask if player wants to play again
5. **Leaderboard:** Save top scores

---

## Key Takeaway

Number guessing games combine random numbers with conditional logic. Perfect practice for if/elif/else chains!
