# Unit 5: Functions & Modularity
> Create reusable code blocks and build modular applications with functions.

# Unit Overview
- **Duration:** 9 days / 3 weeks (Days 34–42)
- **Key Concepts:** Function definition, parameters, return values, variable scope, default parameters, multiple returns, modularity
- **Big Idea:** Functions let you write code once and reuse it anywhere — breaking big problems into small, manageable pieces is the foundation of professional programming
- **TN Standards Addressed:** Functions, modularity, parameter passing, return values, scope

# Learning Targets
- I can define functions and call them multiple times
- I can write functions with parameters and use them correctly
- I can return values from functions and use them in expressions
- I can explain variable scope (local vs. global)
- I can design modular programs where each function has one job
- I can use default parameters and keyword arguments
- I can return multiple values using tuples
- I can pass lists and other data structures as function arguments
- I can build a complete modular application using functions

---

# Day 1: Defining & Calling Functions

### Key Concepts
A **function** is a named, reusable block of code. You write it once and can run it many times by calling its name.

- `def` keyword starts a function definition
- The function body is indented
- Call a function by writing its name followed by `()`
- Functions without `return` statements return `None` automatically

### Why Functions?
Without functions, you repeat yourself. With functions, you write once, use everywhere — and fixing one bug fixes it everywhere it's used.

### Code Examples

```python
# ── Basic function ─────────────────────────────────────────
def greet():
    print("Hello, world!")

greet()   # Hello, world!
greet()   # Hello, world!
greet()   # Hello, world!  (called 3 times — same code reused)

# ── Function with a parameter ──────────────────────────────
def greet_person(name):
    print(f"Hello, {name}!")

greet_person("Alice")   # Hello, Alice!
greet_person("Bob")     # Hello, Bob!
greet_person("Ms. Smith")  # Hello, Ms. Smith!

# ── Function with multiple parameters ──────────────────────
def introduce(first_name, grade):
    print(f"Hi! I'm {first_name} and I'm in grade {grade}.")

introduce("Carlos", 9)
introduce("Priya", 10)

# ── What happens without calling the function? ─────────────
def say_bye():
    print("Goodbye!")

# say_bye   <-- This does NOT call it; it just refers to the function object
say_bye()    # <-- This calls it
```

### Practice Problems — Day 1

**Beginner:**
1. Define a function called `print_name` that prints your name. Call it 3 times.
2. Define a function called `draw_line` that prints `"----------"`. Call it 5 times.

**Intermediate:**
3. Write a function `announce(subject)` that prints `"Now studying: <subject>"`. Test it with three different subjects.
4. Write a function `print_header(title)` that prints a row of `=` signs, then the title, then another row of `=` signs.

**Challenge:**
5. Write a function `countdown(start)` that prints numbers from `start` down to 1, then prints `"Blastoff!"`.

<details>
<summary>💡 Hint for #4</summary>

```python
def print_header(title):
    border = "=" * len(title)
    print(border)
    print(title)
    print(border)
```
</details>

<details>
<summary>✅ Answer for #5</summary>

```python
def countdown(start):
    for i in range(start, 0, -1):
        print(i)
    print("Blastoff!")

countdown(5)
```
</details>

---

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

# Day 5: Modular Design

### Key Concepts
- **Modular design:** Breaking a program into small functions, each with one job
- **Single responsibility:** Each function should do exactly one thing well
- Makes code easier to read, test, fix, and reuse
- Good function names describe *what* the function does

### Signs of Good Modular Design
| Good | Bad |
|------|-----|
| Short functions (5–15 lines) | One huge function (50+ lines) |
| Descriptive names | `f1()`, `do_stuff()` |
| Each function does one thing | Functions that do everything |
| Functions call other functions | Repeated code everywhere |
| Easy to test each piece | Can only test the whole thing |

### Code Examples

