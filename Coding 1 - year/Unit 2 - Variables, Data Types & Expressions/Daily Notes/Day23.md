# Day 23: String Slicing — [start:stop:step] Notation

**Learning Target:** I can extract substrings using slicing with start, stop, and step values.

### Key Concepts

**Slicing** is a way to extract a portion (substring) of a string. It uses square brackets with up to three values: `string[start:stop:step]`.

**Start** is the index where slicing begins (inclusive). If omitted, slicing starts at index 0.

**Stop** is the index where slicing ends (exclusive)—the character at the stop index is NOT included. This is different from indexing! If omitted, slicing goes to the end of the string.

**Step** is how many characters to skip. The default is 1 (consecutive characters). If step is 2, you get every 2nd character; if step is -1, you go backwards.

**Important:** Unlike indexing, slicing does NOT raise an error if the indices are out of range. For example, `"hello"[0:100]` safely returns `"hello"` (the whole string).

**Reversing a string** is easy with slicing: `string[::-1]` reverses it. This means "start at the end, go to the beginning, step backwards by 1."

### Code Examples

```python
word = "Python"
# Indices: P=0, y=1, t=2, h=3, o=4, n=5

# Basic slicing
print(word[0:3])    # "Pyt" (indices 0, 1, 2; stop at 3 is exclusive)
print(word[1:4])    # "yth" (indices 1, 2, 3)
print(word[2:6])    # "thon" (indices 2, 3, 4, 5)

# Omitting start (starts at 0)
print(word[:3])     # "Pyt"
print(word[:4])     # "Pyth"

# Omitting stop (goes to end)
print(word[2:])     # "thon"
print(word[3:])     # "hon"

# Omitting both (copy the whole string)
print(word[:])      # "Python"

# Using step
print(word[0:6:2])  # "Pto" (indices 0, 2, 4)
print(word[1:5:2])  # "yh" (indices 1, 3)
print(word[::2])    # "Pto" (every 2nd character, whole string)

# Reversing with negative step
print(word[::-1])   # "nohtyP" (backwards)
print(word[5:2:-1]) # "noh" (backwards from index 5 to 3)

# Slicing a sentence
sentence = "Python is awesome"
print(sentence[0:6])      # "Python"
print(sentence[7:9])      # "is"
print(sentence[10:17])    # "awesome"
print(sentence[:6])       # "Python"
print(sentence[-7:])      # "awesome"
```

### Guided Practice

1. Create a string with your name.
2. Use slicing to print:
   - The first 3 characters
   - The last 3 characters
   - Every 2nd character (using step)
   - The string reversed
3. Create a sentence and use slicing to extract individual words.
4. Predict the output of `"Hello"[1:4:2]` before running it.

### Practice Problems

**Problem 1 — Beginner:** Given `word = "Programming"`, use slicing to print:
- First 4 characters ("Prog")
- Last 4 characters ("ming")
- Every 2nd character ("Pormig")

```python
word = "Programming"

print()  # First 4
print()  # Last 4
print()  # Every 2nd
```

**Problem 2 — Intermediate:** Ask the user for a sentence and print:
- The first word (you'll need to find where the space is)
- The last word
- The sentence reversed

**Problem 3 — Challenge:** Explain what `"Slice"[1:-1:1]` returns and why. Then write code that extracts every 3rd character from a string the user provides.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `word[0:4]`, `word[-4:]`, `word[::2]`.
- Problem 2: The first word is `sentence[0:sentence.find(" ")]` or use slicing if you know the length. Last word is `sentence[sentence.rfind(" ")+1:]` (you'll learn `.rfind()` in the next day).
- Problem 3: `[1:-1:1]` means start at index 1, end at the last character (not including it), step by 1. It removes the first and last characters.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
word = "Programming"
print(word[0:4])    # "Prog"
print(word[-4:])    # "ming"
print(word[::2])    # "Pormig"

# Problem 2 Example
sentence = input("Enter a sentence: ")
space_index = sentence.find(" ")
first_word = sentence[0:space_index]
last_word = sentence[sentence.rfind(" ")+1:]
print(first_word)
print(last_word)
print(sentence[::-1])

# Problem 3
text = input("Enter text: ")
print(text[::3])  # Every 3rd character
```

</details>

---
