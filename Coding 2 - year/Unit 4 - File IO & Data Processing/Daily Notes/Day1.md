# Day 1: File Reading — open(), read(), with Statement
**Learning Target:** I can open files in different modes and read their entire contents using the open() function and with statement.

### Key Concepts

**open() function:** Opens a file and returns a file object. Syntax: `open(filename, mode)`.
- Modes: `'r'` (read), `'w'` (write), `'a'` (append), `'r+'` (read/write).

**File modes:**
- `'r'` — Read mode (default). File must exist.
- `'rb'` — Read binary mode.
- `'w'` — Write mode. Creates or overwrites the file.
- `'a'` — Append mode. Adds content to the end.

**with statement:** Context manager that automatically closes the file. Best practice for safe file handling.

**read() method:** Returns the entire file content as a single string.

**File object properties:** `.name`, `.mode`, `.closed`.

### Code Examples

```python
# Example 1: Basic file reading with open()
file_obj = open('sample.txt', 'r')
content = file_obj.read()
print(content)
file_obj.close()

# Example 2: Using with statement (preferred)
with open('sample.txt', 'r') as file_obj:
    content = file_obj.read()
    print(content)
# File is automatically closed after the with block

# Example 3: Reading with file path
import os
file_path = os.path.join('data', 'students.txt')
with open(file_path, 'r') as f:
    data = f.read()
    print(f"File name: {f.name}")
    print(f"Mode: {f.mode}")
    print(f"Content:\n{data}")

# Example 4: Sample data (simulating file content)
# If 'sample.txt' contains:
# Hello, World!
# This is a test file.
# Python is awesome!

sample_content = """Hello, World!
This is a test file.
Python is awesome!"""

# Simulating file read
print("Full content:")
print(sample_content)

# Example 5: Checking file status
with open('sample.txt', 'r') as f:
    print(f"Is file closed? {f.closed}")  # False (inside with block)
    content = f.read()

print(f"Is file closed now? {f.closed}")  # True (after with block)
```

### Guided Practice

**Activity: Read and Display File Contents**

1. Create a simple text file named `welcome.txt` with 3-4 lines of text about your favorite hobby.
2. Write a Python program that:
   - Opens `welcome.txt` in read mode
   - Reads the entire content using `.read()`
   - Prints the content to the console
   - Verifies the file is closed after reading
3. Run the program and verify the output.
4. Modify the program to use the `with` statement instead of `close()`.

**Step-by-step code:**
```python
# Step 1: Open and read
with open('welcome.txt', 'r') as f:
    content = f.read()

# Step 2: Process and display
print("File contents:")
print(content)

# Step 3: Verify closure
print(f"File is closed: {f.closed}")
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that opens a file called `greeting.txt` and prints its entire content to the console.

**Problem 2 — Intermediate:** Write a program that opens a file, reads it, counts the total number of characters (including spaces and newlines), and displays the count.

**Problem 3 — Challenge:** Write a program that opens a file called `poem.txt`, reads the entire content, and prints only the first and last 50 characters of the file.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use `open()` with mode `'r'`.
- Use `.read()` to get the entire content.
- Use `print()` to display it.

**Problem 2:**
- Use `.read()` to get the content as a string.
- Use `len()` to count characters.
- Remember that newlines are also characters.

**Problem 3:**
- Read the entire content using `.read()`.
- Use string slicing: `content[:50]` for the first 50, `content[-50:]` for the last 50.
- Use `with` statement for safety.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
with open('greeting.txt', 'r') as f:
    content = f.read()
    print(content)

# Problem 2
with open('greeting.txt', 'r') as f:
    content = f.read()
    char_count = len(content)
    print(f"Total characters: {char_count}")

# Problem 3
with open('poem.txt', 'r') as f:
    content = f.read()
    first_50 = content[:50]
    last_50 = content[-50:]
    print(f"First 50 characters:\n{first_50}")
    print(f"\nLast 50 characters:\n{last_50}")
```

</details>
