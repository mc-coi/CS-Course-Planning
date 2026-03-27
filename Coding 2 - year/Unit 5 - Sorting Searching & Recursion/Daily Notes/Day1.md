# Day 1: Recursion Fundamentals Review

**Learning Target:** I can explain the call stack and identify the base case and recursive case in a recursive function.

---

## Key Concepts

**Recursion**: A function that calls itself to solve smaller versions of the same problem.

**Base Case**: The condition that stops the recursion. Without it, the function calls itself infinitely.

**Recursive Case**: The part where the function calls itself with a simpler or smaller input.

**Call Stack**: The memory structure that tracks function calls. Each call waits for the inner call to complete.

### Recursion Structure
```
function(n):
  if n is small enough (BASE CASE):
    return answer
  else:
    return something + function(n-1)  (RECURSIVE CASE)
```

### Call Stack Visualization
When we call `factorial(4)`:
```
factorial(4) calls factorial(3) calls factorial(2) calls factorial(1) → returns 1
    ↓              ↓               ↓                 ↑
  waiting        waiting         waiting         (unwinds)
  4 * 6 = 24    3 * 2 = 6       2 * 1 = 2       base case reached
```

---

## Code Examples

```python
# Factorial using recursion
def factorial(n):
    # Base case: when to stop recursing
    if n == 1:
        return 1
    # Recursive case: break the problem into smaller pieces
    else:
        return n * factorial(n - 1)

print(factorial(5))  # Output: 120

# Fibonacci using recursion
def fibonacci(n):
    # Base cases
    if n <= 1:
        return n
    # Recursive case: sum the previous two fibonacci numbers
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(6))  # Output: 8
```

---

## Guided Practice

**Step 1:** Trace `factorial(3)` on paper. Write down each call to the function and when it returns.

**Step 2:** For each return statement, write what value is actually returned (e.g., when `factorial(1)` returns, it returns 1).

**Step 3:** Work backwards from the base case to find the final answer (3 * 2 * 1 = 6).

**Step 4:** Now trace `fibonacci(4)`. Notice how the same call might happen multiple times (inefficiency!).

**Step 5:** In your own words, explain why we MUST have a base case.

---

## Practice Problems

**Beginner:** Write a recursive function that counts down from n to 1 and prints each number. What is the base case? What is the recursive case?

**Intermediate:** Write a recursive function that sums all integers from 1 to n. For example, `sum_to(5)` should return 1+2+3+4+5 = 15. Trace through `sum_to(3)`.

**Challenge:** The function below has a bug. Identify the base case issue and explain what happens if we call `mystery(5)`:
```python
def mystery(n):
    if n > 10:
        return 1
    else:
        return n + mystery(n + 1)
```

<details>
<summary>💡 Hints</summary>
- **Beginner:** Your base case should check if n == 1 (or n == 0). Your recursive case should print n and call the function with n-1.
- **Intermediate:** The pattern is similar to countdown, but instead of printing, you're adding to a total. Think: sum_to(n) = n + sum_to(n-1).
- **Challenge:** Does the condition `n > 10` ever become true if we start with n=5 and keep adding 1?
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def countdown(n):
    if n == 1:  # BASE CASE
        print(n)
    else:  # RECURSIVE CASE
        print(n)
        countdown(n - 1)

# Intermediate
def sum_to(n):
    if n == 1:  # BASE CASE
        return 1
    else:  # RECURSIVE CASE
        return n + sum_to(n - 1)

# sum_to(3):
#   = 3 + sum_to(2)
#   = 3 + (2 + sum_to(1))
#   = 3 + (2 + 1)
#   = 6

# Challenge
# The bug: base case checks if n > 10, but we're calling mystery(5) and ADDING 1 each time.
# So n goes 5, 6, 7, 8, 9, 10, 11... and finally becomes > 10.
# This will work, but it's confusing logic. Better base case: if n > 10: return 1
# or if n == 11: return 1. The issue is that the logic is backwards — we should be
# decrementing n, not incrementing it.
```
</details>
