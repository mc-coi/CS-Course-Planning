# Day 4: String Methods
**Learning Target:** I can use common string methods to manipulate text.

### Key Concepts
**String methods** are built-in functions that work on strings. Use syntax: `string.method()`

Common methods:
- `.upper()` - return uppercase version
- `.lower()` - return lowercase version
- `.title()` - return title case (first letter of each word capitalized)
- `.strip()` - remove leading/trailing whitespace
- `.replace(old, new)` - replace all occurrences
- `.split()` - split into a list of words
- `.find(substring)` - return index of substring (-1 if not found)
- `.count(substring)` - count occurrences
- `.startswith(prefix)` - True if starts with prefix
- `.endswith(suffix)` - True if ends with suffix

Methods can be **chained**: `input().strip().lower().title()`

### Code Examples
```python
msg = "  Hello World  "

# Case methods
print(msg.upper())          # "  HELLO WORLD  "
print(msg.lower())          # "  hello world  "
print(msg.title())          # "  Hello World  "
print(msg.strip())          # "Hello World" (no spaces)
print(msg.strip().upper())  # "HELLO WORLD" (chaining)

# Replace and split
text = "hello world"
print(text.replace("world", "Python"))  # "hello Python"
print(text.split())         # ['hello', 'world']

# Find and count
word = "programming"
print(word.find("ram"))     # 3 (index where "ram" starts)
print(word.count("m"))      # 2 (two m's)

# Starts/ends with
print("hello.txt".endswith(".txt"))      # True
print("alice@email.com".startswith("alice"))  # True

# Chaining methods
user_input = "  ZACH  "
clean = user_input.strip().lower().title()
print(clean)                # "Zach"
```

### Guided Practice
Write a program that asks the user for a sentence and performs these operations:
1. Print uppercase and lowercase versions
2. Replace all spaces with hyphens
3. Print the first word using `.split()`
4. Count how many times the letter 'e' appears
5. Check if it starts with a capital letter

### Practice Problems
**Problem 1 — Beginner:** Use string methods on the phrase "PYTHON IS FUN": lowercase, titlecase, and replace "FUN" with "AWESOME".

```python
phrase = "PYTHON IS FUN"

print()  # lowercase
print()  # titlecase
print()  # replace
```

**Problem 2 — Intermediate:** Write a program that asks for a word and tells the user if it's a palindrome (reads the same forwards and backwards) using string methods.

**Problem 3 — Challenge:** Chain 4+ string methods together to clean user input: remove whitespace, convert to lowercase, replace punctuation, and check if a word is in it.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use .lower(), .title(), .replace()
- Problem 2: Use .lower() to make comparison case-insensitive, then compare to [::-1]
- Problem 3: Strip, lower, replace, then find or endswith
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
word = input("Enter word: ").strip().lower()
if word == word[::-1]:
    print("It's a palindrome!")
else:
    print("Not a palindrome.")
```
</details>

---