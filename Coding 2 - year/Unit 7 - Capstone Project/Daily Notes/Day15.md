# Day 15: Sprint 2 Continued – Integration & Testing

**Session Goal:** Ensure all features work together seamlessly. Test edge cases and user scenarios.

---

## Today's Focus

You've built lots of features. Today you make sure they all play nicely together. You'll test real-world scenarios: What if a user does X then Y then Z? What if they enter bad data? What if they run out of memory? Real software is tested, not just built.

---

## Work Session Agenda

**Minutes 0-5:** **Standup**
- Teacher: importance of integration testing
- Show: test plan example (what scenarios to test)
- Students: identify 3–5 user scenarios to test today

**Minutes 5-50:** **Scenario Testing & Edge Case Handling**
- Write down 3–5 realistic user scenarios
- Run through each one manually
  - Scenario 1: "Add student → save → load → search"
  - Scenario 2: "Enter invalid data → app handles gracefully"
  - Scenario 3: "Delete all data → app recovers"
- Fix bugs as you find them
- Add error handling for edge cases you discover

**Minutes 50-55:** **Wrap-up**
- Document any bugs you found and fixed
- Commit work
- Prepare for final Sprint 2 push tomorrow

---

## Test Scenarios by Project

**Data Analyzer:**
1. Load CSV → compute stats → generate chart (end-to-end)
2. Search for non-existent data → app handles gracefully
3. Load corrupted CSV → app shows error and continues
4. Very large file → performance is acceptable
5. Export results → verify output file is correct

**API App:**
1. Fetch data from API → parse and display (end-to-end)
2. API is down → app shows error gracefully
3. Invalid API key → app explains the issue
4. Save favorites → reload and verify they're there
5. No internet connection → app caches old data or shows offline message

**Student System:**
1. Add student → save → load → verify data intact
2. Search for non-existent student → returns empty
3. Duplicate student ID → app prevents or handles gracefully
4. Delete all students → reload file → empty list works
5. Sort by GPA with ties → sorts consistently

**Algorithm Visualizer:**
1. Sort small array (10 elements) → verify correctness
2. Sort large array (1000+ elements) → measure time
3. Compare two algorithms → report accurate timings
4. Algorithm fails (e.g., stack overflow) → graceful error
5. Generate chart → save to file successfully

---

## Edge Cases to Test

Think about what could go wrong:

- **Empty data** — No students, no records, empty file
- **Invalid input** — Wrong type, out-of-range, negative numbers
- **Missing files** — Data file deleted, API unreachable
- **Bad format** — Corrupted CSV, invalid JSON
- **Boundary values** — First/last element, 0, very large numbers
- **Duplicates** — Same record twice, same ID twice
- **Performance** — Many records, large files, slow API

---

## Testing Checklist

For each scenario, answer:

- [ ] Did the app do what I expected?
- [ ] Did it show the right output?
- [ ] Did it save data correctly?
- [ ] Did it handle errors gracefully?
- [ ] Was performance acceptable?
- [ ] Would a user understand what happened?

---

## Example: Testing Student System End-to-End

```python
# Manual test script (save as test_end_to_end.py)

from system import StudentSystem
from student import Student

# Test 1: Add → Save → Load → Verify
print("Test 1: Add → Save → Load")
system1 = StudentSystem()
system1.add_student(Student("Alice", 100, 3.8))
system1.add_student(Student("Bob", 101, 3.5))
system1.save_to_json("test_data.json")

system2 = StudentSystem()
system2.load_from_json("test_data.json")
assert len(system2.students) == 2, "Should have 2 students"
assert system2.students[0].name == "Alice", "First student should be Alice"
print("✓ Test 1 passed")

# Test 2: Search
print("Test 2: Search")
results = system2.search_by_name("Alice")
assert len(results) == 1, "Should find 1 Alice"
print("✓ Test 2 passed")

# Test 3: Edge case - search for non-existent student
print("Test 3: Search non-existent")
results = system2.search_by_name("Charlie")
assert len(results) == 0, "Should find 0 Charlies"
print("✓ Test 3 passed")

print("\nAll tests passed!")
```

---

## Debugging Integration Issues

**Problem: Feature A works alone but breaks Feature B**
- Usually: Feature A modifies shared data (list, file) unexpectedly
- Solution: Check for side effects, use copies instead of references

**Problem: User scenario works once but fails second time**
- Usually: State not reset, old data persists, file not saved properly
- Solution: Verify load/save logic, check for hardcoded values

**Problem: Data gets corrupted during save**
- Usually: Invalid data in JSON/CSV format
- Solution: Validate data before saving, handle exceptions

---

## Reflection / Exit Ticket

1. Which user scenario found the most bugs?
2. What edge case surprised you?
3. Is your app ready for users? Why or why not?

---

## Progress Checklist

- [ ] 3–5 user scenarios tested end-to-end
- [ ] Edge cases identified and tested
- [ ] Bugs found and fixed
- [ ] Error handling improved
- [ ] Integration verified
- [ ] Code committed/saved