```python
# ── BEFORE modular design (everything in one place) ────────
def run_program():
    name = input("Name: ")
    score = float(input("Score: "))
    if score >= 90:
        grade = "A"
    elif score >= 80:
        grade = "B"
    elif score >= 70:
        grade = "C"
    elif score >= 60:
        grade = "D"
    else:
        grade = "F"
    print(f"\nStudent: {name}")
    print(f"Score:   {score}")
    print(f"Grade:   {grade}")

# ── AFTER modular design (each job has its own function) ───
def get_student_info():
    name = input("Name: ")
    score = float(input("Score: "))
    return name, score

def calculate_grade(score):
    if score >= 90: return "A"
    if score >= 80: return "B"
    if score >= 70: return "C"
    if score >= 60: return "D"
    return "F"

def print_report(name, score, grade):
    print(f"\nStudent: {name}")
    print(f"Score:   {score}")
    print(f"Grade:   {grade}")

def run_program():
    name, score = get_student_info()
    grade = calculate_grade(score)
    print_report(name, score, grade)

run_program()

# ── Building a modular temperature converter ───────────────
def celsius_to_fahrenheit(c):
    return (c * 9/5) + 32

def fahrenheit_to_celsius(f):
    return (f - 32) * 5/9

def celsius_to_kelvin(c):
    return c + 273.15

def get_temperature():
    return float(input("Enter temperature in Celsius: "))

def show_all_conversions(celsius):
    f = celsius_to_fahrenheit(celsius)
    k = celsius_to_kelvin(celsius)
    print(f"\n{celsius}°C = {f:.1f}°F = {k:.2f}K")

def main():
    celsius = get_temperature()
    show_all_conversions(celsius)

main()
```

### Practice Problems — Day 5

**Beginner:**
1. Take the following one-big-function code and split it into 3 smaller functions:
```python
def calculate():
    a = float(input("First number: "))
    b = float(input("Second number: "))
    result = a + b
    print(f"Sum: {result}")
    if result > 100:
        print("That's a big number!")
```

**Intermediate:**
2. Write a modular tip calculator with separate functions for: getting the bill amount, getting the tip percentage, calculating the tip, and printing the final receipt.

**Challenge:**
3. Write a modular number guessing game where each step is its own function: generating a random number, getting a valid guess, giving a hint (too high/too low), and checking if the player won. The `main()` function should call these in the right order.

---

# Day 6: Functions with Lists

### Key Concepts
- Lists can be passed as arguments just like numbers and strings
- Functions can process, filter, transform, and analyze list data
- Returning a new list is cleaner than modifying the original (in most cases)
- You can build list-processing functions that work for any list

### Code Examples

```python
# ── Pass a list to a function ──────────────────────────────
def print_all(items):
    for item in items:
        print(f"  - {item}")

fruits = ["apple", "banana", "cherry"]
print_all(fruits)

# ── Calculate stats on a list ──────────────────────────────
def list_sum(numbers):
    total = 0
    for n in numbers:
        total += n
    return total

def list_average(numbers):
    if len(numbers) == 0:
        return 0
    return list_sum(numbers) / len(numbers)

def list_max(numbers):
    biggest = numbers[0]
    for n in numbers:
        if n > biggest:
            biggest = n
    return biggest

def list_min(numbers):
    smallest = numbers[0]
    for n in numbers:
        if n < smallest:
            smallest = n
    return smallest

scores = [85, 92, 78, 95, 88, 73, 90]
print(f"Sum:     {list_sum(scores)}")
print(f"Average: {list_average(scores):.1f}")
print(f"Max:     {list_max(scores)}")
print(f"Min:     {list_min(scores)}")

# ── Return a new filtered list ─────────────────────────────
def passing_scores(scores, threshold=70):
    passing = []
    for s in scores:
        if s >= threshold:
            passing.append(s)
    return passing

grades = [55, 82, 70, 91, 44, 78, 65]
print(passing_scores(grades))        # [82, 70, 91, 78]
print(passing_scores(grades, 80))    # [82, 91]

# ── Modify a list in-place ─────────────────────────────────
def double_all(numbers):
    for i in range(len(numbers)):
        numbers[i] *= 2   # modifies the original list!

data = [1, 2, 3, 4, 5]
double_all(data)
print(data)    # [2, 4, 6, 8, 10]

# ── Return a transformed version (no mutation) ─────────────
def doubled_copy(numbers):
    return [n * 2 for n in numbers]

original = [1, 2, 3, 4, 5]
new_list = doubled_copy(original)
print(original)   # [1, 2, 3, 4, 5]  (unchanged)
print(new_list)   # [2, 4, 6, 8, 10]
```

### Practice Problems — Day 6

**Beginner:**
1. Write `count_evens(numbers)` that returns how many even numbers are in the list.
2. Write `all_caps(words)` that returns a new list with every string converted to uppercase.

**Intermediate:**
3. Write `remove_negatives(numbers)` that returns a new list with all negative numbers removed.
4. Write `grade_stats(scores)` that prints the average, highest, lowest, and number of passing scores (≥70) for a list of grades.

**Challenge:**
5. Write `normalize(numbers)` that returns a new list where every number is scaled to a 0–100 range: `normalized = (value - min) / (max - min) * 100`. Handle the case where all numbers are the same.

