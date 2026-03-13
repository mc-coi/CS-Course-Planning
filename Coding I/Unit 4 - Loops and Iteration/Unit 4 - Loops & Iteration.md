# Unit 4: Loops & Iteration
> Master loops to automate repetitive tasks and process collections of data.

##  Unit Overview
- **Duration:** 9 days / 3 weeks
- **Key Concepts:** while loops, for loops, range(), loop control (break/continue), nested loops, accumulator pattern, and loop applications
- **Big Idea:** Loops let you repeat code without copying it, enabling you to process many items efficiently

##  Learning Targets
- I can write while loops with proper loop control variables
- I can use for loops with range() in various forms
- I can use loops with user input and validation
- I can write nested loops for complex iteration
- I can use break and continue to control loop flow
- I can iterate over strings and use the accumulator pattern
- I can choose between while and for loops appropriately
- I can debug loop errors and trace execution
- I can build a complete program using loops

---

# Day 1: while Loops
**Learning Target:** I can write while loops with proper loop control variables.

### Key Concepts
A **while loop** repeats code as long as a condition is True. It continues until the condition becomes False.

**Loop control variable:** A variable that changes each iteration, eventually making the condition False. Without it, you get an infinite loop.

Pattern:
```
initialize counter
while condition:
    do work
    update counter
```

### Code Examples
```python
# Countdown with while
count = 10
while count > 0:
    print(count)
    count -= 1  # MUST update counter
print("Blast off!")

# Sum numbers with while
total = 0
num = 1
while num <= 10:
    total += num
    num += 1
print("Sum 1-10:", total)  # 55

# Sentinel value pattern (stop when user enters -1)
total = 0
num = int(input("Enter number (-1 to quit): "))
while num != -1:
    total += num
    num = int(input("Enter number (-1 to quit): "))
print("Total:", total)

# Infinite loop WARNING (DON'T DO THIS!)
# while True:
#     print("Help!")  # Never stops!
```

### Guided Practice
Write a program that asks for test scores until the user enters -1, then prints the average.

### Practice Problems
**Problem 1 — Beginner:** Write a while loop that prints numbers 1-10.

```python
count = 1
while :
    print()
    count += 1
```

**Problem 2 — Intermediate:** Ask for a positive number. Use a while loop that keeps asking until one is entered.

**Problem 3 — Challenge:** Sum all numbers from 1-100 using a while loop.

<details>
<summary>💡 Hints</summary>

- Problem 1: Condition is `count <= 10`
- Problem 2: Condition is `num <= 0` (keep looping while invalid)
- Problem 3: Initialize total and counter, update both each iteration
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
count = 1
while count <= 10:
    print(count)
    count += 1

# Problem 2 Example
num = int(input("Positive number: "))
while num <= 0:
    num = int(input("Positive number: "))
print(f"You entered {num}")

# Problem 3 Example
total = 0
count = 1
while count <= 100:
    total += count
    count += 1
print(f"Sum: {total}")  # 5050
```
</details>

---

# Day 2: for Loops & range()
**Learning Target:** I can use for loops with range() in various forms.

### Key Concepts
A **for loop** iterates a fixed number of times. **range()** generates a sequence of numbers.

range() forms:
- `range(stop)` → 0 to stop-1
- `range(start, stop)` → start to stop-1
- `range(start, stop, step)` → start to stop-1 by step

### Code Examples
```python
# range(stop) — 0 to 9
for i in range(10):
    print(i)  # 0 1 2 3 4 5 6 7 8 9

# range(start, stop) — 1 to 10
for i in range(1, 11):
    print(i)  # 1 2 3 4 5 6 7 8 9 10

# range(start, stop, step) — by 2s
for i in range(0, 11, 2):
    print(i)  # 0 2 4 6 8 10

# Counting down
for i in range(10, 0, -1):
    print(i)  # 10 9 8 ... 1

# Sum numbers
total = 0
for i in range(1, 101):
    total += i
