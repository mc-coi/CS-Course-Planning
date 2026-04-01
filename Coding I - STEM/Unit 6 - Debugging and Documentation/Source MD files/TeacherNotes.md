# Unit 6 - Debugging and Documentation: Teacher Misconception & Callout Guide

## Overview
Unit 6 is where students stop blaming Python and start blaming themselves—positively. This unit bridges the gap between "code that works by accident" and "code I understand and can fix." The critical misconceptions are: (1) treating error messages as mysterious rather than informative, (2) confusing syntax errors with runtime errors, (3) not systematically testing edge cases, (4) thinking comments and docstrings are extra/optional, and (5) writing defensive code (error handling) as an afterthought rather than a core practice. File I/O introduces new errors (`FileNotFoundError`) that must be handled gracefully. Since this is the final conceptual unit before the capstone project, solidifying debugging skills and documentation habits here directly impacts the quality of student work in Unit 7. Teach debugging as a **systematic methodology**, not a random trial-and-error process.

---

## Misconceptions by Topic

### Error Classification (Day 1)

**⚠️ Misconception:** "An error means my code is broken; I should start over."

**What it looks like in code:**
```python
# Student sees any error and wants to delete and rewrite
for i in range(10)
    print(i)           # SyntaxError: expected ':'
# Student thinks: "This is all wrong!"
```

**Why students think this:** They don't yet see errors as normal and fixable.

**How to address it:** Reframe: "Errors are normal and informative. They tell you exactly what's wrong and where. Every programmer gets errors—that's not failure, that's progress. The error is a gift; it's showing you something to fix." Classify errors together:
- Syntax errors stop the program before it runs
- Runtime errors crash the program while running
- Logic errors let the program run but produce wrong output

**STEM priority:** Critical—affects attitude about debugging.

**⚠️ Misconception:** "Syntax errors and runtime errors are the same thing; they both mean the code is wrong."

**What it looks like in code:**
```python
# Syntax error (code doesn't run)
for i in range(10)
    print(i)

# Runtime error (code starts but crashes)
nums = [1, 2, 3]
print(nums[10])
# Student treats both as "errors I can't fix"
```

**Why students think this:** Both stop the program; students conflate them.

**How to address it:** Distinguish: "Syntax errors mean Python can't even read your code—it's broken English. Runtime errors mean Python *understood* your code but something went wrong while running it. Syntax errors need code structure fixes. Runtime errors need logic fixes (like checking bounds)." Show the flow:
```
Write code → Check syntax → Run code → Runtime errors?
            ↓
         SyntaxError (can't even run)
                              ↓
                         RuntimeError (crashes while running)
```

**STEM priority:** Critical—helps students classify and fix.

**⚠️ Misconception:** "Logic errors are the worst because they don't give me an error message."

**What it looks like in code:**
```python
# Logic error: wrong output, no crash
total = 0
for i in range(10):
    total = i               # BUG: should be total += i
print(total)                # Prints 9, not 45
# No error message — student is lost
```

**Why students think this:** Silent failures feel more mysterious than crashes.

**How to address it:** Explain: "Logic errors are tricky because there's no error message—the program runs fine. You have to think: 'Does the output match what I expected?' If not, it's a logic error. Use print statements to trace your variables and see where they diverge from your expectation." Teach the debugging process.

**STEM priority:** Critical—logic errors are most common and hardest to find.

---

### Debugging Strategies (Days 1–2)

**⚠️ Misconception:** "When debugging, I should just keep changing things until it works; the order doesn't matter."

**What it looks like in code:**
```python
# Student randomly changes:
# - variable names
# - operator symbols
# - indentation
# - loop bounds
# ...hoping something fixes it
```

**Why students think this:** They see debugging as random trial-and-error.

**How to address it:** Teach a **systematic process**:
1. Read the error message carefully (line number, type, message)
2. Understand what the code is supposed to do
3. Add print statements to trace variable values
4. Compare actual values to expected values
5. Pinpoint where they diverge
6. Fix the specific issue

Say: "Debugging is detective work. You gather clues (error message, print output), form a hypothesis (what's wrong), and test it. Random changes make it worse because you lose track of what changed."

