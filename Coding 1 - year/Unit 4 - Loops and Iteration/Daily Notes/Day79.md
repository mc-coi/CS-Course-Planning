# Day 79: For vs While — Choosing the Right Loop

**Learning Target:** I can decide whether to use a for loop or while loop based on the problem requirements.

### Key Concepts

**When to use a for loop:**
- You know exactly how many iterations (count 1–10, loop through 5 items)
- You're iterating over a sequence (list, string, range)
- Clean, predictable iteration

**When to use a while loop:**
- You don't know when the loop should stop (user input, changing condition)
- You need a sentinel loop (special value to exit)
- You need to validate input repeatedly
- Condition is complex and might change unpredictably

**Comparison:**

| Aspect | For Loop | While Loop |
|--------|----------|-----------|
| **Iterations known?** | Yes | No |
| **Over a sequence?** | Usually yes | Not necessarily |
| **Typical use** | Counting, iterating lists | User input, sentinels, validation |
| **Syntax** | `for var in seq:` | `while condition:` |
| **Example** | `for i in range(5)` | `while user_input != "quit"` |

**Key Insight:** Anything you can do with a for loop, you can do with a while loop (but it's less elegant). But some problems are naturally suited to while loops, and forcing a for loop would be awkward.

### Code Examples

```python
# Example 1: Print 1-10
print("FOR LOOP:")
for i in range(1, 11):
    print(i)

print("\nWHILE LOOP:")
i = 1
while i <= 10:
    print(i)
    i += 1
print()

# Example 2: Sum a list
numbers = [5, 2, 8, 1, 9]
total = 0

print("FOR LOOP:")
for num in numbers:
    total += num
print(f"Sum: {total}")

total = 0
i = 0
print("WHILE LOOP:")
while i < len(numbers):
    total += numbers[i]
    i += 1
print(f"Sum: {total}\n")

# Example 3: Get valid input (while loop is better)
# For loop doesn't work well here—you don't know how many times to ask
while True:
    age = int(input("Age (1-120): "))
    if 1 <= age <= 120:
        break
    print("Invalid. Try again.")
print(f"Your age: {age}\n")

# Example 4: Print a pattern (for loop is cleaner)
size = 4
for i in range(1, size+1):
    for j in range(i):
        print("*", end="")
    print()  # Newline
```

### Guided Practice

For each scenario, decide: for loop or while loop? Then write the code.

1. Print the squares of numbers 1-20 (1, 4, 9, 16, ..., 400)
2. Ask the user for a number repeatedly until they enter a negative number
3. Loop through the string "HELLO" and print each character
4. Ask the user for words until they type "DONE", then print the count

### Practice Problems

**Problem 1 — Beginner:** Rewrite this while loop as a for loop:
```python
i = 0
while i < 7:
    print(i * 2)
    i += 1
```

**Problem 2 — Intermediate:** Rewrite this for loop as a while loop:
```python
total = 0
for num in [10, 20, 30, 40]:
    total += num
print(total)
```

**Problem 3 — Challenge:** Write a program that:
- Asks the user for their name (validate: not empty) — use while loop
- Asks how many favorite numbers they have — use input validation
- Asks for that many numbers (using a for loop)
- Prints them all

Identify which loop type is best for each part.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `for i in range(0, 7):` or `range(7)`
- Problem 2: Create a list `[10, 20, 30, 40]`, use `while` with counter and indexing
- Problem 3: While for validation, for for the fixed count

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example (while to for)
for i in range(7):
    print(i * 2)

# Problem 2 Example (for to while)
total = 0
numbers = [10, 20, 30, 40]
i = 0
while i < len(numbers):
    total += numbers[i]
    i += 1
print(total)

# Problem 3 Example
while True:
    name = input("Your name: ")
    if len(name) > 0:
        break
    print("Name cannot be empty.")

while True:
    count = int(input("How many favorite numbers? "))
    if count > 0:
        break
    print("Must be at least 1.")

numbers = []
for i in range(count):
    num = int(input(f"Number {i+1}: "))
    numbers.append(num)

print(f"Your numbers: {numbers}")
```

</details>

---
