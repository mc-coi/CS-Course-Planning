# Unit 1: Introduction to Programming
> Learn the fundamentals of computer science, algorithms, and writing your first Python programs.

##  Unit Overview
- **Duration:** 6 days / 2 weeks
- **Key Concepts:** Computer science and problem-solving, algorithms, Python syntax, variables, data types, user input, and basic calculations
- **Big Idea:** Programs are instructions that solve problems step-by-step

##  Learning Targets
- I can define computer science and explain what an algorithm is
- I can write and run a basic Python program
- I can store information in variables and identify Python's four basic data types
- I can collect user input and perform basic arithmetic
- I can apply the 5-step software development process to solve problems
- I can build a complete beginner Python program from scratch

---

# Day 1: What is Computer Science?
**Learning Target:** I can define computer science and explain what an algorithm is.

### Key Concepts
Computer Science is the study of problem-solving using computers. At its core, it's not really about computers—it's about breaking down complex problems into simple, step-by-step instructions that anyone (or anything) can follow. These step-by-step instructions are called **algorithms**.

An **algorithm** is an ordered sequence of steps that solves a problem or accomplishes a task. Think of it like a recipe: if you follow the steps in order, you get the desired result. Algorithms must be:
- **Precise:** No ambiguity; each step must be clear
- **Unambiguous:** Only one way to interpret each instruction
- **Finite:** Must eventually end
- **Effective:** Actually solves the problem

**Programs** are algorithms written in a programming language that computers can execute. Computers need very precise instructions because they are literal—if you say "make a sandwich," a computer won't know what that means. You must break it down into tiny steps: "Pick up bread," "Place bread on plate," "Spread peanut butter on bread," etc.

**Flowcharts** are visual diagrams used to represent algorithms:
- **Rectangles** represent processes (actions)
- **Diamonds** represent decisions (yes/no questions)
- **Ovals** represent start/end points
- **Arrows** show the flow of execution

### Code Examples
```python
# The classic first program
print("Hello, World!")

# Multiple print statements
print("Welcome to Python!")
print("I am excited to learn programming.")
print("This is fun!")

# Using comments — the # symbol
# This line is a comment and will not execute
print("This will print")  # This comment explains the line
# Comments help future readers understand your code
```

### Guided Practice
Write a 3-line Python program that outputs a haiku (5-7-5 syllable structure). Then write an algorithm in plain English for brushing your teeth—make sure each step is precise and unambiguous.

### Practice Problems
**Problem 1 — Beginner:** Write three `print()` statements that together output your name, your grade level, and your favorite hobby, each on its own line.

```python
# Starter code
print()
print()
print()
```

**Problem 2 — Intermediate:** Describe an everyday algorithm (like making a peanut butter sandwich) in 7-10 precise steps.

**Problem 3 — Challenge:** Draw a simple flowchart (or describe one in text) for the following: "If the door is locked, find a key and unlock it. Then open the door and go inside."

<details>
<summary>💡 Hints</summary>

- Problem 1: Remember to put your information in quotes inside print()
- Problem 2: Think about every single action—if a robot did it, would it understand?
- Problem 3: Use "Start," "Decision (diamond)," and "End" shapes
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
print("Zach McCoy")
print("10th Grade")
print("Basketball")
```
### Problem 2 Example (first 3 steps)
**Step 1: Get the bread from the pantry**<br>
**Step 2: Place two slices on a plate**<br>
**Step 3: Get the peanut butter jar from the cupboard**<br>
</details>

---

# Day 2: Setting Up Python & First Program
**Learning Target:** I can write and run a basic Python program.

### Key Concepts
A **Python interpreter** reads your code and executes it line-by-line, translating it into actions the computer understands. Python is known for being beginner-friendly because it reads almost like English.

The `print()` function displays text on the screen. Text must be enclosed in quotes (either single `'` or double `"`). Python is **case-sensitive**, meaning `print` and `Print` are different—only `print` (lowercase) works.

**Comments** start with `#` and tell the computer to ignore that line. Comments are for humans to read and understand the code.

### Code Examples
```python
# Basic print statements
print("Hello World")
print('Single quotes work too')
print("My name is Zach")

# Multiple things in one print (comma-separated)
print("I am", 17, "years old")

# Comments explain your code
print("This line will execute")
# This line is ignored by Python

# You can print blank lines
print()
print("There was a blank line above")
```

