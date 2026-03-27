# Day 2: Reading Files Line-by-Line, readlines()
**Learning Target:** I can read files line-by-line using readline() and readlines() methods, and iterate through file objects.

### Key Concepts

**readline() method:** Reads a single line from the file, including the newline character (`\n`). Returns empty string when end of file is reached.

**readlines() method:** Reads all lines from the file and returns a list of strings, each including its newline character.

**Iterating through file objects:** Files are iterable; you can use a `for` loop to read line-by-line efficiently.

**Stripping whitespace:** Use `.strip()` to remove leading/trailing whitespace, including newlines.

**Line numbering:** Keep track of the current line number when iterating.

### Code Examples

```python
# Example 1: Using readline() in a loop
with open('data.txt', 'r') as f:
    line = f.readline()
    line_num = 1
    while line:  # Continue until readline() returns empty string
        print(f"Line {line_num}: {line.strip()}")
        line = f.readline()
        line_num += 1

# Example 2: Using readlines() to get all lines as a list
with open('data.txt', 'r') as f:
    lines = f.readlines()
    for i, line in enumerate(lines, 1):
        print(f"Line {i}: {line.strip()}")

# Example 3: Iterating directly (most Pythonic way)
with open('data.txt', 'r') as f:
    for i, line in enumerate(f, 1):
        print(f"Line {i}: {line.strip()}")

# Example 4: Processing lines with conditions
sample_content = """Alice: 85
Bob: 92
Charlie: 78
Diana: 88"""

lines = sample_content.split('\n')
print("Names with scores >= 85:")
for line in lines:
    if line:  # Skip empty lines
        name, score = line.split(': ')
        score = int(score)
        if score >= 85:
            print(f"  {name}: {score}")

# Example 5: Counting lines in a file
with open('data.txt', 'r') as f:
    line_count = sum(1 for line in f)
    print(f"Total lines: {line_count}")

# Example 6: Collecting specific lines
# Reading only non-empty lines
with open('data.txt', 'r') as f:
    non_empty_lines = [line.strip() for line in f if line.strip()]
    print(f"Non-empty lines: {non_empty_lines}")
```

### Guided Practice

**Activity: Line-by-Line File Analysis**

1. Create a file called `scores.txt` with the following content:
   ```
   Alice 85
   Bob 92
   Charlie 78
   Diana 88
   ```

2. Write a program that:
   - Opens the file and reads it line-by-line
   - For each line, extracts the name and score
   - Prints lines where the score is >= 85
   - Counts the total number of lines

3. Write two versions:
   - Version A: Use `readlines()`
   - Version B: Iterate directly over the file object

**Step-by-step code:**
```python
# Version A: Using readlines()
with open('scores.txt', 'r') as f:
    lines = f.readlines()
    print(f"Total lines: {len(lines)}")
    for line in lines:
        parts = line.strip().split()
        name, score = parts[0], int(parts[1])
        if score >= 85:
            print(f"{name}: {score}")

# Version B: Direct iteration (preferred)
with open('scores.txt', 'r') as f:
    for line in f:
        parts = line.strip().split()
        if len(parts) == 2:
            name, score = parts[0], int(parts[1])
            if score >= 85:
                print(f"{name}: {score}")
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that opens a file called `words.txt`, reads each line, and prints the line number and the word.

**Problem 2 — Intermediate:** Write a program that reads a file called `numbers.txt` (each line contains one integer), finds the maximum number, and prints it along with which line it was on.

**Problem 3 — Challenge:** Write a program that reads a file called `data.txt` (CSV-like: Name, Age, City), filters lines where Age > 30, and prints a formatted table of matching records.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use a `for` loop to iterate over the file object.
- Use `enumerate()` to get both index and line.
- Use `.strip()` to remove the newline character.

**Problem 2:**
- Read each line and convert to an integer.
- Keep track of the maximum value and its line number.
- Use `readlines()` or iterate directly.

**Problem 3:**
- Use `.split(',')` to parse each line.
- Extract the age value and convert to integer.
- Build a formatted output string for each matching record.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
with open('words.txt', 'r') as f:
    for line_num, line in enumerate(f, 1):
        word = line.strip()
        print(f"Line {line_num}: {word}")

# Problem 2
with open('numbers.txt', 'r') as f:
    max_num = None
    max_line = 0
    for line_num, line in enumerate(f, 1):
        num = int(line.strip())
        if max_num is None or num > max_num:
            max_num = num
            max_line = line_num
    print(f"Maximum: {max_num} (Line {max_line})")

# Problem 3
with open('data.txt', 'r') as f:
    for line in f:
        parts = line.strip().split(', ')
        name, age, city = parts[0], int(parts[1]), parts[2]
        if age > 30:
            print(f"{name:15} | Age: {age:2} | {city}")
```

</details>
