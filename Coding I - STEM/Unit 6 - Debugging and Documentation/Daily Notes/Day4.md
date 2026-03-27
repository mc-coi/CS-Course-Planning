# Day 4: try/except/finally — Exception Handling

### Key Concepts
- `try` block: code that might fail
- `except` block: what to do if that specific error occurs
- `else` block: runs only if no exception occurred
- `finally` block: always runs, whether or not there was an error
- Catch specific exceptions, not just bare `except`
- You can have multiple `except` blocks for different error types

### Structure

```
try:
    risky code
except SpecificError:
    handle that error
except AnotherError:
    handle this different error
else:
    runs only if no error happened
finally:
    always runs (cleanup)
```

### Code Examples

```python
# ── Basic try/except ──────────────────────────────────────
try:
    number = int(input("Enter a number: "))
    result = 100 / number
    print(f"100 / {number} = {result}")
except ValueError:
    print("That's not a valid number!")
except ZeroDivisionError:
    print("Can't divide by zero!")

# ── else and finally ──────────────────────────────────────
try:
    x = int(input("Enter a number: "))
    y = int(input("Enter another: "))
    result = x / y
except ValueError:
    print("Not a number!")
except ZeroDivisionError:
    print("Can't divide by zero!")
else:
    print(f"Result: {result}")     # only if no exceptions
finally:
    print("Calculation attempt complete.")  # always runs

# ── Handling FileNotFoundError ────────────────────────────
def read_file_safely(filename):
    try:
        with open(filename, "r") as f:
            return f.read()
    except FileNotFoundError:
        print(f"Error: '{filename}' not found.")
        return None

content = read_file_safely("data.txt")
if content:
    print(content)

# ── Input validation with try/except ─────────────────────
def get_valid_integer(prompt):
    while True:
        try:
            return int(input(prompt))
        except ValueError:
            print("Please enter a whole number.")

age = get_valid_integer("Enter your age: ")
print(f"Your age: {age}")

# ── Multiple exceptions in one block ─────────────────────
def safe_divide(a, b):
    try:
        return a / b
    except (ZeroDivisionError, TypeError) as e:
        print(f"Error: {e}")
        return None

print(safe_divide(10, 2))     # 5.0
print(safe_divide(10, 0))     # Error: division by zero
print(safe_divide("10", 2))   # Error: unsupported operand type(s)

# ── Getting error details ─────────────────────────────────
try:
    items = [1, 2, 3]
    print(items[10])
except IndexError as e:
    print(f"Index error: {e}")         # list index out of range
    print(f"Error type: {type(e).__name__}")  # IndexError

# ── Raising your own exceptions ───────────────────────────
def set_age(age):
    if age < 0 or age > 150:
        raise ValueError(f"Age {age} is not realistic (must be 0–150)")
    return age

try:
    set_age(-5)
except ValueError as e:
    print(f"Invalid age: {e}")
```

### Practice Problems — Day 4

**Beginner:**
1. Write a program that asks for two numbers and divides them. Use `try/except` to handle both `ValueError` (not a number) and `ZeroDivisionError`.
2. Wrap `open("missing.txt")` in a `try/except` block that prints a friendly message if the file doesn't exist.

**Intermediate:**

3. Write `get_float(prompt)` that keeps asking until the user enters a valid decimal number.
4. Write `safe_list_get(lst, index, default=None)` that returns `lst[index]` or `default` if the index is out of range.

**Challenge:**

5. Write a `safe_calculator()` program that:
   - Accepts two numbers and an operator (+, -, *, /)
   - Uses `try/except` to handle invalid number input, division by zero, and invalid operators
   - Loops until the user types "quit"
   - Logs each successful calculation to `calc_history.txt`

<details>
<summary>✅ Answer for #5 (partial)</summary>

```python
def safe_calculator():
    log_file = "calc_history.txt"
    print("Calculator — type 'quit' to exit")

    while True:
        try:
            entry = input("\nExpression (e.g. 10 + 5): ").strip()
            if entry.lower() == "quit":
                break

            parts = entry.split()
            if len(parts) != 3:
                raise ValueError("Format must be: number operator number")

            a = float(parts[0])
            op = parts[1]
            b = float(parts[2])

            if op == "+": result = a + b
            elif op == "-": result = a - b
            elif op == "*": result = a * b
            elif op == "/":
                if b == 0:
                    raise ZeroDivisionError("Cannot divide by zero")
                result = a / b
            else:
                raise ValueError(f"Unknown operator: {op}")

            output = f"{a} {op} {b} = {result}"
            print(output)
            with open(log_file, "a") as f:
                f.write(output + "\n")

        except ValueError as e:
            print(f"Input error: {e}")
        except ZeroDivisionError as e:
            print(f"Math error: {e}")
```
</details>

---