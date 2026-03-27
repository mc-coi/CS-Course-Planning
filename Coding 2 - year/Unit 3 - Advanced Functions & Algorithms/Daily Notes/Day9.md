# Day 9: Closures and Scope (LEGB Rule)

**Learning Target:** I can understand variable scope using the LEGB rule and write closures that "remember" variables from their enclosing scope.

---

## Key Concepts

**Scope** — The region of a program where a variable can be accessed. Python uses the LEGB rule to determine which variable to use when multiple variables share the same name.

**LEGB Rule** (in order of lookup):
1. **L**ocal — Inside the current function
2. **E**nclosing — In the scope of any enclosing function
3. **G**lobal — At the top level of the module/script
4. **B**uilt-in — Python's built-in scope (like `print`, `len`, etc.)

**Closure** — A function that captures variables from its enclosing scope. The function "remembers" these variables even after the outer function has finished executing.

**nonlocal keyword** — Used inside a nested function to modify a variable from an enclosing (non-global) scope.

**global keyword** — Used to modify a global-scope variable from inside a function.

---

## Code Examples

```python
# Example 1: Understanding local scope
def greet(name):
    message = f"Hello, {name}!"  # Local variable
    print(message)

greet("Alice")  # Output: Hello, Alice!
# print(message)  # Error! message only exists inside the function

# Example 2: Global scope
count = 0  # Global variable

def increment():
    global count  # Declare we're using the global count
    count += 1
    return count

print(increment())  # Output: 1
print(increment())  # Output: 2
print(count)        # Output: 2

# Example 3: Enclosing scope - nested functions
def outer(x):
    def inner():
        print(x)  # Can access x from outer's scope
    inner()

outer(5)  # Output: 5

# Example 4: LEGB in action
x = "global"  # Global

def outer():
    x = "enclosing"  # Enclosing scope
    
    def inner():
        x = "local"  # Local scope
        print(x)
    
    inner()  # Output: local
    print(x)  # Output: enclosing

outer()
print(x)  # Output: global

# Example 5: Closure - function remembers variables
def make_multiplier(n):
    def multiplier(x):
        return x * n  # Uses n from enclosing scope
    return multiplier

times_3 = make_multiplier(3)
times_5 = make_multiplier(5)

print(times_3(10))  # Output: 30
print(times_5(10))  # Output: 50

# Example 6: Using nonlocal to modify enclosing variable
def counter():
    count = 0  # Enclosing scope
    
    def increment():
        nonlocal count  # Declare we're modifying enclosing count
        count += 1
        return count
    
    return increment

counter_func = counter()
print(counter_func())  # Output: 1
print(counter_func())  # Output: 2
print(counter_func())  # Output: 3

# Example 7: Bank account closure (practical example)
def create_account(initial_balance):
    balance = initial_balance  # Enclosing scope variable
    
    def deposit(amount):
        nonlocal balance
        balance += amount
        return balance
    
    def withdraw(amount):
        nonlocal balance
        if amount <= balance:
            balance -= amount
            return balance
        else:
            return "Insufficient funds"
    
    def check_balance():
        return balance
    
    return {"deposit": deposit, "withdraw": withdraw, "balance": check_balance}

account = create_account(100)
print(account["balance"]())     # Output: 100
print(account["deposit"](50))   # Output: 150
print(account["withdraw"](30))  # Output: 120
print(account["balance"]())     # Output: 120

# Example 8: Closure with multiple parameters
def make_adder(x):
    def adder(y):
        return x + y  # Remembers x
    return adder

add_10 = make_adder(10)
add_20 = make_adder(20)

print(add_10(5))   # Output: 15
print(add_20(5))   # Output: 25

# Example 9: When NOT to use global (avoid when possible)
# BAD - relying on global state
count = 0

def bad_increment():
    global count
    count += 1

# GOOD - use parameters and return values
def good_increment(n):
    return n + 1

result = good_increment(0)  # Clearer and more testable

# Example 10: Closure factory for greeting functions
def make_greeter(greeting):
    def greet(name):
        return f"{greeting}, {name}!"
    return greet

english_greet = make_greeter("Hello")
spanish_greet = make_greeter("Hola")

print(english_greet("Alice"))   # Output: Hello, Alice!
print(spanish_greet("Alice"))   # Output: Hola, Alice!
```

---

## Guided Practice

**Step 1:** Write a closure that creates a function to multiply by a given number.
```python
def make_multiplier(factor):
    def multiply(x):
        return x * factor  # Uses factor from enclosing scope
    return multiply

times_2 = make_multiplier(2)
print(times_2(5))  # Should print: 10
```

**Step 2:** Write a counter that remembers its state using a closure.
```python
def make_counter():
    count = 0
    def counter():
        nonlocal count
        count += 1
        return count
    return counter

counter = make_counter()
print(counter())  # Should print: 1
print(counter())  # Should print: 2
print(counter())  # Should print: 3
```

**Step 3:** Demonstrate the LEGB rule with a nested function.
```python
x = "global"

def outer():
    x = "enclosing"
    def inner():
        print(x)  # Which x is printed?
    inner()

outer()  # Should print: enclosing
```

**Step 4:** Use `nonlocal` to modify a variable in an enclosing scope.
```python
def make_accumulator():
    total = 0
    def add(x):
        nonlocal total
        total += x
        return total
    return add

acc = make_accumulator()
print(acc(5))   # Should print: 5
print(acc(10))  # Should print: 15
```

---

## Practice Problems

**Beginner:** Create a closure that returns a function to add a specific number to its input. Test with adding 5.

**Intermediate:** Create a function that makes password validators. Each validator should remember its required password.

**Challenge:** Create a closure-based system for tracking multiple independent counters with their own state.

<details>
<summary>💡 Hints</summary>
- For Beginner: Use a parameter and return a function that uses it
- For Intermediate: Store the password in the enclosing scope
- For Challenge: Use a factory function that returns multiple functions sharing the same state
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def make_adder(n):
    def add(x):
        return x + n
    return add

add_5 = make_adder(5)
print(add_5(10))  # Output: 15

# Intermediate
def make_password_validator(password):
    def validate(attempt):
        return attempt == password
    return validate

validator = make_password_validator("secret123")
print(validator("secret123"))  # Output: True
print(validator("wrong"))      # Output: False

# Challenge
def make_counter_system():
    counters = {}
    def get_counter(name):
        if name not in counters:
            counters[name] = 0
        def increment():
            nonlocal counters
            counters[name] += 1
            return counters[name]
        return increment
    return get_counter

counter_system = make_counter_system()
counter1 = counter_system("counter1")
counter2 = counter_system("counter2")
print(counter1())  # Output: 1
print(counter1())  # Output: 2
print(counter2())  # Output: 1
```
</details>
