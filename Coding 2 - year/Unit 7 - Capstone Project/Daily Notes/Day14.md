# Day 14: Sprint 2 Continued – Refinement & Extensions

**Session Goal:** Apply code review feedback and build additional features or improvements.

---

## Today's Focus

Day 13 gave you feedback; now you apply it. You'll refactor code based on peer suggestions, fix any identified issues, and add stretch features if you're ahead of schedule. By the end of Sprint 2 (Day 16), your app should be feature-complete and polished.

---

## Work Session Agenda

**Minutes 0-5:** **Standup**
- Review: what feedback will you apply today?
- Teacher: common feedback themes and how to address them
- Plan: prioritize what to work on today

**Minutes 5-50:** **Improvement & Feature Work**
- Apply code review feedback (variable names, docstrings, error handling)
- Fix bugs identified in code review
- Add stretch features if you've completed all planned features
- Continue testing and integration
- Ask for help if refactoring gets complicated

**Minutes 50-55:** **Wrap-up**
- Test after refactoring (make sure changes didn't break things)
- Commit changes with clear messages: "Apply peer feedback: improve variable names"
- Update progress

---

## Common Code Review Feedback & How to Address It

**Feedback: "Variable names are unclear"**
```python
# BEFORE
for s in self.students:
    if s.g > 3.5:
        top.append(s)

# AFTER
for student in self.students:
    if student.gpa > 3.5:
        top_students.append(student)
```
**Action:** Use find-and-replace (carefully) or manually update.

**Feedback: "No error handling for bad input"**
```python
# BEFORE
gpa = float(input("GPA: "))

# AFTER
try:
    gpa = float(input("GPA: "))
    if not 0 <= gpa <= 4.0:
        raise ValueError("GPA must be 0–4.0")
except ValueError:
    print("Invalid input. Try again.")
    return
```
**Action:** Add try/except blocks around risky operations.

**Feedback: "Functions are too long"**
```python
# BEFORE: one function does too much
def manage_students(self):
    # ... 50 lines of code

# AFTER: break into smaller functions
def display_menu(self):
    """Show menu options."""
    pass

def handle_user_choice(self, choice):
    """Process user's menu selection."""
    pass

def manage_students(self):
    """Main loop for student management."""
    while True:
        self.display_menu()
        choice = input("Pick: ")
        self.handle_user_choice(choice)
```
**Action:** Extract repeated or complex logic into helper functions.

---

## Stretch Features (If You're Ahead)

If you've completed all planned features, consider:

**Data Analyzer:**
- Trend analysis or simple prediction
- Multiple file comparison
- Export to Excel or PDF

**API App:**
- Filter or sort results
- Save user favorites
- Display historical data

**Student System:**
- Course management (add/remove courses)
- Grade calculation and reporting
- Data validation and duplicate detection

**Algorithm Visualizer:**
- Additional sorting algorithm
- Interactive step-through mode
- Detailed comparison report

---

## Refactoring Safely

When you refactor (improve code without changing behavior):

1. **Make a backup** — Commit your current code first
2. **Change one thing at a time** — Small changes are easier to test
3. **Test immediately** — After each change, verify it still works
4. **Use git** — If you mess up, you can revert

```python
# Example: refactor variable names
# Step 1: Rename s to student in load_students()
def load_students(filename):
    students = []
    with open(filename) as f:
        data = json.load(f)
    for student_data in data:
        student = Student(**student_data)
        students.append(student)
    return students

# Step 2: Test — does it still work?
# Step 3: Commit: "Refactor: improve variable names in load_students()"
# Step 4: Move to next function
```

---

## Reflection / Exit Ticket

1. Which piece of feedback did you apply?
2. Did refactoring break anything? How did you fix it?
3. How confident are you about your code now?

---

## Progress Checklist

- [ ] Code review feedback applied
- [ ] Variables renamed for clarity
- [ ] Error handling improved
- [ ] Refactoring tested and verified
- [ ] Stretch features started (optional)
- [ ] Code committed/saved