print(f"Sum 1-100: {total}")  # 5050
```

### Guided Practice
Create a program that prints a multiplication table for a number the user enters (rows 1-10).

### Practice Problems
**Problem 1 — Beginner:** Print numbers 1-20 using for loop with range().

**Problem 2 — Intermediate:** Print every 3rd number from 0-30 (0, 3, 6, 9...).

**Problem 3 — Challenge:** Print numbers 100 down to 1.

<details>
<summary>💡 Hints</summary>

- Problem 1: `range(1, 21)`
- Problem 2: `range(0, 31, 3)`
- Problem 3: `range(100, 0, -1)`
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
for i in range(1, 21):
    print(i)

# Problem 2
for i in range(0, 31, 3):
    print(i)

# Problem 3
for i in range(100, 0, -1):
    print(i)
```
</details>

---

# Day 3: Loops with User Input
**Learning Target:** I can use loops with user input and validation.

### Key Concepts
Loops are perfect for repeated user interaction: getting input, validating, prompting again if invalid, etc.

**Sentinel value pattern:** Keep looping until user enters a specific value (like -1 or "quit").

### Code Examples
```python
# Validation loop
while True:
    try:
        age = int(input("Age (0-120): "))
        if 0 <= age <= 120:
            break
        print("Please enter 0-120")
    except ValueError:
        print("Please enter a number")

# Accumulate user scores
total = 0
count = 0
while True:
    score = int(input("Score (-1 to quit): "))
    if score == -1:
        break
    total += score
    count += 1
average = total / count if count > 0 else 0
print(f"Average: {average:.2f}")

# Keep asking until correct
password = "secret"
while True:
    guess = input("Password: ")
    if guess == password:
        print("Correct!")
        break
    print("Wrong, try again")
```

### Guided Practice
Create a program that asks for test scores (stop on -1), calculates average, and validates all entries are 0-100.

### Practice Problems
**Problem 1 — Beginner:** Ask the user for 5 numbers and print the sum.

**Problem 2 — Intermediate:** Ask for scores until -1 is entered, print highest and lowest score.

**Problem 3 — Challenge:** Ask for a password with retry limit (3 attempts, then lock out).

---

# Day 4: Nested Loops
**Learning Target:** I can write nested loops for complex iteration.

### Key Concepts
A **nested loop** is a loop inside another loop. The inner loop runs completely for each iteration of the outer loop.

**Total iterations** = outer × inner

### Code Examples
```python
# Multiplication table
for i in range(1, 6):
    for j in range(1, 6):
        print(f"{i*j:4}", end=" ")  # 4-char width
    print()  # newline after inner loop

# Star pattern
for row in range(1, 6):
    for col in range(row):
        print("*", end="")
    print()  # 1 star, 2 stars, 3 stars...

# Print coordinates
for x in range(1, 4):
    for y in range(1, 4):
        print(f"({x},{y})", end=" ")
    print()
```

### Guided Practice
Create a program that prints a 5×5 grid of numbers (1-25).

### Practice Problems
**Problem 1 — Beginner:** Print a rectangle of stars: 3 rows × 4 columns.

**Problem 2 — Intermediate:** Print a triangle: row 1 has 1 star, row 2 has 2 stars, etc. (up to 6).

**Problem 3 — Challenge:** Print a multiplication table formatted as a grid (1-10 × 1-10).

<details>
<summary>💡 Hints</summary>

- Problem 1: Outer loop for rows, inner for columns
- Problem 2: Outer loop for rows, inner loop `range(row + 1)`
- Problem 3: Format with colons for alignment
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
for row in range(3):
    for col in range(4):
        print("*", end="")
    print()

# Problem 2
for row in range(1, 7):
    for star in range(row):
        print("*", end="")
    print()

# Problem 3
for i in range(1, 11):
    for j in range(1, 11):
        print(f"{i*j:4}", end="")
    print()
```
</details>

---

# Day 5: break & continue
**Learning Target:** I can use break and continue to control loop flow.

### Key Concepts
- **break:** Exits the loop immediately
- **continue:** Skips the rest of the current iteration, goes to next iteration
- **for/else:** Else block runs if loop completes without break

### Code Examples
```python
# break — exit when found
for i in range(1, 101):
    if i % 7 == 0 and i % 11 == 0:
        print(f"Found: {i}")
        break  # Exit loop

# continue — skip multiples of 3
for i in range(1, 11):
    if i % 3 == 0:
        continue  # Skip to next iteration
    print(i)  # Prints 1,2,4,5,7,8,10

