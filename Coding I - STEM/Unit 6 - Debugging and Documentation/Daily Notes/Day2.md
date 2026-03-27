# Day 2: Writing to Files

### Key Concepts
- **File I/O:** Input/Output — reading from and writing to files
- `open(filename, mode)` opens a file; always close it when done
- **`with` statement** automatically closes the file — always use this!
- File modes: `"w"` (write/overwrite), `"a"` (append), `"r"` (read), `"x"` (create new, fail if exists)
- `f.write(text)` writes a string — you must add `"\n"` yourself for newlines
- `f.writelines(list)` writes a list of strings

### File Modes Summary

| Mode | Behavior | File Exists? | File Missing? |
|------|---------|-------------|--------------|
| `"w"` | Write (overwrite) | Clears old content | Creates new |
| `"a"` | Append | Adds to end | Creates new |
| `"r"` | Read only | Opens file | Raises error |
| `"x"` | Exclusive create | Raises error | Creates new |

### Code Examples

```python
# ── Write to a file (creates or overwrites) ────────────────
with open("notes.txt", "w") as f:
    f.write("First line\n")
    f.write("Second line\n")
    f.write("Third line\n")

# ── Append to existing file ────────────────────────────────
with open("notes.txt", "a") as f:
    f.write("Fourth line\n")
    f.write("Fifth line\n")

# ── Write multiple lines at once ──────────────────────────
lines = ["Monday\n", "Tuesday\n", "Wednesday\n"]
with open("days.txt", "w") as f:
    f.writelines(lines)

# ── Write formatted data ───────────────────────────────────
students = [
    ("Alice", 92),
    ("Bob", 85),
    ("Carlos", 78),
]
with open("grades.csv", "w") as f:
    f.write("Name,Score\n")   # header row
    for name, score in students:
        f.write(f"{name},{score}\n")

# ── Write using a loop ─────────────────────────────────────
with open("countdown.txt", "w") as f:
    for i in range(10, 0, -1):
        f.write(f"{i}\n")
    f.write("Blastoff!\n")

# ── Check if file was created ──────────────────────────────
import os
if os.path.exists("notes.txt"):
    print(f"File created! Size: {os.path.getsize('notes.txt')} bytes")
```

### Practice Problems — Day 2

**Beginner:**
1. Write a program that creates `my_info.txt` with your name, grade, and favorite class on separate lines.
2. Write a function `save_numbers(filename, numbers)` that writes each number in the list to a separate line of the file.

**Intermediate:**

3. Write a function `append_log(filename, message)` that appends a message to a log file along with a timestamp. (Use Python's `datetime.datetime.now()` for the timestamp.)
4. Write a function `save_scores(filename, scores_dict)` where `scores_dict` maps student names to scores. Save in CSV format: `Name,Score`.

**Challenge:**

5. Write a `FileJournal` class — no wait, write a functional journal program: `start_journal(filename)` writes a header, `add_entry(filename, entry)` appends a dated entry, `view_journal(filename)` reads and prints all entries.

---