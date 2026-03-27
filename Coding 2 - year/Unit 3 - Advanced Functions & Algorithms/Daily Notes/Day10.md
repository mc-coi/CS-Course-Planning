# Day 10: Advanced Scope and Closure Applications

**Learning Target:** I can apply closures to real-world problems and understand scope pitfalls in Python.

---

## Key Concepts

**Scope Pitfalls:**
- Mutable default arguments (function definitions capture values at definition time)
- Loop variables in closures (all closures share the same loop variable)
- Accidental global modifications (forgetting `global` or `nonlocal`)

**Common Closure Uses:**
- **Factory functions** — Create customized functions
- **Callbacks** — Functions passed to other functions that need state
- **State management** — Encapsulate private state without classes
- **Decorators** — Advanced pattern built on closures (coming next!)

**Best Practices:**
- Prefer clear parameters and return values over relying on closure scope
- Use `nonlocal` explicitly when modifying enclosing variables
- Avoid complex nested scopes (consider using classes instead)
- Test closure state management carefully

---

## Code Examples

```python
# Example 1: The loop variable closure pitfall
def create_functions():
    functions = []
    for i in range(3):
        def func():
            return i  # All functions share the same i!
        functions.append(func)
    return functions

funcs = create_functions()
print(funcs[0]())  # Output: 2 (not 0!)
print(funcs[1]())  # Output: 2 (not 1!)
print(funcs[2]())  # Output: 2

# FIX: Use a default argument to capture the value
def create_functions_fixed():
    functions = []
    for i in range(3):
        def func(i=i):  # Default argument captures current i
            return i
        functions.append(func)
    return functions

funcs = create_functions_fixed()
print(funcs[0]())  # Output: 0
print(funcs[1]())  # Output: 1
print(funcs[2]())  # Output: 2

# Example 2: Mutable default argument pitfall
def append_to_list(item, items=[]):  # DON'T DO THIS!
    items.append(item)
    return items

print(append_to_list(1))     # [1]
print(append_to_list(2))     # [1, 2] - unexpected!
print(append_to_list(3))     # [1, 2, 3] - unexpected!

# FIX: Use None as default
def append_to_list_fixed(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items

print(append_to_list_fixed(1))     # [1]
print(append_to_list_fixed(2))     # [2]
print(append_to_list_fixed(3))     # [3]

# Example 3: Rate limiter using closure
def make_rate_limiter(max_calls, time_window):
    """Create a function that tracks calls within a time window"""
    call_count = 0
    
    def is_allowed():
        nonlocal call_count
        if call_count < max_calls:
            call_count += 1
            return True
        return False
    
    def reset():
        nonlocal call_count
        call_count = 0
    
    return {"is_allowed": is_allowed, "reset": reset}

limiter = make_rate_limiter(3, 60)
print(limiter["is_allowed"]())  # True
print(limiter["is_allowed"]())  # True
print(limiter["is_allowed"]())  # True
print(limiter["is_allowed"]())  # False
limiter["reset"]()
print(limiter["is_allowed"]())  # True

# Example 4: Partial function application (curry)
def make_operation(op):
    """Create functions for specific operations"""
    def add(a, b):
        return a + b
    def multiply(a, b):
        return a * b
    def subtract(a, b):
        return a - b
    
    operations = {
        "+": add,
        "*": multiply,
        "-": subtract,
    }
    return operations.get(op)

add_func = make_operation("+")
print(add_func(5, 3))  # Output: 8

multiply_func = make_operation("*")
print(multiply_func(5, 3))  # Output: 15

# Example 5: Configuration wrapper using closure
def make_api_client(base_url, api_key):
    """Create an API client with fixed configuration"""
    def get(endpoint):
        return f"GET {base_url}{endpoint} with key {api_key}"
    
    def post(endpoint, data):
        return f"POST {base_url}{endpoint} with data {data} and key {api_key}"
    
    return {"get": get, "post": post}

client = make_api_client("https://api.example.com", "secret123")
print(client["get"]("/users"))  # GET https://api.example.com/users with key secret123

# Example 6: Memoization using closure
def make_fibonacci():
    """Create a fibonacci function that remembers previous results"""
    cache = {}
    
    def fib(n):
        if n in cache:
            return cache[n]
        if n <= 1:
            result = n
        else:
            result = fib(n - 1) + fib(n - 2)
        cache[n] = result
        return result
    
    return fib

fibonacci = make_fibonacci()
print(fibonacci(10))  # Faster because results are cached

# Example 7: Event emitter pattern
def make_event_emitter():
    """Simple event system using closures"""
    listeners = {}
    
    def on(event, callback):
        if event not in listeners:
            listeners[event] = []
        listeners[event].append(callback)
    
    def emit(event, data):
        if event in listeners:
            for callback in listeners[event]:
                callback(data)
    
    return {"on": on, "emit": emit}

emitter = make_event_emitter()
emitter["on"]("user_login", lambda data: print(f"User logged in: {data}"))
emitter["emit"]("user_login", "Alice")  # Output: User logged in: Alice

# Example 8: Safe state isolation
def make_user(name, age):
    """Encapsulate user data with getter/setter methods"""
    _name = name  # Underscore suggests private (not enforced, but conventional)
    _age = age
    
    def get_name():
        return _name
    
    def get_age():
        return _age
    
    def have_birthday():
        nonlocal _age
        _age += 1
    
    return {
        "get_name": get_name,
        "get_age": get_age,
        "have_birthday": have_birthday,
    }

user = make_user("Alice", 20)
print(user["get_age"]())   # Output: 20
user["have_birthday"]()
print(user["get_age"]())   # Output: 21
```

