# Day 92: Review — Nested Loops, Break/Continue, and Lists

**Learning Target:** I can review nested loops, control flow, list creation and methods, and apply them in combination.

### Key Concepts Review

**Nested Loops:** Loop inside a loop. Inner completes all iterations per outer iteration.
```python
for i in range(3):
    for j in range(3):
        print(f"({i},{j})", end=" ")
    print()  # Newline after each outer iteration
```

**Break and Continue:**
- **break:** Exit loop immediately
- **continue:** Skip to next iteration

**Lists:** Ordered collections, indexed from 0.
```python
numbers = [1, 2, 3, 4, 5]
print(numbers[0])     # 1
print(numbers[-1])    # 5
print(len(numbers))   # 5
```

**List Methods:**
- `.append(value)` — Add to end
- `.remove(value)` — Remove first occurrence
- `.sort()` — Sort ascending
- `.reverse()` — Reverse order
- `.index(value)` — Find position
- `.count(value)` — Count occurrences

**For-Each Loops:** Iterate directly over list elements.
```python
for item in list:
    print(item)
```

---

### Practice Problems

**Problem 1 — Beginner:** Write nested loops to print a 3×3 grid of asterisks.

**Problem 2 — Intermediate:** Create a list, append 5 numbers to it, sort it, then print each with a break statement when you find a specific value.

**Problem 3 — Challenge:** Write nested loops to create a 5×5 multiplication table, using break/continue strategically if needed.

<details>
<summary>✅ Solutions</summary>

```python
# Problem 1
for i in range(3):
    for j in range(3):
        print("*", end=" ")
    print()

# Problem 2
numbers = []
for i in range(5):
    num = int(input(f"Number {i+1}: "))
    numbers.append(num)
numbers.sort()

target = int(input("Find: "))
for num in numbers:
    if num == target:
        print(f"Found {target}")
        break
    print(num)

# Problem 3
for i in range(1, 6):
    for j in range(1, 6):
        print(f"{i*j:3}", end=" ")
    print()
```

</details>

---

### Self-Assessment

Check your understanding:
- [ ] Can you trace nested loops mentally?
- [ ] Do you understand outer × inner iterations?
- [ ] Can you use break to exit a loop?
- [ ] Can you use continue to skip iterations?
- [ ] Can you create a list from user input?
- [ ] Can you iterate over a list with for-each?
- [ ] Can you use list methods (.append(), .sort(), etc.)?
- [ ] Can you find min/max in a list?

---

### Nested Loop Tracing Tip

When unsure what a nested loop does:
1. Trace the first few iterations by hand
2. Count total iterations (outer × inner)
3. Identify what changes each iteration
4. Draw a grid or table to visualize

---