<details>
<summary>✅ Answer for #5</summary>

```python
def normalize(numbers):
    mn = min(numbers)
    mx = max(numbers)
    if mx == mn:
        return [50.0] * len(numbers)  # all same, use midpoint
    return [(n - mn) / (mx - mn) * 100 for n in numbers]

print(normalize([10, 20, 30, 40, 50]))
# [0.0, 25.0, 50.0, 75.0, 100.0]
```
</details>

---

# Day 7: Default Parameters & Multiple Returns

### Key Concepts
- **Default parameter:** A parameter with a pre-set value if no argument is given
- **Multiple return values:** A function can return multiple values as a tuple
- You can unpack returned tuples directly into separate variables

### Code Examples

```python
# ── Default parameters ─────────────────────────────────────
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")              # Hello, Alice!  (uses default)
greet("Bob", "Good morning")  # Good morning, Bob!  (overrides default)
greet("Carlos", "Hola")    # Hola, Carlos!

# ── Multiple defaults ──────────────────────────────────────
def create_profile(name, grade=9, sport="none", gpa=0.0):
    print(f"Name: {name}, Grade: {grade}, Sport: {sport}, GPA: {gpa}")

create_profile("Destiny")
create_profile("Marcus", grade=11)
create_profile("Priya", 10, "soccer", 3.9)
create_profile("Jordan", sport="basketball", gpa=3.5)

# Default params must come AFTER required params
# def bad(default=5, required):  ← SyntaxError!

# ── Returning multiple values ──────────────────────────────
def min_max(numbers):
    return min(numbers), max(numbers)    # returns a tuple

result = min_max([3, 1, 7, 2, 8])
print(result)           # (1, 8)
print(type(result))     # <class 'tuple'>

# ── Unpacking the tuple ────────────────────────────────────
low, high = min_max([3, 1, 7, 2, 8])
print(f"Min: {low}, Max: {high}")   # Min: 1, Max: 8

# ── Real-world example ─────────────────────────────────────
def analyze_scores(scores):
    total = sum(scores)
    average = total / len(scores)
    highest = max(scores)
    lowest = min(scores)
    passing = sum(1 for s in scores if s >= 70)
    return average, highest, lowest, passing

grades = [85, 92, 78, 55, 90, 67, 88]
avg, hi, lo, passed = analyze_scores(grades)
print(f"Average: {avg:.1f}")
print(f"Highest: {hi}, Lowest: {lo}")
print(f"Passing: {passed}/{len(grades)}")

# ── Divmod: built-in multiple return ──────────────────────
quotient, remainder = divmod(17, 5)
print(f"17 ÷ 5 = {quotient} remainder {remainder}")   # 3 remainder 2
```

### Practice Problems — Day 7

**Beginner:**
1. Write `power(base, exponent=2)` that returns `base ** exponent`. Test with both one and two arguments.
2. Write `get_range(numbers)` that returns both the minimum and maximum of a list as a tuple.

**Intermediate:**
3. Write `split_list(items, split_point=None)` where if `split_point` is `None`, it splits at the midpoint. Return two lists.
4. Write `stats(numbers)` that returns a tuple of (mean, median, mode). Use a helper function for each.

**Challenge:**
5. Write `parse_name(full_name)` that returns `(first, middle, last)` handling names with 2 words (no middle name — return `""` for middle) and 3+ words. Test with `"John Doe"`, `"Mary Jane Watson"`, and `"Cher"`.

---

# Day 8: Debugging Functions

### Key Concepts
Common function-related bugs and how to fix them:
- **Calling before defining:** `def` must come before the call in the file
- **Wrong number of arguments:** Count params in `def` — match at call
- **Missing return:** Function gives `None` when you expected a value
- **Using return value of a `print`-only function:** Gets `None`
- **Scope errors:** Using a local variable outside its function
- **Infinite recursion:** A function that calls itself without stopping

### Code Examples

