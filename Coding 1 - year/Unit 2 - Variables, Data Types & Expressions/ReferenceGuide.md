# Unit 2 Reference Guide — Quick Lookup

## Data Types Summary

| Type | Example | Notes |
|------|---------|-------|
| `int` | `42`, `-5`, `0` | Whole numbers; division `/` returns float |
| `float` | `3.14`, `-0.5`, `2.0` | Decimals; always has decimal point |
| `str` | `"hello"`, `'world'` | Text in quotes; immutable (can't change individual chars) |
| `bool` | `True`, `False` | Must be capitalized; used in conditionals |

## Operators & Precedence

**Order of Operations: PEMDAS**
1. Parentheses `()`
2. Exponents `**`
3. Multiplication `*`, Division `/`, `//`, Modulo `%` (left-to-right)
4. Addition `+`, Subtraction `-` (left-to-right)

### Arithmetic Operators

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `5 - 3` | `2` |
| `*` | Multiplication | `5 * 3` | `15` |
| `/` | Division | `5 / 2` | `2.5` (float!) |
| `//` | Floor Division | `5 // 2` | `2` (int) |
| `%` | Modulo (remainder) | `5 % 2` | `1` |
| `**` | Exponentiation | `2 ** 3` | `8` |

### Comparison Operators (return Boolean)

| Operator | Meaning | Example |
|----------|---------|---------|
| `==` | Equal to | `5 == 5` → `True` |
| `!=` | Not equal | `5 != 3` → `True` |
| `>` | Greater than | `5 > 3` → `True` |
| `<` | Less than | `5 < 3` → `False` |
| `>=` | Greater or equal | `5 >= 5` → `True` |
| `<=` | Less or equal | `5 <= 3` → `False` |

### Assignment & Compound Operators

| Operator | Equivalent | Example |
|----------|-----------|---------|
| `=` | Assignment | `x = 5` |
| `+=` | Add and assign | `x += 3` means `x = x + 3` |
| `-=` | Subtract and assign | `x -= 2` means `x = x - 2` |
| `*=` | Multiply and assign | `x *= 2` means `x = x * 2` |
| `/=` | Divide and assign | `x /= 2` means `x = x / 2` |
| `//=` | Floor divide and assign | `x //= 2` means `x = x // 2` |
| `%=` | Modulo and assign | `x %= 3` means `x = x % 3` |
| `**=` | Exponentiate and assign | `x **= 2` means `x = x ** 2` |

## String Operations

### Basic Operations

```python
# Concatenation (joining)
"Hello" + " " + "World"  # "Hello World"

# Repetition (repeating)
"Ha" * 3  # "HaHaHa"

# Length
len("hello")  # 5

# Indexing (accessing single character)
"hello"[0]   # "h" (first)
"hello"[-1]  # "o" (last)
"hello"[-2]  # "l" (second-to-last)

# Slicing (extracting portion)
"hello"[1:4]    # "ell" (indices 1,2,3)
"hello"[:3]     # "hel" (from start to 3)
"hello"[2:]     # "llo" (from 2 to end)
"hello"[::2]    # "hlo" (every 2nd character)
"hello"[::-1]   # "olleh" (reversed)
```

### String Methods (called with dot notation)

**Case Conversion:**
```python
s.upper()      # "HELLO"
s.lower()      # "hello"
s.title()      # "Hello" (capitalize each word)
```

**Cleaning & Modification:**
```python
s.strip()      # Remove leading/trailing whitespace
s.replace(old, new)  # Replace substring
s.split()      # Split into list of words
```

**Searching & Counting:**
```python
s.find(sub)    # Index where substring starts (-1 if not found)
s.count(sub)   # How many times substring appears
s.startswith(pre)  # True if starts with prefix
s.endswith(suf)    # True if ends with suffix
```

## Type Conversion Functions

```python
int("42")        # 42 (string to int)
int(3.7)         # 3 (float to int, truncates)
float("3.14")    # 3.14 (string to float)
float(5)         # 5.0 (int to float)
str(42)          # "42" (int to string)
str(3.14)        # "3.14" (float to string)
bool(0)          # False (0 is falsy)
bool(1)          # True (non-zero is truthy)
bool("")         # False (empty string is falsy)
bool("hello")    # True (non-empty is truthy)
```

## F-String Formatting

```python
name = "Alice"
age = 25

# Basic interpolation
f"Name: {name}, Age: {age}"  # "Name: Alice, Age: 25"

# Decimal places
f"{3.14159:.2f}"  # "3.14" (2 decimal places)
f"{9.5:.2f}"      # "9.50"
f"${price:.2f}"   # "$9.50"

# Thousands separator
f"{1234567:,.2f}"  # "1,234,567.00"

# Alignment (width=10)
f"{word:>10}"     # Right-aligned
f"{word:<10}"     # Left-aligned
f"{word:^10}"     # Centered

# Percentage
f"{0.856:.1%}"    # "85.6%"

# Expressions in f-strings
f"Sum: {5 + 3}"   # "Sum: 8"
f"Average: {(a+b)/2:.1f}"  # Formatted expression
```

## Math Module

**Must `import math` first**

```python
import math

math.sqrt(16)      # 4.0 (square root)
math.pow(2, 8)     # 256.0 (2 to power 8)
math.ceil(3.2)     # 4 (round up)
math.floor(3.8)    # 3 (round down)
math.pi            # 3.14159...
math.e             # 2.71828...
math.fabs(-5)      # 5.0 (absolute value)
```

## Common Built-In Functions

```python
len(s)             # Length of string/list
abs(x)             # Absolute value
round(x, n)        # Round to n decimal places
max(a, b, c)       # Maximum value
min(a, b, c)       # Minimum value
type(x)            # Data type of x
print(x)           # Display output
input(prompt)      # Get user input (returns string)
```

## Naming Conventions

**Variables & Functions (snake_case):**
```python
user_name = "Alice"
calculate_total()
hours_worked = 40
```

**Constants (UPPER_CASE):**
```python
PI = 3.14159
MAX_ATTEMPTS = 5
SALES_TAX_RATE = 0.08
DEFAULT_NAME = "Guest"
```

## Common Mistakes to Avoid

| Mistake | Wrong | Right |
|---------|-------|-------|
| Assignment vs comparison | `if x = 5:` | `if x == 5:` |
| Division returns float | Expect `10/2 = 5` | Actually `10/2 = 5.0` |
| String indexing | `"hello"[1]` = "h" | `"hello"[1]` = "e" |
| Slice stop inclusive | `"hello"[0:4]` = "hello" | `"hello"[0:5]` = "hello" |
| String immutability | `s[0] = "x"` | `s = "x" + s[1:]` |
| Type mismatch | `"Score: " + 100` | `"Score: " + str(100)` |
| Forgot .strip() | `input()` might have spaces | `input().strip()` |
| Float precision | `0.1 + 0.2 == 0.3` | Use `round()` for comparison |
| Negative indices | Index -1 is first char | Index -1 is last char |
| Forgot import | `sqrt(16)` → error | `math.sqrt(16)` ✓ |
| Boolean capitalization | `true` and `false` | `True` and `False` |

## Quick Problem-Solving Steps

**For calculations:**
1. Identify inputs
2. Write the formula
3. Perform step-by-step (respect PEMDAS)
4. Round if necessary (especially money)
5. Format output with f-strings

**For string problems:**
1. Identify what you need (part of string, case, search)
2. Choose tool (indexing, slicing, method)
3. Remember: indexing starts at 0, slice stops are exclusive
4. Test with examples

**For programs:**
1. Get input
2. Convert types if needed (int(), float())
3. Validate input
4. Calculate
5. Format and display output

---

**Keep this reference handy while coding!**
