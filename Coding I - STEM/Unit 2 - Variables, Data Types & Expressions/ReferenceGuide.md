## 🔑 Vocabulary & Quick Reference

**Key Terms:**
- **Casting:** Converting from one data type to another
- **Concatenation:** Joining strings with +
- **Slicing:** Extracting a portion of a string with [start:stop]
- **Method:** A function that belongs to a data type, used with dot notation
- **f-string:** Formatted string literal for clean output
- **Constant:** A variable that never changes (use ALL_CAPS)
- **Operator Precedence:** Order that operations are performed (PEMDAS)

**Key Operators & Methods:**
```python
# Compound assignment
+=, -=, *=, /=, //=

# Arithmetic
+, -, *, /, //, %, **

# String operations
concatenation (+), repetition (*), len(), indexing [n], slicing [a:b], [a:b:c]

# String methods
.upper(), .lower(), .title(), .strip(), .replace(), .split(), .find(), .count(), .startswith(), .endswith()

# Comparison
==, !=, <, >, <=, >=

# Type conversion
int(), float(), str(), bool()

# Formatting
f"text {variable}" or f"{value:.2f}"

# Math module
import math; math.sqrt(), math.pi, math.ceil(), math.floor()
```

**Common Formulas:**
- Circle area: π × r²
- Circle circumference: 2π × r
- Distance: √((x₂-x₁)² + (y₂-y₁)²)

---
## 🔍 Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Using `=` for comparison: `if x = 5:` | SyntaxError | Use `==` for comparison: `if x == 5:` |
| Forgetting quotes on string: `name = Alex` | NameError: Alex is undefined | Add quotes: `name = "Alex"` |
| `print("Hello" + 5)` | TypeError: can't add str and int | Convert: `print("Hello " + str(5))` |
| `name[0] = "J"` — trying to change string | TypeError: 'str' is immutable | Strings can't be changed; create new: `name = "J" + name[1:]` |
| Using wrong quotes: `name = "Alex'` | SyntaxError: unterminated string | Match quotes: `name = "Alex"` or `name = 'Alex'` |
| `int("3.14")` — trying to convert float string to int | ValueError | Convert to float first: `int(float("3.14"))` |
| Division returns float: `10 / 2` gives `5.0` not `5` | Not really an error, but unexpected | Use `//` for integer division: `10 // 2` returns `5` |
| Forgetting `import math` then using `math.sqrt()` | NameError: name 'math' is undefined | Add `import math` at the top |

---