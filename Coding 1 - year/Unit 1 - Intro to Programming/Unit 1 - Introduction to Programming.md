# Unit 1: Introduction to Programming
> Learn the fundamentals of computer science, algorithms, and writing your first Python programs.

## Unit Overview
- **Duration:** 20 days / 4 weeks (Traditional Schedule, 55-minute periods)
- **Key Concepts:** Computer science and problem-solving, algorithms, Python syntax, variables, data types, user input, arithmetic operations, formatting, type conversion, and the software development process
- **Big Idea:** Programs are instructions that solve problems step-by-step. By breaking down complex tasks into simple, precise steps, we can write code that computers can execute reliably and efficiently.

---

## Getting Started — Installing Python & Choosing an IDE

Before writing your first line of code, you need two things: **Python** (the programming language) and an **IDE** (Integrated Development Environment — the app where you write and run your code). An IDE gives you a code editor with helpful features like syntax highlighting, error detection, and a built-in terminal to run your programs.

### On a Windows Machine

1. **Install Python** — Open the Microsoft Store, search for "Python," and install it (free). This gives you the Python interpreter that actually runs your code.
2. **Install Visual Studio Code** — Open the Microsoft Store, search for "Visual Studio Code," and install it (free). VS Code is a professional-grade code editor used by developers worldwide.
3. **Install the Python Extension in VS Code** — Open VS Code, click the Extensions icon on the left sidebar (or press `Ctrl+Shift+X`), search for "Python," and install the official Python extension by Microsoft. This adds code completion, debugging, and a "Run" button for Python files.

Once installed, you can create a new file ending in `.py` (like `hello.py`), write your code, and press the green play button to run it.

### On a Chromebook (Also Works on Windows/Mac If You Can't Install Software)

If you're on a Chromebook or a school computer where you can't install software, use **Kira Learning's online IDE** — it runs entirely in your browser with no installation required.

