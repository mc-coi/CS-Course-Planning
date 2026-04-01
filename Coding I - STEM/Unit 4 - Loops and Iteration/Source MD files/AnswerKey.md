# Unit 4: Loops and Iteration - Answer Key

---

## Problem 1: While Loop (1-10)

### Solution
```python
# Print 1-10 using a while loop
i = 1
while i <= 10:
    print(i)
    i += 1
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
- Forgetting to increment i (creates infinite loop)
- Using i < 10 instead of i <= 10 (stops at 9)
- Using i = 1 instead of i += 1 (resets to 1 each iteration)
- Not initializing i before the loop

---

## Problem 2: For Loop with Range

### Solution
```python
# For loop with range(5, 16)
for i in range(5, 16):
    print(i)
```

### Expected Output
```
5
6
7
8
9
10
11
12
13
14
15
```

### Common Mistakes
- Thinking range(5, 16) includes 16 (it stops before the end value)
- Using range(5, 15) instead (missing 15)
- Swapping the start and end
- Not understanding range parameters

---

## Problem 3: Reverse Range

### Solution
```python
# What does range(10, 0, -1) produce?
result = list(range(10, 0, -1))
print("range(10, 0, -1) produces:")
for i in range(10, 0, -1):
    print(i)

# Explanation
print("\nExplanation:")
print("range(start, stop, step)")
print("range(10, 0, -1) means: start at 10, go down to (but not including) 0, step by -1")
```

### Expected Output
```
range(10, 0, -1) produces:
10
9
8
7
6
5
4
3
2
1

Explanation:
range(start, stop, step)
range(10, 0, -1) means: start at 10, go down to (but not including) 0, step by -1
```

### Common Mistakes
- Thinking it includes 0 (it stops before reaching 0)
- Not understanding negative step means reverse
- Confusing the start and stop values

---

## Problem 4: Score Input with Sentinel

### Solution
```python
# Ask for scores until -1, then print total and average
scores = []
while True:
    score = float(input("Enter score (or -1 to quit): "))
    if score == -1:
        break
    scores.append(score)

# Calculate total and average
if scores:
    total = sum(scores)
    average = total / len(scores)
    print(f"\nTotal scores entered: {len(scores)}")
    print(f"Total: {total}")
    print(f"Average: {average:.2f}")
else:
    print("No scores entered.")
```

### Expected Output
```
Enter score (or -1 to quit): 85
Enter score (or -1 to quit): 90
Enter score (or -1 to quit): 78
Enter score (or -1 to quit): -1

Total scores entered: 3
Total: 253
Average: 84.33
```

### Common Mistakes
- Not using a sentinel value (-1)
- Forgetting to break the loop
- Not storing scores in a list
- Including -1 in the calculation
- Not checking for empty list before dividing

---

## Problem 5: Multiplication Table

### Solution
```python
# Print multiplication table for a number
number = int(input("Enter a number (1-12): "))

print(f"\nMultiplication table for {number}:")
for i in range(1, 11):
    product = number * i
    print(f"{number} × {i} = {product}")
```

### Expected Output
```
Enter a number (1-12): 5

Multiplication table for 5:
5 × 1 = 5
5 × 2 = 10
5 × 3 = 15
5 × 4 = 20
5 × 5 = 25
5 × 6 = 30
5 × 7 = 35
5 × 8 = 40
5 × 9 = 45
5 × 10 = 50
```

### Common Mistakes
- Using range(0, 11) instead of range(1, 11) (starts at 0)
- Using range(1, 10) instead (stops at 9)
- Not formatting output clearly
- Computing wrong product

---

## Problem 6: Count Vowels

### Solution
```python
# Count vowels in a word
word = input("Enter a word: ").lower()
vowels = "aeiou"
count = 0

for letter in word:
    if letter in vowels:
        count += 1

print(f"The word '{word}' has {count} vowels.")

