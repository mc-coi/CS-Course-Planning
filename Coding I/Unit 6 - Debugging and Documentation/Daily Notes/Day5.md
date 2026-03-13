# Day 5: Documentation — Comments & Docstrings

### Key Concepts
- **Inline comments (`#`):** Short notes explaining *why* something is done
- **Docstrings (`"""..."""`):** Multi-line documentation for functions, classes, and modules
- Docstrings appear right after the `def` line and describe what the function does
- Docstrings are accessible at runtime: `help(my_function)` or `my_function.__doc__`
- Good comments explain *why*, not *what* — the code already shows what

### When to Comment vs. When Not To

| Comment This | Don't Comment This |
|-------------|-------------------|
| Complex algorithm choices | `x = x + 1  # add 1 to x` (obvious) |
| Business rules / magic numbers | `for i in range(10):  # loop 10 times` |
| Workarounds or known limitations | `name = "Alice"  # set name to Alice` |
| Why a particular approach was chosen | Self-explanatory variable names |

### Docstring Formats

```python
# ── Simple one-liner docstring ─────────────────────────────
def double(n):
    """Return n multiplied by 2."""
    return n * 2

# ── Multi-line (Google style) ─────────────────────────────
def calculate_grade(score):
    """Convert a numeric score to a letter grade.

    Args:
        score (int): Numeric score from 0 to 100.

    Returns:
        str: Letter grade ('A', 'B', 'C', 'D', or 'F').

    Raises:
        ValueError: If score is outside the 0–100 range.

    Examples:
        >>> calculate_grade(92)
        'A'
        >>> calculate_grade(75)
        'C'
    """
    if not 0 <= score <= 100:
        raise ValueError(f"Score {score} out of valid range (0-100)")
    if score >= 90: return "A"
    if score >= 80: return "B"
    if score >= 70: return "C"
    if score >= 60: return "D"
    return "F"

# ── Access docstrings at runtime ──────────────────────────
print(calculate_grade.__doc__)   # prints the docstring
help(calculate_grade)             # formatted help output
```

### Code Examples — Full Documentation

```python
"""
student_tracker.py
Module for tracking student grades and generating reports.
Author: [Your Name]
Date: [Date]
"""

# Constants — these numbers have special meaning
PASSING_SCORE = 70       # school policy: 70 is passing
MAX_SCORE = 100          # all scores out of 100
HONOR_ROLL_GPA = 3.5     # minimum GPA for honor roll

def get_letter_grade(score):
    """Convert a numeric score (0-100) to a letter grade.

    Args:
        score (float): The numeric score.

    Returns:
        str: Letter grade A through F.
    """
    if score >= 90: return "A"
    if score >= 80: return "B"
    if score >= 70: return "C"
    if score >= 60: return "D"
    return "F"

def is_passing(score):
    """Check if a score meets the passing threshold.

    Args:
        score (float): The score to check.

    Returns:
        bool: True if passing (>= 70), False otherwise.
    """
    return score >= PASSING_SCORE

def class_average(scores):
    """Calculate the average of a list of scores.

    Args:
        scores (list of float): Non-empty list of numeric scores.

    Returns:
        float: The arithmetic mean of the scores.
        Returns 0.0 if the list is empty.
    """
    if not scores:
        return 0.0
    return sum(scores) / len(scores)

def generate_report(student_name, scores):
    """Print a formatted grade report for a student.

    Args:
        student_name (str): The student's full name.
        scores (list of float): List of scores for the semester.
    """
    avg = class_average(scores)
    grade = get_letter_grade(avg)
    status = "PASSING" if is_passing(avg) else "FAILING"

    # Build header — same width regardless of name length
    print("=" * 40)
    print(f"  Grade Report: {student_name}")
    print("=" * 40)
    print(f"  Scores:  {scores}")
    print(f"  Average: {avg:.1f}")
    print(f"  Grade:   {grade}")
    print(f"  Status:  {status}")
    print("=" * 40)
```

### Practice Problems — Day 5

**Beginner:**
1. Add a docstring to each of these functions (write them yourself, then add docs):
   - `fahrenheit_to_celsius(f)` — converts temperature
   - `is_palindrome(text)` — checks if string reads same backwards
2. Add meaningful inline comments to a bubble sort algorithm.

**Intermediate:**

3. Write `validate_password(password)` with a full docstring including Args, Returns, Raises, and at least 3 inline comments explaining the logic.
4. Take a poorly commented program and improve it: add module-level docstring, function docstrings, and fix any confusing comments.

**Challenge:**

5. Write a fully documented `todo_list` module with functions: `create_list()`, `add_item(lst, task)`, `complete_item(lst, index)`, `remove_item(lst, index)`, `show_list(lst)`. Every function must have a complete docstring.

---
