# Vocabulary & Quick Reference

**Key Terms:**
- **Algorithm:** Step-by-step procedure to solve a problem
- **Data Type:** Category of data (str, int, float, bool)
- **Variable:** Named container storing a value
- **Input:** Information the user gives to the program
- **Output:** Information the program displays to the user
- **Syntax:** Rules for writing code correctly
- **Comment:** Explanation in code, ignored by Python, starts with #
- **Function:** Reusable block of code (intro only; more in Unit 5)

**Key Syntax:**
```python
# Comments
print("Output text")                    # Display output
variable = value                        # Create/assign variable
name = input("Prompt: ")               # Get user input
type(value)                             # Check data type
x = int(input("Number: "))             # Get and convert input
print(f"Hello {name}, you are {age}")  # F-string formatting
round(3.14159, 2)                      # Round to 2 decimals
```

**Arithmetic Operators:**
- `+` add, `-` subtract, `*` multiply, `/` divide, `//` floor divide, `%` remainder, `**` exponent
- ---

**Quick Formula Reference:**
- Temperature: C = (F - 32) × 5/9
- Area of rectangle: length × width
- Perimeter of rectangle: 2 × length + 2 × width
---
## Common Mistakes & How to Fix Them
| Mistake | What Happens | Fix |
|---------|--------------|-----|
| `Print("Hello")` instead of `print()` | NameError: uppercase P | Remember Python is case-sensitive; use `print()` (lowercase) |
| `name = input()` then `print(name + 5)` | TypeError: can't add str and int | Convert input: `name = int(input())` or `print(str(5))` |
| `print(Hello)` without quotes | NameError: name 'Hello' undefined | Strings need quotes: `print("Hello")` |
| `age = "17"` then use in math | Result is string concatenation, not math | Convert: `age = int(input(...))` or use `int("17")` |
| Using spaces in variable names: `my age = 25` | SyntaxError: invalid syntax | Use underscores: `my_age = 25` |
| `print 5` instead of `print(5)` | SyntaxError: missing parentheses | Python 3 requires parentheses: `print(5)` |
| Forgetting to convert `input()` | Can't do math on strings | Always use `int()` or `float()`: `num = int(input("Number: "))` |

---