# Day 4: Development Session 3 — Polish & Documentation

### Key Concepts

**Refactoring:** Improving code structure without changing behavior.

Signs your code needs refactoring:
- A function is longer than ~20 lines — can it be split?
- The same code appears in multiple places — extract it to a function
- Variable names are unclear (`x`, `temp`, `stuff`)
- A function does more than one thing

**Code polish checklist:**
- [ ] All functions have docstrings
- [ ] Variable names are descriptive
- [ ] No duplicate code
- [ ] Error handling for all user inputs
- [ ] Edge cases tested (empty input, 0, large values)
- [ ] Code is consistently indented
- [ ] Comments explain *why*, not *what*

### Code Examples — Before and After Refactoring

```python
# ── BEFORE: messy, undocumented ────────────────────────────
def f(x):
    t = 0
    for i in x:
        t += i
    a = t / len(x)
    if a >= 90:
        g = "A"
    elif a >= 80:
        g = "B"
    elif a >= 70:
        g = "C"
    elif a >= 60:
        g = "D"
    else:
        g = "F"
    print("Avg:", a, "Grade:", g)

# ── AFTER: clean, modular, documented ──────────────────────
def calculate_average(scores):
    """Return the mean of a non-empty list of numbers."""
    return sum(scores) / len(scores)

def assign_letter_grade(average):
    """Convert numeric average to letter grade A through F."""
    if average >= 90: return "A"
    if average >= 80: return "B"
    if average >= 70: return "C"
    if average >= 60: return "D"
    return "F"

def print_grade_summary(scores):
    """Calculate and display average and letter grade for scores."""
    if not scores:
        print("No scores to analyze.")
        return
    avg = calculate_average(scores)
    grade = assign_letter_grade(avg)
    print(f"Average: {avg:.1f}  |  Grade: {grade}")

# ── What improved: ─────────────────────────────────────────
# 1. Split one function into three (single responsibility)
# 2. Meaningful names: f → print_grade_summary
# 3. Descriptive variable names: t → total (via sum()), a → avg, g → grade
# 4. Docstrings added
# 5. Edge case handled (empty list)
```

### Final Polish Checklist

Work through your entire project and check each item:

**Function Quality**
- [ ] Every function has a clear, descriptive name
- [ ] Every function has a docstring
- [ ] Every function does exactly one job
- [ ] No function is longer than ~20 lines

**Error Handling**
- [ ] All user inputs are validated
- [ ] File operations use `try/except`
- [ ] Division checks for zero
- [ ] List access checks length first

**Code Style**
- [ ] Consistent indentation (4 spaces)
- [ ] Blank lines between functions
- [ ] Module-level docstring at top of file
- [ ] No commented-out dead code left in

**Testing**
- [ ] Each function tested individually
- [ ] Edge cases tested (empty, 0, max values)
- [ ] Full program run-through on normal input
- [ ] Full program run-through on bad input

---