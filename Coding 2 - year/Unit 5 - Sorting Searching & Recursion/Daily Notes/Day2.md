# Day 2: Call Stack & Recursive Patterns

**Learning Target:** I can trace a recursive function through the call stack and identify common recursion patterns.

---

## Key Concepts

**Call Stack Unwinding**: Recursive calls pile up on the stack until the base case is reached, then each level "unwinds" and returns a value back up the stack.

**Stack Overflow**: When recursion goes too deep, the call stack runs out of space. Each function call takes up memory.

**Tail Recursion**: When the recursive call is the last thing the function does. Some languages optimize this.

**Linear vs. Tree Recursion**:
- **Linear recursion** makes one recursive call (like factorial or countdown)
- **Tree recursion** makes multiple recursive calls (like Fibonacci; less efficient)

---

## Code Examples

```python
# Example 1: Linear Recursion (one recursive call)
def linear_example(n):
    if n == 0:
        print("Base case reached")
        return
    else:
        print(f"Going down: n = {n}")
        linear_example(n - 1)
        print(f"Coming back up: n = {n}")

# Example 2: Tree Recursion (multiple recursive calls) — SLOW!
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)  # TWO recursive calls!

# Example 3: Tail Recursion (recursive call is the last line)
def tail_recursive_sum(n, accumulator=0):
    if n == 0:
        return accumulator
    else:
        return tail_recursive_sum(n - 1, accumulator + n)

print(tail_recursive_sum(5))  # Output: 15

# Example 4: String reversal using recursion
def reverse_string(s):
    if len(s) == 0:
        return ""
    else:
        return reverse_string(s[1:]) + s[0]

print(reverse_string("hello"))  # Output: "olleh"
```

---

## Guided Practice

**Activity: Trace Linear Recursion**

Run this code and trace what happens:
```python
def trace_me(n):
    if n == 0:
        print("At base case")
        return
    print(f"Before call: n = {n}")
    trace_me(n - 1)
    print(f"After call: n = {n}")

trace_me(3)
```

1. What prints first? Last?
2. Write down the order of the function calls (going down the stack).
3. Write down the order of the returns (unwinding the stack).
4. Why does "After call: n = 3" print AFTER "After call: n = 2"?

**Challenge:** Modify the code to trace a tree recursion (like Fibonacci). How many times does the function get called?

---

## Practice Problems

**Beginner:** Write a recursive function that multiplies two numbers using only addition. For example, `multiply(4, 3)` should return 12 by computing 4 + 4 + 4. What is the base case?

**Intermediate:** Write a recursive function that finds the maximum value in a list. Hint: Compare the first element with the max of the rest of the list.

**Challenge:** Explain why this function is inefficient and rewrite it to be faster:
```python
def bad_fibonacci(n):
    if n <= 1:
        return n
    return bad_fibonacci(n-1) + bad_fibonacci(n-2)
```

<details>
<summary>💡 Hints</summary>
- **Beginner:** Base case: `if n == 0, return 0`. Recursive case: `return m + multiply(m, n-1)`.
- **Intermediate:** Base case: list with one element. Recursive case: compare first element with max of the rest using `max()` or manual comparison.
- **Challenge:** Fibonacci recalculates the same values many times. Use **memoization** (storing results) or dynamic programming to avoid redundant calls.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def multiply(m, n):
    if n == 0:
        return 0
    else:
        return m + multiply(m, n - 1)

# Intermediate
def find_max(lst):
    if len(lst) == 1:
        return lst[0]
    else:
        max_of_rest = find_max(lst[1:])
        return lst[0] if lst[0] > max_of_rest else max_of_rest

# Challenge - Memoized Fibonacci
def fast_fibonacci(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fast_fibonacci(n-1, memo) + fast_fibonacci(n-2, memo)
    return memo[n]

# Why it's inefficient: bad_fibonacci(5) calls bad_fibonacci(4) and bad_fibonacci(3),
# and bad_fibonacci(4) ALSO calls bad_fibonacci(3), so we compute it twice.
# This exponential duplication gets worse as n grows.
```
</details>
