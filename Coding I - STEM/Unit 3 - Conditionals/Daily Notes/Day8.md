# Day 8: Review & Debugging
**Learning Target:** I can debug logic errors in conditional statements.

### Key Concepts
Common logic errors in conditionals:
- **Using = instead of ==:** `if x = 5:` (should be `if x == 5:`)
- **Off-by-one errors:** Using > instead of >=, or vice versa
- **Wrong operator:** Using and instead of or, or vice versa
- **Missing else:** Forgetting that you need to handle False condition
- **Fall-through:** elif not stopping execution

### Code Examples
```python
# WRONG: using = instead of ==
# if score = 90:
#     print("A")

# CORRECT
if score == 90:
    print("A")

# WRONG: >= vs >
# if score > 90:
#     print("A")  # 90 doesn't print!

# CORRECT (if 90 should be A)
if score >= 90:
    print("A")

# WRONG: not stopping at right place
if grade == "A":
    print("Excellent")
elif grade == "B":
    print("Good")
# Falls through and also prints "Done"
print("Done")  # Always runs—that's correct!

# WRONG: and instead of or
# if day == "Sat" and day == "Sun":  # NEVER true!
#     print("Weekend")

# CORRECT
if day == "Sat" or day == "Sun":
    print("Weekend")
```

### Guided Practice
Debug three faulty programs with conditional errors.

### Practice Problems
**Problem 1 — Beginner:** Fix: `if age = 18: print("Adult")`

**Problem 2 — Intermediate:** Fix: grade check that should print "A" for 90+, but doesn't work correctly.

**Problem 3 — Challenge:** Trace through complex nested conditions and identify what will print.

---