**STEM priority:** Critical—methodology matters.

**⚠️ Misconception:** "Error messages are written for experts; I can't understand them."

**What it looks like in code:**
```python
# TypeError: can only concatenate str (not "int") to str
# Student reads this and gives up, thinking it's incomprehensible
```

**Why students think this:** Error messages use technical language.

**How to address it:** Teach error message reading as a skill:
1. The error type (e.g., `TypeError`) tells you the category
2. The message (after the colon) describes what went wrong
3. The line number tells you where to look

Say: "Error messages are written in a formula. Once you know the pattern, they're your friends. Let's decode them together." Practice reading errors in class, translating them to plain English.

**STEM priority:** Critical—error literacy is fundamental.

**⚠️ Misconception:** "Print statements are for showing output; I shouldn't use them for debugging."

**What it looks like in code:**
```python
# Student writes code and runs it, but when something is wrong,
# they stare at the code instead of adding print statements
```

**Why students think this:** They think print is only for final output.

**How to address it:** Teach: "Print statements are debugging tools. Add them to trace what's happening. Print variable values at each step and check if they're what you expect. Once you find the bug, remove the debug prints." Show the technique:
```python
total = 0
for i in range(10):
    total = i
    print(f"DEBUG: i={i}, total={total}")  # Track it
print(total)

# Output shows the bug:
# DEBUG: i=0, total=0
# DEBUG: i=1, total=1
# ...
# The assignment is wrong (should be +=)
```

**STEM priority:** Critical—debugging technique.

---

### Exception Handling (Days 2–3)

**⚠️ Misconception:** "Try/except is for catching errors I don't understand; I should use it everywhere."

**What it looks like in code:**
```python
try:
    everything()       # Catches ALL errors, good and bad
except:
    pass               # Silently ignores all problems
```

**Why students think this:** They see `try/except` as a blanket safety net.

**How to address it:** Warn: "Bare `except:` hides errors and makes debugging impossible. Only catch specific errors you expect and can handle. If an unexpected error happens, let it crash so you can see what's wrong." Show the right way:
```python
# WRONG: catches everything, hides real bugs
try:
    x = int(input("Number: "))
except:
    pass

# RIGHT: catch specific errors
try:
    x = int(input("Number: "))
except ValueError:
    print("Please enter a number")
```

**STEM priority:** Critical—bad practice leads to hidden bugs.

**⚠️ Misconception:** "Try/except is for file operations; I don't need it for normal code."

**What it looks like in code:**
```python
# Student uses try/except for file I/O but not for input conversion
age = int(input("Age: "))     # Can crash with ValueError!
with open("data.txt") as f:   # But here they use try/except
    content = f.read()
```

**Why students think this:** Files feel "special" so they associate try/except with them.

**How to address it:** Explain: "Try/except is for any code that might crash. File operations, type conversion, list access, division—any of these can fail. Wrap them in try/except if failure is possible and you want to recover." Show examples:
```python
# User input can fail (ValueError)
try:
    age = int(input("Age: "))
except ValueError:
    print("Please enter a number")

# File operations can fail (FileNotFoundError)
try:
    with open("data.txt") as f:
        content = f.read()
except FileNotFoundError:
    print("File not found")

# List access can fail (IndexError)
try:
    first = numbers[0]
except IndexError:
    print("List is empty")
```

**STEM priority:** Critical—defensive programming is professional practice.

**⚠️ Misconception:** "`finally` is optional; I only need `try` and `except`."

**What it looks like in code:**
```python
with open("data.txt") as f:
    content = f.read()
    # File closes automatically with `with`

# But without `with`, they might forget to close:
f = open("data.txt")
content = f.read()
# f stays open!
```

**Why students think this:** With the `with` statement, they don't see why `finally` is needed.

**How to address it:** Explain: "`with` automatically closes files (good!). If you use `try/except` without `with`, use `finally` to guarantee cleanup (close files, release resources). But `with` is preferred because it's clearer." Show both:
```python
# GOOD: with statement handles cleanup
try:
    with open("data.txt") as f:
        content = f.read()
except FileNotFoundError:
    print("File not found")
# File is automatically closed

# ALSO OK: finally for cleanup
try:
    f = open("data.txt")
    content = f.read()
except FileNotFoundError:
    print("File not found")
finally:
    if f:
        f.close()   # Guaranteed to run
```

