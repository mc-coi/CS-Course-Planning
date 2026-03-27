# Day 16: Introduction to Recursion

**Learning Target:** I can understand how recursion works and write simple recursive functions with base cases and recursive cases.

---

## Key Concepts

**Recursion** — A function that calls itself to solve a smaller version of the same problem.

**Base Case** — The condition that stops the recursion. Without it, infinite recursion occurs.

**Recursive Case** — The function calling itself with simpler/smaller input to progress toward the base case.

**Call Stack** — Python keeps track of all function calls. Each recursive call adds a new frame to the stack.

**Stack Overflow** — If recursion goes too deep (too many calls), Python raises `RecursionError`.

**How Recursion Works:**
1. Function calls itself with simpler input
2. Each call adds to the call stack
3. Base case is reached, function returns
4. Result propagates back up the stack

---

## Code Examples

```python
# Example 1: Simple countdown (base case = 0)
def countdown(n):
    if n == 0:  # Base case
        print("Blastoff!")
        return
    else:  # Recursive case
        print(n)
        countdown(n - 1)

countdown(3)
# Output:
# 3
# 2
# 1
# Blastoff!

# Example 2: Sum of numbers (base case = 1)
def sum_to_n(n):
    if n == 1:  # Base case
        return 1
    else:  # Recursive case
        return n + sum_to_n(n - 1)

print(sum_to_n(5))  # Output: 15 (5 + 4 + 3 + 2 + 1)

# How it works:
# sum_to_n(5) = 5 + sum_to_n(4)
# sum_to_n(4) = 4 + sum_to_n(3)
# sum_to_n(3) = 3 + sum_to_n(2)
# sum_to_n(2) = 2 + sum_to_n(1)
# sum_to_n(1) = 1  <- Base case!
# Working back: 1 + 2 + 3 + 4 + 5 = 15

# Example 3: Factorial (n! = n * (n-1)!)
def factorial(n):
    if n == 0 or n == 1:  # Base case
        return 1
    else:  # Recursive case
        return n * factorial(n - 1)

print(factorial(5))  # Output: 120 (5 * 4 * 3 * 2 * 1)

# Example 4: Power function (a^b)
def power(base, exp):
    if exp == 0:  # Base case
        return 1
    else:  # Recursive case
        return base * power(base, exp - 1)

print(power(2, 3))  # Output: 8 (2 * 2 * 2)

# Example 5: String reversal
def reverse_string(s):
    if len(s) == 0:  # Base case: empty string
        return ""
    else:  # Recursive case: last char + reverse of rest
        return reverse_string(s[1:]) + s[0]

print(reverse_string("hello"))  # Output: olleh

# Example 6: Check if palindrome
def is_palindrome(s):
    s = s.replace(" ", "").lower()  # Clean up
    if len(s) <= 1:  # Base case
        return True
    else:  # Recursive case: check first and last, then rest
        return s[0] == s[-1] and is_palindrome(s[1:-1])

print(is_palindrome("racecar"))  # Output: True
print(is_palindrome("hello"))    # Output: False

# Example 7: Sum of list elements
def list_sum(lst):
    if len(lst) == 0:  # Base case: empty list
        return 0
    else:  # Recursive case: first + sum of rest
        return lst[0] + list_sum(lst[1:])

print(list_sum([1, 2, 3, 4, 5]))  # Output: 15

# Example 8: Recursion with multiple calls (Fibonacci)
def fib(n):
    if n <= 1:  # Base case
        return n
    else:  # Recursive case (calls itself twice!)
        return fib(n - 1) + fib(n - 2)

print(fib(6))  # Output: 8

# Example 9: Recursion with strings
def count_char(s, char):
    if len(s) == 0:  # Base case: empty string
        return 0
    else:  # Recursive case: check first char, then rest
        if s[0] == char:
            return 1 + count_char(s[1:], char)
        else:
            return count_char(s[1:], char)

print(count_char("hello", "l"))  # Output: 2

# Example 10: Understanding the call stack
def call_stack_demo(n):
    print(f"  " * n + f"Entering with n={n}")
    if n == 0:
        print(f"  " * n + "Base case reached!")
        return
    call_stack_demo(n - 1)
    print(f"  " * n + f"Exiting with n={n}")

call_stack_demo(3)
# Shows how the call stack builds up and then unwinds
```

---

## Guided Practice

**Step 1:** Write a function that returns the factorial of a number.
```python
def factorial(n):
    if n == 0 or n == 1:  # Base case
        return 1
    else:  # Recursive case
        return n * factorial(n - 1)

print(factorial(5))  # Should print: 120
```

**Step 2:** Write a function that adds all digits in a number.
```python
def sum_digits(n):
    if n == 0:  # Base case
        return 0
    else:  # Recursive case: last digit + sum of rest
        return (n % 10) + sum_digits(n // 10)

print(sum_digits(123))  # Should print: 6 (1 + 2 + 3)
```

**Step 3:** Write a function that finds the length of a string recursively.
```python
def string_length(s):
    if s == "":  # Base case
        return 0
    else:  # Recursive case: 1 + length of rest
        return 1 + string_length(s[1:])

print(string_length("hello"))  # Should print: 5
```

**Step 4:** Write a function that checks if a list contains a value.
```python
def contains(lst, target):
    if len(lst) == 0:  # Base case: not found
        return False
    elif lst[0] == target:  # Found it!
        return True
    else:  # Recursive case: check rest
        return contains(lst[1:], target)

print(contains([1, 2, 3, 4], 3))  # Should print: True
```

---

## Practice Problems

**Beginner:** Write a recursive function that multiplies two numbers (repeated addition).

**Intermediate:** Write a recursive function that finds the maximum value in a list.

**Challenge:** Write a recursive function that solves a classic problem (like computing GCD or checking nested list structure).

<details>
<summary>💡 Hints</summary>
- For Beginner: Similar to power function
- For Intermediate: Compare first element to max of rest
- For Challenge: Consider GCD using Euclidean algorithm
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def multiply(a, b):
    if b == 0:
        return 0
    else:
        return a + multiply(a, b - 1)

print(multiply(3, 4))  # Output: 12

# Intermediate
def find_max(lst):
    if len(lst) == 1:
        return lst[0]
    else:
        rest_max = find_max(lst[1:])
        return lst[0] if lst[0] > rest_max else rest_max

print(find_max([3, 1, 4, 1, 5]))  # Output: 5

# Challenge (GCD)
def gcd(a, b):
    if b == 0:
        return a
    else:
        return gcd(b, a % b)

print(gcd(48, 18))  # Output: 6
```
</details>
