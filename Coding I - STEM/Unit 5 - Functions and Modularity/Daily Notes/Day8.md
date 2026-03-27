# Day 8: Debugging Functions

### Key Concepts
Common function-related bugs and how to fix them:
- **Calling before defining:** `def` must come before the call in the file
- **Wrong number of arguments:** Count params in `def` — match at call
- **Missing return:** Function gives `None` when you expected a value
- **Using return value of a `print`-only function:** Gets `None`
- **Scope errors:** Using a local variable outside its function
- **Infinite recursion:** A function that calls itself without stopping

### Code Examples

```python
# ── Bug 1: Forgot to return ────────────────────────────────
def add(a, b):
    result = a + b
    # forgot return!

answer = add(3, 5)
print(answer)   # None  ← Bug! Should be 8

# Fix:
def add(a, b):
    return a + b     # ← add return

# ── Bug 2: Using None from a print function ─────────────────
def double(n):
    print(n * 2)    # prints but returns None

x = double(5)      # prints 10
print(x * 3)       # TypeError: unsupported operand type(s): NoneType * int

# Fix: change print to return
def double(n):
    return n * 2

# ── Bug 3: Wrong number of arguments ──────────────────────
def greet(name, greeting):
    print(f"{greeting}, {name}!")

# greet("Alice")         # ❌ TypeError: missing 1 required positional argument
# greet("Alice", "Hi", "Extra")  # ❌ TypeError: takes 2 positional arguments but 3 were given
greet("Alice", "Hello")  # ✅

# ── Bug 4: NameError — using local variable outside ────────
def calculate():
    subtotal = 100
    tax = subtotal * 0.08
    # doesn't return anything

calculate()
# print(subtotal)   # ❌ NameError: subtotal not defined

# Fix:
def calculate():
    subtotal = 100
    tax = subtotal * 0.08
    return subtotal + tax

total = calculate()
print(total)    # 108.0

# ── Bug 5: Missing colon ───────────────────────────────────
# def greet(name)    # ❌ SyntaxError: expected ':'
#     print(name)

def greet(name):    # ✅ colon required
    print(name)

# ── Debugging strategy: trace with print ──────────────────
def mystery(n):
    print(f"  mystery called with n={n}")   # trace input
    result = n * 2 + 5
    print(f"  returning {result}")           # trace output
    return result

x = mystery(7)
print(x)
# Remove trace prints once fixed
```

### Fix the Bug Exercises

Fix each buggy function below:

```python
# Bug A: What's wrong?
def multiply(a, b)
    return a * b

# Bug B: What's wrong?
def is_positive(n):
    if n > 0:
        return True

result = is_positive(-5)
print("Positive:", result)   # prints: Positive: None

# Bug C: What's wrong?
def format_name(first, last):
    full = first + " " + last
    print(full)

name = format_name("John", "Smith")
greeting = "Hello, " + name   # TypeError!
print(greeting)
```

<details>
<summary>✅ Answers to Bug A, B, C</summary>

```python
# Bug A: Missing colon
def multiply(a, b):
    return a * b

# Bug B: Missing return for False case
def is_positive(n):
    if n > 0:
        return True
    return False   # ← add this

# Bug C: Should return, not print
def format_name(first, last):
    return first + " " + last   # ← change print to return

name = format_name("John", "Smith")
greeting = "Hello, " + name
print(greeting)
```
</details>

---