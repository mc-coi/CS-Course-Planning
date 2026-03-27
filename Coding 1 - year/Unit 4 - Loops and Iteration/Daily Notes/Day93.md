# Day 93: Review — Code Tracing and Debugging Loops

**Learning Target:** I can trace loop code step-by-step, identify bugs, and debug loop logic.

### Key Concepts Review

**Code Tracing:** Follow code line-by-line, tracking variables.
- Write down variable values after each line
- Identify when conditions change
- Predict output before running

**Common Loop Bugs:**
1. Infinite loops (condition never becomes false)
2. Off-by-one errors (loop one too many or too few times)
3. Wrong condition (< vs <=, == vs !=)
4. Loop variable not updated (counter forgotten)
5. Break/continue misused (outside loop, wrong condition)

**Debugging Strategy:**
1. Read the error message—it tells you the problem
2. Check indentation (must be consistent)
3. Verify loop condition (will it ever be false?)
4. Trace first few iterations by hand
5. Add print statements to see variable values
6. Test with simple input first, then complex

---

### Practice: Trace and Predict

**Code 1: What does this print?**
```python
for i in range(1, 4):
    for j in range(2):
        print(i, j, end=" ")
    print()
```

Expected output:
```
1 0 1 1
2 0 2 1
3 0 3 1
```

---

**Code 2: What does this print?**
```python
numbers = [3, 1, 4, 1, 5]
max_val = numbers[0]
for num in numbers:
    if num > max_val:
        max_val = num
print(max_val)
```

Expected output: `5`

---

**Code 3: Find the bug.**
```python
total = 0
for i in range(5):
    num = int(input("Number: "))
    total += num
    i += 1  # BUG! This doesn't affect range
print(total)
```

**Bug:** `i += 1` inside a for loop doesn't change the loop count. The loop runs 5 times regardless. (This line is unnecessary.)

---

**Code 4: Find the bug.**
```python
while count < 5:
    print(count)
```

**Bug:** `count` is never initialized, so the code crashes with NameError. Fix: `count = 0` before the loop.

---

**Code 5: Find the bug.**
```python
while True:
    num = int(input("Positive: "))
    if num > 0
        break
    print("Invalid")
```

**Bug:** Missing colon after `if num > 0`. Should be `if num > 0:`.

---

### Practice Problems

**Problem 1 — Beginner:** Trace this code and write what it prints.
```python
for i in range(1, 4):
    print(i * 2)
```

**Problem 2 — Intermediate:** Find the bug(s) and fix them.
```python
total = 0
while x < 10:
    total += x
    x += 1
print(total)
```

**Problem 3 — Challenge:** Trace this nested loop and predict the output.
```python
for i in range(2):
    for j in range(3):
        if j == 1:
            continue
        print(f"{i},{j}", end=" ")
    print()
```

<details>
<summary>✅ Solutions</summary>

```
# Problem 1 Output:
2
4
6

# Problem 2 Fixed Code:
x = 0  # Initialize x
total = 0
while x < 10:
    total += x
    x += 1
print(total)  # Prints 45

# Problem 3 Output:
0,0 0,2
1,0 1,2
```

</details>

---

### Debugging Checklist

Before submitting code:
- [ ] Does it run without crashing?
- [ ] Does it produce expected output for normal input?
- [ ] Have you tested edge cases (empty, single item, very large)?
- [ ] Are all variables initialized before use?
- [ ] Does the loop condition eventually become false (no infinite loops)?
- [ ] Are colons present after loops and if statements?
- [ ] Is indentation correct?
- [ ] Did you test with different inputs?

---

### Tips for Success on Tomorrow's Assessment

1. **Read questions carefully.** Make sure you understand what's being asked.
2. **Trace before coding.** For code analysis questions, trace the code first.
3. **Show your work.** For code writing, include comments explaining your logic.
4. **Test your code.** If possible, run it with sample inputs.
5. **Check for common errors.** Indentation, colons, initialization, loop conditions.

---
