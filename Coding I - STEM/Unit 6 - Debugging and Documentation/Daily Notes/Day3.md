# Day 3: Reading from Files

### Key Concepts
- `f.read()` reads the entire file as one string
- `f.readline()` reads one line (including the `\n`)
- `f.readlines()` reads all lines as a list of strings
- Iterate with `for line in f:` — most memory-efficient way
- `.strip()` removes trailing whitespace/newline from a line
- Always handle `FileNotFoundError` when reading files you don't control

### Code Examples

```python
# ── Read entire file as one string ────────────────────────
with open("notes.txt", "r") as f:
    content = f.read()
print(content)          # prints everything including newlines

# ── Read all lines as a list ──────────────────────────────
with open("notes.txt", "r") as f:
    lines = f.readlines()   # e.g., ["First line\n", "Second line\n"]

for i, line in enumerate(lines):
    print(f"Line {i+1}: {line.strip()}")

# ── Read line by line (best for large files) ───────────────
with open("notes.txt", "r") as f:
    for line in f:
        print(line.strip())   # strip() removes the trailing \n

# ── Read and process CSV data ─────────────────────────────
scores = []
with open("grades.csv", "r") as f:
    next(f)   # skip the header line
    for line in f:
        parts = line.strip().split(",")
        name = parts[0]
        score = int(parts[1])
        scores.append((name, score))

for name, score in scores:
    print(f"{name}: {score}")

# ── Read into a dictionary ────────────────────────────────
student_grades = {}
with open("grades.csv", "r") as f:
    next(f)   # skip header
    for line in f:
        name, score = line.strip().split(",")
        student_grades[name] = int(score)

print(student_grades)

# ── Read a config-style file ──────────────────────────────
# config.txt:
# school=Westside High
# year=2024
# subject=Python

config = {}
with open("config.txt", "r") as f:
    for line in f:
        key, value = line.strip().split("=")
        config[key] = value

print(config["school"])
```

### Practice Problems — Day 3

**Beginner:**
1. Read the file you created in Day 44 (`my_info.txt`) and print each line with its line number.
2. Write `count_lines(filename)` that returns the number of lines in a file.

**Intermediate:**

3. Write `read_scores(filename)` that reads a CSV file of name,score pairs and returns a dictionary.
4. Write `find_in_file(filename, keyword)` that reads a file and returns a list of all lines containing the keyword.

**Challenge:**

5. Write a complete word frequency counter: read a text file, split into words (lowercase, strip punctuation), count how often each word appears, and write a new file with the results sorted from most to least frequent.

<details>
<summary>💡 Hint for #5</summary>

```python
import string

def count_word_frequency(input_file, output_file):
    freq = {}
    with open(input_file, "r") as f:
        for line in f:
            words = line.lower().split()
            for word in words:
                word = word.strip(string.punctuation)
                if word:
                    freq[word] = freq.get(word, 0) + 1

    sorted_words = sorted(freq.items(), key=lambda x: x[1], reverse=True)

    with open(output_file, "w") as f:
        for word, count in sorted_words:
            f.write(f"{word}: {count}\n")
```
</details>

---
