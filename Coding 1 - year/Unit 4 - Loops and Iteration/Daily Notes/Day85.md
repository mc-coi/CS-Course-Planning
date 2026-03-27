# Day 85: Practice Lab — Advanced Loop Challenges

**Learning Target:** I can apply all loop concepts (while, for, nested, patterns) to solve complex, multi-step problems.

### Key Concepts

This lab consolidates Week 17 (Days 81–84). You'll combine:
- Break and continue for control flow
- Nested loops for 2D structures
- Min/max, search, and flag patterns
- Complex conditionals within loops

Problems require multiple nested loops, careful use of control flow, and thoughtful design.

### Guided Practice

**Option A: Grade Analysis Program**
- Ask the user to enter test grades until they type "done" or "quit"
- Track: highest, lowest, average, count
- Find the "outlier" (grade furthest from average)
- Display a summary report

**Option B: Word Game**
- Computer picks a random word (hardcode a list of words)
- User guesses letters
- Track: correct guesses, wrong guesses, attempts
- Display progress: (_ _ _ _ _) with guessed letters filled in
- Win when all letters guessed; lose after too many wrong guesses

**Option C: Matrix Search**
- Create a 5×5 grid of random numbers (1-50)
- User enters a target number
- Find all positions where it appears
- Display the grid with found positions highlighted

### Practice Problems

**Problem 1 — Beginner:** Write a loop that finds both the highest and lowest numbers in a list and prints both values.

**Problem 2 — Intermediate:** Write a program that:
- Asks for a list of words
- Counts how many times each unique word appears
- Prints a summary (word: count)

Use nested loops or dictionaries (if learned).

**Problem 3 — Challenge:** Write a program that simulates "Hangman":
1. Computer picks a word from a list
2. User guesses letters one at a time
3. Display: (blank for unguessed letters, letter if guessed)
4. Track wrong guesses (max 6)
5. Win if word is guessed; lose if too many wrong
6. Offer to play again

<details>
<summary>💡 Hints</summary>

- Problem 1: Use min/max patterns. Initialize both to first element.
- Problem 2: Use nested loops to compare all words, or use a dictionary to count occurrences.
- Problem 3: Nested loops: outer for play-again, inner for guess-letters. Use a "word" string and a "guessed" string. Loop through word to build display.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
numbers = [5, 2, 8, 1, 9, 3, 7]
min_val = numbers[0]
max_val = numbers[0]
for num in numbers:
    if num < min_val:
        min_val = num
    if num > max_val:
        max_val = num
print(f"Min: {min_val}, Max: {max_val}")

# Problem 2 Example (using nested loops)
words = ["apple", "banana", "apple", "cherry", "banana", "apple"]
for i in range(len(words)):
    word = words[i]
    count = 0
    for j in range(len(words)):
        if words[j] == word:
            count += 1
    print(f"{word}: {count}")
# Note: This counts duplicates. Better with dict, but shows nested loops.

# Problem 3 Example (simplified)
import random
word_list = ["python", "hangman", "computer", "programming"]
while True:
    word = random.choice(word_list)
    guessed = set()
    wrong_guesses = 0
    max_wrong = 6

    while True:
        display = ""
        for char in word:
            if char in guessed:
                display += char
            else:
                display += "_"

        print(f"Word: {display}")
        print(f"Wrong guesses left: {max_wrong - wrong_guesses}")

        if display == word:
            print(f"You won! The word is {word}!")
            break

        if wrong_guesses >= max_wrong:
            print(f"You lost! The word was {word}.")
            break

        guess = input("Guess a letter: ").lower()
        if guess in guessed:
            print("Already guessed!")
            continue

        guessed.add(guess)
        if guess not in word:
            wrong_guesses += 1
            print("Wrong!")

    again = input("Play again? (yes/no): ").lower()
    if again != "yes":
        break
```

</details>

---

## Week 17 Reflection

**What you've learned:**
- Break and continue for precise loop control
- Nested loops for complex structures
- Common algorithmic patterns: min/max, search, flag
- How to trace nested loops
- Debugging loop logic

**Key takeaway:** Nested loops are powerful but require careful thinking. Always trace them on paper first. The patterns (min/max, search, flag) appear everywhere in real programming—mastering them unlocks many possibilities.

---
