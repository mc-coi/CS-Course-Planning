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

**Print formatting** makes output look better and more organized:
- Use `\n` for line breaks within a single string
- Use `\t` for indentation and column alignment
- Combine multiple formatting techniques for professional output

### Code Examples
```python
# Using escape characters for newlines
print("Hello\nWorld")  # Newline: Hello then World on next line

# Using tabs for alignment
print("Name\tAge\tGrade")     # Tab characters align columns
print("Alex\t17\tA")
print("Jordan\t16\tB")

# Escaping quotes
print("He said \"Hello\"")  # Prints: He said "Hello"
print('It\'s a beautiful day')  # Prints: It's a beautiful day

# Multi-line output in one print statement
print("Line 1\nLine 2\nLine 3")

# Combining backslashes in paths
print("Path: C:\\Users\\Documents\\code.py")

# Good comments explain the purpose
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

**Problem 3 — Challenge:** Create a program that prints a formatted schedule or menu using escape characters. Include at least 5 items with proper alignment and organization.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use \n for new lines and \t for indentation
- Problem 2: Multiple \t characters will align columns nicely
- Problem 3: Think about using \n and \t together to create a professional-looking table
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
