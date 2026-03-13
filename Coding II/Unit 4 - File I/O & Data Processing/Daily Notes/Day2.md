# Day 2: Text File Processing
**Learning Target:** I can process text files, parsing and transforming line-by-line data.

### Key Concepts
Text file processing: splitting, parsing, transforming data.

### Code Examples
```python
# Process each line
with open("names.txt", "r") as file:
    for line in file:
        name, age = line.strip().split(",")
        print(f"{name} is {age} years old")

# Filter and write
with open("input.txt", "r") as infile, open("output.txt", "w") as outfile:
    for line in infile:
        if len(line.strip()) > 0:  # Skip empty lines
            outfile.write(line.upper())

# Parse structured text
data = []
with open("data.txt", "r") as file:
    for line in file:
        parts = line.strip().split(":")
        data.append({"key": parts[0], "value": parts[1]})
```

### Guided Practice
Read a file with student names/grades, filter by passing grade, write to new file.

### Practice Problems
**Problem 1 — Beginner:** Read a file and count occurrences of a word.

**Problem 2 — Intermediate:** Read a CSV-like file and parse it.

**Problem 3 — Challenge:** Transform and clean messy data from a file.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
with open("file.txt", "r") as f:
    content = f.read()
    count = content.count("word")
```
</details>

---

---
