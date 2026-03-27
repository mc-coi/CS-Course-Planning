# Day 81: Break and Continue — Loop Control Statements

**Learning Target:** I can use break and continue to control loop execution and alter loop flow.

### Key Concepts

**break:** Immediately exits the loop, stopping all remaining iterations.
```python
for i in range(10):
    if i == 5:
        break  # Stop the loop
    print(i)  # 0, 1, 2, 3, 4
```

**continue:** Skips the current iteration and jumps to the next one.
```python
for i in range(5):
    if i == 2:
        continue  # Skip when i is 2
    print(i)  # 0, 1, 3, 4
```

**When to use break:**
- Stop searching when you found what you're looking for
- Exit a sentinel loop
- Exit early if a condition is met

**When to use continue:**
- Skip invalid or unwanted items
- Skip processing for certain values
- Filter within a loop

**Important:** Both work in for and while loops. Both skip any code after them in the current iteration.

### Code Examples

```python
# Example 1: break — search for a number
numbers = [3, 1, 7, 4, 2, 9, 5]
target = 7
found = False
for num in numbers:
    if num == target:
        print(f"Found {target}!")
        found = True
        break  # Stop searching
if not found:
    print("Not found.")
print()

# Example 2: continue — skip negative numbers
values = [5, -2, 8, -1, 3, -4, 6]
total = 0
for val in values:
    if val < 0:
        continue  # Skip negative, go to next
    total += val
print(f"Sum of positive: {total}\n")

# Example 3: continue in input validation
count = 0
while count < 5:
    value = int(input("Enter a positive number: "))
    if value <= 0:
        print("Negative or zero! Try again.")
        continue  # Skip incrementing count
    count += 1
    print(f"Got {value}")
print()

# Example 4: break with while loop
while True:
    command = input("Enter command (quit to exit): ")
    if command == "quit":
        break  # Stop the loop
    print(f"You said: {command}")
```

### Guided Practice

Write a program that:
1. Asks the user for 10 numbers
2. Uses continue to skip negative numbers
3. Uses break if they enter 999 (stop early)
4. Prints the average of numbers entered

Trace through your code manually to verify break and continue work correctly.

### Practice Problems

**Problem 1 — Beginner:** Write a loop that prints 1-20, but continues (skips) when the number is even.

```python
for i in range(1, 21):
    if i % 2 == 0:
        continue
    # Your code here
```

**Problem 2 — Intermediate:** Write a program that asks for names until the user types "quit", then breaks. Count how many names were entered (not counting "quit").

**Problem 3 — Challenge:** Write a program that finds the first number in a list divisible by both 3 and 5. Use break when found. Use continue to skip numbers that don't meet criteria.

<details>
<summary>💡 Hints</summary>

- Problem 1: Just print i when you don't continue. This prints only odd numbers.
- Problem 2: Increment count before or after checking for "quit", but use continue to skip the break.
- Problem 3: Use `if num % 3 == 0 and num % 5 == 0:` to find the number. Use break when found.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
for i in range(1, 21):
    if i % 2 == 0:
        continue
    print(i)

# Problem 2 Example
count = 0
while True:
    name = input("Name (quit to exit): ")
    if name == "quit":
        break
    count += 1
print(f"You entered {count} names")

# Problem 3 Example
numbers = [2, 5, 9, 15, 20, 45, 30, 8]
for num in numbers:
    if num % 3 != 0 or num % 5 != 0:
        continue  # Skip if doesn't meet both criteria
    print(f"Found: {num}")
    break
```

</details>

---
