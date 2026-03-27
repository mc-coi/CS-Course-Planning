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