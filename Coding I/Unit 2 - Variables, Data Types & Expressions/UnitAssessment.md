# Unit Assessment Prep

**Review Questions:**

1. What is the difference between `=` and `==`?
2. Explain compound assignment: what does `x += 10` do?
3. What does `/` division return vs `//` floor division?
4. Demonstrate indexing and slicing on the string "Python".
5. List and explain 5 string methods.
6. What is the difference between `"5"` and `5`?
7. How do you convert a string to a number in Python?
8. Write an f-string that prints a number with 2 decimal places.
9. How do you import the math module and use `math.sqrt()`?
10. What is a constant and why use ALL_CAPS?

**Answers:**
1. `=` assigns; `==` compares for equality
2. `x += 10` means `x = x + 10` (add 10 to x)
3. `/` always returns float (3.0); `//` returns integer (3)
4. `"Python"[0]` = "P", `"Python"[-1]` = "n", `"Python"[1:4]` = "yth"
5. `.upper()`, `.lower()`, `.strip()`, `.replace()`, `.split()` (or others)
6. `"5"` is text (string); `5` is a number (integer)
7. `int("5")` or `float("3.14")`
8. `f"{price:.2f}"`
9. `import math` at top; then `math.sqrt(16)` returns `4.0`
10. Constants are values that shouldn't change; ALL_CAPS makes this clear: `MAX_ATTEMPTS = 3`

---