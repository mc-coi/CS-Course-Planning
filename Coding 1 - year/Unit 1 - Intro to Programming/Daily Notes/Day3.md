# Day 3: Intro to Python & the print() Function
**Learning Target:** I can set up Python and run a basic program using the print() function.

### Key Concepts
A **Python interpreter** reads your code line-by-line and executes it, translating it into actions the computer understands. Python is known for being beginner-friendly because it reads almost like English.

The `print()` function displays text (or other information) on the screen. Text must be enclosed in quotes (either single `'` or double `"`). Python is **case-sensitive**, meaning `print` and `Print` are different—only `print` (lowercase) works. This applies to all functions and variable names.

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

# You can print blank lines for spacing
print()
print("There was a blank line above")

# Printing numbers (no quotes needed for actual numbers)
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

Test your program by running it and verifying the output is exactly as you intended.

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

- Problem 1: Each print() creates a separate line of output
- Problem 2: Use comments with # to label what your haiku represents
- Problem 3: Use special characters like *, /, ^, \, | to create the image
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
print("Morgan")
print("Rivera")
print("10")

# Problem 2 Example
# My haiku about Python programming
print("Code flows like water")
print("Solving problems step by step")
print("Logic comes alive")

# Problem 3 Example (a simple tree)
print("    /\\")
print("   /  \\")
print("  /____\\")
print("    ||")
print("    ||")
```

</details>

---
