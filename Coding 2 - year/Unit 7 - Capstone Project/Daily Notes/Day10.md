# Day 10: Sprint 2 Begins – Feature Expansion

**Session Goal:** Start implementing the next set of features. Build on your Sprint 1 foundation.

---

## Today's Focus

Sprint 2 is about expansion and polish. You've proven your core architecture works; now add features, improve user experience, and connect more components. Your code should be less buggy and more integrated.

---

## Work Session Agenda

**Minutes 0-5:** **Sprint 2 Standup**
- Teacher: what makes Sprint 2 different (polish, expand, integrate)
- Students: identify 2–3 new features for this sprint
- Reminder: your foundation is solid; build with confidence

**Minutes 5-50:** **Feature Development**
- Implement new features from your plan (search, sort, reports, visualizations, etc.)
- Test integration: do new features work with existing code?
- Focus on one feature at a time; finish before moving to the next
- Ask for help early if stuck

**Minutes 50-55:** **Wrap-up & Save**
- Test your new features
- Commit code
- Log progress

---

## Sprint 2 Feature Examples by Project

**Data Analyzer:**
- Filter data by criteria
- Create a second chart type
- Calculate additional statistics (median, standard deviation)

**API App:**
- Second API endpoint or data source
- User preferences/configuration saved to file
- Caching to reduce API calls

**Student System:**
- Search by name
- Sort by GPA or name
- Bulk add students from CSV

**Algorithm Visualizer:**
- Second sorting algorithm
- Benchmark and compare speeds
- Visualize the sorting process

---

## Building Features in Sprint 2

Same process as Sprint 1, but with more confidence:

1. **Write a stub** with docstring
2. **Implement** — you know how now
3. **Test immediately** — print statements, manual testing
4. **Error handling** — same rigor as Sprint 1
5. **Clean up** — remove debug code, improve names
6. **Integrate** — connect to existing features
7. **Move on** — don't polish yet

---

## Debugging with Confidence

By now you've fixed some bugs. Use what you learned:

```python
# You know to test file I/O:
system.save_to_json("test.json")
system2 = StudentSystem()
system2.load_from_json("test.json")
assert len(system2.students) == len(system.students)

# You know to validate input:
try:
    gpa = float(input("GPA: "))
    if not 0 <= gpa <= 4.0:
        raise ValueError("GPA must be 0-4")
except ValueError as e:
    print(f"Invalid: {e}")
```

---

## Reflection / Exit Ticket

1. Which new feature did you start today?
2. Did it integrate smoothly with Sprint 1 code?
3. What's your goal for Day 11?

---

## Progress Checklist

- [ ] Sprint 2 features identified
- [ ] First new feature implemented
- [ ] Feature tested and integrated
- [ ] Code committed/saved
