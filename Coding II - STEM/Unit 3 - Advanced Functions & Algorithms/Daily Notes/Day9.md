# Day 9: Project Day — Recursive Calculator & Algorithm Showcase
**Learning Target:** I can apply advanced function techniques to build a complete program.

### Project Overview
Build a calculator demonstrating:
- Lambda functions and higher-order functions
- Recursion for complex calculations
- Algorithm efficiency
- Decorators for timing/logging

### Requirements
- Support basic operations (+, -, *, /)
- Implement exponentiation with recursion
- Use lambda for operation selection
- Time operations to show efficiency
- Create a menu-driven interface

### Scaffold & Starter Code
```python
import time

# Decorator for timing
def timer(func):
    def wrapper(*args):
        start = time.time()
        result = func(*args)
        elapsed = time.time() - start
        print(f"Result: {result} (Computed in {elapsed:.6f}s)")
        return result
    return wrapper

# Recursive power (demonstrates recursion)
@timer
def power_recursive(base, exp):
    if exp == 0:
        return 1
    return base * power_recursive(base, exp - 1)

# Lambda-based operations
operations = {
    '+': lambda x, y: x + y,
    '-': lambda x, y: x - y,
    '*': lambda x, y: x * y,
    '/': lambda x, y: x / y if y != 0 else "Error: Division by zero"
}

# Higher-order function for filtering
def filter_results(results, threshold):
    return list(filter(lambda r: r > threshold, results))

# Main program
def main():
    while True:
        print("\n--- Calculator ---")
        print("1. Basic calculation")
        print("2. Power (recursive)")
        print("3. Exit")

        choice = input("Select: ")

        if choice == "1":
            op = input("Operation (+, -, *, /): ")
            x = float(input("First number: "))
            y = float(input("Second number: "))
            result = operations[op](x, y)
            print(f"Result: {result}")

        elif choice == "2":
            base = int(input("Base: "))
            exp = int(input("Exponent: "))
            power_recursive(base, exp)

        elif choice == "3":
            break

if __name__ == "__main__":
    main()
```

### Enhancement Ideas
- Fibonacci calculator with memoization
- Sorting algorithm comparison (show Big O)
- Scientific calculator functions
- History of operations

---

# Unit Practice Bank

1. **Beginner:** Write a lambda that adds two numbers.
2. **Beginner:** Use map() to double all numbers in a list.
3. **Beginner:** Use filter() to keep only even numbers.
4. **Intermediate:** Write a list comprehension with a condition.
5. **Intermediate:** Write a recursive factorial function.
6. **Intermediate:** Use zip() to combine two lists into pairs.
7. **Intermediate:** Write a dictionary comprehension.
8. **Challenge:** Write memoized Fibonacci.
9. **Challenge:** Write binary search recursively.
10. **Challenge:** Create a decorator that validates function arguments.
11. **Challenge:** Write a function composition tool.
12. **Challenge:** Implement merge sort with Big O analysis.
13. **Challenge:** Create a caching decorator for expensive functions.
14. **Challenge:** Flatten a deeply nested list recursively.
15. **Challenge:** Analyze and optimize an algorithm from O(n²) to O(n log n).

---

# Common Mistakes & How to Fix Them
| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Forgetting base case in recursion | RecursionError: maximum recursion depth | Always include base case |
| Using mutable default in function | Function mutates shared object | Use None as default, create inside |
| Lambda with multiple statements | Syntax error | Lambdas only take expressions, not statements |
| Infinite recursion | RecursionError | Ensure base case is reachable |
| Confusing map() returns iterator | Can't reuse map result | Wrap in list() or iterate only once |
| Complex comprehensions hard to read | Unreadable code | Use intermediate variables or regular loops |

---

# Unit Assessment Prep

**Review Questions:**

1. What is a lambda function? When would you use one?
2. Explain the difference between map(), filter(), and zip().
3. Write a list comprehension that squares numbers 1-5.
4. What is recursion? Give an example.
5. Explain the base case and recursive case.
6. What does Big O notation measure?
7. Compare O(n) and O(n²) complexity.
8. What is a decorator?
9. Explain what a closure is.
10. How would you optimize an O(n²) algorithm?

**Answers:**

1. A lambda is a small anonymous function. Use for simple operations with map(), filter(), sorted().
2. map() applies function to each item; filter() keeps items where function returns True; zip() combines iterables.
3. `[x**2 for x in range(1, 6)]` → `[1, 4, 9, 16, 25]`
4. Recursion is when a function calls itself. Example: factorial(n) = n * factorial(n-1)
5. Base case stops recursion; recursive case calls function with simpler input.
6. Big O measures how algorithm performance scales with input size.
7. O(n) is linear (fast); O(n²) is quadratic (slow for large inputs).
8. A decorator is a function that modifies another function's behavior.
9. A closure is a nested function that captures variables from its outer scope.
10. Use more efficient algorithm (sorting, binary search), reduce nested loops, use caching.

---

# Vocabulary & Quick Reference

**Key Terms:**
- **Lambda:** Anonymous function defined with lambda keyword
- **Higher-order function:** Function that takes/returns functions
- **Recursion:** Function calling itself
- **Base case:** Condition that stops recursion
- **Memoization:** Caching function results
- **Big O:** Notation for algorithm complexity
- **Closure:** Nested function capturing outer variables
- **Decorator:** Function that wraps another function
- **Pseudocode:** English-like description of algorithm

**Key Syntax:**
```python
# Lambda
square = lambda x: x ** 2

# map, filter, zip
map(func, iterable)
filter(condition, iterable)
zip(iter1, iter2)

# Comprehension
[x for x in range(10) if x % 2 == 0]

# Recursion
def factorial(n):
    return 1 if n <= 1 else n * factorial(n-1)

# Decorator
@decorator_name
def func():
    pass
```

---
