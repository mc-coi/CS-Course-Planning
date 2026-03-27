# Day 62: Rock-Paper-Scissors Game

**Learning Target:** I can build a complete game that applies conditionals to game logic and win/loss determination.

---

## Key Concepts

Rock-Paper-Scissors is an ideal conditional exercise:
- Two players (user vs. computer)
- Multiple outcomes (win, lose, tie)
- Logic-based: rock beats scissors, scissors beats paper, paper beats rock
- Demonstrates all conditional concepts in context

**Game Rules:**
- Rock beats Scissors
- Scissors beats Paper
- Paper beats Rock
- Same choice = Tie

---

## Code Examples

```python
import random

# Single round
print("=== Rock-Paper-Scissors ===")
choices = ["rock", "paper", "scissors"]

player = input("Your choice (rock/paper/scissors): ").lower()
computer = random.choice(choices)

print(f"You chose: {player}")
print(f"Computer chose: {computer}")

# Determine winner
if player == computer:
    print("Tie!")
elif player == "rock":
    if computer == "scissors":
        print("You win!")
    else:
        print("You lose!")
elif player == "paper":
    if computer == "rock":
        print("You win!")
    else:
        print("You lose!")
elif player == "scissors":
    if computer == "paper":
        print("You win!")
    else:
        print("You lose!")
else:
    print("Invalid choice")

# Better version with logic table
def check_winner(p1, p2):
    if p1 == p2:
        return "Tie"
    elif (p1 == "rock" and p2 == "scissors") or \
         (p1 == "scissors" and p2 == "paper") or \
         (p1 == "paper" and p2 == "rock"):
        return "Player 1 wins!"
    else:
        return "Player 2 wins!"

# Full game with validation
import random

def is_valid(choice):
    return choice in ["rock", "paper", "scissors"]

print("=== Rock-Paper-Scissors ===")
player_choice = input("Choose (rock/paper/scissors): ").lower()

if not is_valid(player_choice):
    print("Invalid choice!")
else:
    computer_choice = random.choice(["rock", "paper", "scissors"])

    print(f"You: {player_choice}")
    print(f"Computer: {computer_choice}")

    if player_choice == computer_choice:
        print("It's a tie!")
    elif (player_choice == "rock" and computer_choice == "scissors"):
        print("You win!")
    elif (player_choice == "scissors" and computer_choice == "paper"):
        print("You win!")
    elif (player_choice == "paper" and computer_choice == "rock"):
        print("You win!")
    else:
        print("Computer wins!")

# Multi-round with score tracking
import random

player_score = 0
computer_score = 0
rounds = 3

for round_num in range(1, rounds + 1):
    print(f"\n=== Round {round_num} ===")

    player = input("Choose (rock/paper/scissors): ").lower()
    computer = random.choice(["rock", "paper", "scissors"])

    print(f"You: {player}, Computer: {computer}")

    if player == computer:
        print("Tie!")
    elif (player == "rock" and computer == "scissors") or \
         (player == "scissors" and computer == "paper") or \
         (player == "paper" and computer == "rock"):
        print("You win this round!")
        player_score += 1
    else:
        print("Computer wins this round!")
        computer_score += 1

print(f"\n=== Final Score ===")
print(f"You: {player_score}")
print(f"Computer: {computer_score}")

if player_score > computer_score:
    print("You won the match!")
elif computer_score > player_score:
    print("Computer won the match!")
else:
    print("Match is tied!")
```

---

## Guided Practice (20 minutes)

**Activity: Implement Basic Version**

```python
import random

# Game setup
player_choice = input("rock, paper, or scissors? ").lower()
computer_choice = random.choice(["rock", "paper", "scissors"])

# Display choices
print(f"You: {player_choice}")
print(f"Computer: {computer_choice}")

# Determine winner (start with this simple version)
if player_choice == computer_choice:
    print("Tie!")
elif player_choice == "rock" and computer_choice == "scissors":
    print("You win!")
elif player_choice == "scissors" and computer_choice == "paper":
    print("You win!")
elif player_choice == "paper" and computer_choice == "rock":
    print("You win!")
else:
    print("Computer wins!")
```

Test with different combinations.

---

## Practice Problems

### Problem 1 — Beginner
Add input validation to the basic game:

```python
import random

player_choice = input("rock, paper, or scissors? ").lower()

if  in ["rock", "paper", "scissors"]:
    computer_choice = random.choice(["rock", "paper", "scissors"])
    # ... game logic ...
else:
    print("Invalid choice")
```

---

### Problem 2 — Intermediate
Modify the game to show detailed outcomes:

```python
import random

player = input("Choose: ").lower()
computer = random.choice(["rock", "paper", "scissors"])

print(f"\nYou chose: {player}")
print(f"Computer chose: {computer}\n")

if player == computer:
    print("Tie - no one wins this round")
elif player == "rock" and computer == "scissors":
    print("Rock crushes scissors - You win!")
elif :  # Add more winning conditions
    print("... - You win!")
# ... etc ...
```

---

### Problem 3 — Challenge
Build a best-of-3 game with score tracking:

```python
import random

you_wins = 0
computer_wins = 0

for round in range(1, 4):
    print(f"\n=== Round {round} ===")

    player = input("Choose (rock/paper/scissors): ").lower()

    if player not in ["rock", "paper", "scissors"]:
        print("Invalid choice")
        continue

    computer = random.choice(["rock", "paper", "scissors"])
    print(f"Computer chose: {computer}")

    # Determine winner and update score
    if :
        print("You win!")
        you_wins += 1
    elif :
        print("Computer wins!")
        computer_wins += 1
    else:
        print("Tie!")

print(f"\nFinal: You {you_wins}, Computer {computer_wins}")
```

---

## Hints

- **Problem 1:** Check `if player_choice in ["rock", "paper", "scissors"]:`
- **Problem 2:** Add all three winning conditions for player
- **Problem 3:** Track wins in a loop, compare scores at end

---

## Sample Answers

### Problem 1 Example
```python
import random

player_choice = input("rock, paper, or scissors? ").lower()

if player_choice in ["rock", "paper", "scissors"]:
    computer_choice = random.choice(["rock", "paper", "scissors"])
    print(f"You: {player_choice}, Computer: {computer_choice}")
    if player_choice == computer_choice:
        print("Tie!")
    elif (player_choice == "rock" and computer_choice == "scissors") or \
         (player_choice == "scissors" and computer_choice == "paper") or \
         (player_choice == "paper" and computer_choice == "rock"):
        print("You win!")
    else:
        print("Computer wins!")
else:
    print("Invalid choice")
```

---

## Extension Ideas

1. Add **best-of-N** games
2. Add **statistics tracking** (win rate, etc.)
3. Add **computer strategies** (random vs. pattern-based)
4. Add **replay option**
5. Add **difficulty levels** (computer plays smarter)

---

## Key Takeaway

Rock-Paper-Scissors demonstrates conditional logic in action. The game logic is simple but illustrates how if/elif/else chains handle multiple cases!