# Alternative - more elegant:
vowel_count = sum(1 for letter in word if letter in vowels)
print(f"Alternative method: {vowel_count} vowels")
```

### Expected Output
```
Enter a word: hello
The word 'hello' has 2 vowels.
Alternative method: 2 vowels
```

### Common Mistakes
- Not converting to lowercase (missing uppercase vowels)
- Using a list instead of a string for vowels
- Forgetting to increment count
- Not using `.lower()` to handle case sensitivity

---

## Problem 7: Calculate Factorial (10!)

### Solution
```python
# Calculate 10! (factorial = 10 × 9 × 8 × ... × 1)
product = 1
for i in range(1, 11):
    product *= i

print(f"10! = {product}")

# Alternative using built-in:
import math
print(f"10! = {math.factorial(10)}")

# Show calculation
print("\nStep by step:")
result = 1
for i in range(1, 11):
    result *= i
    print(f"{i}! = {result}")
```

### Expected Output
```
10! = 3628800
10! = 3628800

Step by step:
1! = 1
2! = 2
3! = 6
4! = 24
5! = 120
6! = 720
7! = 5040
8! = 40320
9! = 362880
10! = 3628800
```

### Common Mistakes
- Starting product at 0 instead of 1 (results in 0)
- Using wrong range (0 to 10 instead of 1 to 10)
- Dividing instead of multiplying
- Off-by-one errors

---

## Problem 8: FizzBuzz

### Solution
```python
# FizzBuzz: print numbers 1-100, but:
# - For multiples of 3: print "Fizz"
# - For multiples of 5: print "Buzz"
# - For multiples of both 3 and 5: print "FizzBuzz"

for i in range(1, 101):
    if i % 3 == 0 and i % 5 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

### Expected Output
```
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
16
...
98
Fizz
Buzz
```

### Common Mistakes
- Checking "and" condition last (must check both 3 and 5 together first)
- Using "or" instead of "and" for the combined condition
- Using wrong modulo checks
- Printing the number when it's a multiple (should print Fizz/Buzz only)

---

## Problem 9: Triangle Pattern

### Solution
```python
# Print triangle: 1, 22, 333, 4444, etc.
for i in range(1, 6):
    # Repeat digit i, i times
    line = str(i) * i
    print(line)
```

### Expected Output
```
1
22
333
4444
55555
```

### Common Mistakes
- Using the wrong range (0-5 instead of 1-6)
- Not repeating the digit the correct number of times
- Using loops instead of string repetition
- Off-by-one errors in the pattern

---

## Problem 10: First Number > 100 Divisible by 7

### Solution
```python
# Find first number > 100 that is divisible by 7
num = 101
while num % 7 != 0:
    num += 1

print(f"First number > 100 divisible by 7: {num}")

# Alternative: start at a better position
num = 105  # First multiple of 7 after 100
print(f"First number > 100 divisible by 7: {num}")

# Show verification
print(f"Verification: {num} % 7 = {num % 7}")
print(f"Verification: {num} / 7 = {num / 7}")
```

### Expected Output
```
First number > 100 divisible by 7: 105
First number > 100 divisible by 7: 105
Verification: 105 % 7 = 0
Verification: 105 / 7 = 15.0
```

### Common Mistakes
- Starting at 100 instead of 101
- Using wrong condition (% 7 == 0 vs % 7 != 0)
- Creating infinite loop with wrong increment
- Not verifying the result

---

## Problem 11: Find Min/Max/Average from List

### Solution
```python
# Ask for list of numbers, find min/max/average
numbers = []
print("Enter numbers (enter 'done' when finished):")

while True:
    user_input = input("Enter a number: ")
    if user_input.lower() == "done":
        break
    try:
        num = float(user_input)
        numbers.append(num)
    except ValueError:
        print("Invalid input, please enter a number")

if numbers:
    print(f"\nResults:")
    print(f"Count: {len(numbers)}")
    print(f"Min: {min(numbers)}")
    print(f"Max: {max(numbers)}")
    print(f"Average: {sum(numbers) / len(numbers):.2f}")
else:
    print("No numbers entered")
```

### Expected Output
```
Enter numbers (enter 'done' when finished):
Enter a number: 10
Enter a number: 25
Enter a number: 15
Enter a number: 30
Enter a number: done

Results:
Count: 4
Min: 10.0
Max: 30.0
Average: 20.00
```

### Common Mistakes
- Not storing numbers in a list
- Not checking for empty list before using min/max
- Wrong calculation of average
- Not handling invalid input

---