### Guided Practice
Create a "Digital Introduction Card" program that prints:
- Your name
- Your current grade level
- Your favorite subject or hobby
- What you want to be when you grow up
- At least one comment explaining what your program does

### Practice Problems
**Problem 1 — Beginner:** Write a program that prints your first name, last name, and current grade, each on a separate line.

```python
# Starter code
print()
print()
print()
```

**Problem 2 — Intermediate:** Write a program that prints a haiku (3 lines: 5 syllables, 7 syllables, 5 syllables). Add a comment at the top explaining what the haiku is about.

**Problem 3 — Challenge:** Write a program that prints a small ASCII art picture (at least 5 lines). Use comments to explain what it is.

<details>
<summary>💡 Hints</summary>

- Problem 1: Each print() is a separate line of output
- Problem 2: Use comments with # to label your haiku
- Problem 3: Use special characters like *, /, ^, etc. to create art
</details>

<details>
<summary>✅ Sample Answers </summary>

```python
# Problem 1 Example
print("Zach")<br>
print("McCoy")<br>
print("10")

# Problem 2 Example
#My haiku about Python
print("Code flows like water")
print("Solving problems step by step")
print("Logic comes alive")
```
</details>

---

# Day 3: Variables & Data Types
**Learning Target:** I can store information in variables and identify Python's four basic data types.

### Key Concepts
A **variable** is a named container that stores a value in the computer's memory. Think of it like a labeled box—you put something inside and give it a name so you can refer to it later.

Python has four main data types:
1. **str (string):** Text, enclosed in quotes. Examples: `"Alice"`, `'hello'`, `"123 Main St"`
2. **int (integer):** Whole numbers without decimals. Examples: `42`, `-7`, `0`
3. **float (floating-point):** Numbers with decimals. Examples: `3.14`, `-0.5`, `99.99`
4. **bool (boolean):** True or False (always capitalized in Python)

**Variable naming rules:**
- Cannot contain spaces; use underscores instead: `first_name` not `first name`
- Cannot start with a number: `age1` is okay, `1age` is not
- Cannot use special characters like `!@#$%`
- Cannot be Python keywords like `print`, `if`, `while`
- Are case-sensitive: `score` and `Score` are different variables

The `type()` function tells you what data type a value is.

### Code Examples
```python
# String variables
name = "Alex"
city = "Nashville"
print(name)        # Alex
print(city)        # Nashville

# Integer variables
age = 17
score = 95
print(age)         # 17

# Float variables
gpa = 3.85
price = 19.99
print(gpa)         # 3.85

# Boolean variables
is_enrolled = True
is_absent = False
print(is_enrolled) # True

# Check data types
print(type("hello"))     # <class 'str'>
print(type(42))          # <class 'int'>
print(type(3.14))        # <class 'float'>
print(type(True))        # <class 'bool'>

# Variables can be reassigned
x = 5
print(x)           # 5
x = 10
print(x)           # 10 — the value changed!

# Multiple assignment
a, b, c = 1, 2, 3
print(a, b, c)     # 1 2 3
```

### Guided Practice
Create a student profile with at least 5 variables of different data types. Print each variable and its type. Then change one variable's value and print it again.

### Practice Problems
**Problem 1 — Beginner:** Declare one variable of each data type (str, int, float, bool) and print them all.

```python
# Starter code
name =
age =
height =
is_student =

print()
```

**Problem 2 — Intermediate:** Create variables for a student: name, age, GPA, and whether they're on the honor roll. Print a sentence using all four variables.

**Problem 3 — Challenge:** What does `type("3.14")` return vs. `type(3.14)`? Write code to demonstrate and explain the difference.

<details>
<summary>💡 Hints</summary>
- Problem 1: Strings need quotes, booleans are True or False (capitalized)<br>
- Problem 2: Use f-strings or + to combine strings and variables<br>
- Problem 3: Quotes make it text, not a number
</details>

<details>
<summary>✅ Sample Answers</summary>

## Problem 1 Example
```python
name = "Jordan"
age = 16
height = 5.75
is_student = True
print(name, age, height, is_student)
print(type(name), type(age), type(height), type(is_student))
```

