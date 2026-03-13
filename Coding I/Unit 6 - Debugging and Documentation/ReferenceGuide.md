# Vocabulary & Quick Reference

| Term | Definition |
|------|-----------|
| **Syntax Error** | Code violates Python's rules; won't even start |
| **Runtime Error** | Code crashes while running; also called an Exception |
| **Logic Error** | Code runs but produces incorrect results |
| **Exception** | An error that occurs during program execution |
| **`try`** | Block of code that might raise an exception |
| **`except`** | Block that handles a specific exception |
| **`else`** | Block that runs if `try` had no exceptions |
| **`finally`** | Block that always runs (cleanup) |
| **`raise`** | Manually trigger an exception |
| **File I/O** | Input/Output — reading from and writing to files |
| **`open()`** | Built-in function to open a file |
| **`with` statement** | Context manager that auto-closes files |
| **`.read()`** | Read entire file as a string |
| **`.readlines()`** | Read all lines as a list |
| **`.write()`** | Write a string to a file |
| **`.strip()`** | Remove leading/trailing whitespace and newlines |
| **Docstring** | String documentation placed at start of a function |
| **Inline comment** | `#` note explaining code; should say *why* |
| **`__doc__`** | Attribute holding a function's docstring |

## Exception Quick Reference

```python
try:
    result = risky_operation()
except ValueError as e:
    print(f"Bad value: {e}")
except (TypeError, AttributeError) as e:
    print(f"Type issue: {e}")
except FileNotFoundError:
    print("File not found!")
except Exception as e:
    print(f"Unexpected error: {e}")   # fallback
else:
    print("Success!")                  # only if no exception
finally:
    print("Done.")                     # always runs
```

## File I/O Quick Reference

```python
# Write
with open("file.txt", "w") as f:
    f.write("line 1\n")

# Append
with open("file.txt", "a") as f:
    f.write("new line\n")

# Read all
with open("file.txt", "r") as f:
    content = f.read()

# Read line by line
with open("file.txt", "r") as f:
    for line in f:
        clean = line.strip()
```
## Common Mistakes

| Mistake | What Goes Wrong | Fix |
|---------|----------------|-----|
| Not using `with` statement | File may not close properly | Always `with open() as f:` |
| Forgetting `\n` in `f.write()` | All text runs together | `f.write("line\n")` — add newline |
| Bare `except:` clause | Catches ALL errors, hides bugs | `except ValueError:` — be specific |
| Opening file without `try/except` | Crashes if file missing | Wrap in `try/except FileNotFoundError` |
| Forgetting `.strip()` on read | Extra `\n` in each string | `line.strip()` removes whitespace |
| Reading closed file | `ValueError` | Stay inside the `with` block |
| Writing without newlines | One long line in file | `f.write(text + "\n")` |
| Over-commenting obvious code | Clutters code | Comment the *why*, not the *what* |
| Missing docstring | Functions undocumented | Add `"""description"""` after `def` |
| Catching then ignoring errors | Silent failures | At minimum, `print(f"Error: {e}")` |

---