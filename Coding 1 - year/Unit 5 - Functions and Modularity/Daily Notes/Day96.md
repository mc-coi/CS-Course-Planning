# Day 96: What Are Functions? Why Use Them?

**Learning Target:** I can define a function, explain why we use functions, and call a function using the correct syntax.

### Key Concepts

A **function** is a named block of code that performs a specific task. Instead of writing the same lines of code over and over, you bundle them into a function and give it a descriptive name. Then you can **call** the function by name whenever you need it to run.

Why use functions? **Reusability** is the main reason. If you need to sort a list in ten different places in your program, you don't write the sorting code ten times—you write it once in a function and call it ten times. This saves time, reduces errors, and makes your code easier to read. Functions also make programs **modular**, meaning they're built from smaller, independent pieces that are easier to understand and test.

The **`def` keyword** tells Python you're defining a new function. Here's the basic syntax:
```
def function_name():
    # code goes here (indented)
```

The function name should be descriptive. By convention, function names use lowercase letters and underscores (`say_hello`, `calculate_average`, `check_password`). After the function name comes a colon and then an **indented block** of code. The indentation is critical in Python—it tells Python which code belongs to the function.

To **call** a function, you use its name followed by parentheses: `function_name()`. When you call a function, Python jumps to that function, executes all the code inside it, and then returns to where it left off.

### Code Examples

```python
# Example 1: Define and call a simple function
def say_hello():
    print("Hello, friend!")

say_hello()  # This calls the function
say_hello()  # You can call it multiple times
say_hello()
```

```python
# Example 2: A function with multiple statements
def sing_song():
    print("🎵 Twinkle, twinkle, little star")
    print("How I wonder what you are")
    print("Up above the world so high")

sing_song()  # Prints all three lines
```

```python
# Example 3: Functions make code reusable
def print_separator():
    print("=" * 40)

print_separator()
print("Part 1: Introduction")
print_separator()
print("Part 2: Main Content")
print_separator()
```

### Guided Practice

1. Write a function called `greet()` that prints a friendly greeting.
2. Call your function three times.
3. Write another function called `print_box()` that prints a 5-character-wide box made of asterisks, like this:
```
*****
*   *
*   *
*   *
*****
```
4. Call `print_box()` to test it.

### Practice Problems

**Problem 1 — Beginner:** Write a function called `favorite_book()` that prints the title and author of your favorite book. Call it once.

```python
# Starter code
def favorite_book():
    # Your code here
    pass

# Call the function here
```

**Problem 2 — Intermediate:** Write a function called `print_menu()` that prints a simple menu for a restaurant (at least 3 items). Call it twice to show the menu appearing in two different parts of a program.

**Problem 3 — Challenge:** Write two functions: `print_top()` that prints a row of dashes (like `-----`), and `print_person()` that prints a simple ASCII person. Then call `print_top()`, `print_person()`, and `print_top()` in sequence to create a picture frame.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `print()` statements inside your function. Remember the indentation!
- Problem 2: Think about what makes a good menu. Use descriptive item names and prices.
- Problem 3: ASCII art is just text. A simple person might be: `👤 (O_O) |_|` or use characters like `O`, `|`, and `-`.
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
def favorite_book():
    print("Title: The Hobbit")
    print("Author: J.R.R. Tolkien")

favorite_book()
```

```python
# Problem 2 Example
def print_menu():
    print("=== MENU ===")
    print("1. Pizza - $12")
    print("2. Burger - $8")
    print("3. Salad - $6")
    print()

print("Customer 1:")
print_menu()
print("Customer 2:")
print_menu()
```

```python
# Problem 3 Example
def print_top():
    print("-------")

def print_person():
    print("  O")
    print(" /|\\")
    print(" / \\")

print_top()
print_person()
print_top()
```
</details>

---
