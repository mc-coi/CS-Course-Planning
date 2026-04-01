# Unit 4 Answer Key — 25 Problems

## Beginner Problems

---

## Problem 1: Simple While Loop

Write a while loop that prints the numbers 1 through 10.

### Solution
```python
# Initialize counter
count = 1

# Loop while count is 10 or less
while count <= 10:
    print(count)
    count += 1
```

### Expected Output
```
1
2
3
4
5
6
7
8
9
10
```

### Common Mistakes
- Forgetting to increment count (creates infinite loop)
- Starting at 0 instead of 1
- Using count < 10 instead of count <= 10 (would miss 10)

---

## Problem 2: While Loop with Sentinel

Write a program that asks the user for numbers until they enter 0, then prints how many numbers were entered (not counting 0).

### Solution
```python
# Initialize counter
count = 0

# Loop until user enters 0
while True:
    num = int(input("Enter number (0 to stop): "))
    if num == 0:
        break
    count += 1

# Display total
print(f"You entered {count} numbers")
```

### Expected Output
```
Enter number (0 to stop): 5
Enter number (0 to stop): 10
Enter number (0 to stop): 0
You entered 2 numbers
```

### Common Mistakes
- Counting the 0 as a number entered
- Not using break to exit the loop
- Incrementing count before checking for sentinel value

---

## Problem 3: For Loop with range()

Write a for loop that prints every other number from 0 to 10 (0, 2, 4, 6, 8, 10).

### Solution
```python
# For loop with range starting at 0, ending at 11, step 2
for i in range(0, 11, 2):
    print(i)
```

### Expected Output
```
0
2
4
6
8
10
```

### Common Mistakes
- Using range(0, 10, 2) which stops at 8 (missing 10)
- Not understanding the third parameter (step)

---

## Problem 4: Accumulator Pattern

Write a loop that calculates the sum of numbers 1 through 20.

### Solution
```python
# Initialize total
total = 0

# Add each number from 1 to 20
for i in range(1, 21):
    total += i

# Display result
print(f"Sum: {total}")  # 210
```

### Expected Output
```
Sum: 210
```

### Common Mistakes
- Not initializing total to 0
- Using range(1, 20) which stops at 19
- Forgetting to add to total in the loop

---

## Problem 5: String Iteration and Vowel Count

Write a loop that counts how many vowels are in the word "programming".

### Solution
```python
# The word to check
word = "programming"

# Initialize vowel counter
vowel_count = 0

# Check each character
for char in word:
    if char in "aeiou":
        vowel_count += 1

# Display result
print(f"Vowels: {vowel_count}")  # 3
```

### Expected Output
```
Vowels: 3
```

### Common Mistakes
- Using "aeiouAEIOU" (program is all lowercase)
- Not understanding the "in" operator for strings
- Forgetting to count correctly (a, o, i = 3)

---

## Problem 6: List Creation and Indexing

Create a list of 5 colors. Print the first color, last color, and length.

### Solution
```python
# Create a list of colors
colors = ["red", "blue", "green", "yellow", "purple"]

# Print first color (index 0)
print(f"First: {colors[0]}")

# Print last color (index -1)
print(f"Last: {colors[-1]}")

# Print length
print(f"Length: {len(colors)}")
```

### Expected Output
```
First: red
Last: purple
Length: 5
```

### Common Mistakes
- Using index 1 instead of 0 for first element
- Not understanding negative indexing for last element

---

## Problem 7: For-Each Loop

Create a list of 4 fruits. Print each fruit with a label using a for-each loop.

### Solution
```python
# Create list of fruits
fruits = ["apple", "banana", "cherry", "date"]

# Iterate through each fruit
for fruit in fruits:
    print(f"Fruit: {fruit}")
```

### Expected Output
```
Fruit: apple
Fruit: banana
Fruit: cherry
Fruit: date
```

### Common Mistakes
- Using index-based loop instead of for-each
- Not using f-strings for output formatting

---

