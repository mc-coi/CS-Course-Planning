# Day 10: The random Module

**Learning Target:** I can use the random module to generate random numbers, shuffle data, and add unpredictability to programs.

---

## Key Concepts

**The random Module:** Built-in Python library for generating random values.

**Common Functions:**
- `random.random()` — Random float between 0.0 and 1.0
- `random.randint(a, b)` — Random integer from a to b (inclusive)
- `random.choice(seq)` — Pick a random item from a sequence
- `random.shuffle(list)` — Shuffle a list in place
- `random.uniform(a, b)` — Random float between a and b
- `random.sample(seq, k)` — Choose k unique items from sequence

**Seed:** `random.seed(n)` sets the starting point for the random generator. Same seed = same sequence.

---

## Code Examples

```python
import random

# Random float (0.0 to 1.0)
print(random.random())  # Example: 0.37

# Random integer
print(random.randint(1, 100))  # Example: 42

# Pick from a list
colors = ["red", "blue", "green", "yellow"]
print(random.choice(colors))  # Example: "green"

# Shuffle a list (modifies original)
deck = [1, 2, 3, 4, 5]
random.shuffle(deck)
print(deck)  # Example: [3, 1, 5, 2, 4]

# Sample without replacement
lottery = random.sample(range(1, 50), 6)
print(lottery)  # 6 unique numbers

# Seed for reproducibility
random.seed(42)
print(random.randint(1, 100))  # Always same with seed 42
random.seed(42)
print(random.randint(1, 100))  # Same value again!
```

---

## Guided Practice

1. **Random Quotes:** Use `random.choice()` on a list of quotes to pick one randomly.

2. **Dice Roller:** Create a function that simulates rolling a die 10 times using `random.randint()`.

3. **Shuffle Cards:** Create a deck of cards and use `random.shuffle()` to shuffle it.

4. **Lottery Picker:** Generate 6 random unique numbers between 1 and 50 using `random.sample()`.

---

## Practice Problems

**Beginner:** Write code that picks a random number from 1 to 10 and asks the user to guess it.

**Intermediate:** Create a "Magic 8-Ball" that picks a random response from a list of possible answers.

**Challenge:** Create a simple card game that shuffles a deck and deals 5 cards to a player.

<details>
<summary>💡 Hints</summary>
- Use `random.randint()` for integer ranges
- Use `random.choice()` for picking one item
- Use `random.shuffle()` to randomize a list order
- Use `random.sample()` for multiple unique items
- Remember that `shuffle()` modifies the list in place
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import random

secret = random.randint(1, 10)
guess = int(input("Guess a number 1-10: "))

if guess == secret:
    print("You got it!")
else:
    print(f"Wrong! The answer was {secret}")
```

**Intermediate:**
```python
import random

responses = [
    "Yes",
    "No",
    "Maybe",
    "Ask again later",
    "The stars say yes",
    "Definitely not"
]

print("Ask the Magic 8-Ball:")
print(random.choice(responses))
```

**Challenge:**
```python
import random

# Create a deck
suits = ["Hearts", "Diamonds", "Clubs", "Spades"]
ranks = ["2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A"]
deck = [f"{rank} of {suit}" for suit in suits for rank in ranks]

# Shuffle
random.shuffle(deck)

# Deal 5 cards
hand = deck[:5]
print("Your hand:")
for card in hand:
    print(f"  {card}")
```
</details>
