# Unit 4 Practice Bank — 25 Problems by Difficulty

## Beginner Problems (Days 71–80 Concepts)

### Problem 1: Simple While Loop
Write a while loop that prints the numbers 1 through 10.

<details>
<summary>✅ Solution</summary>

```python
count = 1
while count <= 10:
    print(count)
    count += 1
```

</details>

---

### Problem 2: While Loop with Sentinel
Write a program that asks the user for numbers until they enter 0, then prints how many numbers were entered (not counting 0).

<details>
<summary>✅ Solution</summary>

```python
count = 0
while True:
    num = int(input("Enter number (0 to stop): "))
    if num == 0:
        break
    count += 1
print(f"You entered {count} numbers")
```

</details>

---

### Problem 3: For Loop with range()
Write a for loop that prints every other number from 0 to 10 (0, 2, 4, 6, 8, 10).

<details>
<summary>✅ Solution</summary>

```python
for i in range(0, 11, 2):
    print(i)
```

</details>

---

### Problem 4: Accumulator Pattern
Write a loop that calculates the sum of numbers 1 through 20.

<details>
<summary>✅ Solution</summary>

```python
total = 0
for i in range(1, 21):
    total += i
print(f"Sum: {total}")  # 210
```

</details>

---

### Problem 5: String Iteration
Write a loop that counts how many vowels are in the word "programming".

<details>
<summary>✅ Solution</summary>

```python
word = "programming"
vowel_count = 0
for char in word:
    if char in "aeiou":
        vowel_count += 1
print(f"Vowels: {vowel_count}")  # 3
```

</details>

---

### Problem 6: List Creation and Indexing
Create a list of 5 colors. Print the first color, last color, and length.

<details>
<summary>✅ Solution</summary>

```python
colors = ["red", "blue", "green", "yellow", "purple"]
print(f"First: {colors[0]}")
print(f"Last: {colors[-1]}")
print(f"Length: {len(colors)}")
```

</details>

---

### Problem 7: For-Each Loop
Create a list of 4 fruits. Print each fruit with a label using a for-each loop.

<details>
<summary>✅ Solution</summary>

```python
fruits = ["apple", "banana", "cherry", "date"]
for fruit in fruits:
    print(f"Fruit: {fruit}")
```

</details>

---

### Problem 8: List Methods (.append and .sort)
Create an empty list. Ask the user for 3 numbers, append each to the list, sort, then print.

<details>
<summary>✅ Solution</summary>

```python
numbers = []
for i in range(3):
    num = int(input(f"Number {i+1}: "))
    numbers.append(num)
numbers.sort()
print(f"Sorted: {numbers}")
```

</details>

---

### Problem 9: Range with Negative Step
Write a loop that prints 20 down to 1 (countdown) using range with negative step.

<details>
<summary>✅ Solution</summary>

```python
for i in range(20, 0, -1):
    print(i)
```

</details>

---

### Problem 10: Simple Nested Loop
Write nested loops to print a 2×3 grid (2 rows, 3 columns) of asterisks.

<details>
<summary>✅ Solution</summary>

```python
for row in range(2):
    for col in range(3):
        print("*", end=" ")
    print()
```

</details>

---

## Intermediate Problems (Days 81–88 Concepts)

### Problem 11: Break and Continue
Write a loop from 1 to 10. Use continue to skip multiples of 3, and break when you reach 8.

<details>
<summary>✅ Solution</summary>

```python
for i in range(1, 11):
    if i == 8:
        break
    if i % 3 == 0:
        continue
    print(i)
```

</details>

---

### Problem 12: Input Validation
Write a program that asks for an age (1-120) repeatedly until valid input is given.

<details>
<summary>✅ Solution</summary>

```python
while True:
    age = int(input("Age (1-120): "))
    if 1 <= age <= 120:
        break
    print("Invalid. Try again.")
print(f"Your age: {age}")
```

</details>

---

### Problem 13: Min/Max Pattern
Write a loop that finds the highest number in the list [3, 7, 2, 9, 1, 5].

<details>
<summary>✅ Solution</summary>

```python
numbers = [3, 7, 2, 9, 1, 5]
max_val = numbers[0]
for num in numbers:
    if num > max_val:
        max_val = num
print(f"Maximum: {max_val}")
```

</details>

---

### Problem 14: Nested Loop (Multiplication Table)
Write nested loops to print a 4×4 multiplication table.

<details>
<summary>✅ Solution</summary>

```python
for i in range(1, 5):
    for j in range(1, 5):
        print(f"{i*j:3}", end=" ")
    print()
```

</details>

---

### Problem 15: Search Pattern
Write a program that searches for a specific name in the list ["Alice", "Bob", "Charlie", "David"]. Use a flag variable.

<details>
<summary>✅ Solution</summary>

```python
names = ["Alice", "Bob", "Charlie", "David"]
target = input("Find: ")
found = False
for name in names:
    if name == target:
        found = True
        break
if found:
    print(f"Found {target}!")
else:
    print(f"{target} not found.")
```

</details>

---

### Problem 16: List Modification
Create a list [1, 2, 3, 4, 5]. Remove the number 3, append 6, sort, then print.

<details>
<summary>✅ Solution</summary>

```python
numbers = [1, 2, 3, 4, 5]
numbers.remove(3)
numbers.append(6)
numbers.sort()
print(numbers)  # [1, 2, 4, 5, 6]
```

