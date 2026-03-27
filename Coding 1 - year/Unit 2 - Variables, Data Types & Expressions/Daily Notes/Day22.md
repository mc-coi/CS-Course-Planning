# Day 22: String Deep Dive — Indexing, len(), String Basics

**Learning Target:** I can create strings, use indexing to access individual characters, and understand how the `len()` function works.

### Key Concepts

**Strings** are sequences of characters enclosed in quotes. You can use single quotes `'hello'` or double quotes `"hello"`—they work the same way. Strings can contain letters, numbers, spaces, and special characters.

**String length** is the number of characters in a string, including spaces and punctuation. The `len()` function returns the length. For example, `len("hello")` is `5`, and `len("hello world")` is `11` (including the space).

**Indexing** accesses individual characters in a string. Every character has an index (position). Importantly, **indexing starts at 0**, not 1. The first character is at index 0, the second at index 1, and so on. You use square brackets: `string[index]`.

**Negative indexing** counts from the end of the string. Index `-1` is the last character, `-2` is the second-to-last, and so on. This is useful for accessing characters near the end without knowing the string's length.

Important: **You cannot change a character in a string using indexing.** Strings are immutable (unchangeable). If you try `s[0] = "x"`, Python will give an error. To modify a string, you must reassign the variable to a new string.

### Code Examples

```python
# Creating strings
greeting = "Hello, World!"
word = 'Python'

# Length of strings
print(len("hello"))        # 5
print(len("hello world"))  # 11
print(len(""))             # 0 (empty string)

# Positive indexing (from the start)
word = "Python"
print(word[0])   # "P" (first character)
print(word[1])   # "y" (second character)
print(word[3])   # "h"
print(word[5])   # "n" (last character)

# Negative indexing (from the end)
print(word[-1])  # "n" (last character)
print(word[-2])  # "o" (second-to-last)
print(word[-6])  # "P" (first character, since word has 6 chars)

# Accessing characters in a sentence
sentence = "Python is awesome"
print(sentence[0])     # "P"
print(sentence[7])     # "i"
print(sentence[-1])    # "e"
print(sentence[-8])    # "a"

# Length and indexing together
text = "Code"
last_index = len(text) - 1
print(text[last_index])  # "e" (the last character)

# Finding the middle character
word = "Python"
middle_index = len(word) // 2
print(word[middle_index])  # "h" (index 3)
```

### Guided Practice

1. Ask the user for a word.
2. Print the length of the word.
3. Print the first character using index `[0]`.
4. Print the last character using index `[-1]`.
5. Print the middle character (use `len(word) // 2`).
6. Predict what happens if you try to access an index that's out of range, like `word[100]`.

### Practice Problems

**Problem 1 — Beginner:** Given the string `name = "Alexandra"`, print:
- The first character
- The last character
- The character at index 3
- The length of the name

```python
name = "Alexandra"

print()  # first character
print()  # last character
print()  # character at index 3
print()  # length
```

**Problem 2 — Intermediate:** Ask the user for a sentence and print:
- The first and last characters
- The character at the middle index
- The total length

**Problem 3 — Challenge:** Ask the user for two strings. Print which string is longer, and print the first character of the longer string.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `name[0]`, `name[-1]`, `name[3]`, and `len(name)`.
- Problem 2: The middle index is `len(sentence) // 2`.
- Problem 3: Use `len()` to compare lengths, then `if`/`else` (you'll learn this soon) or just print based on comparison.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = "Alexandra"
print(name[0])      # A
print(name[-1])     # a
print(name[3])      # x
print(len(name))    # 9

# Problem 2 Example
sentence = input("Enter a sentence: ")
print(sentence[0])
print(sentence[-1])
print(sentence[len(sentence) // 2])
print(len(sentence))

# Problem 3 Example
str1 = input("String 1: ")
str2 = input("String 2: ")
if len(str1) > len(str2):
    print(f"{str1} is longer, first character: {str1[0]}")
else:
    print(f"{str2} is longer, first character: {str2[0]}")
```

</details>

---