# for/else — runs if no break
for i in range(2, 20):
    if 20 % i == 0:
        print(f"{i} divides 20")
        break
else:
    print("20 is prime")  # Only if no break occurred
```

### Guided Practice
Write a program that finds the first number divisible by both 3 and 5 starting from 1.

### Practice Problems
**Problem 1 — Beginner:** Print numbers 1-20, skip multiples of 5 using continue.

**Problem 2 — Intermediate:** Find the first number greater than 100 that's prime, exit with break.

**Problem 3 — Challenge:** Search for a user's name in a list; break when found, print "Found" or "Not found".

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `if i % 5 == 0: continue`
- Problem 2: Check if any number < i divides it
- Problem 3: Use break when name matches, with for/else for "not found"
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
for i in range(1, 21):
    if i % 5 == 0:
        continue
    print(i)

# Problem 3
names = ["Alice", "Bob", "Charlie"]
search = input("Search for: ")
for name in names:
    if name == search:
        print("Found!")
        break
else:
    print("Not found")
```
</details>

---

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

# Day 7: Accumulator Pattern
**Learning Target:** I can recognize and use the accumulator pattern in various situations.

### Key Concepts
**Accumulator pattern:** Initialize before loop, update inside loop with compound operator (+=, -=, etc.), use result after loop.

Works for: sum, product, count, min, max, string building, list building.

### Code Examples
```python
# Sum accumulator
total = 0
for i in range(1, 101):
    total += i
print(f"Sum: {total}")  # 5050

# Product accumulator
product = 1
for i in range(1, 6):
    product *= i
print(f"5! = {product}")  # 120

# Count accumulator
text = "hello world"
count = 0
for ch in text:
    if ch == "l":
        count += 1
print(f"L count: {count}")  # 3

# Min/max accumulators
numbers = [34, 12, 78, 5, 90, 23]
min_val = numbers[0]
max_val = numbers[0]
for num in numbers:
    if num < min_val:
        min_val = num
    if num > max_val:
        max_val = num
print(f"Min: {min_val}, Max: {max_val}")  # Min: 5, Max: 90

# String accumulator
text = "Python"
result = ""
for ch in text:
    if ch != "o":
        result += ch
print(result)  # "Pythn"
```

### Guided Practice
Write a program that:
1. Sums numbers 1-50
2. Finds product 1-5 (factorial)
3. Counts vowels in a sentence
4. Finds min and max in a list

### Practice Problems
**Problem 1 — Beginner:** Calculate factorial using accumulator: 5! = 1×2×3×4×5.

**Problem 2 — Intermediate:** Count how many times each vowel appears in a sentence.

**Problem 3 — Challenge:** Find the average of numbers input by user (until -1).

<details>
<summary>💡 Hints</summary>

- Problem 1: Initialize product = 1, then *=
- Problem 2: Five accumulators (one per vowel) or one loop counting each
- Problem 3: Accumulate total and count, divide at end
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
product = 1
for i in range(1, 6):
    product *= i
print(f"5! = {product}")

# Problem 3
total = 0
count = 0
while True:
    num = int(input("Number (-1 to quit): "))
    if num == -1:
        break
    total += num
    count += 1
average = total / count if count > 0 else 0
print(f"Average: {average:.2f}")
```
</details>

---

# Day 8: FizzBuzz & Review
**Learning Target:** I can trace loop execution and solve classic loop problems.

### Key Concepts
**FizzBuzz** is a classic programming problem: print 1-100, but:
- Multiples of 3: print "Fizz"
- Multiples of 5: print "Buzz"
- Multiples of both: print "FizzBuzz"
- Otherwise: print the number

### Code Examples
```python
# FizzBuzz
for i in range(1, 101):
    if i % 15 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)

# Number pyramid
for i in range(1, 6):
    print(str(i) * i)  # 1, 22, 333, 4444, 55555

# Print numbers in order (review for/while choice)
for i in range(10):
    print(i, end=" ")  # for loop — fixed count