</details>

---

### Problem 17: Average Calculation
Write a program that asks for test scores until -1 is entered, then calculates the average.

<details>
<summary>✅ Solution</summary>

```python
scores = []
while True:
    score = int(input("Score (-1 to stop): "))
    if score == -1:
        break
    scores.append(score)
if len(scores) > 0:
    average = sum(scores) / len(scores)
    print(f"Average: {average:.2f}")
```

</details>

---

### Problem 18: Character Counting
Write a loop that counts uppercase letters in the string "Hello World".

<details>
<summary>✅ Solution</summary>

```python
text = "Hello World"
uppercase_count = 0
for char in text:
    if char.isupper():
        uppercase_count += 1
print(f"Uppercase letters: {uppercase_count}")  # 2
```

</details>

---

### Problem 19: Nested Loop (Pattern)
Write nested loops to print a right triangle:
```
*
* *
* * *
* * * *
```

<details>
<summary>✅ Solution</summary>

```python
for i in range(1, 5):
    for j in range(i):
        print("*", end=" ")
    print()
```

</details>

---

### Problem 20: Building a List from Input
Ask the user for 5 favorite movies. Store in a list. Print them with numbers (1, 2, 3, ...).

<details>
<summary>✅ Solution</summary>

```python
movies = []
for i in range(5):
    movie = input(f"Movie {i+1}: ")
    movies.append(movie)
for i in range(len(movies)):
    print(f"{i+1}: {movies[i]}")
```

</details>

---

## Advanced/Challenge Problems (Days 86–89 Concepts)

### Problem 21: Palindrome Checker
Write a program that checks if a word is a palindrome (reads same forwards and backwards) using a loop.

<details>
<summary>✅ Solution</summary>

```python
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

### Problem 22: Fibonacci Sequence
Write a program that prints the first 10 Fibonacci numbers (0, 1, 1, 2, 3, 5, 8, ...).

<details>
<summary>✅ Solution</summary>

```python
a, b = 0, 1
for i in range(10):
    print(a, end=" ")
    a, b = b, a + b
```

</details>

---

### Problem 23: Grade Analyzer
Write a program that:
- Asks for test grades until "done" is entered
- Finds highest, lowest, and average
- Counts how many passed (>= 70)

<details>
<summary>✅ Solution</summary>

```python
grades = []
while True:
    grade_input = input("Grade ('done' to stop): ")
    if grade_input == "done":
        break
    grades.append(int(grade_input))

if len(grades) > 0:
    print(f"Highest: {max(grades)}")
    print(f"Lowest: {min(grades)}")
    print(f"Average: {sum(grades)/len(grades):.2f}")

    passed = 0
    for grade in grades:
        if grade >= 70:
            passed += 1
    print(f"Passed: {passed}/{len(grades)}")
```

</details>

---

### Problem 24: Word Frequency Counter
Write a program that asks for words until "done", then counts how many times each unique word appears.

<details>
<summary>✅ Solution</summary>

```python
words = []
while True:
    word = input("Word ('done' to stop): ")
    if word == "done":
        break
    words.append(word.lower())

# Count occurrences
unique_words = []
for word in words:
    if word not in unique_words:
        unique_words.append(word)
        count = words.count(word)
        print(f"{word}: {count}")
```

</details>

---

### Problem 25: Simple Number Guessing Game
Write a game where:
- Computer picks a random number (1-50)
- User guesses repeatedly
- Program says "higher" or "lower"
- Count attempts and display when guessed correctly

<details>
<summary>✅ Solution</summary>

```python
import random
secret = random.randint(1, 50)
attempts = 0

while True:
    guess = int(input("Guess (1-50): "))
    attempts += 1

    if guess == secret:
        print(f"Correct! You got it in {attempts} attempts!")
        break
    elif guess < secret:
        print("Too low!")
    else:
        print("Too high!")
```

</details>

---

## Practice Problem Summary by Topic

### While Loops
Problems: 1, 2, 12, 17

### For Loops & range()
Problems: 3, 4, 9

### String Iteration
Problems: 5, 18, 21

### Lists
Problems: 6, 7, 8, 16, 20

### Nested Loops
Problems: 10, 14, 19

### Patterns (Min/Max, Search, etc.)
Problems: 11, 13, 15, 22, 23, 24, 25

### Mini-Projects
Problems: 23, 24, 25

---

## Self-Paced Practice Tips

1. **Start with beginner problems.** Get comfortable with basic loops.
2. **Progress to intermediate.** Apply patterns and multiple concepts.
3. **Challenge yourself.** Try advanced problems; they're synthesis of earlier concepts.
4. **Test your code.** Run it with sample inputs.
5. **Trace on paper.** Before running, predict the output.
6. **Debug actively.** Use print statements to see variable values.
7. **Read solutions.** Compare your approach to the sample solution.

---

## Hints by Difficulty

**Beginner Tips:**
- Focus on the basic structure (while/for)
- Make sure loop body is indented
- Test with simple inputs first

**Intermediate Tips:**
- Think about edge cases (empty list, single item)
- Use patterns you've learned (min/max, search)
- Test both expected and unexpected inputs

**Advanced Tips:**
- Break complex problems into smaller parts
- Use multiple loops if needed
- Comment your code thoroughly
- Test extensively

---
