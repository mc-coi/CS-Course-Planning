# Day 76: For Loops with range() — Counting Loops

**Learning Target:** I can write for loops using range() to iterate a specific number of times, and understand how range() generates sequences.

### Key Concepts

A **for loop** iterates over a sequence. When you want to loop a known number of times, **for loops are cleaner than while loops**.

**For Loop Structure:**
```python
for variable in sequence:
    # Loop body (indented)
    # variable takes on each value in sequence
```

**range() function:** Generates a sequence of numbers.
```python
range(stop)              # 0 to stop-1
range(start, stop)       # start to stop-1
range(start, stop, step) # start to stop-1, incrementing by step
```

**Examples:**
```python
range(5)           # 0, 1, 2, 3, 4 (5 numbers)
range(1, 6)        # 1, 2, 3, 4, 5
range(0, 10, 2)    # 0, 2, 4, 6, 8
```

**For vs While:**
- **for loop:** Use when you know exactly how many iterations (count 1-10, loop over a list)
- **while loop:** Use when condition might change unpredictably (user input, sentinel, validation)

### Code Examples

```python
# Example 1: Simple counting loop
print("Counting 1-5:")
for i in range(1, 6):
    print(i)
print()

# Example 2: Print "hello" 3 times
for count in range(3):
    print("Hello!")
print()

# Example 3: Sum numbers 1-100 (much cleaner than while!)
total = 0
for num in range(1, 101):
    total += num
print(f"Sum: {total}\n")

# Example 4: Print multiplication table
for i in range(1, 11):
    print(f"5 × {i} = {5 * i}")
print()

# Example 5: Variable loop count
n = int(input("How many times? "))
for i in range(n):
    print(f"Iteration {i+1}")
```

### Guided Practice

Write a for loop that:
1. Asks the user for a number N
2. Loops from 1 to N (using range)
3. Prints each number squared (1, 4, 9, 16, ... N²)

### Practice Problems

**Problem 1 — Beginner:** Write a for loop that prints 10, 9, 8, ..., 1 (countdown using range).

```python
# Starter code
for i in range(10, 0, -1):
    # Your code here
```

**Problem 2 — Intermediate:** Write a for loop that prints a multiplication table for a number the user enters. For example, if they enter 7, print: 7×1=7, 7×2=14, ... 7×10=70.

**Problem 3 — Challenge:** Write a program that asks the user for a starting number and ending number, then prints all numbers in that range (using range) that are divisible by 3.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `range(10, 0, -1)` to count down
- Problem 2: Get the number from user, loop `range(1, 11)`, multiply and print
- Problem 3: Use two range() calls, or one with variables. Check `num % 3 == 0`

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
for i in range(10, 0, -1):
    print(i)

# Problem 2 Example
num = int(input("What number? "))
for i in range(1, 11):
    print(f"{num}×{i}={num*i}")

# Problem 3 Example
start = int(input("Start: "))
end = int(input("End: "))
for num in range(start, end+1):
    if num % 3 == 0:
        print(num)
```

</details>

---
