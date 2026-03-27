# Day 1: Types of Errors & Debugging Strategies

### Key Concepts

Every bug fits into one of three categories:

| Error Type | When It Appears | Description | Example |
|-----------|----------------|-------------|---------|
| **Syntax Error** | Before running | Code breaks the rules of Python | Missing colon, wrong indent |
| **Runtime Error** | While running | Legal code causes a crash | Dividing by 0, using undefined variable |
| **Logic Error** | While running (no crash) | Program runs but gives wrong answer | Off-by-one, wrong operator |

### Common Runtime Errors (Exceptions)

| Exception | Cause | Example |
|-----------|-------|---------|
| `NameError` | Using undefined variable | `print(x)` when x never set |
| `TypeError` | Wrong data type | `"hello" + 5` |
| `ValueError` | Right type, wrong value | `int("hello")` |
| `ZeroDivisionError` | Dividing by zero | `10 / 0` |
| `IndexError` | List index out of range | `mylist[99]` on a 3-element list |
| `FileNotFoundError` | File doesn't exist | `open("missing.txt")` |
| `AttributeError` | Method doesn't exist | `"hello".push("!")` |
| `KeyError` | Dict key doesn't exist | `mydict["bad_key"]` |

### Debugging Strategies

1. **Read the error message** — it tells you the line number and type
2. **Add print statements** — trace what values actually are
3. **Check assumptions** — is that variable really what you think it is?
4. **Rubber duck debugging** — explain your code out loud line by line
5. **Isolate the problem** — comment out sections to narrow it down
6. **Check edge cases** — what happens with 0, empty list, very large numbers?

### Code Examples

```python
# ── Syntax Error (Python won't even start) ─────────────────
# for i in range(10)     # ❌ SyntaxError: expected ':'
#     print(i)           # ❌ IndentationError

# ── Runtime Error (crashes during execution) ───────────────
x = int("hello")         # ❌ ValueError: invalid literal for int()
nums = [1, 2, 3]
print(nums[10])          # ❌ IndexError: list index out of range
print(10 / 0)            # ❌ ZeroDivisionError

# ── Logic Error (runs, but answer is wrong) ────────────────
# Goal: sum of 1 to 10
total = 0
for i in range(10):      # BUG: should be range(1, 11)
    total = i            # BUG: should be total += i
print(total)             # prints 9, not 55

# ── Fixed version ──────────────────────────────────────────
total = 0
for i in range(1, 11):   # 1 through 10 inclusive
    total += i            # accumulate
print(total)             # 55 ✅

# ── Debugging with print statements ───────────────────────
def calculate_bonus(sales, rate):
    print(f"DEBUG: sales={sales}, rate={rate}")   # trace inputs
    bonus = sales * rate
    print(f"DEBUG: bonus={bonus}")                 # trace output
    return bonus

result = calculate_bonus(5000, 0.1)
print(f"Bonus: ${result}")

# Remove DEBUG lines once problem is found
```

### Find & Fix the Bugs

```python
# Problem 1: Find all bugs
def average(numbers)
    total = 0
    for n in numbers
        total = total + n
    return total / len(numbers)

# Problem 2: Logic error — what's wrong?
def is_teenager(age):
    if age > 12 and age < 18:
        return True
    return False
# Test: is_teenager(18) should return False... does it?

# Problem 3: What error will this produce?
name = "Alice"
score = 95
print("Name: " + name + ", Score: " + score)
```

<details>
<summary>✅ Answers</summary>

```python
# Problem 1 fixes:
def average(numbers):            # added colon
    total = 0
    for n in numbers:            # added colon
        total = total + n
    return total / len(numbers)

# Problem 2: is actually correct — 18 is NOT a teenager
# is_teenager(18) → (18 > 12 and 18 < 18) → (True and False) → False ✅

# Problem 3: TypeError — can't concatenate str and int
# Fix:
print(f"Name: {name}, Score: {score}")
# OR
print("Name: " + name + ", Score: " + str(score))
```
</details>

---