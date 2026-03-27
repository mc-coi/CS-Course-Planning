# Day 18: Sprint 3 – Comprehensive Testing

**Session Goal:** Test your entire application systematically. Find and fix remaining bugs.

---

## Today's Focus

Today is bug-hunting day. You'll run through your app with fresh eyes, document what you find, and fix it. The goal: a stable, reliable application ready for presentation.

---

## Work Session Agenda

**Minutes 0-5:** **Testing Strategy**
- Teacher: what is comprehensive testing? (every feature, every scenario, every path)
- Remind: test-driven fixes (find bug, write minimal fix, verify, move on)
- Time management: prioritize critical bugs over nice-to-haves

**Minutes 5-50:** **Systematic Testing & Bug Fixing**
- Follow your **Test Plan** (see below)
- Document bugs on a **Bug Tracker** (see below)
- For each bug: reproduce it, understand it, fix it, verify it's fixed
- Don't get stuck: if a bug takes >20 min, note it and ask teacher
- Test after each fix to ensure you didn't break something else

**Minutes 50-55:** **Wrap-up**
- Prioritize remaining bugs (critical vs. minor)
- Commit fixes with clear messages: "Fix: handle missing file gracefully"
- Plan Day 19 focus

---

## Test Plan Template

Create a test plan for your app:

```
TEST PLAN: Student Information System

FEATURE 1: Add Student
- Normal: Add student with valid data → verify in list
- Edge: Add student with GPA = 0.0 → should work
- Edge: Add student with GPA = 4.0 → should work
- Error: Add student with GPA = 5.0 → reject with error
- Error: Add student with empty name → reject with error

FEATURE 2: Save to JSON
- Normal: Add student, save, reload → data persists
- Error: No write permission → show error
- Edge: Save empty system → creates valid empty JSON

FEATURE 3: Load from JSON
- Normal: Load valid file → students appear
- Error: File doesn't exist → start with empty list
- Error: File is corrupted → show error and start fresh
- Edge: Load file with 1000+ students → should work

FEATURE 4: Search by Name
- Normal: Search for "Alice" → find Alice
- Case: Search for "alice" → find Alice (case-insensitive)
- Partial: Search for "Al" → find "Alice", "Allan"
- Empty: Search for "Zebra" when not present → return empty list
- Edge: Search for "" (empty string) → return all or error

...
```

---

## Bug Tracker

Create a simple file to track bugs:

```
BUG #1: Crash when loading corrupted JSON
Status: OPEN
Priority: HIGH (app crashes)
Steps to reproduce:
  1. Create file with invalid JSON: data/test.json = "{invalid"
  2. Run app and select "Load from file"
  3. Choose test.json
Result: App crashes with JSONDecodeError
Expected: Show error message and continue
Fix: Add try/except around json.load()

BUG #2: Slow performance with large file
Status: OPEN
Priority: MEDIUM (works but slow)
Steps to reproduce:
  1. Create JSON file with 10,000 students
  2. Load file
  3. Search for a student
Result: Takes 5+ seconds
Expected: Results in <1 second
Investigation: Probably O(n) search instead of indexed

BUG #3: Can add student with negative GPA
Status: OPEN
Priority: LOW (app works but allows bad data)
...
```

---

## Testing Checklist by Project

**Data Analyzer:**
- [ ] Load CSV file successfully
- [ ] Handle missing/corrupted CSV files
- [ ] Compute all statistics correctly
- [ ] Generate all chart types
- [ ] Export results successfully
- [ ] Search/filter works on all fields
- [ ] App doesn't crash on empty dataset
- [ ] Performance acceptable for large files

**API App:**
- [ ] Fetch data from API successfully
- [ ] Parse JSON correctly
- [ ] Handle API errors (down, rate limit, auth)
- [ ] Cache works when API is down
- [ ] User preferences save and load
- [ ] App doesn't crash on invalid API response
- [ ] Handles network timeouts gracefully
- [ ] Display formatted results clearly

**Student System:**
- [ ] Add, remove, search, sort all work
- [ ] Save to JSON preserves all data
- [ ] Load from JSON reconstructs correct data
- [ ] Handle duplicate IDs
- [ ] Validate GPA range (0–4.0)
- [ ] Validate empty name
- [ ] Search is case-insensitive
- [ ] Sort stable and correct
- [ ] No crashes on edge cases

**Algorithm Visualizer:**
- [ ] Each sorting algorithm produces correct result
- [ ] Benchmarking times are accurate
- [ ] Chart generation works
- [ ] Compare algorithms shows meaningful differences
- [ ] Handle small arrays (1 element)
- [ ] Handle large arrays (10,000+ elements)
- [ ] No stack overflow or memory errors
- [ ] Visualization displays clearly

---

## Bug Fixing Process

For each bug:

1. **Reproduce** — Verify you can make it happen consistently
2. **Understand** — Why does it happen? What's the root cause?
3. **Fix** — Write minimal code to fix it
4. **Verify** — Does the bug go away? Did anything else break?
5. **Commit** — Save with clear message: "Fix: [bug description]"

Example:
```
Bug: Can add student with negative GPA

Reproduce:
  system.add_student(Student("Alice", 100, -1.5))
  # Should fail but doesn't

Root cause:
  No validation in Student.__init__ or system.add_student()

Fix:
  def __init__(self, name, student_id, gpa):
      if not 0 <= gpa <= 4.0:
          raise ValueError("GPA must be 0-4.0")
      self.gpa = gpa

Verify:
  try:
      Student("Alice", 100, -1.5)
  except ValueError:
      print("✓ Correctly rejected negative GPA")

Commit:
  git add student.py
  git commit -m "Fix: validate GPA range in Student.__init__"
```

---

## Reflection / Exit Ticket

1. What was the most critical bug you found?
2. How did you fix it?
3. Are there any bugs you couldn't fix? Why?

---

## Progress Checklist

- [ ] Test plan created and reviewed
- [ ] All features tested systematically
- [ ] Critical bugs found and fixed
- [ ] Medium-priority bugs found and fixed
- [ ] App tested end-to-end multiple times
- [ ] No crashes on normal usage
- [ ] Code committed/saved
