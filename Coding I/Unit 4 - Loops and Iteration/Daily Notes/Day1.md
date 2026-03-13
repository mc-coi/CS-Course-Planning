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