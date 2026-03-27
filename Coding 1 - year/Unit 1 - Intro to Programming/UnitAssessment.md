# Unit 1 Assessment Preparation — 15 Essential Questions & Answers

## Part 1: Concept & Vocabulary Questions

**Question 1: What is the difference between an algorithm and a program?**

Answer: An algorithm is a step-by-step procedure that solves a problem or accomplishes a task. It's language-independent and focuses on the logic. A program is an algorithm written in a programming language (like Python) that a computer can actually execute. In other words, every program implements an algorithm, but not every algorithm is a program yet.

---

**Question 2: What are Python's four basic data types? Give an example of each.**

Answer:
- str (string) = text in quotes. Example: `"Hello"` or `'world'`
- int (integer) = whole numbers. Example: `42` or `-5`
- float (floating-point) = decimal numbers. Example: `3.14` or `-0.5`
- bool (boolean) = True or False. Example: `True` or `False`

---

**Question 3: Why must input() be converted to int() or float() before doing math?**

Answer: The `input()` function always returns a string, even if the user types a number like "17". To perform mathematical operations with this input, you must first convert it to a numeric data type. For example: `age = int(input("Age: "))` converts the string to an integer so you can do math like `age + 10`.

---

**Question 4: What does the // operator do? Give an example.**

Answer: The `//` operator performs floor division. It divides two numbers and rounds down to the nearest whole number, discarding any remainder. Example: `10 // 3` equals `3` (not 3.333...). It's different from `/` which returns a decimal: `10 / 3` equals `3.333...`

---

**Question 5: Why is x = "5" different from x = 5? Demonstrate with code.**

Answer: `"5"` is a string (text), while `5` is an integer (number). They cannot be used interchangeably:

```python
x = "5"
y = 5
print(x + 3)      # TypeError: can't add string and int
print(y + 3)      # Works fine, result is 8
print("5" + "3")  # Works fine, result is "53" (concatenation, not addition)
print(5 + 3)      # Works fine, result is 8 (math)
```

---

**Question 6: What is a variable? Why are they useful?**

Answer: A variable is a named container that stores a value in the computer's memory. Variables are useful because they allow you to:
- Store information for later use
- Give meaningful names to data
- Reuse values without retyping them
- Update values as needed throughout a program
- Write code that's readable and maintainable

Example: Instead of writing the same number repeatedly, you store it in a variable: `price = 19.99`

---

**Question 7: What does the type() function do? Give an example.**

Answer: The `type()` function returns the data type of a value. It tells you whether a value is a string, integer, float, or boolean.

Example:
```python
print(type("hello"))    # <class 'str'>
print(type(42))         # <class 'int'>
print(type(3.14))       # <class 'float'>
print(type(True))       # <class 'bool'>
```

---

**Question 8: Write the formula for Celsius to Fahrenheit conversion.**

Answer: F = C × 9/5 + 32

Or in Python: `fahrenheit = celsius * 9/5 + 32`

Example: 0°C = 32°F, 100°C = 212°F

---

**Question 9: What are three variable naming rules in Python?**

Answer:
1. Cannot start with a number: `age1` is valid, but `1age` is not
2. Cannot contain spaces; use underscores instead: `first_name` not `first name`
3. Cannot be Python keywords like `print`, `if`, `while`, or `input`

Additional rules:
- Cannot use special characters like `!@#$%`
- Are case-sensitive: `score` and `Score` are different variables
- Should be descriptive: `student_name` is better than `x`

---

**Question 10: Explain the 5-step software development process.**

Answer:
1. **Define (Ask):** Understand the problem. What are the inputs? What should the output be?
2. **Plan (Design):** Break the solution into steps. Write pseudocode or flowchart.
3. **Code (Implement):** Write the actual Python program based on your plan.
4. **Test (Verify):** Run the program with different inputs to check if it works correctly.
5. **Refine (Debug/Improve):** Fix any bugs and improve the code for clarity or efficiency.

Example: If creating a calculator, you Define what operations it needs, Plan the steps, Code the program, Test it with different numbers, and Refine the output format.

---

## Part 2: Code Analysis & Problem-Solving

**Question 11: What will this print? Explain why using PEMDAS.**

```python
print(2 + 3 * 4)
```

Answer: Prints `14`

Explanation: Using PEMDAS (Parentheses, Exponents, Multiplication/Division, Addition/Subtraction):
- First, multiply: 3 * 4 = 12
- Then, add: 2 + 12 = 14

If you wanted 20, you'd need parentheses: `(2 + 3) * 4`

