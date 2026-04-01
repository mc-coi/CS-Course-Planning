# Vocabulary & Quick Reference

| Term | Definition |
|------|-----------|
| **Function** | A named, reusable block of code |
| **`def`** | Keyword to define a function |
| **Parameter** | Variable in function definition (placeholder) |
| **Argument** | Value passed to function at call time |
| **`return`** | Keyword to send a value back to the caller |
| **`None`** | Default return value when no `return` is used |
| **Local variable** | Variable defined inside a function; only visible there |
| **Global variable** | Variable defined outside all functions |
| **Scope** | The region of code where a variable is accessible |
| **Default parameter** | Parameter with a preset value if none is given |
| **Keyword argument** | Argument passed by name: `func(b=5, a=3)` |
| **Tuple** | Ordered, immutable sequence — used for multiple returns |
| **Modular design** | Breaking programs into small, single-purpose functions |
| **Single responsibility** | Each function does exactly one thing |
| **Function call** | Running a function by writing its name with `()` |

### Syntax Quick Reference

```python
# Define a function
def function_name(param1, param2, param3="default"):
    # function body
    return value

# Call a function
result = function_name(arg1, arg2)
result = function_name(arg1, arg2, param3="custom")

# Multiple return values
def get_both(items):
    return min(items), max(items)

low, high = get_both([3, 1, 7])

# Check function output
print(function_name(test_value))
```

## Common Mistakes

| Mistake | What Goes Wrong | Fix |
|---------|----------------|-----|
| Missing colon after `def` | `SyntaxError` | `def greet(name):` — always end with `:` |
| Calling function before defining | `NameError` | Move `def` above the call |
| Wrong argument count | `TypeError` | Count parameters and match them |
| Using `print` when you mean `return` | Gets `None` | Change `print(result)` to `return result` |
| Using local variable outside function | `NameError` | Pass value out with `return` |
| Modifying global inside function | Hard-to-find bugs | Use `global` only when truly necessary |
| Forgetting to store return value | Value is lost | `result = my_function()` |
| Default param before required | `SyntaxError` | Required params first, defaults last |
| Not returning `False` case | Returns `None` | Always `return` a value in every branch |
| Too many jobs in one function | Hard to debug | One function = one job |

---