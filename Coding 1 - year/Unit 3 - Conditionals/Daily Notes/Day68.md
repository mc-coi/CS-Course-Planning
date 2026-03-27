# Day 68: Review — Common Mistakes Workshop

**Learning Target:** I can identify and fix the most common conditional errors.

---

## Top 10 Conditional Mistakes

### Mistake 1: Using `=` instead of `==`

**WRONG:**
```python
if x = 5:
    print("x is 5")
# SyntaxError: invalid syntax
```

**CORRECT:**
```python
if x == 5:
    print("x is 5")
```

**Why:** `=` assigns (sets value), `==` compares
**Fix:** Always use `==` in conditions

---

### Mistake 2: Forgetting the Colon

**WRONG:**
```python
if x > 5
    print("Big")
# SyntaxError: expected ':'
```

**CORRECT:**
```python
if x > 5:
    print("Big")
```

**Why:** Python requires `:` after condition
**Fix:** Always end conditions with `:`

---

### Mistake 3: Wrong Indentation

**WRONG:**
```python
if x > 5:
print("Big")  # Not indented!
# IndentationError
```

**CORRECT:**
```python
if x > 5:
    print("Big")  # 4 spaces indented
```

**Why:** Python uses indentation to define blocks
**Fix:** Use exactly 4 spaces (not tabs)

---

### Mistake 4: Using `and` instead of `or`

**WRONG:**
```python
if day == "Saturday" and day == "Sunday":
    print("Weekend")
# day can't be two values simultaneously!
```

**CORRECT:**
```python
if day == "Saturday" or day == "Sunday":
    print("Weekend")
```

**Why:** `and` requires both; `or` requires at least one
**Fix:** Use `or` when checking multiple values

---

### Mistake 5: Missing `else` Path

**WRONG (logic error):**
```python
is_logged_in = False
if is_logged_in:
    show_profile()
# What if not logged in? Silent failure!
```

**CORRECT:**
```python
if is_logged_in:
    show_profile()
else:
    print("Please log in")
```

**Why:** Both paths need handling
**Fix:** Use else to handle False case

---

### Mistake 6: Off-by-One Errors

**WRONG:**
```python
score = 90
if score > 90:  # Should be >=
    print("A")
# 90 doesn't print A!
```

**CORRECT:**
```python
if score >= 90:
    print("A")
```

**Why:** Boundary conditions matter
**Fix:** Use `>=` or `<=` when boundary should be included

---

### Mistake 7: Wrong Order in elif

**WRONG (too general first):**
```python
score = 85
if score >= 70:  # This matches!
    print("Passing")
elif score >= 80:  # Never reaches here
    print("B")
# Prints "Passing" instead of "B"
```

**CORRECT:**
```python
if score >= 90:
    print("A")
elif score >= 80:  # More specific
    print("B")
elif score >= 70:  # Less specific
    print("C")
```

**Why:** First True match wins; check specific first
**Fix:** Order conditions from most to least specific

---

### Mistake 8: Condition Never True (Impossible Logic)

**WRONG:**
```python
x = 5
if x > 5 and x < 5:  # Impossible!
    print("Impossible")
# x can't be > 5 AND < 5 simultaneously
```

**CORRECT:**
```python
if x > 5 or x < 5:  # Possible
    print("x is not 5")
```

**Why:** Both conditions can't be true
**Fix:** Use `or` for alternatives

---

### Mistake 9: Comparing String to Number

**WRONG:**
```python
age = input("Age: ")
if age >= 18:  # Comparing string to number!
    print("Adult")
# TypeError or wrong comparison
```

**CORRECT:**
```python
age = int(input("Age: "))
if age >= 18:
    print("Adult")
```

**Why:** Types must match for comparison
**Fix:** Convert input with `int()`

---

### Mistake 10: Not Validating Input

**WRONG:**
```python
score = int(input("Score: "))
if score > 100:
    print("Too high")
# What if user enters -50? Not caught!
```

**CORRECT:**
```python
score = int(input("Score: "))
if 0 <= score <= 100:
    print("Valid")
elif score < 0:
    print("Score can't be negative")
elif score > 100:
    print("Score can't exceed 100")
```

**Why:** Invalid input crashes programs
**Fix:** Always validate before using input

---

## Practice: Fix These

### Error 1
```python
name = "Alice"
if name = "Bob":
    print("Found Bob")
```

**What's wrong?**
- Using `=` instead of `==`

**Fixed:**
```python
if name == "Bob":
```

---

### Error 2
```python
age = 17
if age >= 16 and age <= 18
    print("Teen")
```

**What's wrong?**
- Missing colon at end of condition

**Fixed:**
```python
if age >= 16 and age <= 18:
```

---

### Error 3
```python
x = 10
if x > 5:
print("Big")
```

**What's wrong?**
- print() not indented

**Fixed:**
```python
if x > 5:
    print("Big")
```

---

### Error 4
```python
day = "Monday"
if day == "Saturday" and day == "Sunday":
    print("Weekend")
```

**What's wrong?**
- day can't be two values; should be `or`

**Fixed:**
```python
if day == "Saturday" or day == "Sunday":
    print("Weekend")
```

---

### Error 5
```python
score = 85
if score >= 80:
    print("B or higher")
elif score >= 90:
    print("A")
```

**What's wrong?**
- 90 matches first condition; elif never runs
- Order: put more specific first

**Fixed:**
```python
if score >= 90:
    print("A")
elif score >= 80:
    print("B")
```

---

## Debug Checklist

When a program doesn't work:

- [ ] Does it have a syntax error? (Use error message)
- [ ] Does it have `=` instead of `==`?
- [ ] Are colons missing?
- [ ] Is indentation wrong?
- [ ] Are operators correct (and vs or)?
- [ ] Is condition order right?
- [ ] Is input validated?
- [ ] Do variable types match?

---

## Testing Strategy

**Before submitting, test:**

1. **Happy path:** Everything works right
2. **Edge cases:** Min/max values (0, 100, etc.)
3. **Invalid input:** Wrong type, out of range
4. **All branches:** Make sure each branch executes
5. **Variable changes:** Are variables updated correctly?

---

## Key Takeaway

Most errors fall into these 10 categories. Master these, and you'll avoid 90% of bugs!
