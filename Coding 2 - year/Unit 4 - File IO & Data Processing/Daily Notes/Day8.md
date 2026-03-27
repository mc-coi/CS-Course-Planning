# Day 8: else and finally Clauses
**Learning Target:** I can use else and finally clauses to execute code conditionally after exception handling and ensure cleanup code always runs.

### Key Concepts

**else clause:** Executes only if no exception occurred in the try block. Useful for code that should only run on success.

**finally clause:** Always executes, regardless of whether an exception occurred. Used for cleanup (e.g., closing files, releasing resources).

**Order:** try → except → else → finally (finally always runs last).

**Exception suppression:** else code doesn't run if an exception was caught, but finally always runs.

**Resource cleanup:** finally is the proper place for cleanup operations.

### Code Examples

```python
# Example 1: Using else with try/except
try:
    number = int("25")
    print(f"Converted: {number}")
except ValueError:
    print("Error: Invalid number")
else:
    print("Conversion was successful!")  # Runs only if no exception

# Example 2: Using finally for cleanup
try:
    f = open('data.txt', 'r')
    content = f.read()
    print(content)
except FileNotFoundError:
    print("File not found")
finally:
    # This runs regardless of success or failure
    if 'f' in locals() and not f.closed:
        f.close()
    print("Cleanup complete")

# Example 3: try/except/else/finally all together
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Cannot divide by zero")
else:
    print(f"Division successful: {result}")
finally:
    print("Operation completed")

# Example 4: else without exception
try:
    x = 5 + 3
    print(f"Sum: {x}")
except TypeError:
    print("Cannot add these types")
else:
    print("No errors occurred")
finally:
    print("Done")

# Example 5: Exception occurs - else is skipped
try:
    result = "hello" + 5
except TypeError:
    print("Type error caught")
else:
    print("This will NOT print because an exception occurred")
finally:
    print("This WILL print regardless")

# Example 6: Using finally with file operations
def safe_read_and_process(filename):
    f = None
    try:
        f = open(filename, 'r')
        lines = f.readlines()
        print(f"Read {len(lines)} lines")
        return lines
    except FileNotFoundError:
        print(f"Error: {filename} not found")
        return None
    finally:
        if f is not None:
            f.close()
            print("File closed")

# Example 7: Multiple operations with individual error handling
try:
    file1 = open('input.txt', 'r')
    content = file1.read()
except FileNotFoundError:
    print("Input file not found")
else:
    print(f"Successfully read {len(content)} characters")
finally:
    file1.close() if 'file1' in locals() else None

# Example 8: Nested try/except/else/finally
try:
    data = "10,20,30"
    try:
        numbers = [int(x) for x in data.split(',')]
    except ValueError:
        print("Invalid number in data")
    else:
        print(f"Numbers: {numbers}")
    finally:
        print("Inner finally executed")
except Exception as e:
    print(f"Outer exception: {e}")
finally:
    print("Outer finally executed")

# Example 9: else clause with validation
def parse_and_validate(line):
    try:
        parts = line.split(',')
        name = parts[0]
        age = int(parts[1])
    except (ValueError, IndexError):
        print(f"Invalid line: {line}")
    else:
        # Only execute if parsing succeeded
        if age < 0:
            print(f"Invalid age: {age}")
        else:
            print(f"Valid: {name}, age {age}")
    finally:
        print("Parsing attempt completed\n")

# Example 10: Using with statement (automatic cleanup)
try:
    with open('data.txt', 'r') as f:
        content = f.read()
except FileNotFoundError:
    print("File not found")
else:
    print(f"File read successfully: {len(content)} chars")
finally:
    print("Done - file automatically closed by 'with' statement")
```

### Guided Practice

**Activity: Safe Data Processing**

1. Create a program that:
   - Attempts to open a file and read it
   - If successful, processes the data (uses else)
   - Always displays a status message (uses finally)
   - Properly closes the file

2. Use all four parts: try, except, else, finally

**Step-by-step code:**
```python
filename = 'data.txt'

try:
    with open(filename, 'r') as f:
        lines = f.readlines()
except FileNotFoundError:
    print(f"Error: Could not find {filename}")
else:
    # Only runs if file was opened successfully
    print(f"Successfully read {len(lines)} lines")
    for i, line in enumerate(lines, 1):
        print(f"  Line {i}: {line.strip()}")
finally:
    print("Processing complete")
```

### Practice Problems

**Problem 1 — Beginner:** Write a program with try/except/else that attempts to convert a string to an integer, prints success if it works, and uses finally to print "Done".

**Problem 2 — Intermediate:** Write a program that tries to open a file, reads it, prints the content (else clause), and always closes the file (finally clause), even if an error occurs.

**Problem 3 — Challenge:** Write a program that reads multiple lines from a file, processes each (try), catches parse errors (except), prints results only if successful (else), and maintains a counter in finally that always displays how many lines were processed.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use `try` with `int()` conversion.
- `except ValueError` for invalid input.
- `else` to print success message.
- `finally` to print "Done".

**Problem 2:**
- Use `try` to open the file.
- `except FileNotFoundError` for missing file.
- `else` to print content.
- `finally` to close the file.

**Problem 3:**
- Use a counter variable outside the try block.
- Increment it in finally.
- Use else to print only successful results.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
try:
    number = int("42")
except ValueError:
    print("Error: Invalid number")
else:
    print(f"Successfully converted: {number}")
finally:
    print("Done")

# Problem 2
filename = 'data.txt'
f = None
try:
    f = open(filename, 'r')
    content = f.read()
except FileNotFoundError:
    print(f"Error: {filename} not found")
else:
    print(f"Content:\n{content}")
finally:
    if f is not None:
        f.close()
        print("File closed")

# Problem 3
file_content = """Alice,85
Bob,92
Charlie,78"""

line_count = 0
try:
    for line in file_content.split('\n'):
        try:
            name, score = line.split(',')
            score = int(score)
        except ValueError:
            print(f"Error parsing: {line}")
        else:
            print(f"✓ {name}: {score}")
finally:
    print(f"\nTotal lines processed: {file_content.count(chr(10)) + 1}")
```

</details>
