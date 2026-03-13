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