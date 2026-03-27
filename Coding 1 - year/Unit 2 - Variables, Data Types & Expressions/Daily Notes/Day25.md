# Day 25: Practice Lab — String Manipulation Programs

**Learning Target:** I can apply string operations and methods to build complete programs that analyze and transform text.

### Key Concepts

This lab integrates everything from Days 21–24:
- Variable assignment and reassignment
- String indexing and slicing
- String methods (.upper(), .lower(), .strip(), .replace(), .find(), .count())
- Combining operations with method chaining
- Using `len()` and `type()`
- Building multi-step programs that process user input

### Code Examples

```python
# Example 1: Simple text analyzer
text = input("Enter a sentence: ").strip().lower()
print(f"Original: {text}")
print(f"Length: {len(text)}")
print(f"Uppercase: {text.upper()}")
print(f"First word: {text[0:text.find(' ')]}")
print(f"Reversed: {text[::-1]}")

# Example 2: Word replacement program
paragraph = "Python is great. Python is powerful. Python is fun."
old_word = "Python"
new_word = "Java"
updated = paragraph.replace(old_word, new_word)
count = paragraph.count(old_word)
print(f"Found {count} occurrences of '{old_word}'")
print(f"Updated: {updated}")

# Example 3: Character counter
sentence = input("Enter text: ").strip().lower()
target = input("Which character to count? ").strip().lower()
total = sentence.count(target)
print(f"The character '{target}' appears {total} times.")
```

### Guided Practice: Build a String Analyzer

Create a program that:
1. Asks the user for a sentence
2. Cleans it (strip and lowercase)
3. Prints the length
4. Prints the first and last character
5. Prints the sentence reversed
6. Asks what word to search for and prints if it's found
7. Prints the sentence in title case

### Practice Problems

**Problem 1 — Beginner: Name Formatter**
Write a program that:
- Asks for the user's first name and last name (separately)
- Converts both to title case
- Combines them into a full name with a space
- Prints the full name in uppercase

```python
# Starter code
first_name = input("First name: ")
last_name = input("Last name: ")

# Your code here
```

**Problem 2 — Intermediate: Email Validator**
Write a program that:
- Asks for an email address
- Cleans it (strip whitespace, convert to lowercase)
- Checks if it contains an "@" symbol
- Extracts and prints the username (part before @) and domain (part after @)
- Prints if the domain ends with ".com"

**Problem 3 — Challenge: Text Statistics Program**
Write a program that:
- Asks for a paragraph of text
- Counts the total number of characters (including spaces)
- Counts the number of words (use `.split()`)
- Counts vowels (a, e, i, o, u)
- Finds the longest word
- Prints a formatted summary

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `.title()` for first and last names, then use `+` to concatenate.
- Problem 2: Use `.find("@")` to locate the @, then use slicing to extract username and domain.
- Problem 3: Use `.split()` to get words (you'll learn this soon, but try it!). For longest word, you'll need to think about comparing lengths.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
first_name = input("First name: ").strip().title()
last_name = input("Last name: ").strip().title()
full_name = first_name + " " + last_name
print(full_name.upper())

# Problem 2 Example
email = input("Email: ").strip().lower()
at_index = email.find("@")
username = email[0:at_index]
domain = email[at_index+1:]
print(f"Username: {username}")
print(f"Domain: {domain}")
if domain.endswith(".com"):
    print("Valid .com domain!")

# Problem 3 Example
text = input("Enter a paragraph: ").strip().lower()
char_count = len(text)
word_list = text.split()
word_count = len(word_list)
vowel_count = text.count("a") + text.count("e") + text.count("i") + text.count("o") + text.count("u")
longest_word = max(word_list, key=len)
print(f"Characters: {char_count}")
print(f"Words: {word_count}")
print(f"Vowels: {vowel_count}")
print(f"Longest word: {longest_word}")
```

</details>

---

## Lab Reflection

Take 5 minutes to answer:
1. Which string method was most useful in your program?
2. What was the trickiest part of string manipulation?
3. How could you extend this program (add more features)?
