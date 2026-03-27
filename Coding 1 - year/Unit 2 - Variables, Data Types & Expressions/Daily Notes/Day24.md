# Day 24: String Methods — .upper(), .lower(), .replace(), .strip(), .find(), .count()

**Learning Target:** I can apply common string methods to analyze and transform text data.

### Key Concepts

**String methods** are built-in functions designed to work on strings. You call them using **dot notation**: `string.method()`. Methods do NOT modify the original string (strings are immutable); instead, they return a new string.

**`.upper()`** converts all characters to uppercase. For example, `"hello".upper()` returns `"HELLO"`.

**`.lower()`** converts all characters to lowercase. For example, `"HELLO".lower()` returns `"hello"`.

**`.title()`** capitalizes the first letter of each word. For example, `"hello world".title()` returns `"Hello World"`.

**`.strip()`** removes leading and trailing whitespace (spaces, tabs, newlines). It's extremely useful for cleaning user input from `input()`. For example, `"  hello  ".strip()` returns `"hello"`.

**`.replace(old, new)`** replaces all occurrences of a substring with another. For example, `"hello world".replace("world", "Python")` returns `"hello Python"`.

**`.find(substring)`** returns the index where a substring starts, or `-1` if not found. For example, `"hello".find("ll")` returns `2`.

**`.count(substring)`** counts how many times a substring appears. For example, `"banana".count("a")` returns `3`.

**Method chaining** lets you call multiple methods in sequence. Each method returns a string, which you can call another method on. For example: `input().strip().lower().title()` cleans and formats user input in one line.

### Code Examples

```python
text = "  Hello World  "

# Case conversion
print(text.upper())         # "  HELLO WORLD  "
print(text.lower())         # "  hello world  "
print(text.title())         # "  Hello World  "

# Removing whitespace
print(text.strip())         # "Hello World" (no spaces)
print(text.strip().lower()) # "hello world" (chaining!)

# Replace
greeting = "Hello, Alice!"
print(greeting.replace("Alice", "Bob"))  # "Hello, Bob!"
print(greeting.replace("Hello", "Hi"))   # "Hi, Alice!"

# Find and count
word = "programming"
print(word.find("gram"))    # 3 (index where "gram" starts)
print(word.find("z"))       # -1 (not found)
print(word.count("m"))      # 2 (two m's in the word)
print(word.count("pro"))    # 1

# Starts and ends with
print("hello.txt".endswith(".txt"))         # True
print("alice@email.com".startswith("alice"))  # True

# Method chaining
user_input = "  ZACH  "
clean_name = user_input.strip().lower().title()
print(clean_name)  # "Zach"

# Practical example: cleaning and analyzing
sentence = "  The quick brown fox  "
clean = sentence.strip().lower()
print(clean)                    # "the quick brown fox"
print(clean.count("the"))       # 1
print(clean.replace("fox", "cat"))  # "the quick brown cat"
```

### Guided Practice

1. Ask the user for a sentence.
2. Print it in uppercase, lowercase, and title case.
3. Replace a specific word with another word (ask the user which).
4. Count how many times a specific letter appears (ask the user which).
5. Check if the sentence starts with a capital letter or ends with a period.

### Practice Problems

**Problem 1 — Beginner:** Use string methods on the phrase `"PYTHON IS FUN"`:
- Convert to lowercase
- Convert to title case
- Replace "FUN" with "AWESOME"

```python
phrase = "PYTHON IS FUN"

print()  # lowercase
print()  # title case
print()  # replace
```

**Problem 2 — Intermediate:** Ask the user for a word. Check if it's a palindrome (reads the same forwards and backwards) by comparing the word (in lowercase) to its reverse.

**Problem 3 — Challenge:** Write a program that asks for a sentence and performs these tasks:
1. Clean it (strip whitespace, convert to lowercase)
2. Replace all spaces with hyphens
3. Count how many vowels (a, e, i, o, u) are in it
4. Check if the word "python" appears in it

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `.lower()`, `.title()`, `.replace("FUN", "AWESOME")`.
- Problem 2: Compare the word to `word[::-1]` after converting to lowercase. If they're equal, it's a palindrome.
- Problem 3: Use `.strip().lower()`, then `.replace(" ", "-")`. For vowels, count each one: `count("a") + count("e")` etc.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
phrase = "PYTHON IS FUN"
print(phrase.lower())                    # "python is fun"
print(phrase.title())                    # "Python Is Fun"
print(phrase.replace("FUN", "AWESOME"))  # "PYTHON IS AWESOME"

# Problem 2 Example
word = input("Enter a word: ").strip().lower()
if word == word[::-1]:
    print("It's a palindrome!")
else:
    print("Not a palindrome.")

# Problem 3 Example
sentence = input("Enter a sentence: ").strip().lower()
sentence = sentence.replace(" ", "-")
vowel_count = sentence.count("a") + sentence.count("e") + sentence.count("i") + sentence.count("o") + sentence.count("u")
print(sentence)
print(f"Vowels: {vowel_count}")
if "python" in sentence:
    print("Contains 'python'!")
```

</details>

---
