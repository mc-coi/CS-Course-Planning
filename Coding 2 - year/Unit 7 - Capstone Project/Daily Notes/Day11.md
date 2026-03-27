# Day 11: Sprint 2 – Continuing Development

**Session Goal:** Complete 2–3 more features. Your app is gaining substance.

---

## Today's Focus

You're in the groove now. Continue building features and refining. The difference between a good capstone and a great one is often polish and completeness—getting more features working smoothly.

---

## Work Session Agenda

**Minutes 0-5:** **Standup**
- Report: what feature did you finish yesterday?
- Teacher: any common issues across the class? (e.g., "Here's a reminder about list comprehensions")
- Students: target 1–2 features today

**Minutes 5-50:** **Focused Development**
- Build second and third Sprint 2 features
- Make sure each one integrates cleanly
- Test frequently
- If you finish early: add error handling, improve comments, test edge cases

**Minutes 50-55:** **Wrap-up**
- Test your app end-to-end
- Commit work
- Update progress

---

## Tips for Speed & Quality

**Speed up debugging:**
- Use `if __name__ == "__main__":` to test individual functions
- Create small test data files to verify quickly

**Keep code clean:**
- Delete debug print statements
- Use consistent naming (students, not studs or s)
- Add comments for tricky logic

**Know when to refactor:**
- If you wrote similar code twice, refactor into a helper function
- If a function is >30 lines, consider breaking it up
- Wait until features work before refactoring (refactor = fine-tuning)

---

## Example: Testing a Search Feature in Isolation

```python
# student.py or system.py

def search_by_name(self, name):
    """Return students matching the name (case-insensitive partial match)."""
    return [s for s in self.students if name.lower() in s.name.lower()]

# At bottom of file:
if __name__ == "__main__":
    # Quick test
    system = StudentSystem()
    system.add_student(Student("Alice Smith", 100, 3.5))
    system.add_student(Student("Bob Johnson", 101, 3.2))
    system.add_student(Student("Alice Jones", 102, 3.8))

    results = system.search_by_name("alice")
    print(f"Found {len(results)} Alices:")
    for s in results:
        print(f"  - {s.name}")

    # Should print: Found 2 Alices
```

---

## Reflection / Exit Ticket

1. How many Sprint 2 features have you completed?
2. Is your app starting to feel "real"? What makes it feel that way?
3. Any features that surprised you in difficulty or ease?

---

## Progress Checklist

- [ ] Second Sprint 2 feature completed
- [ ] Third Sprint 2 feature in progress or completed
- [ ] All features tested and integrated
- [ ] Code committed/saved
