# Day 2: Development Session 1 — Build the Foundation

### Key Concepts

**Bottom-Up Development:** Start with the helper functions (the smallest, most isolated pieces) and build upward to `main()`.

**Why bottom-up?**
- Each piece is easy to test in isolation
- Bugs are easier to find when the scope is small
- You build confidence as each piece works

**Development order:**
1. Write and test the simplest function first
2. Test it immediately (don't wait!)
3. Add the next layer
4. Integrate gradually

### Development Session Strategy

**Hour breakdown for today:**
- 10 min: Review your project spec and plan
- 5 min: Identify which function to build first (the most basic, no dependencies)
- 30 min: Write 2–3 foundational functions
- 10 min: Test each function individually
- 5 min: Note what's left, plan tomorrow

### Unit Testing Your Functions

Before connecting everything, test each function alone:

```python
# ── Testing functions in isolation ─────────────────────────

def calculate_average(scores):
    """Return the mean of a list of scores."""
    if not scores:
        return 0.0
    return sum(scores) / len(scores)

def letter_grade(average):
    """Convert average to letter grade."""
    if average >= 90: return "A"
    if average >= 80: return "B"
    if average >= 70: return "C"
    if average >= 60: return "D"
    return "F"

# ── Test each function BEFORE connecting them ──────────────
print("Testing calculate_average:")
print(calculate_average([90, 85, 92]))   # Expected: 89.0
print(calculate_average([70, 70, 70]))   # Expected: 70.0
print(calculate_average([]))             # Expected: 0.0

print("\nTesting letter_grade:")
print(letter_grade(95))   # Expected: A
print(letter_grade(83))   # Expected: B
print(letter_grade(55))   # Expected: F

# ── Add a simple test runner ───────────────────────────────
def test_calculate_average():
    assert calculate_average([100, 90, 80]) == 90.0, "Test 1 failed"
    assert calculate_average([70, 70]) == 70.0, "Test 2 failed"
    assert calculate_average([]) == 0.0, "Test 3 failed"
    print("calculate_average: All tests passed ✓")

test_calculate_average()
```

### Common Development Pitfalls

| Pitfall | How to Avoid |
|---------|-------------|
| Writing everything at once | Write one function at a time |
| Never testing until the end | Test after every function |
| No error handling | Add `try/except` from the start |
| Unclear function names | Name says what it does: `get_user_age()` |
| Forgetting edge cases | Always test: empty input, 0, very large numbers |
| Copy-pasting code | Extract repeated code into a function |

---