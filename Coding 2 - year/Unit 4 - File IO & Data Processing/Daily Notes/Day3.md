# Day 3: File Writing — write(), writelines(), append Mode
**Learning Target:** I can write data to files using write() and writelines() methods, and append data without overwriting existing content.

### Key Concepts

**write() method:** Writes a string to the file. Does not add newlines automatically. Returns the number of characters written.

**writelines() method:** Writes a list of strings to the file. Does not add newlines between elements.

**Write mode (`'w'`):** Creates a new file or overwrites an existing one. Dangerous—use with caution.

**Append mode (`'a'`):** Adds content to the end of a file without overwriting. Safe for adding data.

**Flushing:** Use `.flush()` to force data to be written to disk immediately.

**Return value:** write() returns the number of characters written.

### Code Examples

```python
# Example 1: Writing a single string
with open('output.txt', 'w') as f:
    f.write("Hello, World!\n")
    f.write("Python is awesome!\n")

# Example 2: Writing multiple lines with writelines()
lines = ["First line\n", "Second line\n", "Third line\n"]
with open('output.txt', 'w') as f:
    f.writelines(lines)

# Example 3: Appending to an existing file
with open('log.txt', 'a') as f:
    f.write("Log entry: Task completed\n")
    f.write("Timestamp: 2024-03-25\n")

# Example 4: Using write() return value
with open('data.txt', 'w') as f:
    text = "Hello"
    chars_written = f.write(text)
    print(f"Wrote {chars_written} characters")

# Example 5: Building content and writing
output = ""
for i in range(1, 6):
    output += f"Line {i}: {i * 10}\n"

with open('numbers.txt', 'w') as f:
    f.write(output)

# Example 6: Using join() for efficient writing
lines = ["Alice", "Bob", "Charlie", "Diana"]
with open('names.txt', 'w') as f:
    f.write('\n'.join(lines))  # No trailing newline in this approach

# Example 7: Append vs Write
# Write mode (overwrites)
with open('test.txt', 'w') as f:
    f.write("First write\n")

# This overwrites the previous content
with open('test.txt', 'w') as f:
    f.write("Second write\n")

# Append mode (adds to end)
with open('test.txt', 'a') as f:
    f.write("First append\n")

with open('test.txt', 'a') as f:
    f.write("Second append\n")
```

### Guided Practice

**Activity: Log File Creator**

1. Create a program that simulates a simple logging system:
   - Prompts the user to enter a log message (or use predefined messages)
   - Appends each message to a file called `activity.log` with a timestamp
   - Displays the contents of the log file

2. Requirements:
   - Use append mode to add entries
   - Each entry should include a timestamp
   - Create at least 3 log entries
   - Read and display the final log file

**Step-by-step code:**
```python
from datetime import datetime

# Create log entries
log_messages = [
    "Application started",
    "User logged in",
    "Data processed successfully"
]

# Append each entry with timestamp
with open('activity.log', 'a') as f:
    for msg in log_messages:
        timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        f.write(f"[{timestamp}] {msg}\n")

# Read and display the log
print("Current log:")
with open('activity.log', 'r') as f:
    print(f.read())
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that creates a file called `greetings.txt` and writes three different greeting messages to it, each on a new line.

**Problem 2 — Intermediate:** Write a program that reads numbers from a list, calculates their squares, and writes the results to a file called `squares.txt` in the format "Number: n, Square: n²".

**Problem 3 — Challenge:** Write a program that creates a CSV file called `students.csv` with columns for Name, Grade, and Score. Write 5 student records to the file using the writelines() method.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use `'w'` mode to create the file.
- Call `write()` three times or use `writelines()` with a list.
- Remember to include `\n` for newlines.

**Problem 2:**
- Create a list of numbers.
- For each number, calculate the square.
- Format the output string correctly (include newline).
- Use append mode if running multiple times.

**Problem 3:**
- Start with a header row.
- Create a list of formatted lines for each student.
- Use `writelines()` to write the entire list.
- Ensure proper CSV formatting (commas, newlines).

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
with open('greetings.txt', 'w') as f:
    f.write("Hello!\n")
    f.write("Good morning!\n")
    f.write("Welcome!\n")

# Problem 2
numbers = [2, 5, 8, 10, 15]
with open('squares.txt', 'w') as f:
    for num in numbers:
        square = num ** 2
        f.write(f"Number: {num}, Square: {square}\n")

# Problem 3
header = "Name,Grade,Score\n"
students = [
    "Alice,A,95\n",
    "Bob,B,87\n",
    "Charlie,A,92\n",
    "Diana,A,98\n",
    "Eve,B,85\n"
]
with open('students.csv', 'w') as f:
    f.write(header)
    f.writelines(students)
```

</details>