## Problem 8: List Methods (.append and .sort)

Create an empty list. Ask the user for 3 numbers, append each to the list, sort, then print.

### Solution
```python
# Create empty list
numbers = []

# Ask user for 3 numbers
for i in range(3):
    num = int(input(f"Number {i+1}: "))
    numbers.append(num)

# Sort the list
numbers.sort()

# Display sorted list
print(f"Sorted: {numbers}")
```

### Expected Output
```
Number 1: 5
Number 2: 2
Number 3: 8
Sorted: [2, 5, 8]
```

### Common Mistakes
- Using list methods incorrectly (append returns None, not the list)
- Forgetting to call .sort() before printing
- Starting counter at 0 when displaying (looks confusing)

---

## Problem 9: Range with Negative Step

Write a loop that prints 20 down to 1 (countdown) using range with negative step.

### Solution
```python
# For loop with negative step to count down
for i in range(20, 0, -1):
    print(i)
```

### Expected Output
```
20
19
18
...
2
1
```

### Common Mistakes
- Using range(20, 0) without the step (counts up)
- Using range(20, -1, -1) which includes 0

---

## Problem 10: Simple Nested Loop

Write nested loops to print a 2×3 grid (2 rows, 3 columns) of asterisks.

### Solution
```python
# Outer loop for rows
for row in range(2):
    # Inner loop for columns
    for col in range(3):
        print("*", end=" ")
    # New line after each row
    print()
```

### Expected Output
```
* * *
* * *
```

### Common Mistakes
- Forgetting end=" " (would print on new line each time)
- Not calling print() without arguments to create newline
- Reversing rows and columns

---

## Intermediate Problems

---

## Problem 11: Break and Continue

Write a loop from 1 to 10. Use continue to skip multiples of 3, and break when you reach 8.

### Solution
```python
# Loop from 1 to 10
for i in range(1, 11):
    # Break when reaching 8
    if i == 8:
        break
    # Skip multiples of 3
    if i % 3 == 0:
        continue
    # Print the number
    print(i)
```

### Expected Output
```
1
2
4
5
7
```

### Common Mistakes
- Using continue before break (order matters)
- Not understanding that break exits completely, continue skips one iteration

---

## Problem 12: Input Validation Loop

Write a program that asks for an age (1-120) repeatedly until valid input is given.

### Solution
```python
# Keep asking until valid input
while True:
    age = int(input("Age (1-120): "))
    if 1 <= age <= 120:
        break
    print("Invalid. Try again.")

# Display the valid age
print(f"Your age: {age}")
```

### Expected Output
```
Age (1-120): 150
Invalid. Try again.
Age (1-120): 25
Your age: 25
```

### Common Mistakes
- Not using a loop for validation
- Not checking both bounds correctly

---

## Problem 13: Min/Max Pattern

Write a loop that finds the highest number in the list [3, 7, 2, 9, 1, 5].

### Solution
```python
# Create the list
numbers = [3, 7, 2, 9, 1, 5]

# Start with first value
max_val = numbers[0]

# Check each number
for num in numbers:
    if num > max_val:
        max_val = num

# Display result
print(f"Maximum: {max_val}")
```

### Expected Output
```
Maximum: 9
```

### Common Mistakes
- Not initializing max_val correctly
- Using max() function instead of looping (though max() is fine)
- Logic error in comparison

---

## Problem 14: Nested Loop Multiplication Table

Write nested loops to print a 4×4 multiplication table.

### Solution
```python
# Outer loop for rows
for i in range(1, 5):
    # Inner loop for columns
    for j in range(1, 5):
        # Print product with formatting
        print(f"{i*j:3}", end=" ")
    # New line after each row
    print()
```

### Expected Output
```
  1   2   3   4
  2   4   6   8
  3   6   9  12
  4   8  12  16
```

### Common Mistakes
- Not formatting output correctly (numbers not aligned)
- Forgetting newline after each row

---

## Problem 15: Search Pattern

