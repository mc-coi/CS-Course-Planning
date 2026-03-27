# Day 84: Common Loop Patterns — Min/Max, Search, Flag

**Learning Target:** I can implement common algorithmic patterns within loops: finding minimum/maximum, searching for a value, and using flag variables.

### Key Concepts

**Min/Max Pattern:** Track the smallest or largest value as you loop.
```python
max_val = numbers[0]  # Start with first value
for num in numbers:
    if num > max_val:
        max_val = num
```

**Search Pattern:** Look for a specific value and record whether found.
```python
found = False
for item in items:
    if item == target:
        found = True
        break
```

**Flag Pattern:** Use a boolean variable to track a condition.
```python
has_vowel = False
for char in word:
    if char in "aeiou":
        has_vowel = True
        break
```

These patterns appear constantly in real programs. Mastering them is essential.

### Code Examples

```python
# Example 1: Find minimum and maximum
numbers = [3, 7, 2, 9, 1, 5]
min_val = numbers[0]
max_val = numbers[0]
for num in numbers:
    if num < min_val:
        min_val = num
    if num > max_val:
        max_val = num
print(f"Min: {min_val}, Max: {max_val}\n")

# Example 2: Search for a value in a list
names = ["Alice", "Bob", "Charlie", "David"]
target = "Charlie"
found = False
position = -1
for i in range(len(names)):
    if names[i] == target:
        found = True
        position = i
        break
if found:
    print(f"Found {target} at position {position}")
else:
    print(f"{target} not found\n")

# Example 3: Flag pattern — check password strength
password = input("Password: ")
is_strong = True
if len(password) < 8:
    is_strong = False
    print("Too short")
if not any(char.isdigit() for char in password):
    is_strong = False
    print("No digits")
if not any(char.isupper() for char in password):
    is_strong = False
    print("No uppercase")
if is_strong:
    print("Strong password!")\nelse:
    print("Weak password\n")

# Example 4: Count matching items
text = input("Text: ")
vowel_count = 0
consonant_count = 0
for char in text.lower():
    if char.isalpha():
        if char in "aeiou":
            vowel_count += 1
        else:
            consonant_count += 1
print(f"Vowels: {vowel_count}, Consonants: {consonant_count}")
```

### Guided Practice

Write a program that:
1. Creates a list of test scores: [85, 92, 78, 95, 88, 79]
2. Finds the highest score using the min/max pattern
3. Finds the lowest score
4. Searches for a specific score entered by the user (search pattern)
5. Uses a flag to track whether any score is 100 (perfect score)

### Practice Problems

**Problem 1 — Beginner:** Write a loop that finds the maximum number in a list: [3, 7, 2, 9, 1, 5, 8].

```python
numbers = [3, 7, 2, 9, 1, 5, 8]
max_val = numbers[0]
for num in numbers:
    # Your code here
print(max_val)
```

**Problem 2 — Intermediate:** Write a program that asks for words until "done" and finds:
- The longest word (using max/length pattern)
- The shortest word (using min/length pattern)

**Problem 3 — Challenge:** Write a program that checks if a string is a "pangram" (contains all 26 letters). Use a flag pattern with a set or counter for each letter.

<details>
<summary>💡 Hints</summary>

- Problem 1: Compare each num to max_val. If num > max_val, update max_val.
- Problem 2: Track max_length and min_length, update when you find longer/shorter words.
- Problem 3: Create a set of all letters found, or count unique letters. Flag is True when you've found all 26.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
numbers = [3, 7, 2, 9, 1, 5, 8]
max_val = numbers[0]
for num in numbers:
    if num > max_val:
        max_val = num
print(max_val)  # 9

# Problem 2 Example
max_word = ""
min_word = ""
while True:
    word = input("Word ('done' to stop): ")
    if word == "done":
        break
    if len(word) > len(max_word):
        max_word = word
    if len(word) < len(min_word) or min_word == "":
        min_word = word
print(f"Longest: {max_word}, Shortest: {min_word}")

# Problem 3 Example
text = input("Text: ").lower()
letters_found = set()
for char in text:
    if char.isalpha():
        letters_found.add(char)
is_pangram = len(letters_found) == 26
if is_pangram:
    print("This is a pangram!")
else:
    print(f"Not a pangram. Missing {26 - len(letters_found)} letters.")
```

</details>

---
