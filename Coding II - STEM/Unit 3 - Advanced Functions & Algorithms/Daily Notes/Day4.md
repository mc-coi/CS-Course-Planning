# Day 4: Recursion Introduction
**Learning Target:** I can understand recursion and write simple recursive functions.

### Key Concepts
**Recursion:** A function calling itself to solve a problem.

**Base case:** When to stop (prevents infinite loops)
**Recursive case:** Function calls itself with simpler input

### Code Examples
```python
# Factorial: 5! = 5 * 4 * 3 * 2 * 1
def factorial(n):
    if n == 0 or n == 1:  # Base case
        return 1
    else:  # Recursive case
        return n * factorial(n - 1)

print(factorial(5))  # 120

# Countdown
def countdown(n):
    if n == 0:
        print("Blastoff!")
    else:
        print(n)
        countdown(n - 1)

countdown(3)  # Prints: 3, 2, 1, Blastoff!

# Sum of numbers
def sum_list(numbers):
    if len(numbers) == 0:  # Base case
        return 0
    else:  # Recursive case
        return numbers[0] + sum_list(numbers[1:])

print(sum_list([1, 2, 3, 4]))  # 10
```

### Guided Practice
Write recursive functions for: sum of digits, power, search in list.

### Practice Problems
**Problem 1 — Beginner:** Write a recursive function that calculates 2^n.

**Problem 2 — Intermediate:** Write a recursive function to find the maximum value in a list.

**Problem 3 — Challenge:** Write a recursive function to count occurrences of a value in a nested list.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
def power(base, exp):
    if exp == 0:
        return 1
    return base * power(base, exp - 1)

# Problem 2
def max_list(lst):
    if len(lst) == 1:
        return lst[0]
    return max(lst[0], max_list(lst[1:]))

# Problem 3
def count_recursive(lst, target):
    if not lst:
        return 0
    count = 0
    if isinstance(lst[0], list):
        count += count_recursive(lst[0], target)
    elif lst[0] == target:
        count += 1
    return count + count_recursive(lst[1:], target)
```
</details>

---

---