```

### Practice Problems
**Problem 1 — Beginner:** Implement basic FizzBuzz (multiples of 3 only).

**Problem 2 — Intermediate:** Implement full FizzBuzz as described.

**Problem 3 — Challenge:** Extend FizzBuzz: add "Bazz" for multiples of 7.

---

# Day 9: Unit 4 Project
**Learning Target:** I can build a complete program using loops.

### Project: Game Number Guessing Game with Statistics

Create a program that plays multiple rounds of guessing. Your program must include:

**Requirements:**
- At least 2 nested loops (outer for rounds, inner for retries or attempts)
- At least 1 loop with break
- At least 1 loop with continue
- Accumulator pattern (track wins, losses, average guesses)
- Clear output showing statistics
- At least 5 comments

**Example:**
```
=== GUESSING GAME ===
Round 1: I'm thinking of 1-10
Guess 1: 5
Guess 2: 7
Correct! (2 guesses)
Play again? (y/n): y
...
=== STATS ===
Rounds played: 5
Wins: 4
Average guesses: 2.5
```

---

## Unit Practice Bank (15 problems)

1. **Beginner:** Write while loop that prints 1-10
2. **Beginner:** Write for loop with range(5, 16)
3. **Beginner:** What does `range(10, 0, -1)` print?
4. **Intermediate:** Ask for scores (-1 to quit), print total and average
5. **Intermediate:** Print multiplication table for number 5 (5×1 through 5×10)
6. **Intermediate:** Count vowels in a word
7. **Intermediate:** Find product 1-10 (10 factorial)
8. **Challenge:** Implement FizzBuzz (multiples of 3 and 5)
9. **Challenge:** Print triangle: 1, 22, 333, 4444, etc.
10. **Challenge:** Find first number > 100 divisible by 7
11. **Challenge:** Ask for list of numbers, find min/max/average
12. **Challenge:** Build reversed string without using slicing
13. **Challenge:** Check if word is palindrome
14. **Challenge:** Count each vowel separately in a sentence
15. **Challenge:** Game: pick random number 1-100, let user guess with hints

---

## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Infinite loop (while True without break) | Program never stops | Add break or make condition eventually False |
| Forgetting loop update: `while x > 0: print(x)` | Infinite loop | Add `x -= 1` or similar |
| Off-by-one in range: `range(10)` when need 1-10 | Prints 0-9 instead of 1-10 | Use `range(1, 11)` |
| Wrong indentation in nested loop | Inner loop doesn't nest properly | Check spacing matches nesting level |
| Using = instead of == in loop condition | SyntaxError | Use `==` for comparison |
| Accumulator starts at wrong value | Wrong result | Initialize at 0 for sum, 1 for product, "" for string |
| Not importing `random` before `random.randint()` | NameError | Add `import random` at top |
| String concatenation slow in loop | Performance issue | OK for small loops, but consider for large |

---

## Unit Assessment Prep

1. Explain the difference between while and for loops. When use each?
2. What does `range(1, 11, 2)` produce?
3. Describe the accumulator pattern for sum.
4. What does break do? What does continue do?
5. How do nested loops work? Calculate iterations.
6. Write a for loop that counts 0-10.
7. Trace through a nested loop and predict output.
8. What is a sentinel value?
9. Implement FizzBuzz in pseudocode.
10. Explain how for/else works.

---

## Vocabulary & Quick Reference

**Key Terms:**
- **Loop:** Repeated code execution
- **Iteration:** One execution of loop body
- **Loop control variable:** Variable that changes each iteration
- **Sentinel value:** Special input that stops loop
- **Nested loop:** Loop inside another loop
- **Accumulator:** Variable updated in loop to accumulate result
- **for/else:** else block runs if loop completes without break

**Syntax:**
```python
# while loop
while condition:
    # code
    # update condition

# for loop
for variable in range(start, stop, step):
    # code

# for with string
for char in "hello":
    # code

# Loop control
break      # exit immediately
continue   # skip to next iteration

# for/else
for i in range(10):
    if i == 5:
        break
else:
    print("No break!")  # won't print (break happened)
```

**range() Quick Reference:**
- `range(5)` → 0,1,2,3,4
- `range(1,6)` → 1,2,3,4,5
- `range(0,10,2)` → 0,2,4,6,8
- `range(10,0,-1)` → 10,9,8,...,1