```python
# ── Bug 1: Forgot to return ────────────────────────────────
def add(a, b):
    result = a + b
    # forgot return!

answer = add(3, 5)
print(answer)   # None  ← Bug! Should be 8

# Fix:
def add(a, b):
    return a + b     # ← add return

# ── Bug 2: Using None from a print function ─────────────────
def double(n):
    print(n * 2)    # prints but returns None

x = double(5)      # prints 10
print(x * 3)       # TypeError: unsupported operand type(s): NoneType * int

# Fix: change print to return
def double(n):
    return n * 2

# ── Bug 3: Wrong number of arguments ──────────────────────
def greet(name, greeting):
    print(f"{greeting}, {name}!")

# greet("Alice")         # ❌ TypeError: missing 1 required positional argument
# greet("Alice", "Hi", "Extra")  # ❌ TypeError: takes 2 positional arguments but 3 were given
greet("Alice", "Hello")  # ✅

# ── Bug 4: NameError — using local variable outside ────────
def calculate():
    subtotal = 100
    tax = subtotal * 0.08
    # doesn't return anything

calculate()
# print(subtotal)   # ❌ NameError: subtotal not defined

# Fix:
def calculate():
    subtotal = 100
    tax = subtotal * 0.08
    return subtotal + tax

total = calculate()
print(total)    # 108.0

# ── Bug 5: Missing colon ───────────────────────────────────
# def greet(name)    # ❌ SyntaxError: expected ':'
#     print(name)

def greet(name):    # ✅ colon required
    print(name)

# ── Debugging strategy: trace with print ──────────────────
def mystery(n):
    print(f"  mystery called with n={n}")   # trace input
    result = n * 2 + 5
    print(f"  returning {result}")           # trace output
    return result

x = mystery(7)
print(x)
# Remove trace prints once fixed
```

### Fix the Bug Exercises

Fix each buggy function below:

```python
# Bug A: What's wrong?
def multiply(a, b)
    return a * b

# Bug B: What's wrong?
def is_positive(n):
    if n > 0:
        return True

result = is_positive(-5)
print("Positive:", result)   # prints: Positive: None

# Bug C: What's wrong?
def format_name(first, last):
    full = first + " " + last
    print(full)

name = format_name("John", "Smith")
greeting = "Hello, " + name   # TypeError!
print(greeting)
```

<details>
<summary>✅ Answers to Bug A, B, C</summary>

```python
# Bug A: Missing colon
def multiply(a, b):
    return a * b

# Bug B: Missing return for False case
def is_positive(n):
    if n > 0:
        return True
    return False   # ← add this

# Bug C: Should return, not print
def format_name(first, last):
    return first + " " + last   # ← change print to return

name = format_name("John", "Smith")
greeting = "Hello, " + name
print(greeting)
```
</details>

---

# Day 9: Unit 5 Project — Modular Application

### Project Options

**Option A — Grade Calculator**
Build a modular grade calculator with:
- `get_scores()` — collect scores from user until they type "done"
- `calculate_average(scores)` — return the average
- `letter_grade(average)` — return A/B/C/D/F
- `print_report(name, scores, average, grade)` — formatted output
- `main()` — orchestrates everything

**Option B — Modular Quiz Game**
Build a modular quiz with:
- `load_questions()` — return a list of question dictionaries
- `ask_question(q)` — display and return whether answered correctly
- `run_quiz(questions)` — loop through all questions
- `show_results(correct, total)` — display final score and grade
- `main()` — ties it together

**Option C — Simple Number Cruncher**
Build a modular stats program with:
- `get_numbers()` — collect numbers from user
- `calculate_sum(numbers)` — return total
- `calculate_average(numbers)` — return mean
- `find_outliers(numbers, threshold)` — return values far from average
- `print_stats(numbers)` — display all stats neatly
- `main()` — run everything

### Template to Get Started

```python
# ── Unit 5 Project: [YOUR TITLE HERE] ─────────────────────

def main():
    # This function runs the whole program
    # Step 1: Get input
    # Step 2: Process
    # Step 3: Display results
    pass

# Define your helper functions here:

def get_input():
    pass

def process_data(data):
    pass

def display_results(results):
    pass

# Run the program:
main()
```

### Evaluation Checklist
- [ ] At least 4 functions defined
- [ ] Each function has exactly one job
- [ ] At least one function uses parameters
- [ ] At least one function uses `return`
- [ ] `main()` ties everything together
- [ ] No global variables (use parameters/returns)
- [ ] Code is readable with clear variable names
- [ ] Program runs without errors

---

##  Unit 5 Practice Bank (15 Problems)

### Tier 1 — Beginner

**P1.** Write `say_hello(name)` that prints `"Hello, <name>!"`. Call it three times with different names.

**P2.** Write `square(n)` that *returns* n². Store the result in a variable and print it.

**P3.** Write `is_odd(n)` that returns `True` if n is odd, `False` if even.

**P4.** Write `full_name(first, last)` that returns the full name as a string.

**P5.** Write `bigger(a, b)` that returns the larger of two numbers.

### Tier 2 — Intermediate

**P6.** Write `clamp(value, low, high)` that returns `low` if value < low, `high` if value > high, and value otherwise.

<details>
<summary>💡 Hint for P6</summary>

