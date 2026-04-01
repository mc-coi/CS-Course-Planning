# Unit 5 Assessment: Functions and Modularity

## Part 1: Multiple Choice (Questions 1–5)

Choose the best answer for each question.

### Question 1
Which is the correct syntax for defining a function that takes one parameter?

a) `function add(x):`
b) `def add(x):`
c) `def add x:`
d) `func add(x):`

<details>
<summary>Answer</summary>

**b) `def add(x):`**

`def` is the keyword, followed by name, parentheses with parameters, and a colon.
</details>

---

### Question 2
What does this code print?

```python
def double(n):
    return n * 2

result = double(5)
print(result)
```

a) 5
b) 10
c) `None`
d) "double(5)"

<details>
<summary>Answer</summary>

**b) 10**

The function returns 5 * 2 = 10. The variable `result` gets 10, which is printed.
</details>

---

### Question 3
What is the difference between a parameter and an argument?

a) They are the same thing
b) A parameter is what you pass; an argument is in the function definition
c) An argument is what you pass; a parameter is in the function definition
d) Parameters work with loops; arguments work with conditionals

<details>
<summary>Answer</summary>

**c) An argument is what you pass; a parameter is in the function definition**

Example: In `def func(x):`, `x` is a parameter. In `func(5)`, `5` is an argument.
</details>

---

### Question 4
What does this code print?

```python
x = 10

def test():
    x = 5
    print(x)

test()
print(x)
```

a) 5, 5
b) 5, 10
c) 10, 5
d) Error

<details>
<summary>Answer</summary>

**b) 5, 10**

Inside the function, `x = 5` creates a local variable. The function prints 5. Outside the function, the global `x` is still 10.
</details>

---

### Question 5
Which of these is a good use of the `global` keyword?

a) To modify a global variable from inside a function
b) Never; avoid `global` by using return values instead
c) To read a global variable from inside a function
d) To create a variable that can be used everywhere

<details>
<summary>Answer</summary>

**b) Never; avoid `global` by using return values instead**

Using `return` values is cleaner and makes code more maintainable than `global`.
</details>

---

## Part 2: Short Answer (Questions 6–10)

Write short answers (1–3 sentences) for each question.

### Question 6
Explain what a return statement does.

<details>
<summary>Answer</summary>

A `return` statement sends a value from a function back to the code that called it. Once `return` executes, the function stops immediately, and any code after it doesn't run. The returned value can be used, stored, or passed to another function.
</details>

---

### Question 7
What is the purpose of the `main()` function pattern?

<details>
<summary>Answer</summary>

The `main()` function pattern organizes a program by putting all the orchestration (main logic) in one place. Helper functions do specific tasks, and `main()` calls them in the right order. This makes code cleaner, more readable, and easier to maintain.
</details>

---

### Question 8
What will this code do, and why?

```python
def add(a, b):
    print(a + b)

result = add(5, 3)
print(result)
```

<details>
<summary>Answer</summary>

The code will print `8` and then `None`. The function prints the sum (8) but doesn't `return` a value. When a function doesn't `return` anything, it returns `None`. So `result` is `None`, which is printed.

**Better approach:** Use `return` instead of `print` inside the function.
</details>

---

### Question 9
Write a function definition for a function called `greet` that takes one parameter called `name` and returns a greeting string.

<details>
<summary>Answer</summary>

```python
def greet(name):
    return f"Hello, {name}!"
```

Or:

```python
def greet(name):
    greeting = "Hello, " + name + "!"
    return greeting
```
</details>

---

### Question 10
Explain top-down design in programming.

<details>
<summary>Answer</summary>

Top-down design is a problem-solving approach where you start with the big picture and break it into smaller pieces. You identify major tasks, create functions for each task, and then implement them. This prevents "spaghetti code" and makes programs organized, maintainable, and easier to debug.
</details>

---

## Part 3: Coding Problems (Questions 11–15)

Write Python code to solve each problem.

### Question 11 (Basic)
Write a function `is_even(n)` that returns `True` if n is even, `False` if odd. Test it with 4 and 7.

<details>
<summary>Answer</summary>

```python
def is_even(n):
    return n % 2 == 0

print(is_even(4))   # True
print(is_even(7))   # False
```
</details>

---

### Question 12 (Basic)
Write a function `count_items(items)` that takes a list and returns the number of items. Test with a list of at least 3 items.

