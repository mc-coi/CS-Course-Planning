# Day 1: File Reading & Writing
**Learning Target:** I can open, read, write, and close files safely using the with statement.

### Key Concepts
File operations: `open()`, `read()`, `write()`, `close()`

**File modes:**
- `'r'` — read (default)
- `'w'` — write (overwrites)
- `'a'` — append (add to end)
- `'r+'` — read and write

**Best practice:** Use `with` statement for automatic closing

### Code Examples
```python
# Reading a file
with open("data.txt", "r") as file:
    content = file.read()
    print(content)

# Reading line by line
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())

# Writing to a file
with open("output.txt", "w") as file:
    file.write("Line 1\n")
    file.write("Line 2\n")

# Appending to a file
with open("output.txt", "a") as file:
    file.write("Line 3\n")

# Reading all lines as list
with open("data.txt", "r") as file:
    lines = file.readlines()
```

### Guided Practice
Create a program that reads a file and counts lines/words.

### Practice Problems
**Problem 1 — Beginner:** Write a program that reads a file and prints its contents.

**Problem 2 — Intermediate:** Create a program that reads a file, counts words, and writes stats.

**Problem 3 — Challenge:** Create a file copy program that reads one file and writes to another.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
with open("input.txt", "r") as f:
    content = f.read()
    word_count = len(content.split())

with open("stats.txt", "w") as f:
    f.write(f"Words: {word_count}\n")
```
</details>

---

---
