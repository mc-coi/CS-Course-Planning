# Day 98: Return Values

**Learning Target:** I can write functions that return values using the `return` keyword and use those returned values in my programs.

### Key Concepts

So far, functions have **done things**—printed output, modified variables. Now they'll **give back results** using the **`return` keyword**. A function with a return value sends data back to the caller, who can then use that data however they want.

The **`return` keyword** stops the function immediately and sends a value back to the code that called the function. Here's the pattern:
```
def function_name(parameters):
    # Do some work
    return value_to_send_back
```

When you call a function that returns a value, the function call itself **becomes** that value. For example:
```
result = add(5, 3)  # The function returns 8, so result becomes 8
```

**Why return values matter:** Without them, functions can only print output. With return values, functions can **calculate** results that other parts of your program can use. You might add two numbers and return the sum. You might search a list and return the item you found. You might check a password and return `True` or `False`. Return values are essential for writing programs where functions collaborate to solve problems.

Functions can return any type of data: numbers, strings, lists, `True`/`False`, even other functions. A function can return on multiple paths (different conditions), but typically it has one main return path.

### Code Examples

```python
# Example 1: Simple return
def add(a, b):
    sum_result = a + b
    return sum_result

answer = add(5, 3)
print(answer)  # 8
print(add(10, 20))  # 30
```

```python
# Example 2: Return a string
def create_username(first, last):
    username = first.lower() + last.lower()
    return username

user = create_username("Alice", "Smith")
print(f"Your username is: {user}")  # Your username is: alicesmith
```

```python
# Example 3: Return based on a condition
def is_adult(age):
    if age >= 18:
        return True
    else:
        return False

if is_adult(17):
    print("Can vote")
else:
    print("Too young to vote")  # This prints
```

### Guided Practice

1. Write a function `square(n)` that takes a number and **returns** its square (not prints it).
2. Call the function and store the result in a variable. Print that variable.
3. Write a function `make_loud(text)` that takes a string and returns it in uppercase.
4. Test it by calling it and printing the result.

### Practice Problems

**Problem 1 — Beginner:** Write a function `double(x)` that takes a number, doubles it, and returns the result. Call it three times with different numbers and print each result.

```python
# Starter code
def double(x):
    # Your code here
    return

# Call the function here
```

**Problem 2 — Intermediate:** Write a function `greet_and_ask(name)` that takes a name, and returns a string like "Hello, Alice! How are you today?" (Don't print—return!). Call it twice, and each time, print the returned value.

**Problem 3 — Challenge:** Write a function `is_positive(n)` that returns `True` if the number is positive and `False` otherwise. Then write a program that calls this function with several numbers and prints a message for each (e.g., "42 is positive" or "-5 is not positive").

<details>
<summary>💡 Hints</summary>

- Problem 1: Remember, you're **returning**, not printing. The caller will do the printing.
- Problem 2: Use an f-string to build your greeting string, then return it.
- Problem 3: Use the return value in an `if` statement. Something like `if is_positive(n):`
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
def double(x):
    return x * 2

result1 = double(5)
result2 = double(10)
result3 = double(3)

print(result1)  # 10
print(result2)  # 20
print(result3)  # 6
```

```python
# Problem 2 Example
def greet_and_ask(name):
    greeting = f"Hello, {name}! How are you today?"
    return greeting

message1 = greet_and_ask("Alice")
print(message1)

message2 = greet_and_ask("Bob")
print(message2)
```

```python
# Problem 3 Example
def is_positive(n):
    return n > 0

numbers = [42, -5, 0, 100, -3]
for num in numbers:
    if is_positive(num):
        print(f"{num} is positive")
    else:
        print(f"{num} is not positive")
```
</details>

---
