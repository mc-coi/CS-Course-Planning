# Day 77: range(start, stop, step) — Flexible Counting

**Learning Target:** I can use all three parameters of range() to create flexible counting patterns (start, stop, step).

### Key Concepts

**range() with all three parameters:**
```python
range(start, stop, step)
```

- **start:** Where to begin (default 0)
- **stop:** Where to stop (exclusive—doesn't include this number)
- **step:** Increment/decrement each iteration (default 1, can be negative)

**Key Point:** The stop value is NOT included. `range(1, 5)` gives 1, 2, 3, 4 (not 5).

**Examples:**
```python
range(2, 8)           # 2, 3, 4, 5, 6, 7 (step defaults to 1)
range(0, 10, 2)       # 0, 2, 4, 6, 8 (every other number)
range(20, 0, -2)      # 20, 18, 16, 14, ..., 2 (count down by 2)
range(100, 0, -10)    # 100, 90, 80, ..., 10 (count down by 10)
range(5, 25, 5)       # 5, 10, 15, 20 (by 5s)
```

**Why step matters:**
- Positive step: counts up
- Negative step: counts down (start must be larger than stop)
- Step > 1: skip values

### Code Examples

```python
# Example 1: Count by 2s
print("Even numbers 0-10:")
for i in range(0, 11, 2):
    print(i)
print()

# Example 2: Countdown by 5s
print("Countdown by 5s:")
for i in range(50, 0, -5):
    print(i)
print()

# Example 3: Odd numbers
print("Odd numbers 1-20:")
for i in range(1, 21, 2):
    print(i)
print()

# Example 4: Powers of 2
print("Powers of 2:")
for exp in range(0, 10):
    print(f"2^{exp} = {2**exp}")
print()

# Example 5: Skip pattern
print("Every 3rd number from 10-50:")
for i in range(10, 51, 3):
    print(i)
```

### Guided Practice

Write a program that:
1. Asks the user for a starting number
2. Asks for an ending number
3. Asks for a step value
4. Prints all numbers in that range with that step (using range)

Test with: start=10, end=50, step=5 (should print 10, 15, 20, ..., 45, 50)

### Practice Problems

**Problem 1 — Beginner:** Write a for loop that prints all numbers from 1 to 50 by 5s (1, 6, 11, 16, ...).

```python
# Starter code
for i in range(1, 51, 5):
    # Your code here
```

**Problem 2 — Intermediate:** Write a program that asks the user for a number, then prints all multiples of that number up to 100. For example, if they enter 7, print: 7, 14, 21, 28, ..., 98.

**Problem 3 — Challenge:** Write a program that prints a "countdown" pattern:
- First iteration: 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
- Second iteration: 9, 8, 7, 6, 5, 4, 3, 2, 1
- ... continuing until just 1

(Use nested loops: outer loop for iterations, inner loop with decreasing range.)

<details>
<summary>💡 Hints</summary>

- Problem 1: `range(1, 51, 5)` starts at 1, goes to 51 (exclusive), steps by 5
- Problem 2: `range(num, 101, num)` for the number and multiples. Or use a counter: `num * i for i in range(1, ...)`
- Problem 3: Outer loop `range(10, 0, -1)` for how many iterations; inner loop `range(i, 0, -1)` counting down from i

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
for i in range(1, 51, 5):
    print(i)

# Problem 2 Example
num = int(input("Number: "))
for multiple in range(num, 101, num):
    print(multiple)

# Problem 3 Example
for i in range(10, 0, -1):
    for j in range(i, 0, -1):
        print(j, end=" ")
    print()  # Newline after each row
```

</details>

---
