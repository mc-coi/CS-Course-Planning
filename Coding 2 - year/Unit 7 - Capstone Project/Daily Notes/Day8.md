# Day 8: Sprint 1 – Feature Completion & Bug Fixes

**Session Goal:** Finish remaining Sprint 1 features and fix any bugs you've found.

---

## Today's Focus

Sprint 1 ends tomorrow with a check-in. Today you finish any incomplete features and squash bugs. By end of day, your core features should all be working. This is your last chance before Sprint 1 review, so be thorough.

---

## Work Session Agenda

**Minutes 0-5:** **Sprint Standup**
- What features are done? What's left?
- Identify blockers: is anything stuck? Need help?
- Teacher: last-minute help and debugging support available

**Minutes 5-50:** **Final Feature Push & Debugging**
- Complete any unfinished features
- Test thoroughly: run through multiple scenarios
- Fix bugs as you find them
- Add comments and improve code readability
- Consider: Is your code ready for someone else to read?

**Minutes 50-55:** **Wrap-up & Preparation for Check-In**
- Make sure all code is committed/saved
- Prepare a quick demo of your app for tomorrow
- Jot down any bugs or limitations you found
- Fill out progress tracker

---

## Pre-Check-In Debugging Checklist

Before Day 9, verify:

- [ ] All Sprint 1 features work without crashing
- [ ] Data persists correctly (save and load work)
- [ ] No typos in variable or function names
- [ ] Comments explain "why" not just "what"
- [ ] User input is validated (try/except for bad input)
- [ ] Your app has a clean menu or entry point
- [ ] You can explain each part of your code
- [ ] No dead code (unused functions/variables)

---

## Common Bugs & Fixes

**Bug: "File not found" when loading data**
```python
# WRONG: assumes file exists
with open("data/students.json") as f:
    students = json.load(f)

# RIGHT: handle missing file
try:
    with open("data/students.json") as f:
        students = json.load(f)
except FileNotFoundError:
    students = []  # Start with empty list
```

**Bug: "TypeError: object of type X is not JSON serializable"**
```python
# WRONG: can't serialize custom objects directly
data = [Student("Alice", 123, 3.8), ...]
json.dump(data, f)

# RIGHT: convert to dict first
data = [s.__dict__ for s in students]  # or custom to_dict() method
json.dump(data, f)
```

**Bug: Accidental modification of shared data**
```python
# WRONG: list aliasing
def get_top_students(system, count):
    top = system.students.sort(key=lambda s: s.gpa, reverse=True)
    return top[:count]  # Modifies original!

# RIGHT: don't modify original
def get_top_students(system, count):
    sorted_list = sorted(system.students, key=lambda s: s.gpa, reverse=True)
    return sorted_list[:count]  # Original unchanged
```

---

## Code Review Yourself

Read through your code as if you're a classmate. Ask:

- Can I understand what this function does from the docstring?
- Are variable names clear? (e.g., `s` vs. `student`)
- Is there commented-out code that should be deleted?
- Are there any `print()` statements that should be removed?
- Do I handle edge cases (empty lists, None values)?

---

## Reflection / Exit Ticket

1. Which feature are you most proud of from Sprint 1?
2. What bug took the longest to fix?
3. What will you do differently in Sprint 2?

---

## Progress Checklist

- [ ] All Sprint 1 features complete and working
- [ ] Major bugs fixed
- [ ] Code cleaned up and commented
- [ ] Demo prepared for Day 9 check-in
- [ ] All code saved/committed
