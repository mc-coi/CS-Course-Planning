# Day 2: Parameters & Arguments

### Key Concepts
- **Parameter:** The variable name in the function definition (placeholder)
- **Argument:** The actual value you pass when you call the function
- Functions can have multiple parameters — separate them with commas
- Order matters: arguments are matched to parameters by position

### Vocabulary
| Term | Definition | Example |
|------|-----------|---------|
| Parameter | Variable listed in `def` line | `def add(a, b):` → `a` and `b` |
| Argument | Value passed at call time | `add(3, 5)` → `3` and `5` |
| Positional arg | Matched by position (order matters) | `add(3, 5)` |
| Keyword arg | Matched by name (order flexible) | `add(b=5, a=3)` |

### Code Examples

```python
# ── One parameter ──────────────────────────────────────────
def square(n):
    result = n * n
    print(f"{n} squared = {result}")

square(4)    # 4 squared = 16
square(7)    # 7 squared = 49
square(12)   # 12 squared = 144

# ── Two parameters ─────────────────────────────────────────
def add(a, b):
    total = a + b
    print(f"{a} + {b} = {total}")

add(3, 5)       # 3 + 5 = 8
add(10, 20)     # 10 + 20 = 30
add(100, -45)   # 100 + -45 = 55

# ── Three parameters ───────────────────────────────────────
def describe_student(name, grade, gpa):
    print(f"{name} is in grade {grade} with a {gpa} GPA.")

describe_student("Aaliyah", 10, 3.8)

# ── Keyword arguments ──────────────────────────────────────
def power(base, exponent):
    print(f"{base}^{exponent} = {base ** exponent}")

power(2, 10)               # positional: base=2, exponent=10
power(base=2, exponent=10) # keyword: same result
power(exponent=3, base=5)  # keyword: order can change

# ── Common mistake: wrong number of arguments ───────────────
def multiply(x, y):
    print(x * y)

# multiply(4)        # ❌ TypeError: missing argument
# multiply(4, 5, 6)  # ❌ TypeError: too many arguments
multiply(4, 5)       # ✅ 20
```

### Practice Problems — Day 2

**Beginner:**
1. Write `greet(name, time_of_day)` that prints `"Good morning, Alice!"` or `"Good evening, Bob!"` depending on the arguments.
2. Write `area_rectangle(width, height)` that prints the area.

**Intermediate:**

3. Write `temperature_info(city, temp_f)` that prints the city and converts Fahrenheit to Celsius: `C = (F - 32) * 5/9`.
4. Write `bmi(weight_kg, height_m)` that prints the BMI value: `BMI = weight / height²`.

**Challenge:**

5. Write `make_box(char, width, height)` that prints a rectangle outline using the given character. Example: `make_box("*", 5, 3)` should print:
```
*****
*   *
*****
```

<details>
<summary>✅ Answer for #5</summary>

```python
def make_box(char, width, height):
    top_bottom = char * width
    middle = char + " " * (width - 2) + char
    print(top_bottom)
    for _ in range(height - 2):
        print(middle)
    print(top_bottom)

make_box("*", 5, 3)
```
</details>

---