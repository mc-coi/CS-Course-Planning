# Day 78: Iterating Over Strings — Character-by-Character Processing

**Learning Target:** I can loop through strings character by character, and manipulate or analyze strings using for loops.

### Key Concepts

Strings are **sequences** (like lists). You can iterate over them directly with a for loop without range():

```python
word = "hello"
for char in word:
    print(char)  # Prints: h, e, l, l, o (each on its own line)
```

This is called a **for-each loop** or **iteration over a sequence**. The loop variable takes on each value in the sequence.

**String iteration is useful for:**
- Counting specific characters (vowels, digits, spaces)
- Checking if a string has certain properties (is palindrome, contains digit)
- Building a new string from the original (reverse, filter, transform)
- Analyzing text

**String methods (helpful for iteration):**
- `.isdigit()` — True if character is 0-9
- `.isalpha()` — True if character is a letter
- `.isalnum()` — True if alphanumeric (letter or digit)
- `.isspace()` — True if whitespace (space, tab, newline)
- `.isupper()` — True if uppercase letter
- `.islower()` — True if lowercase letter
- `.upper()` — Return uppercase version
- `.lower()` — Return lowercase version

### Code Examples

```python
# Example 1: Count vowels
word = input("Enter a word: ")
vowel_count = 0
for char in word.lower():
    if char in "aeiou":
        vowel_count += 1
print(f"Vowels: {vowel_count}\n")

# Example 2: Check for digit
password = input("Password: ")
has_digit = False
for char in password:
    if char.isdigit():
        has_digit = True
        break
print(f"Contains digit: {has_digit}\n")

# Example 3: Reverse a string
text = input("Text: ")
reversed_text = ""
for char in text:
    reversed_text = char + reversed_text  # Prepend each char
print(f"Reversed: {reversed_text}\n")

# Example 4: Count character types
sentence = input("Enter text: ")
letters = 0
digits = 0
spaces = 0
for char in sentence:
    if char.isalpha():
        letters += 1
    elif char.isdigit():
        digits += 1
    elif char.isspace():
        spaces += 1
print(f"Letters: {letters}, Digits: {digits}, Spaces: {spaces}\n")

# Example 5: Build a string with filter
text = input("Text: ")
consonants_only = ""
for char in text.lower():
    if char.isalpha() and char not in "aeiou":
        consonants_only += char
print(f"Consonants: {consonants_only}")
```

### Guided Practice

Write a program that:
1. Asks the user for a word
2. Counts and prints the frequency of each vowel (a, e, i, o, u)
3. Prints the result like: "a: 2, e: 1, i: 0, o: 1, u: 0"

Use a loop to iterate over the word and count occurrences.

### Practice Problems

**Problem 1 — Beginner:** Write a loop that asks for a word and prints each character on its own line.

```python
# Starter code
word = input("Word: ")
for char in word:
    # Your code here
```

**Problem 2 — Intermediate:** Write a program that asks for a sentence and counts:
- Total characters (excluding spaces)
- Number of spaces
- Number of uppercase letters

**Problem 3 — Challenge:** Write a program that checks if a word is a palindrome (reads the same forwards and backwards), like "racecar" or "madam". Use a for loop to build the reversed version.

<details>
<summary>💡 Hints</summary>

- Problem 1: Simple—just print each char
- Problem 2: Use `if char.isspace()` and `char.isupper()`. Count total non-space chars.
- Problem 3: Build reversed string by prepending each character. Compare original to reversed (using `.lower()` to ignore case).

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
word = input("Word: ")
for char in word:
    print(char)

# Problem 2 Example
sentence = input("Sentence: ")
non_space = 0
spaces = 0
uppercase = 0
for char in sentence:
    if char.isspace():
        spaces += 1
    else:
        non_space += 1
    if char.isupper():
        uppercase += 1
print(f"Characters (no space): {non_space}")
print(f"Spaces: {spaces}")
print(f"Uppercase: {uppercase}")

# Problem 3 Example
word = input("Word: ").lower()
reversed_word = ""
for char in word:
    reversed_word = char + reversed_word
if word == reversed_word:
    print(f"'{word}' is a palindrome!")
else:
    print(f"'{word}' is not a palindrome.")
```

</details>

---
