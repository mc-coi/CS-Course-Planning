# Day 80: Practice Lab — Pattern Printing and String Analysis

**Learning Target:** I can write complete programs combining for loops, string iteration, range() parameters, and pattern printing.

### Key Concepts

This lab consolidates Week 16 (Days 76–79). You'll apply:
- For loops with range() (counting loops)
- range(start, stop, step) (flexible counting)
- String iteration (character-by-character)
- Choosing for vs while loops

Common applications: patterns, text analysis, visual output.

### Guided Practice

**Option A: Pattern Printing**
Write a program that creates visual patterns using nested for loops:
1. **Right triangle:** 1 star, 2 stars, 3 stars, up to n rows
2. **Square:** n×n grid of stars
3. **Diamond:** wide in middle, narrow at top/bottom

**Option B: Text Analysis**
Write a program that:
- Asks the user for text
- Counts: letters, digits, spaces, punctuation
- Identifies: longest word, shortest word
- Finds: most common letter

**Option C: Number Patterns**
Write a program that prints:
- Multiplication tables (user enters a number, prints 1×n through 10×n)
- Fibonacci sequence (first n numbers)
- Prime numbers (all primes up to a given number)

### Practice Problems

**Problem 1 — Beginner:** Write nested for loops to print a 3×3 grid:
```
* * *
* * *
* * *
```

**Problem 2 — Intermediate:** Write a program that asks for a word and prints:
- The word (original)
- The word (reversed)
- The word in UPPERCASE
- The word in lowercase
- Count of vowels and consonants

**Problem 3 — Challenge:** Write a program that prints a "staircase" pattern:
```
*
* *
* * *
* * * *
* * * * *
```
Where the number of rows is user-defined.

<details>
<summary>💡 Hints</summary>

- Problem 1: Outer loop for rows (3), inner loop for columns (3), print "*" with space
- Problem 2: Use string iteration for vowel/consonant count. Use `.upper()` and `.lower()` methods.
- Problem 3: Outer loop from 1 to n+1, inner loop from 1 to i+1. Each inner iteration prints "*", newline after outer iteration.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
for row in range(3):
    for col in range(3):
        print("*", end=" ")
    print()  # Newline after each row

# Problem 2 Example
word = input("Word: ")
reversed_word = ""
for char in word:
    reversed_word = char + reversed_word

vowels = 0
consonants = 0
for char in word.lower():
    if char.isalpha():
        if char in "aeiou":
            vowels += 1
        else:
            consonants += 1

print(f"Original: {word}")
print(f"Reversed: {reversed_word}")
print(f"Uppercase: {word.upper()}")
print(f"Lowercase: {word.lower()}")
print(f"Vowels: {vowels}, Consonants: {consonants}")

# Problem 3 Example
n = int(input("Number of rows: "))
for i in range(1, n+1):
    for j in range(i):
        print("*", end=" ")
    print()
```

</details>

---

## Week 16 Reflection

**What you've learned:**
- For loops as the primary tool for counting iterations
- range() with one, two, and three parameters
- String iteration for text analysis
- Choosing between for and while loops
- Nested loops for patterns

**Key takeaway:** For loops are perfect for known iterations. When you want to repeat something a specific number of times or iterate over a sequence, reach for a for loop. When you need user input control or complex conditions, use while.

---
