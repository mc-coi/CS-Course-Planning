# Day 4: Variable Scope

### Key Concepts
- **Scope** = where a variable can be seen and used
- **Local variable:** Defined inside a function — only visible inside that function
- **Global variable:** Defined outside all functions — visible everywhere
- Functions get their own "bubble" — changes inside don't affect the outside (unless you use `global`)
- Best practice: pass values in as parameters and return them — avoid `global`

### Code Examples

```python
# ── Local scope ────────────────────────────────────────────
def my_function():
    local_var = "I only exist inside!"
    print(local_var)   # works fine

my_function()
# print(local_var)   # ❌ NameError: local_var not defined here

# ── Global scope ───────────────────────────────────────────
school_name = "Westside High"   # global variable

def show_school():
    print(school_name)          # can READ global variables

show_school()   # Westside High

# ── Local shadows global ───────────────────────────────────
x = 100   # global

def change_x():
    x = 999              # creates a NEW local x; does not change global
    print(f"Inside: x = {x}")

change_x()              # Inside: x = 999
print(f"Outside: x = {x}")  # Outside: x = 100  (global unchanged!)

# ── Using global keyword (use sparingly!) ──────────────────
counter = 0

def increment():
    global counter      # explicitly modify the global variable
    counter += 1

increment()
increment()
increment()
print(counter)   # 3

# ── Better approach: pass and return ──────────────────────
def increment_value(n):
    return n + 1

count = 0
count = increment_value(count)
count = increment_value(count)
count = increment_value(count)
print(count)   # 3  (same result, cleaner design)

# ── Scope example with same variable name ─────────────────
total = 0

def calculate_total(numbers):
    total = 0           # local total — separate from global
    for n in numbers:
        total += n
    return total        # returns local value

result = calculate_total([10, 20, 30])
print(result)   # 60
print(total)    # 0  (global total unchanged)
```

### Practice Problems — Day 4

**Beginner:**
1. Predict the output of this code before running it:
```python
x = "global"
def test():
    x = "local"
    print(x)
test()
print(x)
```

2. Write a function `reset_score()` that uses `global` to set a variable `score` to 0. Then write `add_points(pts)` that uses `global` to add `pts` to `score`. Demonstrate with a short game simulation.

**Intermediate:**

3. Explain why this code doesn't work as expected, and fix it:
```python
def add_tax(price):
    tax_rate = 0.08
    total = price + price * tax_rate

add_tax(50)
print(total)   # NameError!
```

4. Rewrite the following function so it doesn't use `global` but produces the same result:
```python
total = 0
def add_to_total(n):
    global total
    total += n
```

**Challenge:**

5. Write three functions: `make_counter()` — no, actually just simulate a counter using pass-and-return style: write `start_counter()` returning 0, `tick(n)` returning n+1, and `reset(n)` returning 0. Write a loop that ticks 10 times and prints the final count.

---