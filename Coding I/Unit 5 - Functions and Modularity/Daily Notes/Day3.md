# Day 3: Return Values

### Key Concepts
- `return` sends a value back to the caller
- After `return`, the function stops — no more code runs in that call
- You can use returned values in expressions, assignments, and prints
- A function without `return` gives back `None`

### The Difference: `print` vs `return`
| | `print` | `return` |
|--|---------|---------|
| Purpose | Shows text to screen | Sends data back to caller |
| Can be stored? | No | Yes |
| Can be used in math? | No | Yes |
| Useful outside function? | No | Yes |

### Code Examples

```python
# ── Function that returns a value ──────────────────────────
def square(n):
    return n * n            # sends back the value, does not print

result = square(5)          # stores returned value
print(result)               # 25

# Use return value directly in expression
print(square(3) + square(4))   # 9 + 16 = 25

# ── Return vs print comparison ─────────────────────────────
def double_print(n):
    print(n * 2)            # prints but returns None

def double_return(n):
    return n * 2            # returns the value

# double_print works once:
double_print(5)             # prints 10
x = double_print(5)         # still prints 10, but x is None!
print(x)                    # None

# double_return is flexible:
y = double_return(5)        # y = 10
print(y + 3)                # 13
print(double_return(5) * double_return(3))   # 10 * 6 = 60

# ── Early return ───────────────────────────────────────────
def check_age(age):
    if age < 0:
        return "Invalid age"
    if age < 18:
        return "Minor"
    if age < 65:
        return "Adult"
    return "Senior"

print(check_age(16))    # Minor
print(check_age(30))    # Adult
print(check_age(-5))    # Invalid age

# ── Chaining function calls ────────────────────────────────
def add(a, b):
    return a + b

def double(n):
    return n * 2

print(double(add(3, 4)))   # double(7) = 14
print(add(double(2), double(3)))  # add(4, 6) = 10
```

### Practice Problems — Day 3

**Beginner:**
1. Write `cube(n)` that *returns* n³. Print the result of calling it with 4.
2. Write `is_even(n)` that returns `True` if n is even, `False` otherwise.

**Intermediate:**

3. Write `max_of_two(a, b)` that returns the larger of two numbers (without using `max()`).
4. Write `celsius_to_fahrenheit(c)` that returns the converted temperature. Then write `fahrenheit_to_celsius(f)` that does the reverse. Show that converting back gives the original value.

**Challenge:**

5. Write `grade_letter(score)` that returns `"A"` (90–100), `"B"` (80–89), `"C"` (70–79), `"D"` (60–69), or `"F"` (below 60). Then write `grade_report(name, score)` that *calls* `grade_letter` and returns a formatted string like `"Alice earned a B (85)."`.

<details>
<summary>💡 Hint for #5</summary>
Write `grade_letter` first and test it. Then call it inside `grade_report`:

```python
def grade_report(name, score):
    letter = grade_letter(score)
    return f"{name} earned a {letter} ({score})."
```
</details>

---