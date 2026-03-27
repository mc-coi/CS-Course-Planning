# Day 61: Building Text-Based Menu Systems

**Learning Target:** I can design and implement interactive menu systems that guide users through program options.

---

## Key Concepts

A **menu system** presents options to users and executes different code based on selection. Menu systems:
- Organize program functionality logically
- Make programs user-friendly
- Use if/elif/else for option selection
- Often loop (preview of next unit)

**Menu Design Principles:**
1. Display options clearly
2. Get user input
3. Validate choice
4. Execute appropriate action
5. Handle invalid choices gracefully
6. Ask if user wants to continue

---

## Code Examples

```python
# Simple single-level menu
print("=== Main Menu ===")
print("1. Add numbers")
print("2. Subtract numbers")
print("3. Multiply numbers")
print("4. Exit")

choice = input("Select (1-4): ")

if choice == "1":
    a = int(input("First number: "))
    b = int(input("Second number: "))
    print(f"{a} + {b} = {a + b}")
elif choice == "2":
    a = int(input("First number: "))
    b = int(input("Second number: "))
    print(f"{a} - {b} = {a - b}")
elif choice == "3":
    a = int(input("First number: "))
    b = int(input("Second number: "))
    print(f"{a} × {b} = {a * b}")
elif choice == "4":
    print("Goodbye!")
else:
    print("Invalid choice")

# Multi-level menu (nested)
print("=== Game Menu ===")
print("1. Play")
print("2. Settings")
print("3. Quit")

main_choice = input("Choose: ")

if main_choice == "1":
    print("Starting game...")
elif main_choice == "2":
    print("=== Settings ===")
    print("1. Sound")
    print("2. Difficulty")
    print("3. Back")
    setting = input("Choose: ")
    if setting == "1":
        print("Sound options...")
    elif setting == "2":
        print("Difficulty options...")
elif main_choice == "3":
    print("Thanks for playing!")
else:
    print("Invalid choice")

# Menu with validation
while True:
    print("\n=== Calculator ===")
    print("1. Add")
    print("2. Subtract")
    print("3. Quit")

    choice = input("Select (1-3): ").strip()

    if choice in ["1", "2", "3"]:
        if choice == "1":
            print(f"Result: {int(input('A: ')) + int(input('B: '))}")
        elif choice == "2":
            print(f"Result: {int(input('A: ')) - int(input('B: '))}")
        else:
            break
    else:
        print("Invalid choice")

# Professional menu with description
def show_menu():
    print("\n" + "="*40)
    print("STUDENT INFORMATION SYSTEM")
    print("="*40)
    print("1. View Student Info")
    print("2. Update Grades")
    print("3. Generate Report")
    print("4. Exit")
    print("="*40)

choice = input("Enter choice (1-4): ")

if choice == "1":
    print("Displaying student information...")
elif choice == "2":
    print("Updating grades...")
elif choice == "3":
    print("Generating report...")
elif choice == "4":
    print("Goodbye!")
else:
    print("Invalid choice. Please try again.")
```

---

## Menu Design Best Practices

```python
# GOOD - Clear, organized
print("\n=== OPTIONS ===")
print("1. Option one description")
print("2. Option two description")
print("3. Exit")
print("-" * 30)
choice = input("Enter choice: ")

# BAD - Unclear
print("1 or 2?")
choice = input("? ")

# GOOD - Input validation
if choice in ["1", "2", "3"]:
    # Process
else:
    print("Please enter 1, 2, or 3")

# BAD - No validation
if choice == "1":
    # Crashes if user enters garbage
```

---

## Guided Practice (15 minutes)

**Activity: Build a Simple Calculator Menu**

```python
print("=== Simple Calculator ===")
print("1. Add")
print("2. Subtract")
print("3. Multiply")
print("4. Divide")

operation = input("Choose (1-4): ")

x = float(input("First number: "))
y = float(input("Second number: "))

if operation == "1":
    print(f"{x} + {y} = {x + y}")
elif operation == "2":
    print(f"{x} - {y} = {x - y}")
elif operation == "3":
    print(f"{x} × {y} = {x * y}")
elif operation == "4":
    if y != 0:
        print(f"{x} ÷ {y} = {x / y}")
    else:
        print("Cannot divide by zero")
else:
    print("Invalid choice")
```

Test with valid and invalid inputs.

---

## Practice Problems

### Problem 1 — Beginner
Build a simple to-do list menu:
- 1. View list
- 2. Add item
- 3. Exit

```python
tasks = ["Study Python", "Do homework"]

print("=== To-Do List ===")
print("1. View")
print("2. Add")
print("3. Exit")

choice = input("Choose: ")

if choice == "1":
    for task in tasks:
        print(f"- {task}")
elif choice == "2":
    new_task = input("New task: ")
    print(f"Added: {new_task}")
elif choice == "3":
    print("Goodbye")
else:
    print("Invalid choice")
```

---

### Problem 2 — Intermediate
Build a movie rental menu:
- 1. Browse movies (print a list)
- 2. Rent movie (ask which one)
- 3. Return movie
- 4. Exit

```python
available = ["Avatar", "Inception", "Interstellar"]
rented = []

print("=== Movie Rental ===")
print("1. Browse")
print("2. Rent")
print("3. Return")
print("4. Exit")

choice = input("Choose: ")

if choice == "1":
    print("Available movies:")
    for movie in available:
        print(f"  - {movie}")
elif choice == "2":
    movie_name = input("Which movie? ")
    if movie_name in available:
        # Add rental logic
        print(f"Rented: {movie_name}")
    else:
        print("Not available")
elif choice == "3":
    # Return logic
    pass
elif choice == "4":
    print("Goodbye")
```

---

### Problem 3 — Challenge
Build a multi-level menu (main menu → submenus):
- Main: 1. File, 2. Edit, 3. Exit
- File submenu: 1. New, 2. Open, 3. Back
- Edit submenu: 1. Copy, 2. Paste, 3. Back

```python
main_choice = input("Main menu (1-3): ")

if main_choice == "1":  # File
    print("1. New")
    print("2. Open")
    print("3. Back")
    file_choice = input("Choose: ")
    if file_choice == "1":
        print("Creating new file...")
    # ... continue
elif main_choice == "2":  # Edit
    # Similar structure
    pass
elif main_choice == "3":
    print("Goodbye")
```

---

## Hints

- **Problem 1:** Use if/elif/else for menu choice
- **Problem 2:** Check if movie name is in available list
- **Problem 3:** Nested if for submenus

---

## Sample Answers

### Problem 1 Example
```python
tasks = ["Study Python", "Do homework"]

print("=== To-Do List ===")
print("1. View")
print("2. Add")
print("3. Exit")

choice = input("Choose: ")

if choice == "1":
    for task in tasks:
        print(f"- {task}")
elif choice == "2":
    new_task = input("New task: ")
    tasks.append(new_task)
    print(f"Added: {new_task}")
elif choice == "3":
    print("Goodbye")
else:
    print("Invalid choice")
```

---

## Key Takeaway

Menu systems organize programs logically. Use clear prompts, validate input, and handle all cases. This is a fundamental pattern in software!
