# Day 71: While Loops — Syntax, Condition, and Body

**Learning Target:** I can write while loops with proper syntax, understand how conditions control iteration, and implement the counter pattern.

### Key Concepts

A **while loop** repeats a block of code while a condition is true. It's the fundamental iteration tool—when a condition is true, the loop body executes; when false, the loop stops.

**Structure:**
```python
while condition:
    # Loop body (indented)
    # Statements executed while condition is true
    # Must eventually make condition false, or loop runs forever
```

The **condition** can be:
- A comparison: `x < 10`, `name != "quit"`
- A boolean variable: `while is_valid:`
- A compound condition: `while x > 0 and y < 100:`

**Key Point:** The loop body must eventually change the condition; otherwise, the loop never stops (infinite loop). The most common way is to use a **counter**—a variable incremented or decremented to control iterations.

**Counter Pattern:**
```python
counter = 0
while counter < 5:
    print(counter)
    counter += 1  # MUST increment, or infinite loop
# Output: 0 1 2 3 4
```

Without `counter += 1`, this loop would print 0 forever. The counter changes the condition until it becomes false.

### Code Examples

```python
# Example 1: Simple counter loop
print("Counting up:")
count = 1
while count <= 5:
    print(count)
    count += 1  # Increment counter
print("Done!\n")

# Example 2: Countdown
print("Countdown:")
seconds = 5
while seconds > 0:
    print(seconds)
    seconds -= 1  # Decrement counter
print("Blastoff!\n")

# Example 3: Summing numbers with a while loop
total = 0
num = 1
while num <= 10:
    total += num
    num += 1
print(f"Sum of 1-10: {total}")  # 55

# Example 4: Input validation (preview)
age = int(input("Enter age: "))
while age < 0:
    print("Age can't be negative!")
    age = int(input("Enter age again: "))
print(f"Your age: {age}")
```

### Guided Practice

Write a while loop that:
1. Starts with a counter at 10
2. Decrements by 2 each iteration
3. Prints the counter value
4. Stops when counter is less than 1

Then trace through your loop manually: what does it print?

### Practice Problems

**Problem 1 — Beginner:** Write a while loop that prints the numbers 1 through 8 using a counter variable.

```python
# Starter code
counter = 1
while counter <= 8:
    # Your code here
```

**Problem 2 — Intermediate:** Write a while loop that asks the user for a number, then prints that number multiplied by itself (squared) up to 5 times. For example, if they enter 3, print: 3, 9, 27, 81, 243 (each is the previous × 3).

**Problem 3 — Challenge:** Write a while loop that calculates how many times you need to divide 1000 by 2 until the result is less than 1. Print each division step.

<details>
<summary>💡 Hints</summary>

- Problem 1: Start counter at 1, increment by 1, check if counter <= 8
- Problem 2: You need two variables: one for the number (from user), one for iterations (counter). Print the growing result each time.
- Problem 3: Start with 1000, divide by 2 each time, count iterations. Loop while result >= 1.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
counter = 1
while counter <= 8:
    print(counter)
    counter += 1

# Problem 2 Example
num = int(input("Enter a number: "))
result = num
times = 0
while times < 5:
    print(result)
    result *= num
    times += 1

# Problem 3 Example
value = 1000
count = 0
while value >= 1:
    print(value)
    value /= 2
    count += 1
print(f"Took {count} divisions")
```

</details>

---