**STEM priority:** Medium—`with` is sufficient for most cases.

---

### File I/O (Days 2–3)

**⚠️ Misconception:** "I can write to a file, then immediately read it without closing and reopening."

**What it looks like in code:**
```python
f = open("data.txt", "w")
f.write("Hello\n")
# File still has unsaved data (buffered)
content = f.read()              # Can't read a file open for writing!
f.close()
```

**Why students think this:** Files feel like in-memory operations.

**How to address it:** Explain: "When you write to a file, the data is buffered (held temporarily). You must close the file to save it. To read it back, you must open it again in read mode. Use `with` to handle this automatically." Show the pattern:
```python
# WRITE to a file
with open("data.txt", "w") as f:
    f.write("Hello\n")
# File is automatically closed and saved

# READ from the file
with open("data.txt", "r") as f:
    content = f.read()
print(content)

# OR: do both with two separate operations
# Don't try to write and read in one operation
```

**STEM priority:** Critical—prevents data loss and errors.

**⚠️ Misconception:** "File paths don't matter; the file is always in the same place."

**What it looks like in code:**
```python
# Works on student's computer
open("data.txt")

# Fails on someone else's computer or in a different directory
# because the file isn't there
```

**Why students think this:** They don't understand file paths and relative/absolute locations.

**How to address it:** Teach: "File paths are relative to where your Python script is. If `data.txt` is in the same folder as your script, `open("data.txt")` works. If it's in a subfolder, use `open("subfolder/data.txt")`. Use absolute paths for portability: `open("/Users/name/Desktop/data.txt")`." Show the importance:
```python
# Relative path (depends on where script is)
open("data.txt")                    # data.txt must be in same folder
open("subfolder/data.txt")          # data.txt in subfolder

# Absolute path (always works, but less portable)
open("/Users/zach/Desktop/data.txt")
```

**STEM priority:** Low—doesn't block learning but prevents frustration.

**⚠️ Misconception:** "I can use `"` or `'` interchangeably in file paths; there's no difference."

**What it looks like in code:**
```python
open('data.txt')        # Works
open("data.txt")        # Also works
# Student thinks they're identical
```

**Why students think this:** In most contexts, they are equivalent.

**How to address it:** Clarify: "Both `'` and `\"` work for file paths (they're string delimiters). Use whichever you prefer, but be consistent. Backslashes in Windows paths need escaping: use `r"C:\Users\..."` (raw string) or forward slashes `"C:/Users/..."`." Show the pitfall:
```python
# Windows path problem
open("C:\Users\zach\data.txt")  # ERROR: \z, \d are escape sequences!
open(r"C:\Users\zach\data.txt")  # OK: raw string
open("C:/Users/zach/data.txt")   # OK: forward slashes
```

**STEM priority:** Low—informational; prevents Windows-specific bugs.

---

### Docstrings & Comments (Days 4–5)

**⚠️ Misconception:** "Comments are for explaining obvious code; if the code is clear, I don't need comments."

**What it looks like in code:**
```python
# BAD: comment repeats code
x = 5
# Set x to 5

# GOOD: comment explains WHY
x = 5
# Threshold for "high score" in game
```

**Why students think this:** They read comments that just restate code and think that's all comments do.

**How to address it:** Teach: "Comments explain **why**, not what. The code shows **what** it does. A good comment answers: 'Why did you do it this way? What assumption are you making? What edge case are you handling?' Don't comment obvious code." Show examples:
```python
# BAD (repeats code)
# i += 1
i += 1

# GOOD (explains intent)
# Skip this user if they're inactive
i += 1

# GOOD (explains algorithm choice)
# Use binary search for efficiency with large lists
index = binary_search(arr, target)
```

**STEM priority:** Low—style, but important for readability.

**⚠️ Misconception:** "Docstrings are the same as comments; I can use them interchangeably."

