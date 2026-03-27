# Day 6: Loops with Strings
**Learning Target:** I can iterate over strings and use the accumulator pattern.

### Key Concepts
Strings are iterable—you can loop through characters with `for ch in string`.

The **accumulator pattern**: initialize a variable (usually 0 for sum, "" for strings, [] for lists), update it in the loop, return/print after.

### Code Examples
```python
# Loop through string
word = "Python"
for ch in word:
    print(ch)  # P, y, t, h, o, n

# Count vowels
text = "programming"
vowel_count = 0
for ch in text:
    if ch in "aeiou":
        vowel_count += 1
print(f"Vowels: {vowel_count}")  # 3

# Build reversed string
word = "hello"
reversed_word = ""
for ch in word:
    reversed_word = ch + reversed_word  # prepend
print(reversed_word)  # "olleh"

# Check palindrome
text = "racecar"
reversed_text = ""
for ch in text:
    reversed_text = ch + reversed_text
print(text == reversed_text)  # True
```

### Guided Practice
Write a program that asks for a word and prints:
- Number of vowels
- Number of consonants
- The word reversed
- Whether it's a palindrome

### Practice Problems
**Problem 1 — Beginner:** Count vowels in a word using a loop.

**Problem 2 — Intermediate:** Print each character of a word with its position (0, 1, 2...).

**Problem 3 — Challenge:** Find the most common letter in a sentence.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use accumulator pattern with vowel_count
- Problem 2: Use `enumerate()` or track index yourself
- Problem 3: Loop through string, count each letter, track max
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
word = input("Word: ")
vowel_count = 0
for ch in word:
    if ch.lower() in "aeiou":
        vowel_count += 1
print(f"Vowels: {vowel_count}")

# Problem 2
word = input("Word: ")
for i, ch in enumerate(word):
    print(f"{i}: {ch}")
```
</details>

---