Write a program that searches for a specific name in the list ["Alice", "Bob", "Charlie", "David"]. Use a flag variable.

### Solution
```python
# Create the list
names = ["Alice", "Bob", "Charlie", "David"]

# Get search target
target = input("Find: ")

# Initialize flag
found = False

# Search through list
for name in names:
    if name == target:
        found = True
        break

# Display result
if found:
    print(f"Found {target}!")
else:
    print(f"{target} not found.")
```

### Expected Output
```
Find: Bob
Found Bob!
```

### Common Mistakes
- Not initializing the flag variable
- Not using break after finding (inefficient)
- Getting if/else logic backwards

---

## Problem 16: List Modification

Create a list [1, 2, 3, 4, 5]. Remove the number 3, append 6, sort, then print.

### Solution
```python
# Create the list
numbers = [1, 2, 3, 4, 5]

# Remove 3
numbers.remove(3)

# Append 6
numbers.append(6)

# Sort the list
numbers.sort()

# Display result
print(numbers)  # [1, 2, 4, 5, 6]
```

### Expected Output
```
[1, 2, 4, 5, 6]
```

### Common Mistakes
- Using del or pop instead of remove
- Not sorting after modifications
- Trying to print each step (only print final result)

---

## Problem 17: Average Calculation with Sentinel

Write a program that asks for test scores until -1 is entered, then calculates the average.

### Solution
```python
# Create empty list for scores
scores = []

# Get scores from user
while True:
    score = int(input("Score (-1 to stop): "))
    if score == -1:
        break
    scores.append(score)

# Calculate average if scores exist
if len(scores) > 0:
    average = sum(scores) / len(scores)
    print(f"Average: {average:.2f}")
```

### Expected Output
```
Score (-1 to stop): 85
Score (-1 to stop): 90
Score (-1 to stop): 78
Score (-1 to stop): -1
Average: 84.33
```

### Common Mistakes
- Not checking if list is empty before dividing
- Not appending scores to the list
- Not formatting the result to 2 decimal places

---

## Problem 18: Character Counting

Write a loop that counts uppercase letters in the string "Hello World".

### Solution
```python
# The text to analyze
text = "Hello World"

# Initialize counter
uppercase_count = 0

# Check each character
for char in text:
    if char.isupper():
        uppercase_count += 1

# Display result
print(f"Uppercase letters: {uppercase_count}")  # 2
```

### Expected Output
```
Uppercase letters: 2
```

### Common Mistakes
- Miscounting (H and W = 2)
- Not using .isupper() method
- Including the space in the count

---

## Problem 19: Nested Loop Pattern (Triangle)

Write nested loops to print a right triangle:
```
*
* *
* * *
* * * *
```

### Solution
```python
# Outer loop for rows
for i in range(1, 5):
    # Inner loop prints i stars
    for j in range(i):
        print("*", end=" ")
    # New line after each row
    print()
```

### Expected Output
```
*
* *
* * *
* * * *
```

### Common Mistakes
- Not using end=" " to keep stars on same line
- Inner loop logic (should print i stars, not a fixed number)
- Forgetting newline after each row

---

## Problem 20: Building a List from Input

Ask the user for 5 favorite movies. Store in a list. Print them with numbers (1, 2, 3, ...).

### Solution
```python
# Create empty list
movies = []

# Get 5 movies from user
for i in range(5):
    movie = input(f"Movie {i+1}: ")
    movies.append(movie)

# Display with numbers
for i in range(len(movies)):
    print(f"{i+1}: {movies[i]}")
```

### Expected Output
```
Movie 1: Inception
Movie 2: Avatar
Movie 3: Interstellar
Movie 4: The Matrix
Movie 5: Titanic
1: Inception
2: Avatar
3: Interstellar
4: The Matrix
5: Titanic
```

### Common Mistakes
- Not numbering output starting at 1 (users expect 1-based counting)
- Not appending to the list

---

## Advanced/Challenge Problems

---

## Problem 21: Palindrome Checker