---

**Question 12: What error is in this code and how would you fix it?**

```python
age = input("How old are you? ")
print(age + 10)
```

Answer: TypeError: unsupported operand type(s) for +: 'str' and 'int'

Explanation: `input()` returns a string, but you're trying to add an integer (10) to it. Strings and integers can't be added together.

Fix:
```python
age = int(input("How old are you? "))
print(age + 10)
```

---

**Question 13: Write a simple program that asks for a name and prints a greeting.**

Answer:
```python
name = input("What is your name? ")
print(f"Hello, {name}! Nice to meet you!")
```

Alternative (without f-string):
```python
name = input("What is your name? ")
print("Hello, " + name + "! Nice to meet you!")
```

---

**Question 14: What are escape characters? Give three examples and what they do.**

Answer: Escape characters are special sequences that represent characters you can't easily type. They start with a backslash `\`:

- `\n` = newline (starts a new line)
  ```python
  print("Line 1\nLine 2")  # Prints on two lines
  ```

- `\t` = tab (indentation for alignment)
  ```python
  print("Name\tAge\nAlex\t17")  # Creates columns
  ```

- `\\` = backslash (to print an actual backslash)
  ```python
  print("C:\\Users\\Documents")  # Prints the path correctly
  ```

---

**Question 15: Describe f-strings and show how to use them with decimal formatting.**

Answer: F-strings (formatted string literals) allow you to embed variables and expressions directly inside strings. They start with the letter `f` before the opening quote.

Basic syntax: `f"text {variable} more text"`

Example with decimal formatting:
```python
price = 19.5
gpa = 3.857
print(f"Price: ${price:.2f}")      # Prints: Price: $19.50
print(f"GPA: {gpa:.2f}")           # Prints: GPA: 3.86
```

The `:.2f` format specifier means:
- `:` = start formatting
- `.2` = 2 decimal places
- `f` = format as float

F-strings are better than concatenation because they're more readable:
- Old way: `"Price: $" + str(price)`
- F-string way: `f"Price: ${price:.2f}"`

---

## Assessment Tips

**When answering questions:**
1. Read carefully—make sure you understand what's being asked
2. Show your work—especially for code problems
3. Be specific—don't be vague about data types or error messages
4. Include examples when asked
5. Test code mentally or on paper before writing it

**For code writing:**
- Use descriptive variable names
- Include comments for clarity
- Test edge cases (very small numbers, very large numbers, zero)
- Format output professionally with f-strings
- Always convert input to the right data type

**For debugging:**
- Read the error message—it usually tells you exactly what's wrong
- Check for matching parentheses and quotes
- Verify variables are defined before using them
- Make sure data types match for operations
- Test with multiple inputs

**Common mistakes to avoid:**
- Forgetting to convert `input()` before math
- Mixing quotes: `print('Hello")` or `print("Hello')`
- Using `=` (assignment) instead of `==` (comparison)
- Forgetting that Python is case-sensitive
- Indentation errors (we'll focus on this in Unit 2)
- Not using f-strings for decimal formatting

---

## Study Checklist

Before your assessment, make sure you can:

- [ ] Define computer science, algorithms, and programs
- [ ] Identify and use Python's four basic data types
- [ ] Create and reassign variables correctly
- [ ] Use the `input()` function and convert input to correct types
- [ ] Use all seven arithmetic operators correctly
- [ ] Apply order of operations (PEMDAS) in Python
- [ ] Write and read f-strings with decimal formatting
- [ ] Use comments and escape characters effectively
- [ ] Follow the 5-step software development process
- [ ] Identify and fix syntax errors and type errors
- [ ] Write a complete program that takes input, performs calculations, and displays formatted output
- [ ] Debug code and explain what went wrong
- [ ] Use string concatenation and proper formatting
- [ ] Write pseudocode and simple flowcharts
- [ ] Test programs with multiple inputs

---

## Sample Assessment Problems

**Short Answer (Example):**
Explain why this code has an error and write the corrected version:
```python
score = input("Score: ")
total = score * 2
print(total)
```

**Code Writing (Example):**
Write a program that asks for the length and width of a rectangle, calculates the area and perimeter, and displays both with labels.

**Debugging (Example):**
Find the error(s) in this code and explain what's wrong:
```python
price = float(input(Price: $))
discount = 0.1
final = price - (price * discount)
print(f"Final price: {final}")
```

**Concept (Example):**
What is the difference between `10 / 2` and `10 // 2`? What does each return and when would you use each?

---

Good luck on your assessment!
