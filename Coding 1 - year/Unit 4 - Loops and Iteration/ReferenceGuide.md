# Unit 4 Reference Guide — Loops, Iteration & Lists

## Loop Syntax Reference

### While Loop
```python
while condition:
    # Loop body
    # Must update something to make condition false
```

**Example:**
```python
count = 0
while count < 5:
    print(count)
    count += 1
```

### For Loop
```python
for variable in sequence:
    # Loop body
    # variable takes each value from sequence
```

**Example:**
```python
for i in range(5):
    print(i)

for name in ["Alice", "Bob", "Charlie"]:
    print(name)
```

---

## range() Function

**Syntax:** `range(stop)` or `range(start, stop)` or `range(start, stop, step)`

**Parameters:**
- `start`: Where to begin (default: 0)
- `stop`: Where to stop (exclusive—not included)
- `step`: Increment each iteration (default: 1)

**Examples:**
| Code | Output |
|------|--------|
| `range(5)` | 0, 1, 2, 3, 4 |
| `range(1, 6)` | 1, 2, 3, 4, 5 |
| `range(0, 10, 2)` | 0, 2, 4, 6, 8 |
| `range(10, 0, -1)` | 10, 9, 8, ..., 1 |
| `range(1, 11, 2)` | 1, 3, 5, 7, 9 |

---

## Loop Control Statements

### break
**Immediately exits the loop.**
```python
for i in range(10):
    if i == 5:
        break
    print(i)  # Prints 0, 1, 2, 3, 4
```

### continue
**Skips the current iteration, moves to next.**
```python
for i in range(5):
    if i == 2:
        continue
    print(i)  # Prints 0, 1, 3, 4
```

---

## Nested Loops

**Structure:** Loop inside a loop.
```python
for outer in range(n):
    for inner in range(m):
        # Executes n × m times
```

**Example:** 3×3 grid
```python
for row in range(3):
    for col in range(3):
        print("*", end=" ")
    print()  # Newline after each row
```

**Output:**
```
* * *
* * *
* * *
```

---

## List Basics

### Creating Lists
```python
empty = []
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]
mixed = [42, "hello", 3.14, True]
```

### Indexing (0-based)
```python
names = ["Alice", "Bob", "Charlie"]
names[0]      # "Alice" (first)
names[1]      # "Bob" (second)
names[-1]     # "Charlie" (last)
names[-2]     # "Bob" (second-to-last)
```

### Length
```python
len(names)  # 3
```

### Slicing
```python
numbers = [1, 2, 3, 4, 5]
numbers[1:4]   # [2, 3, 4]
numbers[:3]    # [1, 2, 3]
numbers[2:]    # [3, 4, 5]
```

### Checking Membership
```python
"Alice" in names     # True
"David" in names     # False
```

---

## List Methods

| Method | Use | Example | Result |
|--------|-----|---------|--------|
| `.append(value)` | Add to end | `list.append(5)` | Adds 5 at end |
| `.remove(value)` | Remove first occurrence | `list.remove(2)` | Removes first 2 |
| `.pop(index)` | Remove at index (default last) | `list.pop()` | Removes last item |
| `.sort()` | Sort ascending (in place) | `list.sort()` | Sorts the list |
| `.reverse()` | Reverse (in place) | `list.reverse()` | Reverses the list |
| `.index(value)` | Find position | `list.index(3)` | Returns position of 3 |
| `.count(value)` | Count occurrences | `list.count(3)` | Returns how many 3's |
| `.insert(index, value)` | Insert at position | `list.insert(0, 99)` | Inserts 99 at index 0 |

**Example:**
```python
numbers = [3, 1, 4, 1, 5]
numbers.append(9)       # [3, 1, 4, 1, 5, 9]
numbers.remove(1)       # [3, 4, 1, 5, 9] (removes first 1)
numbers.sort()          # [1, 3, 4, 5, 9]
print(numbers.count(1)) # 1
```

---

## Looping Patterns

### Counter Pattern (While)
```python
count = 0
while count < 10:
    print(count)
    count += 1  # MUST update or infinite loop
```

### Sentinel Pattern
```python
while True:
    value = input("Enter (quit to stop): ")
    if value == "quit":
        break
    # Process value
```

