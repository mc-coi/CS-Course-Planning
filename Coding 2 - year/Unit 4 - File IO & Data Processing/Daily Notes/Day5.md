# Day 5: File I/O Lab — Text Processing
**Learning Target:** I can apply file reading, writing, and text processing skills to solve a real-world problem.

### Key Concepts

**Text processing pipeline:** Read → Parse → Process → Write.

**String methods:** `.upper()`, `.lower()`, `.strip()`, `.split()`, `.replace()`, `.startswith()`, `.endswith()`.

**List comprehensions:** Efficient way to filter and transform data.

**Combining file operations:** Using read/write together to transform data.

**File organization:** Structuring input and output files logically.

### Code Examples

```python
# Example 1: Word frequency counter
content = """Python is great. Python is fun.
Java is verbose. Python is powerful."""

words = content.lower().split()
word_count = {}
for word in words:
    word = word.rstrip('.,')  # Remove punctuation
    word_count[word] = word_count.get(word, 0) + 1

print("Word frequencies:")
for word, count in sorted(word_count.items(), key=lambda x: x[1], reverse=True):
    print(f"{word}: {count}")

# Example 2: Converting text to uppercase and writing
input_text = """hello world
this is a test
python is awesome"""

with open('uppercase_output.txt', 'w') as f:
    f.write(input_text.upper())

# Example 3: Filtering lines based on criteria
content = """Alice: 85
Bob: 92
Charlie: 78
Diana: 88
Eve: 75"""

lines = content.split('\n')
passing_students = []

for line in lines:
    if line:
        name, score = line.split(': ')
        if int(score) >= 80:
            passing_students.append(line)

print("Students with 80+:")
for student in passing_students:
    print(student)

# Example 4: Removing duplicates while preserving order
content = """apple
banana
apple
cherry
banana
apple
date"""

lines = content.strip().split('\n')
unique_lines = []
for line in lines:
    if line not in unique_lines:
        unique_lines.append(line)

print("Unique items:")
for item in unique_lines:
    print(item)

# Example 5: Line numbering and reformatting
content = """first line
second line
third line"""

lines = content.split('\n')
output = ""
for i, line in enumerate(lines, 1):
    output += f"{i:3}. {line}\n"

print(output)

# Example 6: Finding and replacing text
content = """The quick brown fox
The lazy dog
The silent night"""

# Replace all instances of "The"
modified = content.replace("The", "A")
print(modified)

# Example 7: Extracting lines that start with a pattern
content = """# Section 1
Content here
## Subsection
More content
# Section 2
Final content"""

lines = content.split('\n')
sections = [line for line in lines if line.startswith('#')]
print("Sections found:")
for section in sections:
    print(section)

# Example 8: Case-insensitive search
content = """Apple
apricot
AVOCADO
banana
Apricot"""

lines = content.split('\n')
a_items = [line for line in lines if line.lower().startswith('a')]
print("Items starting with A:")
for item in a_items:
    print(item)
```

### Guided Practice

**Activity: Data Cleaner and Formatter**

1. Create a program that reads a file containing messy data:
   ```
   Name: alice , Score: 85
   Name: bob, Score: 92
   Name: charlie , Score: 78
   ```

2. The program should:
   - Read the file line-by-line
   - Extract name and score, cleaning up extra spaces
   - Filter out scores below 80
   - Write the cleaned data to a new file in a neat format
   - Display statistics (how many records kept, how many removed)

**Step-by-step code:**
```python
# Read and process
input_data = """Name: alice , Score: 85
Name: bob, Score: 92
Name: charlie , Score: 78"""

cleaned_records = []
removed_count = 0

for line in input_data.split('\n'):
    if not line.strip():
        continue

    # Parse
    parts = line.split('Score:')
    name = parts[0].replace('Name:', '').strip()
    score = int(parts[1].strip())

    # Filter
    if score >= 80:
        cleaned_records.append(f"{name},{score}")
    else:
        removed_count += 1

# Write output
output = "Name,Score\n" + "\n".join(cleaned_records)
print(output)
print(f"\nStatistics: {len(cleaned_records)} kept, {removed_count} removed")
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that reads a file with one word per line and creates a new file with the words converted to uppercase.

**Problem 2 — Intermediate:** Write a program that reads a CSV-like file (Name,Age,City), filters records where Age >= 25, and writes the filtered results to a new file.

**Problem 3 — Challenge:** Write a program that reads a text file, removes duplicate lines while preserving order, counts occurrences of each line, and writes a report showing lines and their counts in descending order of frequency.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Read the file line-by-line.
- Use `.upper()` to convert to uppercase.
- Write each uppercase word to the output file with a newline.

**Problem 2:**
- Split each line by commas.
- Convert the age to an integer and compare.
- Write matching lines to the output file.

**Problem 3:**
- Keep track of duplicates using a dictionary or Counter.
- Preserve order by iterating through the original list.
- Sort by count (frequency) in descending order.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
input_text = """hello
world
python
coding"""

output = input_text.upper()
with open('uppercase.txt', 'w') as f:
    f.write(output)

# Problem 2
input_data = """Alice,28,NYC
Bob,22,LA
Charlie,30,Boston
Diana,24,Seattle"""

output_lines = ["Name,Age,City"]
for line in input_data.split('\n'):
    if line:
        name, age, city = line.split(',')
        if int(age) >= 25:
            output_lines.append(line)

with open('filtered.txt', 'w') as f:
    f.write('\n'.join(output_lines))

# Problem 3
input_data = """apple
banana
apple
cherry
banana
apple
date"""

lines = input_data.strip().split('\n')
line_count = {}
unique_order = []

for line in lines:
    if line not in line_count:
        line_count[line] = 0
        unique_order.append(line)
    line_count[line] += 1

# Sort by count
sorted_lines = sorted(unique_order, key=lambda x: line_count[x], reverse=True)

output = []
for line in sorted_lines:
    output.append(f"{line}: {line_count[line]}")

result = '\n'.join(output)
with open('frequency_report.txt', 'w') as f:
    f.write(result)
```

</details>
