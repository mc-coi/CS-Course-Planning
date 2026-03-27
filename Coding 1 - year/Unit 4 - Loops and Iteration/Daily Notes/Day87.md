# Day 87: Looping Through Lists — For-Each Iteration

**Learning Target:** I can iterate over lists using for-each loops and process all elements systematically.

### Key Concepts

**For-each loop:** Iterates directly over list elements without needing indices or range().
```python
for item in list:
    # item takes on each value in list
```

This is much cleaner than index-based loops for most tasks.

**For-each vs index-based:**
```python
# For-each (cleaner)
for name in names:
    print(name)

# Index-based (useful when you need index)
for i in range(len(names)):
    print(f"{i}: {names[i]}")
```

**When to use for-each:**
- You just need the values (not indices)
- Simpler, more readable code

**When to use index-based:**
- You need the position (to modify list or track location)
- You need to access multiple lists in parallel

### Code Examples

```python
# Example 1: Print all elements
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
print()

# Example 2: Calculate sum using for-each
numbers = [10, 20, 30, 40, 50]
total = 0
for num in numbers:
    total += num
print(f"Sum: {total}\n")

# Example 3: Check if all elements meet a condition
scores = [85, 92, 78, 95, 88]
all_passing = True
for score in scores:
    if score < 60:
        all_passing = False
print(f"All passing: {all_passing}\n")

# Example 4: Build a new list from another
words = ["hello", "world", "python"]
upper_words = []
for word in words:
    upper_words.append(word.upper())
print(f"Original: {words}")
print(f"Uppercase: {upper_words}\n")

# Example 5: Find and count
text = "mississippi"
letter_count = 0
for char in text:
    if char == "s":
        letter_count += 1
print(f"Letter 's' appears: {letter_count} times")
```

### Guided Practice

Write a program that:
1. Creates a list of test scores
2. Uses a for-each loop to calculate the average
3. Uses a for-each loop to find the highest score
4. Uses a for-each loop to count how many passed (>= 70)

### Practice Problems

**Problem 1 — Beginner:** Create a list of 5 numbers and print each one with a label using a for-each loop.

```python
numbers = [15, 23, 42, 8, 35]
for num in numbers:
    # Your code here
```

**Problem 2 — Intermediate:** Create a list of words. Count how many words contain the letter 'a' (case-insensitive).

**Problem 3 — Challenge:** Create two lists of numbers. Use for-each loops to find the sum of each list, then print which list has the larger sum.

<details>
<summary>💡 Hints</summary>

- Problem 1: Print with an f-string: `f"{num}: {num*2}"`
- Problem 2: Use `'a' in word.lower()` to check
- Problem 3: Use two separate for-each loops (or one loop through pairs with zip())

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
numbers = [15, 23, 42, 8, 35]
for num in numbers:
    print(f"Value: {num}")

# Problem 2 Example
words = ["apple", "banana", "cherry", "date", "fig"]
count = 0
for word in words:
    if 'a' in word.lower():
        count += 1
print(f"Words with 'a': {count}")

# Problem 3 Example
list1 = [10, 20, 30]
list2 = [15, 15, 25]

sum1 = 0
for num in list1:
    sum1 += num

sum2 = 0
for num in list2:
    sum2 += num

if sum1 > sum2:
    print(f"List 1 is larger ({sum1} > {sum2})")
else:
    print(f"List 2 is larger ({sum2} > {sum1})")
```

</details>

---
