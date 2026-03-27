# Unit 6 Practice Bank (15 Problems)

### Tier 1 — Beginner

**P1.** Label each error as Syntax, Runtime, or Logic:
```python
# a)
for i in range(5)
    print(i)

# b)
x = 0
print(10 / x)

# c)
total = 0
for i in range(1, 6):
    total = i   # supposed to sum 1+2+3+4+5
```

**P2.** Write a program that writes the numbers 1–20 to `numbers.txt`, one per line.

**P3.** Write a program that reads `numbers.txt` and prints the sum of all numbers.

**P4.** Add a `try/except` block to handle `ValueError` when converting user input to `int`.

**P5.** Write a one-line docstring for each: `area_circle(r)`, `is_leap_year(year)`, `reverse_string(s)`.

### Tier 2 — Intermediate

**P6.** Write `safe_open(filename)` that returns the file contents as a string, or `None` if the file doesn't exist. Use `try/except`.

<details>
<summary>✅ Answer for P6</summary>

```python
def safe_open(filename):
    """Return file contents or None if file not found."""
    try:
        with open(filename, "r") as f:
            return f.read()
    except FileNotFoundError:
        return None
```
</details>

**P7.** Write `append_to_log(filename, message)` that appends a timestamped entry:
`[2024-03-15 10:30:22] User logged in`

**P8.** Write `load_csv(filename)` that reads a 2-column CSV file and returns a list of `(key, value)` tuples.

**P9.** Write `get_valid_input(prompt, min_val, max_val)` that keeps asking until the user enters an integer in the given range.

**P10.** Add complete docstrings (Args, Returns, Raises, Examples) to:
```python
def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("b cannot be zero")
    return a / b
```

### Tier 3 — Challenge

**P11.** Write a modular contact book: `load_contacts(file)`, `save_contacts(file, contacts)`, `add_contact(contacts, name, phone)`, `find_contact(contacts, name)`, `delete_contact(contacts, name)`. All data persists to file between runs.

**P12.** Write `parse_config(filename)` that reads a `.ini`-style config file (lines like `key=value`) and returns a dictionary. Handle missing file, malformed lines, and empty values gracefully.

**P13.** Write a fully documented `retry` wrapper: `retry(func, args, max_attempts=3, delay=1)` that calls `func(*args)`, catching exceptions, and retries up to `max_attempts` times before giving up.

**P14.** Build a modular score tracker that: loads scores from CSV on startup, lets user add/remove/edit scores, shows stats, and saves back to CSV on exit — all with complete docstrings and error handling.

**P15.** Write a program that scans a Python `.py` file and reports any functions that are missing docstrings. Read the file line by line, detect `def` lines, and check if the next non-empty line starts with `"""`.

---