**What it looks like in code:**
```python
def add(a, b):
    # Add two numbers
    return a + b

# vs.

def add(a, b):
    """Add two numbers."""
    return a + b
```

**Why students think this:** Both document code; they look similar.

**How to address it:** Clarify: "Comments (with `#`) are for inline explanations. Docstrings (with `\"\"\"`) document entire functions/modules. Docstrings come right after the `def` line and appear in help. Docstrings are professional; they describe parameters, return values, and examples." Show the format:
```python
def calculate_average(scores):
    """Calculate the arithmetic mean of a list of scores.

    Args:
        scores (list): A list of numeric scores.

    Returns:
        float: The average of the scores, or 0 if the list is empty.

    Example:
        >>> calculate_average([85, 90, 92])
        89.0
    """
    if not scores:
        return 0.0
    return sum(scores) / len(scores)
```

**STEM priority:** Medium—professional practice, not critical for basic code.

**⚠️ Misconception:** "Documentation is extra; I should write code first and document later."

**What it looks like in code:**
```python
# Student writes 50 lines of code, then says:
# "I'll add comments later"
# (Later never comes)
```

**Why students think this:** Documentation feels separate from coding.

**How to address it:** Teach: "Document as you write. Add docstrings right after defining functions. Add comments for non-obvious logic. Later, you'll forget why you wrote things. Documentation while coding captures your thinking." Make it a habit.

**STEM priority:** Medium—professional practice.

---

### Testing & Edge Cases (Day 5)

**⚠️ Misconception:** "If my code works on the examples, it's correct; I don't need to test edge cases."

**What it looks like in code:**
```python
def divide(a, b):
    return a / b

# Works fine:
print(divide(10, 2))   # 5.0

# But crashes on:
print(divide(10, 0))   # ZeroDivisionError!
# Student didn't test this edge case
```

**Why students think this:** They test happy paths and assume that's enough.

**How to address it:** Teach: "Always test edge cases: empty input, zero, negative numbers, very large numbers, boundary values. These are where bugs hide." Create a testing checklist:
```python
# Test cases to consider:
# - Normal case: average([85, 90, 92])
# - Empty case: average([])
# - Single item: average([85])
# - Negative: average([-5, 10])
# - Zeros: average([0, 0, 0])
# - Very large: average([1000000, 2000000])
```

**STEM priority:** Critical—edge cases are where real bugs hide.

**⚠️ Misconception:** "I should only test code after I write the whole program."

**What it looks like in code:**
```python
# Student writes 100 lines, then runs it all at once
# When it fails, they can't tell where the bug is
```

**Why students think this:** They see testing as a final step.

**How to address it:** Teach: "Test incrementally. Write a function, test it alone, then move to the next. If each piece works, the whole program is more likely to work. You catch bugs early when they're easy to fix." Show the process:
```python
# Test function immediately after writing
def double(n):
    return n * 2

print(double(5))       # 10 ✓
print(double(0))       # 0 ✓
print(double(-5))      # -10 ✓

# Function is solid; move on
```

**STEM priority:** Critical—incremental testing is professional practice.

---

## Whole-Class Warning Signs

- **Students not reading error messages; they just say "it's broken"** — Stop and teach error message literacy. Practice reading them together.
- **Widespread `FileNotFoundError`** — Students don't understand file paths. Review how file paths work relative to the script.
- **Code that catches all errors with bare `except:`** — Teach specific exception catching. Bad habit now causes nightmares later.
- **Missing `try/except` on user input** — Make input validation a habit from now on.
- **No comments or docstrings; code is uncommented** — Set minimum documentation standards. Make it graded.
- **Tests only "happy path"; no edge cases tested** — Teach testing methodology. Have students write test cases before code.
- **Logic errors left unfixed because students don't know how to debug** — Teach systematic debugging: read error, add prints, trace execution.

---

## Questions That Reveal Understanding

1. **"A program crashes with `TypeError: unsupported operand type(s)`. What does this mean?"**
   - Good answer: "You tried to do an operation on incompatible types, like adding text and a number. Find the line where you're doing math and check the types."
   - What it reveals: Can they read and interpret error messages?