Write a program that checks if a word is a palindrome (reads same forwards and backwards) using a loop.

### Solution
```python
# Get word from user
word = input("Word: ").lower()

# Reverse the word using a loop
reversed_word = ""
for char in word:
    reversed_word = char + reversed_word

# Check if palindrome
if word == reversed_word:
    print(f"'{word}' is a palindrome!")
else:
    print(f"'{word}' is not a palindrome.")
```

### Expected Output
```
Word: racecar
'racecar' is a palindrome!
```

### Common Mistakes
- Not converting to lowercase before comparison
- Using word[::-1] (which is fine, but the problem asks for a loop)
- Not building the reversed string correctly

---

## Problem 22: Fibonacci Sequence

Write a program that prints the first 10 Fibonacci numbers (0, 1, 1, 2, 3, 5, 8, ...).

### Solution
```python
# Initialize first two Fibonacci numbers
a, b = 0, 1

# Print first 10 Fibonacci numbers
for i in range(10):
    print(a, end=" ")
    # Update to next pair
    a, b = b, a + b
```

### Expected Output
```
0 1 1 2 3 5 8 13 21 34
```

### Common Mistakes
- Not using tuple assignment for update (a, b = b, a + b)
- Using wrong initial values
- Printing both a and b instead of just a

---

## Problem 23: Grade Analyzer

Write a program that:
- Asks for test grades until "done" is entered
- Finds highest, lowest, and average
- Counts how many passed (>= 70)

### Solution
```python
# Create list for grades
grades = []

# Get grades from user
while True:
    grade_input = input("Grade ('done' to stop): ")
    if grade_input == "done":
        break
    grades.append(int(grade_input))

# Analyze grades if any exist
if len(grades) > 0:
    print(f"Highest: {max(grades)}")
    print(f"Lowest: {min(grades)}")
    print(f"Average: {sum(grades)/len(grades):.2f}")

    # Count passing grades
    passed = 0
    for grade in grades:
        if grade >= 70:
            passed += 1
    print(f"Passed: {passed}/{len(grades)}")
```

### Expected Output
```
Grade ('done' to stop): 85
Grade ('done' to stop): 92
Grade ('done' to stop): 78
Grade ('done' to stop): 65
Grade ('done' to stop): done
Highest: 92
Lowest: 65
Average: 80.00
Passed: 3/4
```

### Common Mistakes
- Not handling empty list
- Not counting passes correctly
- Using string instead of int for grades

---

## Problem 24: Word Frequency Counter

Write a program that asks for words until "done", then counts how many times each unique word appears.

### Solution
```python
# Create list for words
words = []

# Get words from user
while True:
    word = input("Word ('done' to stop): ")
    if word == "done":
        break
    words.append(word.lower())

# Count occurrences of each unique word
unique_words = []
for word in words:
    if word not in unique_words:
        unique_words.append(word)
        count = words.count(word)
        print(f"{word}: {count}")
```

### Expected Output
```
Word ('done' to stop): hello
Word ('done' to stop): world
Word ('done' to stop): hello
Word ('done' to stop): done
hello: 2
world: 1
```

### Common Mistakes
- Counting duplicates multiple times
- Using a list instead of set for unique words
- Not converting to lowercase for consistency

---

## Problem 25: Simple Number Guessing Game

Write a game where:
- Computer picks a random number (1-50)
- User guesses repeatedly
- Program says "higher" or "lower"
- Count attempts and display when guessed correctly

### Solution
```python
# Import random module
import random

# Computer picks a random number
secret = random.randint(1, 50)

# Initialize attempt counter
attempts = 0

# Loop until correct guess
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

### Expected Output
```
Guess (1-50): 25
Too high!
Guess (1-50): 12
Too low!
Guess (1-50): 18
Too high!
Guess (1-50): 15
Correct! You got it in 4 attempts!
```

### Common Mistakes
- Not counting attempts before checking answer
- Reversing "too high" and "too low"
- Not breaking out of loop after correct guess

---