---

## Guided Practice

**Step 1:** Fix the loop closure pitfall. Create three functions that return 0, 1, and 2 respectively.
```python
# Fixed version
def create_functions_fixed():
    functions = []
    for i in range(3):
        def func(i=i):  # Capture i with default argument
            return i
        functions.append(func)
    return functions

funcs = create_functions_fixed()
print([f() for f in funcs])  # Should print: [0, 1, 2]
```

**Step 2:** Create a simple counter that uses closure to maintain state.
```python
def make_counter():
    count = 0
    def increment():
        nonlocal count
        count += 1
        return count
    def get():
        return count
    return {"increment": increment, "get": get}

counter = make_counter()
print(counter["get"]())      # Should print: 0
print(counter["increment"]())  # Should print: 1
print(counter["get"]())      # Should print: 1
```

**Step 3:** Demonstrate the mutable default argument pitfall and its fix.
```python
# The pitfall - DON'T DO THIS
# def add_item(item, items=[]):
#     items.append(item)
#     return items

# The fix - DO THIS
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items

print(add_item(1))  # Should print: [1]
print(add_item(2))  # Should print: [2]
```

---

## Practice Problems

**Beginner:** Create a function factory that generates different greeting messages. Test with "Hello" and "Hi".

**Intermediate:** Create a password strength checker that remembers attempted passwords and prevents rapid re-attempts.

**Challenge:** Implement a simple memoization wrapper that caches function results based on arguments.

<details>
<summary>💡 Hints</summary>
- For Beginner: Use make_greeter(greeting) pattern from yesterday
- For Intermediate: Track last attempt time and count
- For Challenge: Store results in a dictionary keyed by arguments
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def make_greeter(greeting):
    def greet(name):
        return f"{greeting}, {name}!"
    return greet

hello = make_greeter("Hello")
hi = make_greeter("Hi")
print(hello("Alice"))  # Output: Hello, Alice!
print(hi("Bob"))       # Output: Hi, Bob!

# Intermediate
def make_password_checker(password):
    attempts = []
    def check(attempt):
        attempts.append(attempt)
        if len(attempts) > 5:
            return "Too many attempts!"
        return "Correct!" if attempt == password else "Wrong!"
    return check

checker = make_password_checker("secret")
print(checker("wrong"))      # Output: Wrong!
print(checker("secret"))     # Output: Correct!

# Challenge
def make_memoizer(func):
    cache = {}
    def memoized(x):
        if x not in cache:
            cache[x] = func(x)
        return cache[x]
    return memoized

def expensive_function(n):
    print(f"Computing {n}...")
    return n ** 2

memoized_func = make_memoizer(expensive_function)
print(memoized_func(5))  # Prints "Computing 5..." then 25
print(memoized_func(5))  # Just prints 25 (cached)
```
</details>