1. Go to [app.kira-learning.com](https://app.kira-learning.com)
2. Open the IDE code editor directly at: [app.kira-learning.com/ide/](https://app.kira-learning.com/ide/)
3. Write your Python code in the editor and click "Run" to see the output

This is a great option for getting started quickly without any setup headaches.

### What is an IDE?

An **IDE (Integrated Development Environment)** is a program that combines everything you need to write code in one place:

- **Code Editor** — Where you type your code, with features like color-coded syntax and auto-indentation
- **Terminal / Console** — Where your program's output appears and where you can type input
- **Error Highlighting** — Underlines mistakes before you even run the program
- **File Management** — Organize your Python files into folders and projects

Think of it like Microsoft Word for code — you *could* write code in Notepad, but an IDE makes it much easier to write, find mistakes, and run your programs.

---

## Learning Targets

By the end of Unit 1, you will be able to:

1. I can define computer science and explain what an algorithm is
2. I can write and trace pseudocode and flowcharts to represent algorithms
3. I can set up Python and run a basic program using the print() function
4. I can use comments, escape characters, and basic print formatting
5. I can create variables, assign values, and reassign them correctly
6. I can identify and work with Python's four basic data types (str, int, float, bool)
7. I can use the input() function to collect information from users
8. I can perform string concatenation to combine text and variables
9. I can convert user input to numeric data types for calculations
10. I can use arithmetic operators (+, -, *, /, //, %, **) to solve problems
11. I can apply the order of operations (PEMDAS) correctly in Python expressions
12. I can build calculator-style programs with variables and arithmetic
13. I can format output using f-strings for professional-looking results
14. I can apply the 5-step software development process to plan and code programs
15. I can identify and fix common syntax errors and type errors in Python
16. I can design, code, and test a complete beginner program from scratch
17. I can evaluate and debug code to improve accuracy and efficiency
18. I can write clean, well-commented code that is easy for others to read

---

## Weekly Breakdown

### Week 1: What is CS & Algorithms (Days 1–5)
Understanding the big picture: What is computer science? What are algorithms? How do we plan solutions before coding?

### Week 2: Variables & Data Types (Days 6–10)
Getting hands-on with Python: storing information in variables, understanding data types, and collecting user input.

### Week 3: Basic Calculations & Expressions (Days 11–15)
Using Python as a calculator: arithmetic operators, order of operations, and building computational programs.

### Week 4: Software Development & Review (Days 16–20)
Putting it all together: the development process, debugging, a mini-project, and unit review and assessment.

---

# WEEK 1: WHAT IS CS & ALGORITHMS

# Day 1: What is Computer Science?
**Learning Target:** I can define computer science and explain what an algorithm is.

### Key Concepts
Computer Science is the study of problem-solving using computers. At its core, it's not really about computers—it's about breaking down complex problems into simple, step-by-step instructions that anyone (or anything) can follow. These step-by-step instructions are called **algorithms**.

An **algorithm** is an ordered sequence of steps that solves a problem or accomplishes a task. Think of it like a recipe: if you follow the steps in order, you get the desired result. Algorithms must be:
- **Precise:** No ambiguity; each step must be clear and exact
- **Unambiguous:** Only one way to interpret each instruction
- **Finite:** Must eventually end (not an infinite loop)
- **Effective:** Actually solves the problem as intended

**Programs** are algorithms written in a programming language that computers can execute. Computers need very precise instructions because they are literal—if you say "make a sandwich," a computer won't know what that means. You must break it down into tiny steps: "Pick up bread," "Place bread on plate," "Spread peanut butter on bread," etc.

Computers can execute billions of instructions per second, making them useful for solving problems that would be tedious or impossible for humans to do manually. The key is learning to think algorithmically—to break down big problems into manageable steps.

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
Write a 3-line Python program that outputs a haiku (5-7-5 syllable structure). Then write an algorithm in plain English for brushing your teeth—make sure each step is precise and unambiguous. Would a robot be able to follow your algorithm without asking questions?

### Practice Problems
**Problem 1 — Beginner:** Write three `print()` statements that together output your name, your grade level, and your favorite hobby, each on its own line.

```python
# Starter code
print()
print()
print()
```

**Problem 2 — Intermediate:** Describe an everyday algorithm (like making a peanut butter sandwich, getting ready for school, or sending a text) in 7-10 precise steps.

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
print("Alex Johnson")
print("10th Grade")
print("Soccer")
```

### Problem 2 Example (first 4 steps of making toast)
**Step 1: Get two slices of bread from the loaf**<br>
**Step 2: Place both slices in the toaster slot**<br>
**Step 3: Push the toaster lever down**<br>
**Step 4: Wait for the toaster to pop up (about 2-3 minutes)**<br>

</details>

---

# Day 2: Pseudocode & Flowcharts
**Learning Target:** I can write and trace pseudocode and flowcharts to represent algorithms.

### Key Concepts
Before writing actual code, it's helpful to plan your solution using **pseudocode** and **flowcharts**. These tools help you think through the logic without worrying about programming syntax.

**Pseudocode** is a way of writing algorithms using English-like statements instead of actual code. It's human-readable and focuses on the logic of the solution. Example:
```
Ask the user for two numbers
Add the two numbers
Display the result
```

**Flowcharts** are visual diagrams that represent the flow of an algorithm using standard shapes:
- **Ovals** = Start/End points
- **Rectangles** = Processes or actions
- **Diamonds** = Decisions (yes/no questions)
- **Arrows** = Direction of flow

A good flowchart should be:
- Clear and easy to follow
- Use standard shapes correctly
- Show decision points explicitly
- Follow a logical sequence

### Code Examples
```python
# Example: Average of two numbers
# Pseudocode:
# 1. Ask user for first number
# 2. Ask user for second number
# 3. Add them together
# 4. Divide by 2
# 5. Print the result

# Python code:
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))
average = (num1 + num2) / 2
print(f"Average: {average}")
```

### Guided Practice
Write pseudocode for a simple task: "Make a cup of tea." Include at least 6 steps. Then convert your pseudocode into a flowchart (you can draw it or describe it using text and ASCII art).

### Practice Problems
**Problem 1 — Beginner:** Convert this algorithm into pseudocode:
```
Start → Ask for your name → Ask for your age → Calculate birth year (2026 - age) →
Display name and birth year → End
```

**Problem 2 — Intermediate:** Write pseudocode for ordering a pizza online (including a decision: what if they're out of your favorite topping?).

**Problem 3 — Challenge:** Create a flowchart for this scenario: "Check if a student can attend a field trip. They must be on time AND not have any failing grades."

<details>
<summary>💡 Hints</summary>

- Problem 1: Pseudocode doesn't need to be code—just English steps
- Problem 2: Think about what happens when something goes wrong
- Problem 3: Use a diamond for the decision and think about AND/OR logic
</details>

<details>
<summary>✅ Sample Answers</summary>

```
# Problem 1 Example Pseudocode:
Start
Display "Welcome"
Ask user for name, store in variable
Ask user for age, store in variable
Subtract age from 2026, store as birth_year
Display name and birth_year
End

# Problem 2 Example Pseudocode (first 5 steps):
Start
Open pizza website
Select restaurant
Browse menu
For each topping:
  If topping is available:
    Add to order
  Else:
    Show customer "out of stock"
Continue with checkout
End
```

</details>

---

# Day 3: Intro to Python & the Print Function
**Learning Target:** I can set up Python and run a basic program using the print() function.

### Key Concepts
A **Python interpreter** reads your code line-by-line and executes it, translating it into actions the computer understands. Python is known for being beginner-friendly because it reads almost like English.

The `print()` function displays text on the screen. Text must be enclosed in quotes (either single `'` or double `"`). Python is **case-sensitive**, meaning `print` and `Print` are different—only `print` (lowercase) works. This applies to all Python functions and variables.

When you run a Python program, the interpreter reads from top to bottom, executing one statement at a time. Once it reaches the end of the file, the program stops.

### Code Examples
```python
# Basic print statements
print("Hello World")
print('Single quotes work too')
print("My name is Alex")

# Multiple things in one print (comma-separated)
print("I am", 17, "years old")

# Comments explain your code
print("This line will execute")
# This line is ignored by Python

# You can print blank lines
print()
print("There was a blank line above")

# Printing numbers (no quotes needed for numbers)
print(42)
print(3.14)
```

### Guided Practice
Create a "Digital Introduction Card" program that prints:
- Your name
- Your current grade level
- Your favorite subject or hobby
- What you want to be when you grow up
- At least one comment explaining what your program does

Test your program by running it and verifying the output is correct.

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
- Problem 3: Use special characters like *, /, ^, \, | to create art
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
print("Morgan")
print("Rivera")
print("10")

# Problem 2 Example
# My haiku about Python
print("Code flows like water")
print("Solving problems step by step")
print("Logic comes alive")

# Problem 3 Example (a tree)
print("    /\\")
print("   /  \\")
print("  /____\\")
print("    ||")
print("    ||")
```

</details>

---

# Day 4: Comments, Print Formatting & Escape Characters
**Learning Target:** I can use comments, escape characters, and basic print formatting.

### Key Concepts
**Comments** start with `#` and tell Python to ignore that line. Comments are for humans to read and understand the code. Good comments explain the "why," not just the "what." Example: `print("Total") # This will show the final sum` is better than just `print("Total")`.

**Escape characters** are special sequences that represent characters you can't easily type:
- `\n` = newline (starts a new line)
- `\t` = tab (indents the text)
- `\\` = backslash (to print an actual backslash)
- `\'` = single quote (inside single-quoted string)
- `\"` = double quote (inside double-quoted string)

**Print formatting** makes output look better:
- Use `\n` for line breaks within a string
- Use `\t` for indentation and alignment
- Combine multiple lines in one print() using escape characters

### Code Examples
```python
# Using escape characters
print("Hello\nWorld")  # Newline: Hello then World on next line

print("Name\tAge")     # Tab for alignment
print("Alex\t17")
print("Jordan\t18")

# Escaping quotes
print("He said \"Hello\"")  # Prints: He said "Hello"
print('It\'s a beautiful day')  # Prints: It's a beautiful day

# Multi-line output in one print
print("Line 1\nLine 2\nLine 3")

# Combining quotes and content
print("Path: C:\\Users\\Documents\\code.py")

# Good comments explain the code
score = 95
print(f"Score: {score}%")  # Display score with percentage symbol
```

### Guided Practice
Create a program that prints a formatted table or receipt. Use:
- At least 2 different escape characters (\n and \t)
- At least 2 comments explaining what each section does
- Aligned columns or sections

Example output:
```
===== RECEIPT =====
Item     Price
-----
Bread    $3.50
Milk     $2.25
-----
Total    $5.75
```

### Practice Problems
**Problem 1 — Beginner:** Write a program that prints your name, grade, and favorite subject using escape characters to format it nicely.

```python
# Starter code
print("Information\n")
print()  # Add your formatted output here
```

**Problem 2 — Intermediate:** Create a formatted table showing 3 students with their names and GPAs, using tabs for alignment.

**Problem 3 — Challenge:** Create a program that prints a formatted schedule or menu using escape characters. Include at least 5 items with proper alignment.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use \n for new lines and \t for indentation
- Problem 2: Multiple \t characters will align columns
- Problem 3: Think about using \n and \t together for clean formatting
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
print("STUDENT PROFILE\n")
print("Name:\tAlex")
print("Grade:\t10")
print("Subject:\tComputer Science")

# Problem 2 Example
print("STUDENT GRADES\n")
print("Name\t\tGPA")
print("-" * 20)
print("Morgan\t\t3.85")
print("Jamie\t\t3.92")
print("Casey\t\t3.78")
```

</details>

---

# Day 5: Practice Lab — Print Art & Multi-line Programs
**Learning Target:** I can use comments, print formatting, and escape characters to create visually appealing programs.

### Key Concepts
This day is for practice and consolidation. You'll apply everything from Week 1:
- Using print() effectively
- Formatting output with escape characters
- Writing clear comments
- Understanding algorithms and pseudocode

A **practice lab** is hands-on time to build confidence with the fundamentals. You'll create your own program from scratch with creative freedom.

### Code Examples
```python
# Example 1: ASCII Art with formatted title
print("=== PYTHON PYRAMID ===\n")
print("    *")
print("   * *")
print("  * * *")
print(" * * * *")
print("* * * * *")

# Example 2: Formatted poem
print("ROSES AND CODE\n")
print("Roses are red,\nViolets are blue,\nI love to code,\nAnd now so do you!")

# Example 3: Simple banner with comments
# This program displays a welcome banner
print("\n" + "="*30)
print("  WELCOME TO PYTHON!")
print("="*30 + "\n")
```

### Guided Practice
Create one of the following projects (your choice):

**Option A: ASCII Art Gallery**
- Create a program that prints 3 different ASCII art images
- Each should be labeled with a comment
- Use formatting to make it visually interesting

**Option B: Formatted Information Card**
- Create a "card" (like a business card or sports card)
- Include formatted sections with borders using special characters
- Use tabs and newlines to align everything nicely

**Option C: ASCII Animation (Static)**
- Create a program that displays multiple "frames" of ASCII art
- You could show a rocket launching or a stick figure moving
- Use comments to explain each frame

### Practice Problems
**Problem 1 — Beginner:** Create a program that prints a simple shape (rectangle, triangle, or diamond) using * characters.

**Problem 2 — Intermediate:** Create a formatted "information card" for a character from a book/movie. Include name, age, special powers, and a border made of special characters.

**Problem 3 — Challenge:** Create a program that prints a more complex ASCII art image (at least 8 lines) with a title and description, properly formatted and commented.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use loops later in the course, but for now, just use multiple print statements
- Problem 2: Think about using = or - characters to create borders
- Problem 3: Plan your image first on paper, then convert to code
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example (Triangle)
print("   *")
print("  * *")
print(" * * *")
print("* * * *")

# Problem 2 Example (Character Card)
print("+" + "-"*28 + "+")
print("| CHARACTER CARD          |")
print("|" + "-"*28 + "|")
print("| Name:    Harry Potter   |")
print("| Age:     17             |")
print("| Powers:  Magic          |")
print("|" + "-"*28 + "|")
print("+  " + "-"*24 + "  +")

# Problem 3 Example (Simple House)
print("       /\\")
print("      /  \\")
print("     / [] \\")
print("    /      \\")
print("   /________\\")
print("   |        |")
print("   | []  [] |")
print("   |________|")
```

</details>

---

# WEEK 2: VARIABLES & DATA TYPES

# Day 6: Variables — Naming Rules, Assignment & Reassignment
**Learning Target:** I can create variables, assign values, and reassign them correctly.

### Key Concepts
A **variable** is a named container that stores a value in the computer's memory. Think of it like a labeled box—you put something inside and give it a name so you can refer to it later. In Python, creating a variable is simple: `variable_name = value`

**Variable naming rules:**
- Cannot contain spaces; use underscores instead: `first_name` not `first name`
- Cannot start with a number: `age1` is okay, `1age` is not
- Cannot use special characters like `!@#$%`
- Cannot be Python keywords like `print`, `if`, `while`, `for`
- Are case-sensitive: `score` and `Score` are different variables
- Should be descriptive: `student_name` is better than `x`

**Naming conventions** (best practices):
- Use lowercase with underscores: `my_age`, `favorite_color`
- Avoid single letters unless it's a loop counter: use `total_score` not `s`
- Be specific: `student_count` is better than `number`

**Assignment** means storing a value in a variable: `name = "Alex"`. The equals sign here is not "equals" mathematically—it means "assign the right side to the left side."

**Reassignment** means changing what a variable holds. A variable can store different values throughout a program: `score = 90; score = 95;` Now score holds 95.

### Code Examples
```python
# Creating variables and assigning values
name = "Morgan"
age = 17
gpa = 3.85
is_honors = True

print(name)        # Morgan
print(age)         # 17
print(gpa)         # 3.85
print(is_honors)   # True

# Reassigning variables
score = 85
print(score)       # 85
score = 92
print(score)       # 92 (changed!)

# Multiple assignment (assigning multiple variables at once)
first, last, grade = "Jordan", "Smith", 10
print(first, last, grade)  # Jordan Smith 10

# Using variables in output
player = "Alex"
points = 23
print(f"{player} scored {points} points")  # Alex scored 23 points
```

### Guided Practice
Create a program that:
1. Creates 5 variables with different data (your name, age, GPA, favorite subject, and whether you like math)
2. Prints each variable on a separate line
3. Then reassigns at least one variable to a new value
4. Prints the updated value
5. Include at least 2 comments explaining your code

### Practice Problems
**Problem 1 — Beginner:** Declare one variable for each piece of information: your name, your age, your height (as a decimal), and whether you're a student. Then print all of them.

```python
# Starter code
my_name =
my_age =
my_height =
am_student =

print()
```

**Problem 2 — Intermediate:** Create a program that demonstrates variable reassignment. Start with `x = 5`, print it, then change it to `x = 15`, and print it again. Add comments explaining what's happening.

**Problem 3 — Challenge:** Create a program that demonstrates that `score` and `Score` are different variables by assigning different values to each and printing both.

<details>
<summary>💡 Hints</summary>

- Problem 1: Don't forget that some variables need quotes, others don't
- Problem 2: Comments should explain that reassignment changes what the variable holds
- Problem 3: This shows case-sensitivity in Python
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
my_name = "Taylor"
my_age = 16
my_height = 5.75
am_student = True

print(my_name)
print(my_age)
print(my_height)
print(am_student)

# Problem 2 Example
x = 5
print(f"x starts as: {x}")
x = 15
print(f"x is now: {x}")  # Reassignment changes the value

# Problem 3 Example
score = 95
Score = 87
print(f"score = {score}, Score = {Score}")  # Two different variables!
```

</details>

---

# Day 7: Data Types — int, float, str, bool & the type() Function
**Learning Target:** I can identify and work with Python's four basic data types.

### Key Concepts
Python has four main basic data types:

1. **str (string):** Text, enclosed in quotes. Examples: `"Alice"`, `'hello'`, `"123 Main St"`
   - Strings are for any text, including numbers that shouldn't be calculated
   - Both single and double quotes work, but be consistent in a program

2. **int (integer):** Whole numbers without decimals. Examples: `42`, `-7`, `0`, `1000000`
   - Can be positive, negative, or zero
   - Used for counting, ages, scores, etc.

3. **float (floating-point):** Numbers with decimals. Examples: `3.14`, `-0.5`, `99.99`, `2.0`
   - Used for measurements, prices, ratings, etc.
   - Even `5.0` is a float because it has a decimal point

4. **bool (boolean):** True or False (always capitalized in Python)
   - Used for yes/no, on/off, enrolled/not enrolled situations
   - Only two possible values: True or False

The `type()` function tells you what data type a value is. It returns a response like `<class 'str'>` or `<class 'int'>`.

### Code Examples
```python
# String variables
name = "Alex"
city = "Nashville"
print(name)           # Alex
print(type(name))     # <class 'str'>

# Integer variables
age = 17
score = 95
print(age)            # 17
print(type(age))      # <class 'int'>

# Float variables
gpa = 3.85
price = 19.99
print(gpa)            # 3.85
print(type(gpa))      # <class 'float'>

# Boolean variables
is_enrolled = True
is_absent = False
print(is_enrolled)    # True
print(type(is_enrolled))  # <class 'bool'>

# Checking types
print(type("hello"))     # <class 'str'>
print(type(42))          # <class 'int'>
print(type(3.14))        # <class 'float'>
print(type(True))        # <class 'bool'>

# Important: "5" and 5 are different!
text_number = "5"        # String
actual_number = 5        # Integer
print(type(text_number))     # <class 'str'>
print(type(actual_number))   # <class 'int'>
```

### Guided Practice
Create a program that:
1. Creates variables of all four data types
2. Prints each variable with its type
3. Explains in comments what each type is used for
4. Shows the difference between `"17"` and `17`

### Practice Problems
**Problem 1 — Beginner:** Declare one variable of each data type (str, int, float, bool) about yourself and print them all.

```python
# Starter code
name =
age =
height =
is_student =

print()  # Print all variables here
```

**Problem 2 — Intermediate:** Create variables for a student profile (name, age, GPA, and whether they're on honor roll). Print each variable with its type.

**Problem 3 — Challenge:** Write code to demonstrate that `type("3.14")` returns `<class 'str'>` while `type(3.14)` returns `<class 'float'>`. Explain in comments why this matters.

<details>
<summary>💡 Hints</summary>

- Problem 1: Strings need quotes, booleans are True or False (capitalized)
- Problem 2: GPA should be a float, name should be a string
- Problem 3: Quotes make anything a string, including numbers
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = "Jordan"
age = 16
height = 5.75
is_student = True

print(name, type(name))
print(age, type(age))
print(height, type(height))
print(is_student, type(is_student))

# Problem 2 Example
student_name = "Sam"
student_age = 17
student_gpa = 3.9
is_honors = True

print(f"{student_name}: {type(student_name)}")
print(f"{student_age}: {type(student_age)}")
print(f"{student_gpa}: {type(student_gpa)}")
print(f"Honors: {type(is_honors)}")

# Problem 3 Example
as_text = "3.14"
as_number = 3.14
print(type(as_text))      # <class 'str'>
print(type(as_number))    # <class 'float'>
# Quotes make it text; without quotes it's a number
```

</details>

---

# Day 8: User Input & String Concatenation
**Learning Target:** I can collect user input and combine text and variables using concatenation.

### Key Concepts
The `input()` function pauses the program and waits for the user to type something, then press Enter. It displays a prompt (message) to guide the user. **Important:** `input()` always returns a **string**, even if the user types numbers like `17`.

**String concatenation** means combining strings together using the `+` operator. Example: `"Hello" + " " + "World"` = `"Hello World"`

You can concatenate:
- String literals (text in quotes)
- String variables
- Multiple strings in one statement

**Example:**
```python
first_name = "Alex"
last_name = "Smith"
full_name = first_name + " " + last_name  # "Alex Smith"
```

**Important:** You can only concatenate strings. To combine strings with numbers, you must convert the number to a string first (or use f-strings, which we'll learn on Day 14).

### Code Examples
```python
# Basic input
name = input("What is your name? ")
print("Hello, " + name + "!")

# Multiple inputs
first = input("First name: ")
last = input("Last name: ")
full = first + " " + last
print("Your name is: " + full)

# Concatenation examples
greeting = "Hello"
username = "Alex"
message = greeting + ", " + username + "!"
print(message)  # Hello, Alex!

# Mixing variables and literals
age = "17"  # Note: this is a string!
print("I am " + age + " years old")

# Multiple concatenations
print("Welcome, " + name + "! You entered: " + name)
```

### Guided Practice
Create a program that:
1. Asks the user for their first and last name
2. Combines them into a full name using concatenation
3. Asks for their favorite hobby
4. Prints a sentence using all the information with proper formatting
5. Include at least one comment

### Practice Problems
**Problem 1 — Beginner:** Write a program that asks the user for their name and favorite color, then prints a sentence combining both using concatenation.

```python
# Starter code
name = input()
color = input()
print()  # Print the combined message
```

**Problem 2 — Intermediate:** Write a program that asks for a student's name, school, and grade, then prints a formatted introduction sentence.

**Problem 3 — Challenge:** Write a program that asks for three favorite things (foods, games, or activities), then prints a sentence combining all three.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use + to combine the strings
- Problem 2: Make sure to include spaces in your concatenation
- Problem 3: Remember to include spaces between your concatenated strings
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = input("What is your name? ")
color = input("What is your favorite color? ")
print("Hello, " + name + "! I like " + color + " too!")

# Problem 2 Example
student_name = input("Student name: ")
school = input("School name: ")
grade = input("Grade: ")
print(student_name + " goes to " + school + " and is in grade " + grade)

# Problem 3 Example
food = input("Favorite food: ")
game = input("Favorite game: ")
activity = input("Favorite activity: ")
print("I love " + food + ", playing " + game + ", and " + activity + "!")
```

</details>

---

# Day 9: Type Conversion — int(), float(), str() with input()
**Learning Target:** I can convert user input to numeric data types for calculations.

### Key Concepts
Since `input()` always returns a string, you must **convert** the string to a number before using it in calculations. This is called **type conversion** or **casting**.

Three main conversion functions:
- `int()` - Converts a value to an integer (whole number)
- `float()` - Converts a value to a float (decimal number)
- `str()` - Converts a value to a string (text)

**Important notes:**
- `int("5")` works → 5
- `int("5.5")` fails → error (can't convert string with decimal directly to int)
- `int(5.9)` works → 5 (truncates/removes the decimal)
- `float("5")` works → 5.0
- `float("5.5")` works → 5.5
- `str(5)` works → "5" (now it's text)

**Common pattern:** `variable = int(input("Prompt: "))` or `variable = float(input("Prompt: "))`

### Code Examples
```python
# Converting input to int
age = int(input("How old are you? "))
print(age)         # Now it's a number, not text

# Converting input to float
height = float(input("How tall are you (in feet)? "))
print(height)      # Now it's a decimal number

# Converting numbers to strings
score = 95
message = "Your score: " + str(score)
print(message)     # Concatenation works now!

# Using converted input in calculations
hours = int(input("Hours worked: "))
pay = hours * 15   # This works because hours is an int
print(f"You earned: ${pay}")

# Multiple conversions
num1 = int(input("First number: "))
num2 = int(input("Second number: "))
sum_result = num1 + num2
print(f"Sum: {sum_result}")
```

### Guided Practice
Create a simple calculator program that:
1. Asks the user for two numbers using `input()`
2. Converts both to integers or floats
3. Calculates the sum, difference, and product
4. Prints the results with labels

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

**Problem 2 — Intermediate:** Write a miles-to-kilometers converter. Ask the user for miles (as a float) and print the equivalent in km (1 mile = 1.60934 km).

**Problem 3 — Challenge:** Write a program that asks for a principal amount (starting money), interest rate (as a decimal), and years, then calculates compound interest.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use the arithmetic operators to combine num1 and num2
- Problem 2: Remember to convert input to float, then multiply
- Problem 3: Formula: New Amount = Principal × (1 + rate)^years
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

# Problem 3 Example
principal = float(input("Principal: $"))
rate = float(input("Interest rate (as decimal): "))
years = int(input("Years: "))
new_amount = principal * ((1 + rate) ** years)
print(f"After {years} years: ${new_amount:.2f}")
```

</details>

---

# Day 10: Practice Lab — Interactive Programs with Input/Output
**Learning Target:** I can create interactive programs that collect input, process it, and produce formatted output.

### Key Concepts
This day consolidates Week 2 learning. You'll create programs that:
- Ask users for information
- Store it in variables
- Process it (possibly with calculations)
- Display results in a user-friendly way

A good interactive program:
- Has clear prompts that tell users what to enter
- Processes input (conversion if needed)
- Shows results with labels and formatting
- Uses comments to explain the logic

### Code Examples
```python
# Example: Personal Profile
print("=== PERSONAL PROFILE ===\n")
first_name = input("First name: ")
last_name = input("Last name: ")
age = int(input("Age: "))
gpa = float(input("GPA: "))

print("\n=== YOUR PROFILE ===")
print("Name: " + first_name + " " + last_name)
print(f"Age: {age}")
print(f"GPA: {gpa}")
print(f"Birth year (approximately): {2026 - age}")
```

### Guided Practice
Create a complete interactive program (choose one):

**Option A: Student Information Program**
- Collect: name, grade, age, favorite subject, GPA
- Calculate: approximate birth year
- Display everything in a formatted profile

**Option B: Simple Currency Converter**
- Collect: an amount in USD
- Collect: which currency to convert to (EUR, JPY, GBP)
- Calculate: the converted amount
- Display with proper formatting

**Option C: Personal Statistics**
- Collect: name, height (in inches), weight (in lbs), age
- Calculate: BMI if desired
- Display in a formatted card

### Practice Problems
**Problem 1 — Beginner:** Create a program that asks for a student's name and three test scores, then calculates and displays the average.

**Problem 2 — Intermediate:** Create a program that asks for hours worked and hourly rate, then calculates gross pay, tax (15%), and net pay.

**Problem 3 — Challenge:** Create a program that builds a "character sheet" for a game. Ask for name, health, mana, strength, and level, then display everything formatted nicely.

<details>
<summary>💡 Hints</summary>

- Problem 1: Ask for three separate scores, add them, divide by 3
- Problem 2: Use proper formatting for money output (dollar signs, 2 decimals)
- Problem 3: Use decorative characters to make a nice border
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = input("Student name: ")
score1 = float(input("Test 1 score: "))
score2 = float(input("Test 2 score: "))
score3 = float(input("Test 3 score: "))
average = (score1 + score2 + score3) / 3
print(f"{name}'s average: {average:.2f}")

# Problem 2 Example
hours = float(input("Hours worked: "))
rate = float(input("Hourly rate: $"))
gross = hours * rate
tax = gross * 0.15
net = gross - tax
print(f"Gross: ${gross:.2f}")
print(f"Tax (15%): ${tax:.2f}")
print(f"Net: ${net:.2f}")
```

</details>

---

# WEEK 3: BASIC CALCULATIONS & EXPRESSIONS

# Day 11: Arithmetic Operators & Their Uses
**Learning Target:** I can use arithmetic operators to solve mathematical problems.

### Key Concepts
Python has seven main arithmetic operators:
- `+` **Addition:** combines two numbers
- `-` **Subtraction:** finds the difference
- `*` **Multiplication:** combines groups
- `/` **Division:** splits a quantity, always returns float even for whole numbers (10 / 2 = 5.0)
- `//` **Floor Division:** divides and rounds down to the nearest whole number (10 // 3 = 3)
- `%` **Modulus (Remainder):** returns what's left over after division (10 % 3 = 1)
- `**` **Exponentiation (Power):** raises a number to a power (2 ** 3 = 8)

**Key points:**
- `/` always returns a float: `10 / 2` = `5.0` (not 5)
- `//` returns an integer (floor division): `10 // 3` = `3`
- `%` is useful for checking if numbers are divisible or finding patterns
- `**` is used for powers and roots: `9 ** 0.5` = `3.0` (square root)

**Real-world uses:**
- Addition: total cost, total time, total distance
- Subtraction: change due, time remaining, difference
- Multiplication: total cost (price × quantity), area, compound calculations
- Division: average, unit price, splitting
- Modulus: checking if even/odd, cycling through patterns, remainders
- Exponentiation: compound interest, area/volume calculations, physics

### Code Examples
```python
# Basic arithmetic
print(10 + 3)      # 13
print(10 - 3)      # 7
print(10 * 3)      # 30
print(10 / 3)      # 3.3333... (float)
print(10 // 3)     # 3 (floor division)
print(10 % 3)      # 1 (remainder)
print(2 ** 8)      # 256 (2 to the power of 8)

# Using variables
principal = 1000
rate = 0.05
interest = principal * rate
print(f"Interest: ${interest:.2f}")

# Modulus for practical use
minutes = 95
hours = minutes // 60
remaining_minutes = minutes % 60
print(f"{minutes} minutes = {hours}h {remaining_minutes}m")

# Exponentiation
base = 5
exponent = 3
result = base ** exponent
print(f"{base} to the power of {exponent} = {result}")
```

### Guided Practice
Create a program that:
1. Uses all 7 arithmetic operators with the same two numbers
2. Shows the result of each operation with a label
3. Includes comments explaining what each operator does
4. Demonstrate a real-world use of modulus (e.g., converting time)

### Practice Problems
**Problem 1 — Beginner:** Write a program that asks for two numbers and prints their sum, difference, product, and quotient.

**Problem 2 — Intermediate:** Convert 365 minutes to hours and remaining minutes using `//` and `%`. Display the result clearly.

**Problem 3 — Challenge:** Write a program that calculates the area and perimeter of a rectangle given length and width. (Area = L × W, Perimeter = 2L + 2W)

<details>
<summary>💡 Hints</summary>

- Problem 1: Use all four basic operators with the same two numbers
- Problem 2: Use // to get hours, % to get remaining minutes
- Problem 3: Make sure your output is labeled and formatted nicely
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
num1 = 15
num2 = 4
print(f"{num1} + {num2} = {num1 + num2}")
print(f"{num1} - {num2} = {num1 - num2}")
print(f"{num1} * {num2} = {num1 * num2}")
print(f"{num1} / {num2} = {num1 / num2:.2f}")

# Problem 2 Example
total_minutes = 365
hours = total_minutes // 60
remaining = total_minutes % 60
print(f"{total_minutes} minutes = {hours} hours and {remaining} minutes")

# Problem 3 Example
length = 12
width = 5
area = length * width
perimeter = 2 * length + 2 * width
print(f"Rectangle: {length} × {width}")
print(f"Area: {area} sq units")
print(f"Perimeter: {perimeter} units")
```

</details>

---

# Day 12: Order of Operations (PEMDAS) in Python
**Learning Target:** I can apply the order of operations correctly in Python expressions.

### Key Concepts
Python follows the standard mathematical order of operations, called **PEMDAS** (or BODMAS in some countries):

1. **Parentheses** (or Brackets) — calculations inside () first
2. **Exponents** (or Orders) — powers like `**`
3. **Multiplication & Division** — left to right (same precedence)
4. **Addition & Subtraction** — left to right (same precedence)

**Important:** Operators with the same precedence are evaluated left to right.

Examples:
- `2 + 3 * 4` = `2 + 12` = `14` (NOT `5 * 4 = 20`)
- `(2 + 3) * 4` = `5 * 4` = `20` (parentheses first!)
- `10 - 5 - 2` = `5 - 2` = `3` (left to right)
- `2 ** 3 ** 2` = `2 ** 9` = `512` (exponents are right to left!)

**Use parentheses** to make your intent clear, even if not strictly necessary:
- `(2 + 3) * 4` is clearer than `2 + 3 * 4`
- `(principal + interest)` is clearer than showing the calculation

### Code Examples
```python
# Order of operations examples
print(2 + 3 * 4)           # 14, not 20
print((2 + 3) * 4)         # 20
print(10 - 3 - 2)          # 5 (left to right)
print(2 ** 3 ** 2)         # 512 (right to left for exponents)
print((2 ** 3) ** 2)       # 64 (8 squared)

# Real-world calculation: compound interest
principal = 1000
rate = 0.05  # 5%
years = 3
amount = principal * (1 + rate) ** years
print(f"Amount after {years} years: ${amount:.2f}")

# Calculating average with proper order
score1, score2, score3 = 85, 92, 78
average = (score1 + score2 + score3) / 3
print(f"Average: {average:.2f}")

# Temperature conversion
fahrenheit = 68
celsius = (fahrenheit - 32) * 5 / 9
print(f"{fahrenheit}°F = {celsius:.1f}°C")
```

### Guided Practice
Create a program that:
1. Calculates the area of a rectangle with complex formula using parentheses
2. Calculates the volume of a rectangular box (length × width × height)
3. Demonstrates why parentheses matter by showing two different results
4. Includes comments explaining the order of operations

### Practice Problems
**Problem 1 — Beginner:** Predict the output of these expressions, then write code to verify:
- `5 + 3 * 2`
- `(5 + 3) * 2`
- `10 / 2 * 5`
- `10 / (2 * 5)`

**Problem 2 — Intermediate:** Write a program that calculates the area of a triangle using the formula: Area = (base × height) / 2. Ensure proper order of operations.

**Problem 3 — Challenge:** Write a program that calculates the future value using compound interest: FV = P(1 + r)^n where P=principal, r=rate, n=years. Use proper parentheses.

<details>
<summary>💡 Hints</summary>

- Problem 1: Remember PEMDAS—multiplication before addition
- Problem 2: Make sure to use parentheses clearly
- Problem 3: The (1 + r) must be calculated before raising to power n
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Verification
print(5 + 3 * 2)          # 11 (multiply first)
print((5 + 3) * 2)        # 16 (parentheses first)
print(10 / 2 * 5)         # 25.0 (left to right)
print(10 / (2 * 5))       # 1.0 (parentheses first)

# Problem 2 Example
base = 8
height = 6
area = (base * height) / 2
print(f"Triangle area: {area}")

# Problem 3 Example
principal = 500
rate = 0.04
years = 10
future_value = principal * (1 + rate) ** years
print(f"Future value: ${future_value:.2f}")
```

</details>

---

# Day 13: Math with Variables — Building Calculator Programs
**Learning Target:** I can build calculator-style programs with variables and arithmetic.

### Key Concepts
Now you can combine what you've learned:
- User input collection
- Type conversion
- Variables and reassignment
- Arithmetic operators
- Order of operations
- Output formatting

**Steps for building calculation programs:**
1. Ask the user for necessary values using `input()`
2. Convert to appropriate types (int or float)
3. Store in well-named variables
4. Perform calculations with proper order of operations
5. Display results clearly with labels and formatting

**Best practices:**
- Use descriptive variable names
- Add comments explaining complex calculations
- Format output with proper decimal places (use f-strings)
- Show calculation steps or intermediate results when helpful
- Include units (dollars, meters, etc.) in output

### Code Examples
```python
# Example 1: Tip Calculator
bill = float(input("Bill amount: $"))
tip_percent = float(input("Tip percentage: "))
tip = bill * (tip_percent / 100)
total = bill + tip
print(f"Tip: ${tip:.2f}")
print(f"Total: ${total:.2f}")

# Example 2: Area and Perimeter
length = float(input("Rectangle length: "))
width = float(input("Rectangle width: "))
area = length * width
perimeter = 2 * (length + width)
print(f"Area: {area:.2f} sq units")
print(f"Perimeter: {perimeter:.2f} units")

# Example 3: Average grade calculator
grades = []  # We'll learn about lists later, but for now:
grade1 = int(input("Grade 1: "))
grade2 = int(input("Grade 2: "))
grade3 = int(input("Grade 3: "))
average = (grade1 + grade2 + grade3) / 3
print(f"Average: {average:.2f}")
```

### Guided Practice
Create a calculator program for one of these:
- **Loan Payment Calculator:** Ask for loan amount, interest rate, and years. Calculate monthly payment.
- **Gas Mileage Calculator:** Ask for miles driven and gallons used. Calculate MPG.
- **Age Calculator:** Ask for birth year. Calculate age and years until 100.

### Practice Problems
**Problem 1 — Beginner:** Create a program that converts US dollars to euros. Ask for dollar amount and exchange rate, then display euros.

**Problem 2 — Intermediate:** Create a program that calculates the total cost of items with tax. Ask for item price and tax rate, then calculate and display total.

**Problem 3 — Challenge:** Create a program that calculates paycheck details. Ask for hours worked, hourly rate, and tax percentage. Calculate gross pay, tax amount, and net pay.

<details>
<summary>💡 Hints</summary>

- Problem 1: Multiply dollars by exchange rate
- Problem 2: Remember order of operations; tax = price × tax_rate
- Problem 3: Show all three calculations (gross, tax, net)
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
dollars = float(input("Dollars: $"))
rate = float(input("Exchange rate (1 USD = ? EUR): "))
euros = dollars * rate
print(f"${dollars:.2f} USD = €{euros:.2f} EUR")

# Problem 2 Example
price = float(input("Item price: $"))
tax_rate = float(input("Tax rate (as decimal): "))
tax = price * tax_rate
total = price + tax
print(f"Price: ${price:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Total: ${total:.2f}")

# Problem 3 Example
hours = float(input("Hours worked: "))
rate = float(input("Hourly rate: $"))
tax_percent = float(input("Tax percentage: "))
gross = hours * rate
tax = gross * (tax_percent / 100)
net = gross - tax
print(f"Gross: ${gross:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Net: ${net:.2f}")
```

</details>

---

# Day 14: F-Strings — Professional Output Formatting
**Learning Target:** I can format output using f-strings for professional-looking results.

### Key Concepts
**F-strings** (formatted string literals) are a powerful way to embed variables and expressions inside strings. They start with `f"..."` or `f'...'`.

**Basic syntax:** `f"text {variable} more text"`

**Formatting options:**
- `:d` = integer (no decimals)
- `:f` = float with decimals (default is 6)
- `:.2f` = float with exactly 2 decimal places
- `:>10` = right-align in 10 characters
- `:<10` = left-align in 10 characters
- `:^10` = center in 10 characters

**Examples:**
```python
name = "Alex"
age = 17
gpa = 3.85

# Basic f-string
print(f"Name: {name}, Age: {age}")

# Formatting decimals
print(f"GPA: {gpa:.2f}")  # 3.85

# Expressions inside f-strings
print(f"Next year I'll be {age + 1}")

# Alignment
print(f"{name:>10}")  # Right-aligned in 10 spaces
```

**F-strings vs string concatenation:**
- Old way: `"Total: $" + str(total)`
- F-string way: `f"Total: ${total:.2f}"`

F-strings are more readable and flexible!

### Code Examples
```python
# Money formatting
price = 19.5
print(f"Price: ${price:.2f}")  # $19.50

# Table with alignment
print(f"{'Item':<15} {'Price':>10}")
print(f"{'Bread':<15} {'$3.50':>10}")
print(f"{'Milk':<15} {'$2.25':>10}")

# Mixing text and variables
name = "Jordan"
score = 95.7
print(f"{name} scored {score:.1f}%")

# Using expressions
hours = 8
rate = 15.50
total_pay = hours * rate
print(f"Pay: {hours} hours × ${rate:.2f}/hr = ${total_pay:.2f}")
```

### Guided Practice
Create a program that:
1. Asks for product name, quantity, and unit price
2. Calculates total
3. Displays a formatted receipt with aligned columns
4. Shows all prices with exactly 2 decimal places

Example output:
```
===== RECEIPT =====
Item              Qty    Unit Price    Total
Bread              2      $3.50       $7.00
Milk               1      $2.25       $2.25
===== TOTAL: $9.25 =====
```

### Practice Problems
**Problem 1 — Beginner:** Write a program that displays student info formatted nicely using f-strings.

**Problem 2 — Intermediate:** Create a formatted table showing 3 products with prices. Use alignment and decimal formatting.

**Problem 3 — Challenge:** Create a program that calculates and displays a formatted invoice with items, quantities, prices, subtotal, tax, and total.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use {variable:.2f} for numbers with decimals
- Problem 2: Use {text:>15} to right-align in a column
- Problem 3: Include line breaks and borders for a professional look
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = "Alex Johnson"
gpa = 3.85
age = 16
print(f"Student: {name}")
print(f"GPA: {gpa:.2f}")
print(f"Age: {age}")

# Problem 2 Example
print(f"{'Item':<15} {'Price':>10}")
print("-" * 25)
print(f"{'Apples':<15} {'$2.99':>10}")
print(f"{'Bananas':<15} {'$1.50':>10}")
print(f"{'Oranges':<15} {'$3.25':>10}")

# Problem 3 Example (simplified)
item = "Notebook"
qty = 3
price_each = 5.99
total = qty * price_each
tax = total * 0.08
final = total + tax
print("=== INVOICE ===")
print(f"{item} × {qty} @ ${price_each:.2f} = ${total:.2f}")
print(f"Tax (8%): ${tax:.2f}")
print(f"Total: ${final:.2f}")
```

</details>

---

# Day 15: Practice Lab — Unit Converters & Calculators
**Learning Target:** I can integrate all Unit 1 concepts to build functional, formatted programs.

### Key Concepts
This lab consolidates Weeks 2-3. You'll apply:
- Input collection and type conversion
- Variables and reassignment
- All arithmetic operators
- Order of operations
- Professional output formatting with f-strings

**Real-world programs** solve practical problems:
- Unit converters (temperature, distance, weight, currency)
- Calculators (tips, taxes, grades, loans)
- Data processors (averages, totals, percentages)

### Code Examples
```python
# Example: Temperature Converter
print("=== TEMPERATURE CONVERTER ===\n")
celsius = float(input("Temperature in Celsius: "))
fahrenheit = (celsius * 9/5) + 32
print(f"{celsius}°C = {fahrenheit:.1f}°F")

# Example: Unit Converter
km = float(input("Distance in kilometers: "))
miles = km * 0.621371
print(f"{km} km = {miles:.2f} miles")
```

### Guided Practice
Create a complete program (choose one):

**Option A: Temperature Converter**
- Asks user for temperature in Celsius
- Converts to Fahrenheit: F = C × 9/5 + 32
- Displays with professional formatting

**Option B: Weight Unit Converter**
- Asks for weight in pounds
- Converts to kilograms (1 lb = 0.453592 kg) and vice versa
- Shows both conversions with proper formatting

**Option C: Time Calculator**
- Asks for hours and minutes
- Calculates total seconds
- Calculates total minutes
- Displays breakdown

### Practice Problems
**Problem 1 — Beginner:** Create a currency converter. Ask for USD and display equivalent in EUR (use 0.92 as exchange rate).

**Problem 2 — Intermediate:** Create a distance converter. Ask for miles and display kilometers, meters, and feet.

**Problem 3 — Challenge:** Create a compound interest calculator. Ask for principal, annual rate, and years. Calculate and display the amount at the end using: A = P(1 + r/100)^n

<details>
<summary>💡 Hints</summary>

- Problem 1: Use proper decimal formatting
- Problem 2: 1 mile = 1.60934 km, 1 km = 3280.84 feet
- Problem 3: Use ** for exponentiation; remember order of operations
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
usd = float(input("Amount in USD: $"))
eur = usd * 0.92
print(f"${usd:.2f} USD = €{eur:.2f} EUR")

# Problem 2 Example
miles = float(input("Distance in miles: "))
km = miles * 1.60934
feet = miles * 5280
print(f"{miles} miles = {km:.2f} km")
print(f"{miles} miles = {feet:.0f} feet")

# Problem 3 Example
principal = float(input("Principal: $"))
rate = float(input("Annual rate (%): "))
years = int(input("Years: "))
amount = principal * (1 + rate/100) ** years
print(f"After {years} years: ${amount:.2f}")
```

</details>

---

# WEEK 4: SOFTWARE DEVELOPMENT & REVIEW

# Day 16: The 5-Step Software Development Process
**Learning Target:** I can apply the 5-step software development process to plan and code programs.

### Key Concepts
Professional programmers don't just sit down and start typing. They follow a systematic process:

**Step 1: Define (Ask)**
- Understand the problem completely
- What are the inputs?
- What should the output be?
- Are there any constraints?
- Example: "Calculate the area of a rectangle. Input: length and width. Output: area."

**Step 2: Plan (Design)**
- Break down the solution into steps
- Write pseudocode (English-like instructions, not code)
- Draw flowcharts if helpful
- Think about edge cases

**Step 3: Code**
- Translate your plan into Python
- Write clean, readable code
- Use descriptive variable names
- Include helpful comments

**Step 4: Test**
- Run your program with different inputs
- Test normal cases, edge cases (very small, very large, zero)
- Check that output is correct
- Look for any errors

**Step 5: Refine (Debug & Improve)**
- Fix any bugs found during testing
- Make code cleaner or more efficient
- Improve output formatting
- Add comments if needed

### Code Examples
```python
# Example: Temperature Converter following 5-step process

# Step 1: Define
# Input: temperature in Fahrenheit
# Output: temperature in Celsius
# Formula: C = (F - 32) × 5/9

# Step 2: Plan (pseudocode):
# a) Ask user for Fahrenheit temperature
# b) Convert using formula
# c) Round to 1 decimal place
# d) Display result

# Step 3: Code
fahrenheit = float(input("Enter temperature (°F): "))
celsius = (fahrenheit - 32) * 5 / 9
celsius_rounded = round(celsius, 1)
print(f"{fahrenheit}°F = {celsius_rounded}°C")

# Step 4: Test
# Test cases:
# - 32°F should be 0°C ✓
# - 212°F should be 100°C ✓
# - 68°F should be 20°C ✓

# Step 5: Refine
# Code looks good, clear variable names, good comments
```

### Guided Practice
Follow the 5-step process to create a BMI calculator:
1. **Define:** BMI = weight(lbs) / height(in)² × 703
2. **Plan:** Write pseudocode
3. **Code:** Write the Python program
4. **Test:** Try several inputs
5. **Refine:** Make sure output is clear

### Practice Problems
**Problem 1 — Beginner:** Follow the 5-step process to create a celsius-to-fahrenheit converter. F = C × 9/5 + 32

**Problem 2 — Intermediate:** Follow the 5-step process to create a simple savings calculator. Ask for starting balance, monthly savings, and months. Calculate total.

**Problem 3 — Challenge:** Follow the 5-step process to create a percentage grade calculator. Ask for points earned and points possible. Calculate percentage and assign a letter grade (90+=A, 80+=B, etc.)

<details>
<summary>💡 Hints</summary>

- Problem 1: Write your define and plan steps first!
- Problem 2: Test with edge cases like 0 months
- Problem 3: Use if statements (you'll learn soon!) or note this for later
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
# Step 1 - Define: Convert C to F using F = C × 9/5 + 32
# Step 2 - Plan: Ask for C, apply formula, display F
celsius = float(input("Celsius: "))
fahrenheit = celsius * 9/5 + 32
print(f"{celsius}°C = {fahrenheit:.1f}°F")
# Step 4 - Test: 0°C = 32°F ✓
# Step 5 - Refine: Code is clear and correct

# Problem 2 Example
principal = float(input("Starting balance: $"))
monthly = float(input("Monthly savings: $"))
months = int(input("Months: "))
total = principal + (monthly * months)
print(f"Total after {months} months: ${total:.2f}")
```

</details>

---

# Day 17: Debugging Intro — Syntax Errors & Reading Error Messages
**Learning Target:** I can identify and fix common syntax errors and type errors in Python.

### Key Concepts
Debugging is the process of finding and fixing errors in code. There are three main types of errors:

**Syntax Errors** - Breaking the rules of Python (code won't run):
- Misspelled keywords: `prin("Hello")` instead of `print("Hello")`
- Missing parentheses: `print "Hello"` instead of `print("Hello")`
- Missing quotes: `print(Hello)` instead of `print("Hello")`
- Wrong operator: `if a = 5` instead of `if a == 5`

**Type Errors** - Using the wrong data type:
- Trying to add a string and number: `"5" + 3`
- Trying to multiply a string by a float: `"hello" * 2.5`
- Not converting input: `age = input("Age: "); print(age + 10)`

**Logic Errors** - Code runs but produces wrong results:
- Incorrect formula: area = length + width instead of length × width
- Wrong order of operations
- Variable initialized to wrong value

**Reading error messages:**
When Python finds an error, it prints a message showing:
- The line number where the error occurred
- The type of error (SyntaxError, TypeError, etc.)
- A description of what went wrong

Example:
```
  File "program.py", line 3
    print("Hello"
           ^
SyntaxError: unexpected EOF while parsing
```

This means: Line 3 has a syntax error—probably a missing closing parenthesis.

### Code Examples
```python
# Syntax Error Examples

# Error: Missing closing parenthesis
# print("Hello"
# Fix:
print("Hello")

# Error: Misspelled function
# Print("Hello")
# Fix:
print("Hello")

# Error: Missing quotes
# print(Hello)
# Fix:
print("Hello")

# Type Error Example
# age = input("Age: ")
# print(age + 10)  # Can't add string to int!
# Fix:
age = int(input("Age: "))
print(age + 10)

# Logic Error Example
# length = 5
# width = 3
# area = length + width  # Should be multiplication!
# Fix:
area = length * width
```

### Guided Practice
Debug the following programs (I'll provide broken code):
1. A program with syntax errors
2. A program with type errors
3. A program with logic errors

Identify the error, explain what's wrong, and write the fix.

### Practice Problems
**Problem 1 — Beginner:** Debug this code:
```python
name = input(What is your name? )
age = int(input("Age: ")
print("Hello, " name + "!")
```

**Problem 2 — Intermediate:** Debug this code:
```python
score1 = int(input("Score 1: "))
score2 = input("Score 2: ")
average = (score1 + score2) / 2
print(f"Average: {average}")
```

**Problem 3 — Challenge:** Debug this code:
```python
principal = float(input("Principal: "))
rate = float(input("Rate: "))
years = input("Years: ")
total = principal * (1 + rate / 100) ** years
print(f"Total: ${total.2f}")
```

<details>
<summary>💡 Hints</summary>

- Problem 1: Look for missing quotes and parentheses
- Problem 2: Check that all variables are the same type before using them in math
- Problem 3: Look for data type issues and formatting issues
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Fixed
name = input("What is your name? ")
age = int(input("Age: "))
print("Hello, " + name + "!")

# Problem 2 Fixed
score1 = int(input("Score 1: "))
score2 = int(input("Score 2: "))  # Convert to int!
average = (score1 + score2) / 2
print(f"Average: {average}")

# Problem 3 Fixed
principal = float(input("Principal: "))
rate = float(input("Rate: "))
years = int(input("Years: "))  # Convert to int!
total = principal * (1 + rate / 100) ** years
print(f"Total: ${total:.2f}")  # Use colon notation
```

</details>

---

# Day 18: Mini-Project — Build a Complete Program from Scratch
**Learning Target:** I can design, code, and test a complete beginner program from scratch.

### Key Concepts
This day is your chance to showcase everything you've learned. You'll:
1. Choose or be given a real-world problem
2. Follow the 5-step development process
3. Create a complete, working program
4. Test it thoroughly
5. Present clean, well-commented code

### Guided Practice - Choose ONE Project

**Project A: Personal Expense Calculator**
- Collect: expense name, amount, category
- Calculate: total expenses, average expense
- Display: formatted summary
- Requirements: 3+ inputs, 1+ calculation, clear output

**Project B: Grade Calculator**
- Collect: student name, 4 test scores
- Calculate: average, letter grade (90+=A, 80+=B, 70+=C, etc.)
- Display: formatted grade report
- Requirements: string input, multiple numeric inputs, calculations, formatted output

**Project C: Trip Budget Planner**
- Collect: destination, days, daily budget
- Calculate: total budget, recommended daily spending by category (accommodation, food, activities)
- Display: formatted budget breakdown
- Requirements: multiple inputs, multiple calculations, formatted output

**Project D: Time Tracker**
- Collect: task name, hours worked, hourly rate
- Calculate: total pay, projected weekly/monthly earnings
- Display: formatted payment details
- Requirements: inputs, calculations with proper order of operations, formatting

### Requirements for Any Project
- **Input:** At least 3 different inputs using `input()`
- **Variables:** At least 4 variables of mixed types
- **Calculations:** At least 2 mathematical operations
- **Comments:** At least 3 comments explaining your code
- **Output:** Clear, formatted output using f-strings
- **Testing:** Evidence that you tested with multiple inputs

### Sample Program Structure
```python
# ===== PROGRAM TITLE & PURPOSE =====
# This program calculates...

# Step 1: Define & Plan (comments)
# Inputs: ...
# Calculation: ...
# Output: ...

# Step 3: Code
# Collect inputs
name = input("Name: ")
value1 = float(input("Value 1: "))
value2 = float(input("Value 2: "))

# Perform calculations
result = value1 + value2
average = result / 2

# Display results
print(f"\n=== RESULTS ===")
print(f"Name: {name}")
print(f"Total: {result:.2f}")
print(f"Average: {average:.2f}")

# Step 4: Testing notes:
# - Tested with: ...
# - Verified: ...
```

### Practice Problems (Pick 1 to complete)

**Option 1 (Beginner):** Create a simple interest calculator.
- Input: principal, rate (%), years
- Calculate: simple interest = principal × rate × years / 100, total = principal + interest
- Output: formatted statement showing starting amount, interest, and total

**Option 2 (Intermediate):** Create a restaurant bill calculator.
- Input: subtotal, tip percentage, tax rate
- Calculate: tax amount, tip amount, total
- Output: itemized receipt

**Option 3 (Challenge):** Create a home workout tracker.
- Input: name, exercises (count), minutes, calories burned
- Calculate: calories per minute, projected daily total (if 2 more workouts)
- Output: detailed workout summary with projections

### Submission Checklist
- [ ] Program runs without errors
- [ ] Has 3+ inputs
- [ ] Has 4+ variables
- [ ] Has 2+ calculations
- [ ] Has 3+ comments
- [ ] Uses f-strings for output
- [ ] Output is clear and labeled
- [ ] Tested with at least 2 different inputs

---

# Day 19: Unit Review — Vocabulary, Concepts & Practice Problems
**Learning Target:** I can review and consolidate all Unit 1 concepts in preparation for assessment.

### Key Concepts - Review

**Computer Science Fundamentals**
- Computer science = problem-solving with computers
- Algorithm = step-by-step procedure
- Program = algorithm written in code
- Pseudocode & flowcharts = planning tools

**Python Basics**
- Python interpreter reads and executes code
- `print()` displays output
- Comments start with `#`
- Case-sensitive (python ≠ Python)

**Variables & Data Types**
- Variable = named container for a value
- str = text (in quotes)
- int = whole numbers
- float = decimal numbers
- bool = True or False
- `type()` function identifies data types

**Input & Conversion**
- `input()` always returns a string
- `int()`, `float()`, `str()` convert types
- Must convert input before using in math

**Operators & Order of Operations**
- Arithmetic: `+`, `-`, `*`, `/`, `//`, `%`, `**`
- Order: Parentheses → Exponents → Mult/Div → Add/Sub
- PEMDAS = P-E-MD-AS (left to right for same precedence)

**Formatting & Functions**
- F-strings: `f"Text {variable} more"`
- Decimal formatting: `f"{value:.2f}"`
- `round()` function: rounds to decimal places
- Escape characters: `\n`, `\t`, `\\`, etc.

**Development Process**
- Define (understand problem)
- Plan (write pseudocode)
- Code (write Python)
- Test (try different inputs)
- Refine (fix and improve)

### Practice Problems (All Tiers)

**Beginner Problems:**
1. Write a program that prints your name, age, and favorite hobby, each on a separate line.
2. Create variables for name (str), age (int), height (float), and is_student (bool). Print each with its type.
3. Ask user for two numbers and print their sum, difference, product, and quotient.
4. Write a program that converts 120 minutes to hours and remaining minutes.
5. Predict the output: `print(2 + 3 * 4)` and explain using PEMDAS.

**Intermediate Problems:**
6. Create a miles-to-kilometers converter. Ask for miles, display kilometers (1 mile = 1.609 km).
7. Write a program that asks for a price and calculates total with 7% tax.
8. Create a program that asks for hours worked and hourly rate, calculates gross pay.
9. Debug this code: `name = input("Name: ); age = int(input("Age: ")); print(name age)`
10. Write a program that calculates the area and perimeter of a rectangle given length and width.

**Challenge Problems:**
11. Create a compound interest calculator: A = P(1 + r/100)^n
12. Write a program that calculates your age in days (approximate).
13. Create a "student profile" program that collects info and displays a formatted card.
14. Fix this code and explain the 3 errors: `GPA = Float(input("GPA: ")); print("Your GPA is" GPA)`
15. Create any calculator program of your choice following the 5-step process.

### Practice Answers
*Answers provided in the next section (Assessment Prep)*

---

# Day 20: Unit 1 Assessment
**Learning Target:** I can demonstrate mastery of Unit 1 concepts.

### Assessment Overview
This is your formal assessment for Unit 1. It will test:
- Understanding of computer science concepts
- Python syntax knowledge
- Ability to write working programs
- Problem-solving and debugging skills
- Code quality and documentation

### Assessment Format
Your teacher will provide:
- **Part A:** Written/multiple choice questions (10-15 questions)
- **Part B:** Code writing tasks (2-3 programs)
- **Part C:** Debugging/explanation tasks

### Topics Covered
- Computer science and algorithms
- Python print(), comments, variables
- Data types and type conversion
- User input collection
- Arithmetic operators and order of operations
- Output formatting with f-strings
- The 5-step development process
- Error identification and correction

### How to Prepare
1. Review the vocabulary on this page
2. Work through the practice problems on Day 19
3. Look back at your daily practice from Days 1-15
4. Make sure you can:
   - Write a program from scratch using input, math, and formatted output
   - Identify syntax and type errors
   - Apply the 5-step development process
   - Explain what your code does

### Tips for Success
- Read each question carefully
- Show your work and reasoning
- Test your code before submitting
- Write clear comments explaining your logic
- Use proper variable names and formatting
- If you get stuck, try breaking the problem into smaller steps

Good luck!

---

## Vocabulary & Quick Reference

**Key Terms:**
- **Algorithm:** Step-by-step procedure to solve a problem
- **Pseudocode:** English-like description of an algorithm
- **Flowchart:** Visual diagram representing an algorithm
- **Data Type:** Category of data (str, int, float, bool)
- **Variable:** Named container storing a value
- **Input:** Information the user gives to the program
- **Output:** Information the program displays to the user
- **Syntax:** Rules for writing code correctly
- **Comment:** Explanation in code, ignored by Python, starts with #
- **Operator:** Symbol representing an operation (+, -, *, etc.)
- **Function:** Pre-built code that performs a task (print, input, type, etc.)
- **Type Conversion:** Converting one data type to another
- **F-string:** Formatted string with embedded variables
- **Escape Character:** Special sequence like \n or \t

**Key Syntax & Functions:**
```python
# Comments
print("Output text")                    # Display output
variable = value                        # Create/assign variable
name = input("Prompt: ")               # Get user input
type(value)                             # Check data type
x = int(input("Number: "))             # Get and convert input to int
y = float(input("Number: "))           # Get and convert input to float
z = str(value)                          # Convert to string
print(f"Hello {name}, you are {age}")  # F-string formatting
print(f"Price: ${price:.2f}")           # F-string with decimal formatting
round(3.14159, 2)                      # Round to 2 decimals
```

**Arithmetic Operators:**
- `+` add
- `-` subtract
- `*` multiply
- `/` divide (returns float)
- `//` floor divide (integer division)
- `%` modulus (remainder)
- `**` exponentiation (power)

**Order of Operations (PEMDAS):**
1. **P**arentheses
2. **E**xponents (`**`)
3. **M**ultiplication & **D**ivision (left to right)
4. **A**ddition & **S**ubtraction (left to right)

**Escape Characters:**
- `\n` = newline
- `\t` = tab
- `\\` = backslash
- `\'` = single quote
- `\"` = double quote

**Common Formulas:**
- Temperature: C = (F - 32) × 5/9, F = C × 9/5 + 32
- Area of rectangle: A = length × width
- Perimeter of rectangle: P = 2L + 2W
- Area of triangle: A = (base × height) / 2
- Simple interest: I = principal × rate × time / 100

---

## Unit Assessment Prep

**Review Questions & Answers:**

1. **What is the difference between an algorithm and a program?**
   - An algorithm is a step-by-step procedure (language-independent). A program is an algorithm written in a programming language that a computer can execute.

2. **What are Python's four basic data types? Give an example of each.**
   - str: "hello" (text)
   - int: 42 (whole numbers)
   - float: 3.14 (decimals)
   - bool: True or False

3. **Why must `input()` be converted to `int()` or `float()` before doing math?**
   - `input()` always returns a string. You must convert it to a number before doing arithmetic operations.

4. **What does the `//` operator do? Give an example.**
   - Floor division: divides and rounds down to the nearest whole number. Example: 10 // 3 = 3

5. **Why is `x = "5"` different from `x = 5`? Demonstrate with code.**
   - "5" is a string (text), while 5 is an integer (number). `"5" + 3` causes an error, but `5 + 3 = 8` works.

6. **What is a variable? Why are they useful?**
   - A variable is a named container that stores a value. They allow us to store, reference, and reuse data throughout a program.

7. **What does the `type()` function do? Give an example.**
   - Returns the data type of a value. Example: `type("hello")` returns `<class 'str'>`

8. **Write the formula: Celsius to Fahrenheit conversion.**
   - F = C × 9/5 + 32

9. **What are three variable naming rules?**
   - Cannot start with a number
   - Cannot contain spaces (use underscores)
   - Cannot use Python keywords like print, if, while

10. **Explain the 5-step software development process.**
    - Define (understand the problem), Plan (write pseudocode), Code (write the program), Test (try different inputs), Refine (fix and improve).

11. **What does an f-string do? Write an example.**
    - F-strings embed variables in strings for easy formatting. Example: `f"My name is {name} and I am {age}"`

12. **What will this print?** `print(2 + 3 * 4)`
    - 14 (multiplication first: 3 * 4 = 12, then 2 + 12 = 14)

13. **What error is in this code?** `age = input("Age: "); print(age + 10)`
    - Type error: input() returns a string, can't add string to int. Fix: `age = int(input("Age: "))`

14. **Write a simple program that asks for a name and prints a greeting.**
    ```python
    name = input("What is your name? ")
    print(f"Hello, {name}!")
    ```

15. **What real-world problems can you solve with Python?**
    - Calculators, converters, data processing, analysis, automation, games, apps, and much more!

---

