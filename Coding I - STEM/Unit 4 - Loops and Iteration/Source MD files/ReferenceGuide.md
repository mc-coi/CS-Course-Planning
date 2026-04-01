# Vocabulary & Quick Reference

**Key Terms:**
- **Loop:** Repeated code execution
- **Iteration:** One execution of loop body
- **Loop control variable:** Variable that changes each iteration
- **Sentinel value:** Special input that stops loop
- **Nested loop:** Loop inside another loop
- **Accumulator:** Variable updated in loop to accumulate result
- **for/else:** else block runs if loop completes without break

**Syntax:**
```python
# while loop
while condition:
    # code
    # update condition

# for loop
for variable in range(start, stop, step):
    # code

# for with string
for char in "hello":
    # code

# Loop control
break      # exit immediately
continue   # skip to next iteration

# for/else
for i in range(10):
    if i == 5:
        break
else:
    print("No break!")  # won't print (break happened)
```

**range() Quick Reference:**
- `range(5)` → 0,1,2,3,4
- `range(1,6)` → 1,2,3,4,5
- `range(0,10,2)` → 0,2,4,6,8
- `range(10,0,-1)` → 10,9,8,...,1

## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Infinite loop (while True without break) | Program never stops | Add break or make condition eventually False |
| Forgetting loop update: `while x > 0: print(x)` | Infinite loop | Add `x -= 1` or similar |
| Off-by-one in range: `range(10)` when need 1-10 | Prints 0-9 instead of 1-10 | Use `range(1, 11)` |
| Wrong indentation in nested loop | Inner loop doesn't nest properly | Check spacing matches nesting level |
| Using = instead of == in loop condition | SyntaxError | Use `==` for comparison |
| Accumulator starts at wrong value | Wrong result | Initialize at 0 for sum, 1 for product, "" for string |
| Not importing `random` before `random.randint()` | NameError | Add `import random` at top |
| String concatenation slow in loop | Performance issue | OK for small loops, but consider for large |

---
