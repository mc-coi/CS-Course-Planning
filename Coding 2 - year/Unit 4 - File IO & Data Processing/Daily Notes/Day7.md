# Day 7: Specific Exception Types (ValueError, TypeError, FileNotFoundError, etc.)
**Learning Target:** I can identify and catch specific exception types to handle different errors appropriately.

### Key Concepts

**ValueError:** Raised when a function receives an argument of the right type but invalid value (e.g., `int("abc")`).

**TypeError:** Raised when an operation is applied to an object of an inappropriate type (e.g., `"hello" + 5`).

**FileNotFoundError:** Raised when trying to open a file that doesn't exist.

**KeyError:** Raised when accessing a dictionary key that doesn't exist.

**IndexError:** Raised when accessing a list index that doesn't exist.

**ZeroDivisionError:** Raised when dividing by zero.

**Exception hierarchy:** All exceptions inherit from the Exception class.

**Specific vs. generic:** Catching specific exceptions is better practice than catching all exceptions.

### Code Examples

```python
# Example 1: ValueError - invalid value for conversion
try:
    age = int("twenty")  # Raises ValueError
except ValueError:
    print("Error: Age must be a valid integer")

# Example 2: TypeError - wrong type for operation
try:
    result = "hello" + 5  # Raises TypeError
except TypeError:
    print("Error: Cannot concatenate string and integer")

# Example 3: FileNotFoundError - file doesn't exist
try:
    with open('nonexistent.txt', 'r') as f:
        content = f.read()
except FileNotFoundError:
    print("Error: The file was not found")

# Example 4: KeyError - accessing missing dictionary key
try:
    person = {'name': 'Alice', 'age': 25}
    print(person['email'])  # Raises KeyError
except KeyError:
    print("Error: 'email' key not found in dictionary")

# Example 5: IndexError - accessing invalid list index
try:
    fruits = ['apple', 'banana', 'cherry']
    print(fruits[10])  # Raises IndexError
except IndexError:
    print("Error: Index is out of range")

# Example 6: ZeroDivisionError - dividing by zero
try:
    result = 10 / 0  # Raises ZeroDivisionError
except ZeroDivisionError:
    print("Error: Cannot divide by zero")

# Example 7: Multiple specific exception types
try:
    user_input = input("Enter a number: ")
    number = int(user_input)
    result = 10 / number
except ValueError:
    print("Error: Invalid number format")
except ZeroDivisionError:
    print("Error: Cannot divide by zero")

# Example 8: Accessing exception message
try:
    value = int("not_a_number")
except ValueError as e:
    print(f"ValueError caught: {e}")
    # Output: ValueError caught: invalid literal for int() with base 10: 'not_a_number'

# Example 9: Processing a list with multiple exception types
data = ['10', '20', 'abc', '40', 30.5, '50']
results = []

for item in data:
    try:
        num = int(item)
        results.append(num)
        print(f"Converted: {num}")
    except ValueError:
        print(f"Skipped (non-numeric): {item}")
    except TypeError:
        print(f"Skipped (wrong type): {item}")

# Example 10: FileNotFoundError with fallback
def read_file_with_default(filename, default_content):
    try:
        with open(filename, 'r') as f:
            return f.read()
    except FileNotFoundError:
        print(f"File '{filename}' not found. Using default content.")
        return default_content

content = read_file_with_default('config.txt', 'Default configuration')
print(content)

# Example 11: Exception type checking
try:
    # Some operation
    x = int("hello")
except Exception as e:
    print(f"Exception type: {type(e).__name__}")
    print(f"Exception message: {str(e)}")
```

### Guided Practice

**Activity: Robust Data Parser**

1. Create a program that reads a CSV line and handles multiple error types:
   ```
   Name,Age,Score
   Alice,25,95
   Bob,twenty-five,87
   Charlie,,78
   ```

2. For each line:
   - Try to parse the fields
   - Catch ValueError (non-numeric Age/Score)
   - Catch KeyError/IndexError (missing fields)
   - Display appropriate error messages
   - Keep track of successful vs. failed parses

**Step-by-step code:**
```python
lines = [
    "Alice,25,95",
    "Bob,twenty-five,87",
    "Charlie,,78"
]

success_count = 0
error_count = 0

for line in lines:
    try:
        parts = line.split(',')
        name = parts[0]
        age = int(parts[1])
        score = int(parts[2])
        print(f"✓ {name}: Age {age}, Score {score}")
        success_count += 1
    except ValueError as e:
        print(f"✗ {line} - Error: Cannot convert to number")
        error_count += 1
    except IndexError:
        print(f"✗ {line} - Error: Missing fields")
        error_count += 1

print(f"\nSuccessful: {success_count}, Failed: {error_count}")
```

### Practice Problems

**Problem 1 — Beginner:** Write a program that asks the user for a number, catches ValueError if the input is not numeric, and displays the appropriate error message.

**Problem 2 — Intermediate:** Write a program that parses a list of items in "key:value" format, catching KeyError if accessing a key that doesn't exist, and ValueError if converting values to integers fails.

**Problem 3 — Challenge:** Write a program that reads a file line-by-line, parses JSON-like data, and catches multiple exception types (ValueError for invalid JSON, FileNotFoundError for missing file, KeyError for missing fields). Display a summary of how many lines succeeded and failed, grouped by error type.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use `float()` or `int()` to convert.
- Catch `ValueError`.
- Wrap in a loop to retry.

**Problem 2:**
- Use `.split(':')` to parse the format.
- Catch `ValueError` when converting to int.
- Test accessing dictionary/list keys safely.

**Problem 3:**
- Use a dictionary to track error counts by type.
- Import `json` module.
- Catch `FileNotFoundError`, `ValueError` (from json), and `KeyError`.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
while True:
    try:
        number = float(input("Enter a number: "))
        print(f"You entered: {number}")
        break
    except ValueError:
        print("Error: Please enter a valid number")

# Problem 2
data = ["age:25", "score:95", "name:Alice", "invalid:abc"]
for item in data:
    try:
        key, value = item.split(':')
        if key in ['age', 'score']:
            value = int(value)
        print(f"{key}: {value}")
    except ValueError:
        print(f"Error in {item}: Could not convert to number")

# Problem 3
import json
file_content = """{"name": "Alice", "age": 25}
{"name": "Bob", "age": "twenty"}
{"name": "Charlie"}"""

error_types = {}
success = 0

for line in file_content.split('\n'):
    try:
        data = json.loads(line)
        age = int(data['age'])
        print(f"✓ {data['name']}: {age}")
        success += 1
    except FileNotFoundError:
        error_types['FileNotFoundError'] = error_types.get('FileNotFoundError', 0) + 1
    except ValueError:
        error_types['ValueError'] = error_types.get('ValueError', 0) + 1
    except KeyError as e:
        error_types['KeyError'] = error_types.get('KeyError', 0) + 1

print(f"\nSuccess: {success}")
for error_type, count in error_types.items():
    print(f"{error_type}: {count}")
```

</details>