## Problem 2 Example
```python
name = "Sam"
age = 17
gpa = 3.9
is_honors = True
print(f"{name} is {age}, has a {gpa} GPA, and honors: {is_honors}")
```

</details>

---

# Day 4: User Input & Simple Calculations
**Learning Target:** I can collect user input and perform basic arithmetic.

### Key Concepts
The `input()` function pauses the program and waits for the user to type something, then press Enter. **Important:** `input()` always returns a **string**, even if the user types numbers.

To use a number entered by the user in calculations, you must **convert** it using `int()` for whole numbers or `float()` for decimals.

**Arithmetic operators:**
- `+` addition
- `-` subtraction
- `*` multiplication
- `/` division (always returns a float, even if result is whole)
- `//` integer division (floor division, discards remainder)
- `%` modulus (returns the remainder)
- `**` exponentiation (power)

### Code Examples
```python
# Getting user input
name = input("What is your name? ")
print(f"Hello, {name}!")

# Converting input to numbers
age = int(input("How old are you? "))
gpa = float(input("What is your GPA? "))

# Arithmetic
print(10 + 3)      # 13
print(10 - 3)      # 7
print(10 * 3)      # 30
print(10 / 3)      # 3.333... (always float)
print(10 // 3)     # 3 (floor division)
print(10 % 3)      # 1 (remainder)
print(2 ** 8)      # 256 (2 to the power of 8)

# Tip calculator
bill = float(input("Enter bill amount: $"))
tip_percent = 0.20
tip = bill * tip_percent
total = bill + tip
print(f"Tip: ${tip:.2f}")
print(f"Total: ${total:.2f}")
```

### Guided Practice
Create a tip calculator that asks the user for:
1. The bill amount (float)
2. The tip percentage (as a decimal like 0.18 for 18%)
Then calculate and print the tip amount and total (including tip).

### Practice Problems
**Problem 1 — Beginner:** Write a program that asks for two numbers and prints their sum, difference, product, and quotient.

```python
# Starter code
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))

print("Sum:", )
print("Difference:", )
print("Product:", )
print("Quotient:", )
```

**Problem 2 — Intermediate:** Write a miles-to-kilometers converter. Ask the user for miles and print the equivalent in km (1 mile = 1.60934 km).

**Problem 3 — Challenge:** Write a program that asks for a rectangle's length and width, then prints its area, perimeter, and diagonal (use `import math` and `math.sqrt()`).

<details>
<summary>💡 Hints</summary>

- Problem 1: Use the arithmetic operators to combine num1 and num2
- Problem 2: Remember to convert input to float, then multiply
- Problem 3: Diagonal = sqrt(length² + width²)
</details>

<details>

<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))
print("Sum:", num1 + num2)
print("Difference:", num1 - num2)
print("Product:", num1 * num2)
print("Quotient:", num1 / num2)

# Problem 2 Example
miles = float(input("Enter miles: "))
kilometers = miles * 1.60934
print(f"{miles} miles = {kilometers:.2f} km")
```
</details>

---

# Day 5: Problem Solving with Python
**Learning Target:** I can apply the 5-step software development process.

### Key Concepts
The **5-Step Software Development Process** helps you solve problems systematically:

1. **Define:** Understand what the problem is asking. What are inputs? What should the output be?
2. **Plan:** Break down the solution into steps. Write pseudocode (instructions in English, not Python).
3. **Code:** Translate your plan into Python. Write the code.
4. **Test:** Run your program with different inputs, including edge cases (very small, very large, zero, negative).
5. **Refine:** Fix any bugs or improve the code. Make it cleaner, more efficient, or easier to read.

Use the `round()` function to format decimal output: `round(3.14159, 2)` returns `3.14`.

### Code Examples
```python
# Temperature converter — Fahrenheit to Celsius
# Step 1 - Define: Input temp in °F, output in °C using formula C = (F - 32) × 5/9
# Step 2 - Plan:
#   a) Ask user for temperature in Fahrenheit
#   b) Apply conversion formula
#   c) Round to 2 decimal places
#   d) Print result in nice format

fahrenheit = float(input("Enter temperature (°F): "))
celsius = (fahrenheit - 32) * 5 / 9
celsius_rounded = round(celsius, 2)
print(f"{fahrenheit}°F = {celsius_rounded}°C")

