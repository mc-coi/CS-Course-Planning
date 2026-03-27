# Day 99: Multiple Parameters and Default Values

**Learning Target:** I can write functions with multiple parameters and use default parameter values to make functions more flexible.

### Key Concepts

Functions often need more than one piece of data. You define multiple parameters by listing them in order, separated by commas:
```
def greet(first_name, last_name, greeting):
    print(f"{greeting}, {first_name} {last_name}!")
```

The order matters: the first argument you pass goes to the first parameter, the second argument to the second parameter, and so on. This is called **positional arguments**.

**Default parameter values** let you make parameters optional. If a caller doesn't provide a value, the function uses the default. Here's the syntax:
```
def greet(first_name, last_name, greeting="Hello"):
    print(f"{greeting}, {first_name} {last_name}!")

greet("Alice", "Smith")  # Uses default greeting
greet("Bob", "Jones", "Hey")  # Overrides default
```

Parameters with defaults must come **after** parameters without defaults. You can't write `def func(x=5, y):` because it's ambiguous.

Default values save you from repeating common arguments. If most function calls use the same value, make it a default. Callers who want something different can override it.

### Code Examples

```python
# Example 1: Multiple parameters, some with defaults
def introduce(first, last, grade=10):
    print(f"Hi, I'm {first} {last} and I'm in grade {grade}.")

introduce("Alice", "Smith")  # Uses default grade
introduce("Bob", "Jones", 11)  # Overrides grade
introduce("Charlie", "Brown", 9)
```

```python
# Example 2: Function with many parameters
def create_account(username, password, email, age=13, verified=False):
    print(f"Account: {username}")
    print(f"Email: {email}")
    print(f"Age: {age}")
    print(f"Verified: {verified}")

create_account("alice_s", "secret123", "alice@example.com")
create_account("bob_j", "mypass", "bob@example.com", 16, True)
```

```python
# Example 3: Function that returns a formatted string
def format_price(amount, currency="$", decimals=2):
    return f"{currency}{amount:.{decimals}f}"

print(format_price(19.5))  # $19.50
print(format_price(20))    # $20.00
print(format_price(15.999, currency="€", decimals=2))  # €15.99
```

### Guided Practice

1. Write a function `describe_car(brand, model, color="black")` with a default color. Call it with and without the color parameter.
2. Write a function `countdown(start=10)` that prints a countdown from `start` to 0. Call it with the default and with a custom start value.
3. Write a function `build_sentence(subject, verb, object_word, punctuation=".")` that builds and returns a sentence. Test it several ways.

### Practice Problems

**Problem 1 — Beginner:** Write a function `say_age(name, age, grade=9)` that prints a sentence like "My name is Alice and I'm 15 years old. I'm in grade 9." Call it three times, using the default grade for at least one call.

```python
# Starter code
def say_age(name, age, grade=9):
    # Your code here
    pass

# Call the function here
```

**Problem 2 — Intermediate:** Write a function `calculate_grade(score, total=100)` that takes a score and the total possible points (default 100) and returns the percentage. Call it with the default and with a custom total.

**Problem 3 — Challenge:** Write a function `build_greeting(name, greeting="Hello", punctuation="!", formal=False)` that builds a personalized greeting. If `formal` is `True`, use a more formal greeting. Return the complete greeting string. Test it several ways, including some with and without defaults.

<details>
<summary>💡 Hints</summary>

- Problem 1: Remember the syntax for default parameters. They go in the function definition, not the call.
- Problem 2: The percentage is `(score / total) * 100`. Think about what the default total represents.
- Problem 3: Use an `if` statement to check the `formal` parameter and adjust your greeting accordingly.
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
def say_age(name, age, grade=9):
    print(f"My name is {name} and I'm {age} years old. I'm in grade {grade}.")

say_age("Alice", 15)
say_age("Bob", 16, 10)
say_age("Charlie", 17, 11)
```

```python
# Problem 2 Example
def calculate_grade(score, total=100):
    percentage = (score / total) * 100
    return percentage

print(calculate_grade(85))       # 85.0
print(calculate_grade(42, 50))   # 84.0
print(calculate_grade(18, 20))   # 90.0
```

```python
# Problem 3 Example
def build_greeting(name, greeting="Hello", punctuation="!", formal=False):
    if formal:
        return f"{greeting}, {name}{punctuation} It is a pleasure to meet you."
    else:
        return f"{greeting} {name}{punctuation}"

print(build_greeting("Alice"))
print(build_greeting("Bob", "Hey", "!"))
print(build_greeting("Dr. Smith", "Greetings", ".", formal=True))
```
</details>

---
