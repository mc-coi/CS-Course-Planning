# Day 12: Sprint 2 – Finalizing & Polishing

**Session Goal:** Complete Sprint 2 features and prepare for peer code review on Day 13.

---

## Today's Focus

Sprint 2 ends tomorrow with a peer code review. Today you finish features and make sure your code is readable and well-documented. Think of Day 13 like having a code reviewer at work—you want to be proud of what you show them.

---

## Work Session Agenda

**Minutes 0-5:** **Standup**
- What features are done? What needs finishing?
- Is anything broken? Identify and fix now.
- Teacher: Day 13 peer review expectations

**Minutes 5-50:** **Final Features & Code Quality**
- Finish any incomplete Sprint 2 features
- Add docstrings to any functions missing them
- Clean up variable names (clear > clever)
- Remove dead code and debug statements
- Add comments for complex logic
- Test again: run through multiple scenarios

**Minutes 50-55:** **Prepare for Peer Review**
- Make sure your code is saved/committed
- Know what features you have and what's missing
- Prepare to explain your architecture
- Jot down any known bugs or limitations

---

## Code Review Checklist

Before Day 13, make sure:

- [ ] Every function has a docstring
- [ ] Variable names are clear (not single letters)
- [ ] No unused code or debug print statements
- [ ] Consistent indentation and spacing
- [ ] Comments explain "why" (the "what" should be obvious from code)
- [ ] File structure is logical and easy to navigate
- [ ] No credentials or sensitive data in code
- [ ] All features work without crashing

---

## Pre-Review Code Cleanup

**Find and remove debug code:**
```bash
# Look for print statements you used for debugging
grep -n "print(" *.py

# Look for commented-out code
grep -n "^[[:space:]]*#[^#]" *.py  # Lines that start with #
```

**Add missing docstrings:**
```python
def sort_by_gpa(self):
    """Sort students by GPA in descending order (highest first).

    Returns:
        list[Student]: Sorted list of students
    """
    return sorted(self.students, key=lambda s: s.gpa, reverse=True)
```

**Improve variable names:**
```python
# BEFORE: unclear
for s in students:
    if s.g > 3.5:
        top.append(s)

# AFTER: clear
for student in students:
    if student.gpa > 3.5:
        top_students.append(student)
```

---

## Documentation Template

If you haven't created a README yet, start now:

```markdown
# [Your Project Name]

## Overview
One sentence: what does this app do?

## How to Run
```bash
python main.py
```

## Features
- Feature 1: description
- Feature 2: description
- ...

## Project Structure
- `main.py`: entry point
- `src/`: main classes
- `data/`: data files
- etc.

## Known Limitations
- (Any features you didn't finish or bugs you found)

## How to Test
1. Step 1
2. Step 2
```

---

## Reflection / Exit Ticket

1. What are you most proud of in Sprint 2?
2. What code are you nervous about showing on Day 13?
3. What will you do differently in Sprint 3?

---

## Progress Checklist

- [ ] All Sprint 2 features complete and working
- [ ] Code is clean and well-documented
- [ ] Docstrings added to all functions
- [ ] Debug code removed
- [ ] README started or completed
- [ ] Code saved/committed and ready for peer review