```python
def clamp(value, low, high):
    if value < low:
        return low
    if value > high:
        return high
    return value
```
</details>

**P7.** Write `count_vowels(text)` that returns the number of vowels in a string.

**P8.** Write `list_stats(numbers)` that returns a tuple of (sum, average, min, max).

**P9.** Write `temperature_converter(temp, scale="C")` where scale can be `"C"` (convert to F) or `"F"` (convert to C). Use a default parameter.

**P10.** Write three functions: `add(a, b)`, `subtract(a, b)`, `multiply(a, b)`, then write `calculate(a, op, b)` that calls the appropriate function based on op (`"+"`, `"-"`, `"*"`).

### Tier 3 — Challenge

**P11.** Write a modular word counter: `get_text()` prompts for input, `count_words(text)` returns word count, `count_unique(text)` returns count of unique words, `print_word_report(text)` calls and displays both.

**P12.** Write `flatten(nested_list)` that takes a list of lists and returns a single flat list. E.g., `flatten([[1,2],[3,4],[5]])` → `[1,2,3,4,5]`.

**P13.** Write `run_length_encode(text)` that returns a list of `(char, count)` tuples. E.g., `"aaabbc"` → `[("a",3),("b",2),("c",1)]`.

**P14.** Write a modular Caesar cipher with: `encode_char(c, shift)`, `decode_char(c, shift)`, `encode_message(message, shift)`, `decode_message(message, shift)`.

**P15.** Complete modular ATM simulation: `check_balance(account)`, `deposit(account, amount)`, `withdraw(account, amount)` (return error message if insufficient funds), `transaction_menu(account)`, `main()`.

<details>
<summary>✅ Answer for P15 (starter)</summary>

```python
def check_balance(account):
    return account["balance"]

def deposit(account, amount):
    if amount <= 0:
        return "Invalid amount"
    account["balance"] += amount
    return f"Deposited ${amount:.2f}. New balance: ${account['balance']:.2f}"

def withdraw(account, amount):
    if amount <= 0:
        return "Invalid amount"
    if amount > account["balance"]:
        return "Insufficient funds"
    account["balance"] -= amount
    return f"Withdrew ${amount:.2f}. New balance: ${account['balance']:.2f}"

def transaction_menu(account):
    while True:
        print("\n1. Check Balance  2. Deposit  3. Withdraw  4. Exit")
        choice = input("Choose: ")
        if choice == "1":
            print(f"Balance: ${check_balance(account):.2f}")
        elif choice == "2":
            amt = float(input("Amount: "))
            print(deposit(account, amt))
        elif choice == "3":
            amt = float(input("Amount: "))
            print(withdraw(account, amt))
        elif choice == "4":
            print("Goodbye!")
            break

def main():
    account = {"name": "Student", "balance": 500.00}
    print(f"Welcome, {account['name']}!")
    transaction_menu(account)

main()
```
</details>

---

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

## Assessment Prep — Q&A

**Q1: What is the difference between a parameter and an argument?**
A parameter is the variable name in the `def` line. An argument is the actual value you pass when calling the function.

**Q2: What does a function return if there is no `return` statement?**
It returns `None`.

**Q3: Why is this code wrong? `def f(default=5, required): ...`**
Default parameters must come *after* required parameters. Should be: `def f(required, default=5):`.

**Q4: What is variable scope?**
Scope is where a variable is accessible. Local variables exist only inside their function. Global variables exist throughout the entire file.

**Q5: What's the output?**
```python
x = 10
def change():
    x = 99
change()
print(x)
```
Output: `10`. The `x = 99` inside `change()` creates a new *local* variable — the global `x` is untouched.

**Q6: How do you return multiple values?**
Separate them with commas: `return a, b, c`. Python automatically packages them as a tuple. Unpack with: `x, y, z = my_func()`.

**Q7: What does "single responsibility" mean?**
Each function should do exactly one thing. A function that validates input, calculates a result, and prints a report has too many responsibilities — split it into three functions.

**Q8: What's wrong here?**
```python
def double(n):
    print(n * 2)
x = double(5)
print(x + 1)
```
`double` prints but doesn't return, so `x` is `None`. `None + 1` causes a `TypeError`. Fix: use `return n * 2`.

**Q9: What is modular design and why does it matter?**
Modular design breaks programs into small, single-purpose functions. Benefits: easier to read, test, debug, reuse, and update code.

**Q10: When should you use the `global` keyword?**
Rarely. Only when a function truly needs to modify a global state. Usually better to pass values as parameters and return new values.

---

## Vocabulary & Quick Reference

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