## Problem 12: Reverse String Without Slicing

### Solution
```python
# Build reversed string without using slicing
text = input("Enter text: ")
reversed_text = ""

for i in range(len(text) - 1, -1, -1):
    reversed_text += text[i]

print(f"Original: {text}")
print(f"Reversed: {reversed_text}")

# Alternative using loop
print("\nAlternative approach:")
reversed_alt = ""
for char in text:
    reversed_alt = char + reversed_alt
print(f"Reversed: {reversed_alt}")
```

### Expected Output
```
Enter text: Hello
Original: Hello
Reversed: olleH

Alternative approach:
Reversed: olleH
```

### Common Mistakes
- Using slicing (that's not allowed for this problem)
- Using wrong range (0 to len instead of len-1 to 0 with step -1)
- Appending to wrong side (char + reversed_alt builds correctly)
- Off-by-one errors in the range

---

## Problem 13: Palindrome Check

### Solution
```python
# Check if word is a palindrome
word = input("Enter a word: ").lower()

# Method 1: Compare with reversed
reversed_word = word[::-1]
if word == reversed_word:
    print(f"'{word}' is a palindrome")
else:
    print(f"'{word}' is not a palindrome")

# Method 2: Check character by character
print("\nMethod 2 - Character by character:")
is_palindrome = True
for i in range(len(word) // 2):
    if word[i] != word[-(i + 1)]:
        is_palindrome = False
        break

if is_palindrome:
    print(f"'{word}' is a palindrome")
else:
    print(f"'{word}' is not a palindrome")
```

### Expected Output
```
Enter a word: racecar
'racecar' is a palindrome

Method 2 - Character by character:
'racecar' is a palindrome
```

### Common Mistakes
- Not converting to lowercase (case-sensitive comparison)
- Using wrong comparison (word != reversed_word)
- Off-by-one errors in character-by-character check
- Not handling spaces/punctuation

---

## Problem 14: Count Each Vowel

### Solution
```python
# Count each vowel separately in a sentence
sentence = input("Enter a sentence: ").lower()
vowels = "aeiou"

# Count each vowel
vowel_counts = {}
for vowel in vowels:
    count = sentence.count(vowel)
    vowel_counts[vowel] = count

# Print results
print(f"\nVowel counts in '{sentence}':")
for vowel in vowels:
    print(f"'{vowel}': {vowel_counts[vowel]}")

# Total vowels
total_vowels = sum(vowel_counts.values())
print(f"Total vowels: {total_vowels}")
```

### Expected Output
```
Enter a sentence: Hello World
Vowel counts in 'hello world':
'a': 0
'e': 1
'i': 0
'o': 2
'u': 0
Total vowels: 3
```

### Common Mistakes
- Not using lowercase conversion
- Not initializing count properly
- Not iterating through each vowel
- Counting consonants instead of vowels

---

## Problem 15: Guessing Game with Hints

### Solution
```python
import random

# Pick random number 1-100
secret = random.randint(1, 100)
guesses = 0
guessed = False

print("Welcome to the Guessing Game!")
print("I'm thinking of a number between 1 and 100.")

while not guessed:
    try:
        guess = int(input("Enter your guess: "))
        guesses += 1

        if guess == secret:
            print(f"Correct! You got it in {guesses} guesses!")
            guessed = True
        elif guess < secret:
            print("Too low, guess higher")
        else:
            print("Too high, guess lower")
    except ValueError:
        print("Invalid input, please enter a number")

# Provide feedback
print("\nGame Over!")
if guesses <= 7:
    print("Excellent! You're a great guesser!")
elif guesses <= 15:
    print("Good job!")
else:
    print("Keep practicing!")
```

### Expected Output
```
Welcome to the Guessing Game!
I'm thinking of a number between 1 and 100.
Enter your guess: 50
Too high, guess lower
Enter your guess: 25
Too low, guess higher
Enter your guess: 37
Too low, guess higher
Enter your guess: 43
Correct! You got it in 4 guesses!

Game Over!
Excellent! You're a great guesser!
```

### Common Mistakes
- Not picking a secret number
- Not checking for too high/too low correctly
- Creating infinite loop without proper exit
- Not counting guesses
- Not handling invalid input

---
