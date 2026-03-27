# Unit 5 Reference Guide

Quick syntax reference and pattern guide for functions and modularity.

## Function Syntax

### Basic Function Definition
```python
def function_name():
    # Function body (indented)
    print("Hello!")

function_name()  # Call the function
```

### Function with Parameters
```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")  # Argument "Alice" is passed to parameter name
```

### Function with Multiple Parameters
```python
def add(a, b):
    result = a + b
    return result

answer = add(5, 3)  # answer = 8
```

### Function with Default Parameters
```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")  # Uses default greeting
greet("Bob", "Hi")  # Overrides default
```

### Function with Return Value
```python
def double(n):
    return n * 2

result = double(5)  # result = 10
```

## Parameters and Arguments

| Term | Definition | Example |
|------|-----------|---------|
| **Parameter** | Variable in function definition | `def func(x):` — `x` is the parameter |
| **Argument** | Value passed when calling function | `func(5)` — `5` is the argument |

## Return Values

```python
# Function that returns a value
def calculate(a, b):
    total = a + b
    return total

# The function call "becomes" the returned value
result = calculate(10, 20)  # result = 30

# You can use returned values directly
print(calculate(5, 5))  # Prints 10

# Or pass them to other functions
answer = double(calculate(3, 4))  # = double(7) = 14
```

**Important:** Once `return` executes, function stops immediately.

```python
def test():
    return 5
    print("This never runs!")  # After return, no more code executes
```

## Variable Scope

### Local Variables
Variables created inside a function exist only in that function.

```python
def example():
    x = 5  # Local variable
    print(x)  # Works (x is in scope)

example()  # Prints 5
print(x)  # ERROR: x is not in scope
```

### Global Variables
Variables created outside any function are global (accessible everywhere).

```python
name = "Alice"  # Global

def greet():
    print(name)  # Can READ global variables

greet()  # Prints "Alice"
```

### Important Scope Rule
**If you assign to a variable inside a function, it's local** (unless you use `global`).

```python
x = 10  # Global

def example():
    x = 5  # This creates a LOCAL x, doesn't modify global
    print(x)

example()  # Prints 5
print(x)   # Prints 10 (global x unchanged)
```

### Reading Globals (Fine)
```python
total = 0

def add_to_total(amount):
    return total + amount  # Just READING global, no assignment
```

### Modifying Globals (Avoid!)
```python
total = 0

def add_to_total(amount):
    global total  # Now assignment modifies global
    total = total + amount

# Better design: use return values instead
def add_to_total(current_total, amount):
    return current_total + amount

total = add_to_total(total, 10)  # Update the global manually
```

## Function Composition

Functions can call other functions.

```python
def double(n):
    return n * 2

def square(n):
    return n * n

def composed(n):
    # Compose functions: square the doubled value
    return square(double(n))

result = composed(5)  # = square(10) = 100
```

## Common Patterns

### Pattern 1: Process a List
```python
def sum_all(numbers):
    """Add up all numbers in a list."""
    total = 0
    for num in numbers:
        total = total + num
    return total
```

### Pattern 2: Filter a List
```python
def get_long_words(words, min_length):
    """Return only words with min_length or more characters."""
    result = []
    for word in words:
        if len(word) >= min_length:
            result.append(word)
    return result
```

### Pattern 3: Transform a List
```python
def double_all(numbers):
    """Return a new list with each number doubled."""
    result = []
    for num in numbers:
        result.append(num * 2)
    return result
```

### Pattern 4: Find Something in a List
```python
def find_max(numbers):
    """Find and return the largest number."""
    max_value = numbers[0]
    for num in numbers:
        if num > max_value:
            max_value = num
    return max_value
```

### Pattern 5: Count Something
```python
def count_vowels(text):
    """Count how many vowels are in text."""
    count = 0
    for char in text:
        if char in "aeiouAEIOU":
            count = count + 1
    return count
```

### Pattern 6: Check a Condition
```python
def is_even(n):
    """Return True if n is even, False if odd."""
    return n % 2 == 0

def is_positive(n):
    """Return True if n is positive."""
    return n > 0
```

### Pattern 7: Conditional Return
```python
def classify_grade(score):
    """Return letter grade based on score."""
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    else:
        return "F"
```

### Pattern 8: main() Pattern
```python
# Helper functions at the top
def get_input():
    return input("Enter something: ")

def process(data):
    return data.upper()

def display(result):
    print(f"Result: {result}")

# Main function
def main():
    data = get_input()
    result = process(data)
    display(result)

# Call main at the bottom
if __name__ == "__main__":
    main()
```

## Docstrings

Document your functions with docstrings:

```python
def calculate_area(radius):
    """
    Calculate the area of a circle.

    Parameters:
    radius (float): The radius of the circle

    Returns:
    float: The area of the circle
    """
    return 3.14159 * radius * radius
```

## Common Errors

| Error | Problem | Fix |
|-------|---------|-----|
| `SyntaxError: invalid syntax` | Missing colon after function definition | `def func():` |
| `IndentationError` | Function body not indented | Indent code after `def` |
| `NameError: name 'func' is not defined` | Calling function before defining it | Define function before calling |
| `TypeError: function() takes 2 positional arguments but 3 were given` | Wrong number of arguments | Check parameters vs arguments |
| `UnboundLocalError: local variable referenced before assignment` | Using local variable before assigning | Assign before using, or read global without assigning |
| Function prints instead of returns result | Forgot `return` | Add `return` statement |

## Cheat Sheet: Writing a Good Function

```python
def descriptive_name(parameter1, parameter2):
    """
    One-line summary of what function does.

    Parameters:
    parameter1 (type): What it is
    parameter2 (type): What it is

    Returns:
    type: What is returned
    """
    # Use local variables
    intermediate_value = parameter1 + parameter2

    # Do the work
    result = intermediate_value * 2

    # Return the result (don't print unless you mean to)
    return result
```

**Key points:**
- Descriptive name
- Parameters with meaningful names
- Docstring
- Local variables (no unnecessary globals)
- `return` statement
- Focused, single purpose

## Quick Testing

Test your functions like this:

```python
def add(a, b):
    return a + b

# Test normal cases
assert add(2, 3) == 5, "Simple addition failed"
assert add(0, 0) == 0, "Zero test failed"
assert add(-1, 1) == 0, "Negative test failed"

print("All tests passed!")
```

---

*Last updated: 2026-03-25*