2. **"What's the difference between a syntax error and a runtime error?"**
   - Good answer: "Syntax error means the code is grammatically wrong—Python can't read it. Runtime error means the code is valid but crashes while running."
   - What it reveals: Do they understand error categories?

3. **"Write a try/except block to safely get an integer from the user."**
   - Good answer:
   ```python
   try:
       num = int(input("Number: "))
   except ValueError:
       print("Please enter a number")
   ```
   - What it reveals: Can they use exception handling for real problems?

4. **"Here's code that has a logic error. How would you debug it?"**
   ```python
   total = 0
   for i in range(10):
       total = i
   print(total)
   ```
   - Good answer: "Add a print statement in the loop to see what `total` is each iteration. It shows the bug—`total = i` should be `total += i`."
   - What it reveals: Can they use debugging techniques systematically?

5. **"Write a docstring for this function: `def is_even(n):`"**
   - Good answer:
   ```python
   def is_even(n):
       """Check if a number is even.

       Args:
           n (int): The number to check.

       Returns:
           bool: True if n is even, False otherwise.
       """
       return n % 2 == 0
   ```
   - What it reveals: Do they understand docstring format and purpose?

6. **"What edge cases should you test for this function: `def divide(a, b): return a / b`"**
   - Good answer: "Test b=0 (ZeroDivisionError), b<0 (negative denominator), a and b very large, a=0 (zero numerator), etc."
   - What it reveals: Do they think about edge cases?

---

## Common Student Questions & How to Answer Them

**Q: "Is `with` statement required for files?"**
A: "Not technically, but it's the best practice. It automatically closes the file, so you don't forget. Without `with`, you must call `f.close()` yourself. Always use `with`."

**Q: "Can I catch multiple exception types at once?"**
A: "Yes: `except (ValueError, KeyError): pass` catches both. Or catch specific ones separately for different handling."

**Q: "Why can't I write and read a file in one operation?"**
A: "When you open a file for writing (`'w'`), it's set up to send data out. You can't read while it's in write mode. You must close and reopen in read mode (`'r'`). Or open it in `'w+'` mode (read/write), but that's less common."

**Q: "Do I need to comment every line?"**
A: "No! Comment the 'why', not the 'what'. One comment per function explaining its purpose is often enough. Comments inside should explain non-obvious logic or important assumptions."

**Q: "Why use docstrings instead of comments?"**
A: "Docstrings are special—Python can read them and generate help documentation. Comments are just for humans reading the code. Docstrings are professional and portable."

---

## Analogies That Work

**1. Debugging as Detective Work:**
"Debugging is like solving a mystery. The error message is your first clue. You gather more clues (print statements), form a hypothesis (what's wrong), test it, and narrow down the culprit. You don't randomly change things hoping one works—that's chaos."

**2. Exception Handling as a Safety Net:**
"Try/except is a safety net for predictable problems. If you expect something might go wrong (user types text instead of a number), you catch it and recover gracefully. But a bare safety net that hides all problems makes you blind to real disasters."

**3. File I/O as Postal Mail:**
"Open a file like opening an envelope. `'r'` mode: you're reading the letter inside. `'w'` mode: you're putting a new letter in and sealing it. You can't read and write the same envelope at the same time—you must close it to send it, then reopen to read the response."

---

## STEM-Specific Notes

**Pacing:** Unit 6 is 6 days / 2 weeks. This unit is denser than it looks:
- **Days 1–2 (Error classification, debugging, try/except):** Pace carefully; methodology takes time to stick.
- **Days 2–3 (File I/O, exception handling):** Practice heavily. File operations feel new to students.
- **Days 4–5 (Docstrings, testing):** Focus on habits. These are skills students must internalize.

**Acceleration Path:** For strong students, introduce custom exceptions or more advanced debugging tools (debuggers, logging module). Push them to write comprehensive tests (unit tests using `assert`).

**Support Path:** Provide **debugging templates**. When a student says "It's broken," have them follow a checklist:
1. Read the error message and line number
2. Add a print statement on that line or before it
3. Run again and check the output
4. Compare to what you expected
5. Change one thing and test again

---
