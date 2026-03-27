# Day 4: Working with File Paths (os.path)
**Learning Target:** I can construct and manipulate file paths using the os.path module to write portable code that works on different operating systems.

### Key Concepts

**os.path module:** Provides functions for working with file paths in a platform-independent way.

**os.path.join():** Joins path components using the correct separator for the operating system (`/` on Unix, `\` on Windows).

**os.path.exists():** Checks if a file or directory exists.

**os.path.isfile():** Checks if a path points to a regular file.

**os.path.isdir():** Checks if a path points to a directory.

**os.path.abspath():** Returns the absolute path from a relative path.

**os.path.dirname():** Returns the directory part of a path.

**os.path.basename():** Returns the filename from a path.

**os.path.splitext():** Splits a filename into name and extension.

### Code Examples

```python
import os

# Example 1: Joining paths
data_dir = "data"
filename = "students.txt"
filepath = os.path.join(data_dir, filename)
print(f"Filepath: {filepath}")  # Output: data/students.txt (or data\students.txt on Windows)

# Example 2: Checking if files/directories exist
if os.path.exists(filepath):
    print(f"{filepath} exists")
else:
    print(f"{filepath} does not exist")

# Example 3: Checking if it's a file or directory
if os.path.isfile(filepath):
    print(f"{filepath} is a file")
elif os.path.isdir(filepath):
    print(f"{filepath} is a directory")

# Example 4: Getting directory and filename
path = os.path.join("documents", "reports", "data.txt")
directory = os.path.dirname(path)
filename = os.path.basename(path)
print(f"Directory: {directory}")   # Output: documents/reports
print(f"Filename: {filename}")     # Output: data.txt

# Example 5: Splitting filename and extension
filepath = "report.pdf"
name, extension = os.path.splitext(filepath)
print(f"Name: {name}, Extension: {extension}")  # Name: report, Extension: .pdf

# Example 6: Getting absolute path
relative_path = "data/file.txt"
absolute_path = os.path.abspath(relative_path)
print(f"Absolute path: {absolute_path}")

# Example 7: Working with nested directories
# Create a path that works on any OS
project_root = os.getcwd()  # Current working directory
data_folder = os.path.join(project_root, "data")
input_file = os.path.join(data_folder, "input.txt")
output_file = os.path.join(data_folder, "output.txt")

print(f"Input: {input_file}")
print(f"Output: {output_file}")

# Example 8: Safe file opening with path checking
def safe_read_file(filepath):
    if not os.path.exists(filepath):
        print(f"Error: {filepath} does not exist")
        return None
    if not os.path.isfile(filepath):
        print(f"Error: {filepath} is not a file")
        return None

    with open(filepath, 'r') as f:
        return f.read()

# Example 9: Processing files in a directory
data_dir = "data"
if os.path.isdir(data_dir):
    files = os.listdir(data_dir)
    for file in files:
        filepath = os.path.join(data_dir, file)
        print(f"File: {filepath}")

# Example 10: Creating output with timestamped filename
from datetime import datetime
output_dir = "output"
timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
output_file = os.path.join(output_dir, f"report_{timestamp}.txt")
print(f"Output will be saved to: {output_file}")
```

### Guided Practice

**Activity: Path Manipulation Utility**

1. Create a program that demonstrates various path operations:
   - Construct a path to a file in a `data` folder using `os.path.join()`
   - Check if the path exists
   - Extract the directory, filename, and extension
   - Create an output file path with a different name
   - Display all the results

2. Create a helper function:
   ```python
   def analyze_filepath(path):
       # Display various properties of the path
   ```

**Step-by-step code:**
```python
import os

filepath = os.path.join("data", "students.txt")

print(f"Full path: {filepath}")
print(f"Exists: {os.path.exists(filepath)}")
print(f"Directory: {os.path.dirname(filepath)}")
print(f"Filename: {os.path.basename(filepath)}")

name, ext = os.path.splitext(filepath)
print(f"Name: {name}, Extension: {ext}")

output_path = os.path.join(os.path.dirname(filepath), "output.txt")
print(f"Output path: {output_path}")
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that uses `os.path.join()` to create a path to a file called `config.txt` in a `settings` folder, then check if the file exists.

**Problem 2 — Intermediate:** Write a program that takes a file path as input, extracts and displays the directory, filename, and extension separately.

**Problem 3 — Challenge:** Write a program that creates multiple output file paths with different extensions (`.txt`, `.csv`, `.json`) based on a base filename, and checks which files actually exist in the output directory.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Import `os`.
- Use `os.path.join("settings", "config.txt")`.
- Use `os.path.exists()` to check.

**Problem 2:**
- Use `os.path.dirname()` for the directory.
- Use `os.path.basename()` for the filename.
- Use `os.path.splitext()` to separate name and extension.

**Problem 3:**
- Store the base name (without extension).
- Create three paths using `os.path.join()` with different extensions.
- Check each with `os.path.exists()`.
- Display results for each.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
import os
filepath = os.path.join("settings", "config.txt")
if os.path.exists(filepath):
    print(f"{filepath} exists")
else:
    print(f"{filepath} does not exist")

# Problem 2
import os
filepath = input("Enter a filepath: ")
directory = os.path.dirname(filepath)
filename = os.path.basename(filepath)
name, extension = os.path.splitext(filename)

print(f"Directory: {directory}")
print(f"Filename: {filename}")
print(f"Name: {name}")
print(f"Extension: {extension}")

# Problem 3
import os
base_name = "report"
output_dir = "output"
extensions = [".txt", ".csv", ".json"]

for ext in extensions:
    filepath = os.path.join(output_dir, base_name + ext)
    exists = os.path.exists(filepath)
    print(f"{filepath}: {'exists' if exists else 'does not exist'}")
```

</details>
