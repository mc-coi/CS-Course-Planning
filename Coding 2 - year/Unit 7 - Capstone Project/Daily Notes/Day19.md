# Day 19: Sprint 3 – Final Testing & Debugging

**Session Goal:** Complete debugging. Resolve remaining issues. Finalize code.

---

## Today's Focus

This is your last day for bug fixes. By end of day, your code should be stable and production-ready. Tomorrow you'll focus on documentation, and Days 23–24 are presentations. Today: make it solid.

---

## Work Session Agenda

**Minutes 0-5:** **Final Standup**
- Review bugs from Day 18
- Triage: what MUST be fixed? What can you live with?
- Timeline: need to finalize code by end of today

**Minutes 5-50:** **Focused Bug Resolution**
- Finish fixing critical bugs from Day 18
- Re-test to verify fixes work and don't break other features
- Don't introduce new features; focus on stability
- If you find new bugs, add to backlog but prioritize finishing existing ones
- Call teacher over for tricky bugs—don't spend >15 min stuck

**Minutes 50-55:** **Code Finalization**
- Ensure all code is saved and committed
- Verify: app runs without errors, all features work
- Mark code as "ready for documentation"

---

## Final Stability Checklist

Before moving to Day 20:

- [ ] App starts without errors
- [ ] All core features work
- [ ] No crashes on normal usage
- [ ] Error messages are helpful
- [ ] Data saves and loads correctly
- [ ] Edge cases handled
- [ ] Code is clean (no debug prints, dead code)
- [ ] Comments and docstrings in place
- [ ] Code committed with clear messages

---

## Quick Wins for Stability

If time is short, focus on these high-impact improvements:

**Add graceful exit:**
```python
def main():
    system = StudentSystem()
    try:
        while True:
            # ... main loop ...
            pass
    except KeyboardInterrupt:
        print("\nGoodbye!")
        system.save_to_json("data/students.json")  # Save before exiting
```

**Improve error messages:**
```python
# BEFORE: cryptic
except FileNotFoundError as e:
    print(e)

# AFTER: helpful
except FileNotFoundError:
    print(f"Error: Could not find data file at {filename}")
    print("Please ensure the file exists, or start fresh with an empty list.")
```

**Add progress indicators:**
```python
print("Loading data...", end="", flush=True)
data = load_from_json("data.json")
print(" Done!")

print("Processing...", end="", flush=True)
results = process_data(data)
print(f" Complete! Found {len(results)} results.")
```

---

## Testing One More Time

Run through these scenarios:

1. **Fresh start** — Delete all data files, run app from scratch
2. **Normal workflow** — Full realistic usage (add → search → save → load)
3. **Recovery** — Delete data file, app should start fresh and still work
4. **Bad input** — Try to break it (wrong type, empty input, huge numbers)
5. **Stress test** — Add 100+ records, sort, search, verify performance

```python
# Comprehensive final test script:

def final_test():
    """Run comprehensive tests before presentation."""

    # Test 1: Fresh start
    print("Test 1: Fresh start...")
    system = StudentSystem()
    assert len(system.students) == 0
    print("✓ Passed")

    # Test 2: Add and save
    print("Test 2: Add and save...")
    system.add_student(Student("Alice", 100, 3.8))
    system.save_to_json("test_data.json")
    print("✓ Passed")

    # Test 3: Load
    print("Test 3: Load...")
    system2 = StudentSystem()
    system2.load_from_json("test_data.json")
    assert len(system2.students) == 1
    print("✓ Passed")

    # Test 4: Search
    print("Test 4: Search...")
    results = system2.search_by_name("Alice")
    assert len(results) == 1
    print("✓ Passed")

    # Test 5: Edge cases
    print("Test 5: Edge cases...")
    try:
        system.add_student(Student("Bob", -1, 5.0))
        assert False, "Should reject invalid data"
    except ValueError:
        print("✓ Passed")

    print("\n✓ All tests passed! Ready for presentation.")

if __name__ == "__main__":
    final_test()
```

---

## Known Issues Documentation

If you have unfixed bugs, document them:

```markdown
## Known Issues

### Issue 1: Slow search on large datasets
- When searching 10,000+ students, search takes 5+ seconds
- Cause: Linear search instead of indexed lookup
- Workaround: Works fine for normal classroom use (100–500 students)
- Future fix: Implement indexed lookup or database

### Issue 2: API rate limiting
- If you make >100 requests in an hour, API returns 429 error
- Cause: Free API tier has rate limits
- Workaround: Cache results between requests
- Future fix: Implement exponential backoff retry logic
```

This is honest and shows you understand the trade-offs.

---

## Reflection / Exit Ticket

1. Did you fix all critical bugs?
2. Are there any remaining issues? Are they acceptable?
3. How confident are you about your code now?

---

## Progress Checklist

- [ ] All critical bugs fixed
- [ ] Code tested end-to-end multiple times
- [ ] Edge cases handled gracefully
- [ ] No crashes on normal usage
- [ ] Error messages are clear
- [ ] Code finalized and committed
- [ ] Ready for documentation on Day 20