### Accumulator Pattern
```python
total = 0
for num in numbers:
    total += num  # Add to accumulator
print(total)
```

### Input Validation Pattern
```python
while True:
    age = int(input("Age (0-120): "))
    if 0 <= age <= 120:
        break
    print("Invalid. Try again.")
```

### For-Each Pattern (Lists)
```python
for item in list:
    print(item)
```

### Index-Based Pattern (Lists)
```python
for i in range(len(list)):
    print(f"{i}: {list[i]}")
```

### Min/Max Pattern
```python
max_val = numbers[0]
for num in numbers:
    if num > max_val:
        max_val = num
```

### Search Pattern
```python
found = False
for item in list:
    if item == target:
        found = True
        break
```

---

## Common Loop Mistakes & Fixes

| Mistake | Error/Problem | Fix |
|---------|---------------|-----|
| **Infinite loop** | Program never stops | Make sure condition changes: `count += 1` |
| **Off-by-one** | Wrong number of iterations | Remember: `range(5)` is 0-4, not 1-5 |
| **Missing colon** | SyntaxError | Always use `:` after loop: `for i in range(5):` |
| **Wrong indentation** | IndentationError | Loop body must be indented 4 spaces |
| **break/continue outside loop** | NameError | These only work inside loops |
| **Forgot to initialize variable** | NameError: name not defined | Declare before using: `count = 0` |
| **List index out of range** | IndexError | Check: `0 <= index < len(list)` |
| **Modifying list while iterating** | Skips elements | Loop over a copy: `for x in list[:]` |
| **Using `=` in condition** | Logic error | Use comparison: `while x < 5:` not `x = 5` |
| **range() parameters wrong** | Off-by-one | `range(1, 6)` gives 1-5; `range(6)` gives 0-5 |

---

## String Methods for Loops

**Testing characters:**
| Method | Returns True If |
|--------|-----------------|
| `.isdigit()` | Character is 0-9 |
| `.isalpha()` | Character is a letter |
| `.isalnum()` | Character is letter or digit |
| `.isspace()` | Character is whitespace |
| `.isupper()` | Character is uppercase |
| `.islower()` | Character is lowercase |

**Example:**
```python
text = "Hello123"
for char in text:
    if char.isdigit():
        print(f"{char} is a digit")
    elif char.isalpha():
        print(f"{char} is a letter")
```

---

## Loop Decision Tree

```
Need to repeat code?
│
├─ Yes, and I know exactly how many times?
│  └─ Use FOR loop with range()
│
├─ Yes, over a list or string?
│  └─ Use FOR loop (for-each)
│
├─ Yes, until user enters special value?
│  └─ Use WHILE loop with break (sentinel)
│
├─ Yes, until input is valid?
│  └─ Use WHILE loop (validation)
│
└─ Yes, condition is complex/changing?
   └─ Use WHILE loop
```

---

## Quick Reference: Common Code Snippets

**Sum all numbers in a list:**
```python
total = 0
for num in numbers:
    total += num
```

**Count items meeting a condition:**
```python
count = 0
for item in items:
    if condition(item):
        count += 1
```

**Find maximum:**
```python
max_val = numbers[0]
for num in numbers:
    if num > max_val:
        max_val = num
```

**Check if value exists:**
```python
found = False
for item in items:
    if item == target:
        found = True
        break
```

**Print list with numbers:**
```python
for i in range(len(items)):
    print(f"{i}: {items[i]}")
```

**Ask until valid:**
```python
while True:
    value = int(input("Enter (1-10): "))
    if 1 <= value <= 10:
        break
```

---

## Debugging Tips

1. **Print variable values:** `print(f"i={i}, count={count}")`
2. **Count iterations:** How many times does it loop?
3. **Trace by hand:** Do first 2-3 iterations manually
4. **Check condition:** Will it eventually be false?
5. **Test edge cases:** Empty list, single item, large numbers
6. **Read error message:** Python tells you what's wrong!

---

## Practice Code Template

```python
# Loop Practice: [Description]

# Step 1: Get input
items = []
while True:
    item = input("Enter item ('done' to stop): ")
    if item == "done":
        break
    items.append(item)

# Step 2: Process
result = 0
for item in items:
    # Process item
    pass

# Step 3: Output
print(f"Result: {result}")
```

---