# BMI Calculator
# BMI = weight (lbs) / (height (in))² × 703

weight = float(input("Enter weight in pounds: "))
height = float(input("Enter height in inches: "))
bmi = (weight / (height ** 2)) * 703
print(f"Your BMI is {round(bmi, 1)}")

# Paycheck calculator with tax
hours = float(input("Hours worked: "))
hourly_rate = float(input("Hourly rate: $"))
gross_pay = hours * hourly_rate
tax = gross_pay * 0.15  # 15% tax
net_pay = gross_pay - tax
print(f"Gross: ${gross_pay:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Net: ${net_pay:.2f}")
```

### Guided Practice
Follow the 5-step process to create a simple BMI calculator:
1. Define: What are inputs? What's the output?
2. Plan: Write the steps in English
3. Code: Write the Python program
4. Test: Try it with different heights and weights
5. Refine: Make the output cleaner or add a message about the BMI

### Practice Problems
**Problem 1 — Beginner:** Write a program using the 5-step process that converts a temperature from Celsius to Fahrenheit. (Formula: F = C × 9/5 + 32)

```python
# Step 1 - Define: ...
# Step 2 - Plan: ...
# Step 3 - Code:
celsius = float(input("Enter Celsius: "))

# Step 4 - Test: (write comments about test cases)
# Step 5 - Refine: (improve output)
```

**Problem 2 — Intermediate:** Create a savings calculator that asks for principal amount, monthly savings, and number of months, then prints total savings.

**Problem 3 — Challenge:** Create a currency converter. Ask for USD, then convert to EUR, JPY, and GBP using current approximate rates (you choose rates). Use proper formatting.

<details>
<summary>💡 Hints</summary>

- Problem 1: Work through the formula step-by-step with a calculator first
- Problem 2: Total = principal + (monthly_savings × months)
- Problem 3: Store exchange rates in variables for easy updating
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
celsius = float(input("Enter temperature (°C): "))
fahrenheit = celsius * 9/5 + 32
print(f"{celsius}°C = {round(fahrenheit, 2)}°F")

# Problem 2 Example
principal = float(input("Principal: $"))
monthly = float(input("Monthly savings: $"))
months = int(input("Number of months: "))
total = principal + (monthly * months)
print(f"Total savings: ${total:.2f}")
```
</details>

---

# Day 6: Unit 1 Project Day
**Learning Target:** I can build a complete beginner Python program.

### Project: Student Life Simulator

Create a program that simulates a day in a high school student's life. Your program must include:

**Requirements:**
- At least 4 variables of different data types
- At least 3 inputs using `input()`
- At least 1 calculation
- At least 3 comments explaining key lines
- Clean, readable output using `print()` and f-strings

**Example Output:**
```
=== STUDENT LIFE SIMULATOR ===
What's your name? Alex
How many hours did you study? 3
What's your average grade? 92
Did you get enough sleep (yes/no)? yes

=== YOUR DAY ===
Name: Alex
Study hours: 3
Average grade: 92%
Sleep: Yes
Study effectiveness score: 2.76  (calculated as hours × average/100)
```

**Submission Checklist:**
- [ ] Code runs without errors
- [ ] Has 4+ variables
- [ ] Has 3+ inputs
- [ ] Has 1+ calculation
- [ ] Has 3+ comments
- [ ] Has clean output with labels

---

## Unit Practice Bank

1. **Beginner:** Write a program that prints your name 5 times, each on its own line.
2. **Beginner:** Declare a variable for each data type (str, int, float, bool) and use `type()` to print each one.
3. **Beginner:** Ask the user for two numbers, then print their sum, difference, product, and quotient.
4. **Intermediate:** Write a miles-to-kilometers converter (1 mile = 1.60934 km).
5. **Intermediate:** Write a program that asks for a rectangle's length and width and prints area and perimeter.
6. **Intermediate:** What does `type("3.14")` return vs `type(3.14)`? Write code to demonstrate and explain.
7. **Intermediate:** Fix this broken code: `num = input("Enter: "); print(num + 10)` and explain the error.
8. **Intermediate:** Write a program that asks for a price and quantity, calculates the total with 8% tax.
9. **Intermediate:** What is 17 % 5? What real-world situation could this operator model?
10. **Intermediate:** Predict the output: `x = 5; y = x + 3; x = 10; print(x, y)` and explain why.
11. **Challenge:** Write a savings calculator: ask for starting balance, monthly savings, and months, print total saved and average per month.
12. **Challenge:** What happens when you run: `print("Hello" + 5)`? Write code to demonstrate, explain the error, and fix it.
13. **Challenge:** Write a study hours tracker: ask for hours studied Mon-Fri, print weekly total and daily average.
14. **Challenge:** Write a currency converter (USD to EUR, JPY, GBP) using current approximate exchange rates.
15. **Challenge:** Debug this code: `gpa = Float(input("GPA: ")); print("Your gpa is" gpa)` — find all 3 errors.