<details>
<summary>Answer</summary>

```python
def count_items(items):
    return len(items)

test_list = [10, 20, 30, 40]
print(count_items(test_list))  # 4
```

Or (counting with a loop):

```python
def count_items(items):
    count = 0
    for item in items:
        count = count + 1
    return count
```
</details>

---

### Question 13 (Intermediate)
Write a function `get_average(numbers)` that takes a list of numbers and returns the average. Test with [10, 20, 30].

<details>
<summary>Answer</summary>

```python
def get_average(numbers):
    if len(numbers) == 0:
        return 0
    total = 0
    for num in numbers:
        total = total + num
    return total / len(numbers)

print(get_average([10, 20, 30]))  # 20.0
```

Or (simpler):

```python
def get_average(numbers):
    return sum(numbers) / len(numbers)

print(get_average([10, 20, 30]))  # 20.0
```
</details>

---

### Question 14 (Intermediate)
Write a function `filter_positive(numbers)` that takes a list of numbers and returns a **new list** containing only positive numbers. Test with [-3, 5, -1, 8, 0, -2, 3].

<details>
<summary>Answer</summary>

```python
def filter_positive(numbers):
    result = []
    for num in numbers:
        if num > 0:
            result.append(num)
    return result

test_data = [-3, 5, -1, 8, 0, -2, 3]
positive_numbers = filter_positive(test_data)
print(positive_numbers)  # [5, 8, 3]
```
</details>

---

### Question 15 (Challenge)
Write a small program with at least 3 functions that calculates the final price of a purchase with a discount and tax. Use the `main()` pattern.

Example: Original price $100, 10% discount, 8% tax → Final price $97.20

**Your program should:**
- Have a function `apply_discount(price, percent)` that returns the discounted price
- Have a function `apply_tax(price, tax_rate)` that returns the price with tax
- Have a `main()` function that orchestrates everything

<details>
<summary>Answer</summary>

```python
def apply_discount(price, percent):
    """Apply a discount and return the new price."""
    discount_amount = price * (percent / 100)
    return price - discount_amount

def apply_tax(price, tax_rate):
    """Apply tax and return the new price."""
    tax_amount = price * tax_rate
    return price + tax_amount

def display_price(label, price):
    """Display a price nicely."""
    print(f"{label}: ${price:.2f}")

def main():
    """Main program."""
    original_price = 100
    discount_percent = 10
    tax_rate = 0.08

    display_price("Original price", original_price)

    discounted = apply_discount(original_price, discount_percent)
    display_price("After 10% discount", discounted)

    final_price = apply_tax(discounted, tax_rate)
    display_price("Final price (with 8% tax)", final_price)

if __name__ == "__main__":
    main()
```

Output:
```
Original price: $100.00
After 10% discount: $90.00
Final price (with 8% tax): $97.20
```
</details>

---

## Assessment Summary

| Part | Type | Questions | Points |
|------|------|-----------|--------|
| Part 1 | Multiple Choice | 1–5 | 10 |
| Part 2 | Short Answer | 6–10 | 15 |
| Part 3 | Coding | 11–15 | 25 |
| **Total** | | | **50** |

## Grading Guide

**Part 1 (Multiple Choice):** 2 points each
- Correct answer = 2 points
- Wrong answer = 0 points

**Part 2 (Short Answer):** 3 points each
- Complete, correct answer = 3 points
- Partially correct = 1–2 points
- Missing or wrong = 0 points

**Part 3 (Coding):** 5 points each
- Correct, working code = 5 points
- Code mostly works, minor errors = 3–4 points
- Code has significant errors = 1–2 points
- No attempt or completely wrong = 0 points

**Criteria for coding problems:**
- Correct syntax
- Function works as specified
- Proper use of parameters and return values
- Code is reasonably clear and readable

## Sample Grading Rubric

| Score | Grade | Interpretation |
|-------|-------|-----------------|
| 45–50 | A | Excellent; mastered concepts |
| 40–44 | B | Good; solid understanding |
| 35–39 | C | Satisfactory; understands main concepts |
| 30–34 | D | Minimal; some understanding, needs review |
| 0–29 | F | Insufficient; needs significant review |

---

**Remember:** If you didn't do well on this assessment, review the material and practice more. Every concept can be learned with effort. Ask your teacher for help if you're stuck.

---

*Last updated: 2026-03-25*
