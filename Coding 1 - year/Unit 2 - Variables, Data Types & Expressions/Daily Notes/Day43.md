# Day 43: Review — Common Mistakes Workshop

**Learning Target:** I can identify, understand, and avoid common mistakes from Unit 2.

### Mistake Categories & Solutions

### 1. ASSIGNMENT vs. COMPARISON

**❌ Mistake:**
```python
if x = 5:
    print("x is 5")
```

**✅ Fix:**
```python
if x == 5:
    print("x is 5")
```

**Why:** `=` assigns a value; `==` compares. Using `=` in an `if` statement causes a SyntaxError.

---

### 2. DIVISION RETURNS FLOAT

**❌ Mistake:**
```python
result = 10 / 2
print(type(result))  # Expects <class 'int'>
print(result == 5)   # Expects True, but result is 5.0
```

**✅ Fix:**
```python
result = 10 // 2  # Use // for integer division
print(type(result))  # <class 'int'>
print(result == 5)   # True
```

**Why:** In Python 3, `/` always returns a float. Use `//` for integer division.

---

### 3. STRING INDEXING STARTS AT 0

**❌ Mistake:**
```python
word = "Hello"
print(word[1])  # Expects "H", gets "e"
```

**✅ Fix:**
```python
word = "Hello"
print(word[0])  # "H" (first character)
print(word[1])  # "e" (second character)
```

**Why:** Indexing is zero-based. Index 0 is the first character.

---

### 4. SLICE STOP IS EXCLUSIVE

**❌ Mistake:**
```python
word = "Hello"
print(word[0:4])  # Expects "Hello" (5 characters)
```

**✅ Fix:**
```python
word = "Hello"
print(word[0:5])  # "Hello" (includes indices 0,1,2,3,4)
# OR
print(word[:])    # "Hello" (whole string)
```

**Why:** The stop index is NOT included. `[0:4]` gives indices 0, 1, 2, 3 (not 4).

---

### 5. CAN'T MODIFY STRINGS WITH INDEXING

**❌ Mistake:**
```python
word = "Hello"
word[0] = "J"  # TypeError: 'str' object does not support item assignment
```

**✅ Fix:**
```python
word = "Hello"
word = "J" + word[1:]  # "Jello"
# OR
word = word.replace("H", "J")  # "Jello"
```

**Why:** Strings are immutable. You can't change individual characters. Reassign the whole string instead.

---

### 6. TYPE MISMATCH IN CONCATENATION

**❌ Mistake:**
```python
score = 100
print("Score: " + score)  # TypeError: can only concatenate str (not "int") to str
```

**✅ Fix:**
```python
score = 100
print("Score: " + str(score))  # "Score: 100"
# OR
print(f"Score: {score}")  # "Score: 100" (better!)
```

**Why:** You can only concatenate strings with strings. Convert numbers to strings with `str()` or use f-strings.

---

### 7. FORGETTING .strip() ON input()

**❌ Mistake:**
```python
name = input("Name: ")
if name == "Alice":
    print("Hi Alice!")
# User types "Alice " (with trailing space) → condition fails
```

**✅ Fix:**
```python
name = input("Name: ").strip()
if name == "Alice":
    print("Hi Alice!")  # Works even if user adds spaces
```

**Why:** `input()` includes any trailing whitespace. Use `.strip()` to remove it.

---

### 8. FLOAT PRECISION ISSUES

**❌ Mistake:**
```python
if 0.1 + 0.2 == 0.3:
    print("True")
else:
    print("False")  # Actually prints "False"!
```

**✅ Fix:**
```python
result = round(0.1 + 0.2, 1)
if result == 0.3:
    print("True")
# OR for money: round to 2 decimals
```

**Why:** Computers can't represent all decimals perfectly. Round when comparing floats.

---

### 9. CONFUSING NEGATIVE INDICES

**❌ Mistake:**
```python
word = "Python"
print(word[-1])  # Expects index -1 to be the first character
# Gets "n" instead of "P"
```

**✅ Fix:**
```python
word = "Python"
print(word[-1])   # "n" (last character)
print(word[-2])   # "o" (second-to-last)
print(word[0])    # "P" (first character)
```

**Why:** Negative indices count from the END. -1 is the last character, -2 is second-to-last.

---

### 10. OPERATOR PRECEDENCE CONFUSION

**❌ Mistake:**
```python
result = 10 + 2 * 3
print(result)  # Expects 36, gets 16
```

**✅ Fix:**
```python
result = 10 + 2 * 3
print(result)  # 16 (multiply before add; PEMDAS)
# Use parentheses if you want addition first:
result = (10 + 2) * 3
print(result)  # 36
```

**Why:** PEMDAS: Parentheses, Exponents, Mult/Div (left-to-right), Add/Sub (left-to-right).

---

### 11. BOOLEAN CAPITALIZATION

**❌ Mistake:**
```python
x = true  # NameError: name 'true' is not defined
```

**✅ Fix:**
```python
x = True  # Correct capitalization
y = False
```

**Why:** Python uses `True` and `False` (capitalized), not `true` and `false`.

---

### 12. FORGETTING IMPORT

**❌ Mistake:**
```python
import math
radius = 5
# Later in code...
area = pi * radius ** 2  # NameError: name 'pi' is not defined
```

**✅ Fix:**
```python
import math
radius = 5
area = math.pi * radius ** 2  # Use math.pi
# OR
from math import pi
area = pi * radius ** 2
```

**Why:** You must use the module name or import the specific item.

---

### Interactive Mistake-Finding Exercise

**Code Snippet 1:**
```python
age = input("Age: ")
next_year = age + 1
print(next_year)
```

**Questions:**
- What's the error?
- How would you fix it?

<details>
<summary>Answer</summary>
Error: `input()` returns a string, can't add int to string. Fix: `age = int(input("Age: "))`
</details>

**Code Snippet 2:**
```python
word = "Programming"
print(word[12])
```

**Questions:**
- What's the error?
- What would `print(word[-1])` print?

<details>
<summary>Answer</summary>
Error: Index 12 is out of range (word only has 11 characters, indices 0-10).
`word[-1]` prints "g" (last character).
</details>

**Code Snippet 3:**
```python
price = 9.99
tax = 0.08
total = price * (1 + tax)
print(f"Total: ${total:.2f}")
```

**Questions:**
- Is this correct?
- What does it print?

<details>
<summary>Answer</summary>
Yes, this is correct! Prints "Total: $10.79"
</details>

### Reflection Questions

1. **Which mistake have you made the most?** (Be honest!)
2. **Why do you think you made it?**
3. **How will you remember not to make it again?**
4. **What's the most common mistake you see classmates make?**

### Practice: Fix These Programs

**Program 1:**
```python
x = input("Number: ")
y = 10
print(x + y)
```

**Program 2:**
```python
text = "hello world"
print(text.upper)
```

**Program 3:**
```python
if score = 100:
    print("Perfect!")
```

**Program 4:**
```python
total = 10.1 + 0.2
if total == 10.3:
    print("Equal")
```

<details>
<summary>✅ Fixes</summary>

Program 1:
```python
x = int(input("Number: "))
y = 10
print(x + y)
```

Program 2:
```python
text = "hello world"
print(text.upper())  # Need parentheses!
```

Program 3:
```python
if score == 100:  # Use == not =
    print("Perfect!")
```

Program 4:
```python
total = round(10.1 + 0.2, 1)
if total == 10.3:
    print("Equal")
```

</details>

---

**By recognizing these patterns, you'll write better, bug-free code. Good luck on the assessment!**