---

## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| `Print("Hello")` instead of `print()` | NameError: uppercase P | Remember Python is case-sensitive; use `print()` (lowercase) |
| `name = input()` then `print(name + 5)` | TypeError: can't add str and int | Convert input: `name = int(input())` or `print(str(5))` |
| `print(Hello)` without quotes | NameError: name 'Hello' undefined | Strings need quotes: `print("Hello")` |
| `age = "17"` then use in math | Result is string concatenation, not math | Convert: `age = int(input(...))` or use `int("17")` |
| Using spaces in variable names: `my age = 25` | SyntaxError: invalid syntax | Use underscores: `my_age = 25` |
| `print 5` instead of `print(5)` | SyntaxError: missing parentheses | Python 3 requires parentheses: `print(5)` |
| Forgetting to convert `input()` | Can't do math on strings | Always use `int()` or `float()`: `num = int(input("Number: "))` |

---

## Unit Assessment Prep

**Review Questions:** Answer these to prepare for the unit assessment.

1. What is the difference between an algorithm and a program?
2. What are Python's four basic data types? Give an example of each.
3. Why must `input()` be converted to `int()` or `float()` before doing math?
4. What does the `//` operator do? Give an example.
5. Why is `x = "5"` different from `x = 5`? Demonstrate with code.
6. What is a variable? Why are they useful?
7. What does the `type()` function do?
8. Write the formula: Celsius to Fahrenheit conversion.
9. What are variable naming rules? List 3 valid and 3 invalid variable names.
10. Explain the 5-step software development process.

**Answers:**
1. An algorithm is a step-by-step procedure; a program is an algorithm written in code.
2. str (text), int (whole numbers), float (decimals), bool (True/False).
3. `input()` returns text (string); to do math, it must become a number.
4. `//` is integer/floor division—returns whole number without remainder. Example: `10 // 3 = 3`
5. `"5"` is text (string); `5` is a number (int). You can't add `"5" + 3`, but you can add `5 + 3`.
6. Variables store values and give them names so you can use them later in your program.
7. `type()` returns the data type of a value, like `<class 'int'>` or `<class 'str'>`.
8. F = C × 9/5 + 32
9. Valid: `age`, `first_name`, `score1`; Invalid: `age!`, `1st`, `my age`
10. Define (understand problem), Plan (write steps), Code (write program), Test (try different inputs), Refine (improve/fix).

---

## Vocabulary & Quick Reference

**Key Terms:**
- **Algorithm:** Step-by-step procedure to solve a problem
- **Data Type:** Category of data (str, int, float, bool)
- **Variable:** Named container storing a value
- **Input:** Information the user gives to the program
- **Output:** Information the program displays to the user
- **Syntax:** Rules for writing code correctly
- **Comment:** Explanation in code, ignored by Python, starts with #
- **Function:** Reusable block of code (intro only; more in Unit 5)

**Key Syntax:**
```python
# Comments
print("Output text")                    # Display output
variable = value                        # Create/assign variable
name = input("Prompt: ")               # Get user input
type(value)                             # Check data type
x = int(input("Number: "))             # Get and convert input
print(f"Hello {name}, you are {age}")  # F-string formatting
round(3.14159, 2)                      # Round to 2 decimals
```

**Arithmetic Operators:**
- `+` add, `-` subtract, `*` multiply, `/` divide, `//` floor divide, `%` remainder, `**` exponent

**Quick Formula Reference:**
- Temperature: C = (F - 32) × 5/9
- Area of rectangle: length × width
- Perimeter of rectangle: 2 × length + 2 × width
