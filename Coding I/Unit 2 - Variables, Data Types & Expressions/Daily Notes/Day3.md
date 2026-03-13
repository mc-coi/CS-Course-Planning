# Day 3: String Data Type & Operations
**Learning Target:** I can create strings and use concatenation, indexing, and slicing.

### Key Concepts
**Strings** are sequences of characters (text). They can use single quotes `'hello'` or double quotes `"hello"`.

**Concatenation** combines strings using `+`:
```python
first = "John"
last = "Doe"
full = first + " " + last  # "John Doe"
```

**Repetition** repeats a string using `*`:
```python
print("Ha" * 3)  # "HaHaHa"
```

**Length** finds how many characters are in a string:
```python
word = "Python"
print(len(word))  # 6
```

**Indexing** accesses individual characters. Indexing starts at 0:
```python
word = "Python"
print(word[0])    # "P" (first character)
print(word[1])    # "y" (second character)
print(word[-1])   # "n" (last character)
print(word[-2])   # "o" (second-to-last)
```

**Slicing** extracts portions of a string using `[start:stop]` (stop is exclusive):
```python
word = "Python"
print(word[0:3])   # "Pyt" (chars 0,1,2)
print(word[2:5])   # "tho" (chars 2,3,4)
print(word[:3])    # "Pyt" (from start to 3)
print(word[3:])    # "hon" (from 3 to end)
print(word[::-1])  # "nohtyP" (reversed!)
```

### Code Examples
```python
# Concatenation
name = "Alex"
greeting = "Hello, " + name + "!"
print(greeting)    # "Hello, Alex!"

# Repetition
print("*" * 10)    # "**********"

# Length
word = "Programming"
print(len(word))   # 11

# Indexing
sentence = "Python is fun"
print(sentence[0])    # "P"
print(sentence[-1])   # "n"

# Slicing
print(sentence[0:6])   # "Python"
print(sentence[10:13]) # "fun"
print(sentence[:6])    # "Python"
print(sentence[7:])    # "is fun"
print(sentence[::-1])  # "nuf si nohtyP" (reversed)
```

### Guided Practice
Write a program that:
1. Asks the user for a word
2. Prints the first character, last character, middle character
3. Prints the word reversed
4. Prints the length of the word

### Practice Problems
**Problem 1 — Beginner:** Create a string with your name and print the first 3 characters, last 3 characters, and the whole string reversed.

```python
name =

print()  # first 3
print()  # last 3
print()  # reversed
```

**Problem 2 — Intermediate:** Write a program that asks for a sentence and counts how many characters are in it.

**Problem 3 — Challenge:** Predict the output of `"Python"[1:5:2]` (slicing with step). Explain what the third number in `[start:stop:step]` does.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use indexing with [0], [-1], [::-1], or slicing
- Problem 2: Use `len()` function
- Problem 3: Step skips characters; `[1:5:2]` takes chars 1 and 3
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = "Alexandra"
print(name[0:3])      # "Ale"
print(name[-3:])      # "dra"
print(name[::-1])     # "ardnaxelA"

# Problem 2 Example
sentence = input("Enter sentence: ")
print(f"Character count: {len(sentence)}")

# Problem 3
print("Python"[1:5:2])  # "yo" (indices 1 and 3)
```
</details>

---