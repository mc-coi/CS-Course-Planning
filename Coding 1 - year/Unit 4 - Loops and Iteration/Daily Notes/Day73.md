# Day 73: The Accumulator Pattern — Running Totals and Counting

**Learning Target:** I can use the accumulator pattern to calculate sums, products, counts, and other aggregate values.

### Key Concepts

The **accumulator pattern** uses a variable that collects or combines values as a loop iterates. It's one of the most powerful and common loop patterns in programming.

**Basic Structure:**
```python
accumulator = initial_value  # Start with empty, 0, 1, etc.
while condition:
    # Get or calculate new value
    accumulator = accumulator operator value  # Combine
# accumulator now holds the result
```

**Common accumulators:**
- **Sum:** Start with 0, use `+=` (addition)
- **Product:** Start with 1, use `*=` (multiplication)
- **Count:** Start with 0, use `+= 1` (increment)
- **String concatenation:** Start with `""`, use `+=` (combine strings)
- **Average:** Accumulate sum and count, divide at the end

**Why it works:** The accumulator retains its value after each iteration, growing with each new value.

### Code Examples

```python
# Example 1: Sum of numbers
print("Sum example:")
total = 0  # Accumulator starts empty
count = 0
while count < 5:
    num = int(input("Enter number: "))
    total += num  # Add to accumulator
    count += 1
print(f"Sum: {total}\n")

# Example 2: Product (factorial-like)
print("Product example:")
product = 1  # For multiplication, start with 1
num = int(input("Enter a number: "))
factor = 1
while factor <= num:
    product *= factor  # Multiply accumulator
    factor += 1
print(f"Factorial of {num}: {product}\n")

# Example 3: Counting occurrences
password = input("Enter a password: ")
vowel_count = 0  # Accumulator for counting
for char in password:
    if char.lower() in "aeiou":
        vowel_count += 1  # Increment accumulator
print(f"Vowels found: {vowel_count}\n")

# Example 4: Building a string
result = ""  # Accumulator for strings
for i in range(1, 6):
    result += f"{i}, "  # Append to accumulator
print(f"Result: {result}\n")

# Example 5: Average (accumulator with count)
total = 0
count = 0
while True:
    score = int(input("Enter score (-1 to stop): "))
    if score == -1:
        break
    total += score
    count += 1
if count > 0:
    average = total / count
    print(f"Average: {average:.2f}")
```

### Guided Practice

Write a program that:
1. Asks the user for numbers until they enter 0
2. Calculates the sum and count of numbers entered
3. Prints both the sum and the average

Trace your accumulators as they grow.

### Practice Problems

**Problem 1 — Beginner:** Write a loop that calculates the sum of all numbers from 1 to 100. Print the result.

```python
# Starter code
total = 0
for num in range(1, 101):
    # Your code here
print(total)
```

**Problem 2 — Intermediate:** Write a program that asks the user for words repeatedly until they enter "done". Count how many words were entered and print the count and the combined string of all words.

**Problem 3 — Challenge:** Write a program that asks the user for test scores until they enter -1. Calculate and print:
- Sum of all scores
- Count of scores
- Average
- Highest score (use accumulator pattern with an if statement)
- Lowest score (use accumulator pattern with an if statement)

<details>
<summary>💡 Hints</summary>

- Problem 1: Initialize total to 0, loop 1 to 100, add each num to total
- Problem 2: Count words (accumulator), concatenate words into a string (accumulator)
- Problem 3: For min/max, initialize max to first score (or very small number), check if new score is larger/smaller each iteration

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
total = 0
for num in range(1, 101):
    total += num
print(total)  # 5050

# Problem 2 Example
count = 0
words_combined = ""
while True:
    word = input("Enter word ('done' to stop): ")
    if word == "done":
        break
    count += 1
    words_combined += word + " "
print(f"Count: {count}")
print(f"Combined: {words_combined}")

# Problem 3 Example
total = 0
count = 0
highest = -1
lowest = 999
while True:
    score = int(input("Score (-1 to stop): "))
    if score == -1:
        break
    total += score
    count += 1
    if score > highest:
        highest = score
    if score < lowest:
        lowest = score

if count > 0:
    print(f"Sum: {total}")
    print(f"Count: {count}")
    print(f"Average: {total / count:.2f}")
    print(f"Highest: {highest}")
    print(f"Lowest: {lowest}")
```

</details>

---
