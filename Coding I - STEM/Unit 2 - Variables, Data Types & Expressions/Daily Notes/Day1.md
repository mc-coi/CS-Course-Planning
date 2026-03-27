# Day 1: Introduction to Variables & Assignment
**Learning Target:** I can declare variables and explain how assignment works.

### Key Concepts
The assignment operator `=` gives a variable a value. It does NOT mean equality (that's `==`, which you'll learn later). Variables can be reassigned—the old value is replaced.

**Compound assignment operators** let you update a variable using its current value:
- `x += 5` means `x = x + 5` (add 5 to x)
- `x -= 3` means `x = x - 3` (subtract 3)
- `x *= 2` means `x = x * 2` (multiply by 2)
- `x /= 4` means `x = x / 4` (divide by 4)
- `x //= 2` means `x = x // 2` (integer divide)

**Multiple assignment** lets you assign several variables at once: `a, b, c = 1, 2, 3`

### Code Examples
```python
# Basic assignment
score = 0
print(score)      # 0

# Reassignment
score = 100
print(score)      # 100

# Compound assignment
score += 10       # score = score + 10; now 110
print(score)      # 110

score -= 5        # score = score - 5; now 105
print(score)      # 105

score *= 2        # score = score * 2; now 210
print(score)      # 210

# Multiple assignment (same value)
a = b = c = 0
print(a, b, c)    # 0 0 0

# Multiple assignment (different values)
x, y, z = 1, 2, 3
print(x, y, z)    # 1 2 3

# Swapping variables
a = 5
b = 10
a, b = b, a       # Swap!
print(a, b)       # 10 5
```

### Guided Practice
Create a game score tracker. Start with a score of 0, then use compound assignment to add 10 points, subtract 3 points, multiply by 2, and divide by 2. Print the score after each operation.

### Practice Problems
**Problem 1 — Beginner:** Declare a variable, assign it a value, reassign it to a different value, then print it.

```python
# Starter code
name =

name =

print()
```

**Problem 2 — Intermediate:** Create a score variable starting at 50. Use all 5 compound assignment operators on it and print the score after each.

**Problem 3 — Challenge:** Swap the values of three variables using multiple assignment. Print before and after.

<details>
<summary>💡 Hints</summary>

- Problem 1: Simple—just choose any value and change it
- Problem 2: Start at 50, then +=, -=, *=, /=, //=
- Problem 3: You can do `x, y, z = y, z, x` to rotate values
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = "Alice"
print(name)       # Alice
name = "Bob"
print(name)       # Bob

# Problem 2 Example
score = 50
score += 10; print(score)     # 60
score -= 5; print(score)      # 55
score *= 2; print(score)      # 110
score /= 5; print(score)      # 22.0
score //= 2; print(score)     # 11.0
```
</details>

---