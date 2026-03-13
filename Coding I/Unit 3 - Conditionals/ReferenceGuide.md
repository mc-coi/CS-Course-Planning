# Vocabulary & Quick Reference

**Key Terms:**
- **Condition:** Expression that evaluates to True or False
- **Boolean:** Data type with values True or False
- **Logical operator:** and, or, not
- **Nested:** One structure inside another (if inside if)
- **Indentation:** Spacing that defines code blocks in Python
- **Mutually exclusive:** Only one path can execute

**Key Syntax:**
```python
if condition:
    # code runs if True

if condition:
    # runs if True
else:
    # runs if False

if condition1:
    # if True
elif condition2:
    # else if condition2 True
elif condition3:
    # else if condition3 True
else:
    # catch all remaining

# Logical operators
condition1 and condition2    # both True
condition1 or condition2     # at least one True
not condition               # reverse

# Chained comparison
1 <= x <= 100              # x is between 1 and 100

# Common patterns
if value in [1, 2, 3]:     # check if in list
if "substring" in "text":  # check if substring exists
if not is_valid:           # check if False
```
## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Using `=` instead of `==`: `if x = 5:` | SyntaxError | Use `==` for comparison: `if x == 5:` |
| Forgetting colon: `if x > 5` | SyntaxError: expected ':' | Add colon: `if x > 5:` |
| Wrong indentation | IndentationError or logic error | Indent exactly 4 spaces after `if` |
| Using `and` instead of `or`: `if day == "Sat" and day == "Sun":` | Condition never True | Use `or`: one variable can't be two values |
| Forgetting `elif`/`else` paths execute | One True condition prints multiple times | Use `elif` or `else` to make conditions mutually exclusive |
| Off-by-one: `if score > 90:` but should include 90 | Score of 90 doesn't qualify | Use `>=` instead of `>` |
| Testing conditions in wrong order | Earlier True condition runs | Put most specific conditions first in elif |

---
