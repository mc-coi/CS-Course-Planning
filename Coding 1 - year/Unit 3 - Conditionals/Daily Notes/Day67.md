# Day 67: Review — Code Tracing & Execution Flow

**Learning Target:** I can trace through conditional code and predict exact output without running it.

---

## Code Tracing Overview

**Code tracing** means following program execution step-by-step:
1. Read first line
2. Execute it
3. Move to next line
4. Repeat until end

**For conditionals:**
- Evaluate condition
- Execute correct branch
- Skip all other branches

---

## Tracing Examples

### Example 1: Simple if

```python
x = 5
if x > 3:
    print("Big")
print("Done")
```

**Trace:**
1. Line 1: Set x to 5
2. Line 2: Check if 5 > 3? **YES, True**
3. Line 3: Print "Big"
4. Line 5: Print "Done"

**Output:**
```
Big
Done
```

### Example 2: if/else

```python
score = 85
if score >= 90:
    print("A")
else:
    print("Not A")
print("Finished")
```

**Trace:**
1. Line 1: Set score to 85
2. Line 2: Check if 85 >= 90? **NO, False**
3. Skip lines 3 (skip if block)
4. Line 5: Execute else block, print "Not A"
5. Line 6: Print "Finished"

**Output:**
```
Not A
Finished
```

### Example 3: if/elif/else

```python
age = 15
if age < 13:
    print("Child")
elif age < 18:
    print("Teen")
else:
    print("Adult")
```

**Trace:**
1. Line 1: Set age to 15
2. Line 2: Is 15 < 13? NO, False → skip
3. Line 4: Is 15 < 18? YES, True → execute!
4. Line 5: Print "Teen"
5. Skip else block (already matched)

**Output:**
```
Teen
```

### Example 4: Nested Conditionals

```python
has_key = True
if has_key:
    print("You have key")
    locked = False
    if locked:
        print("Unlock door")
    else:
        print("Enter")
```

**Trace:**
1. Set has_key to True, locked to False
2. Is has_key True? YES
3. Print "You have key"
4. Is locked True? NO, False
5. Skip print "Unlock door"
6. Print "Enter"

**Output:**
```
You have key
Enter
```

### Example 5: Logical Operators

```python
x = 5
y = 10
if x > 0 and y > 5:
    print("Both true")
else:
    print("Not both true")
```

**Trace:**
1. Set x=5, y=10
2. Evaluate: Is x > 0? YES (True)
3. AND: Check second: Is y > 5? YES (True)
4. True and True = True
5. Print "Both true"

**Output:**
```
Both true
```

### Example 6: Complex Expression

```python
score = 75
if 70 <= score < 80:
    print("C")
elif 80 <= score < 90:
    print("B")
else:
    print("A or F")
```

**Trace:**
1. Set score to 75
2. Is 70 <= 75 < 80? YES, True
3. Print "C"
4. Skip elif and else

**Output:**
```
C
```

---

## Practice: Trace These Programs

### Problem 1 — Beginner
```python
num = 10
if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

What prints? (Hint: 10 % 2 = 0)
- **Answer:** Even

### Problem 2 — Intermediate
```python
x = 5
y = 10
if x > y:
    print("X bigger")
elif x == y:
    print("Equal")
else:
    print("Y bigger")
```

What prints?
- **Answer:** Y bigger

### Problem 3 — Intermediate
```python
name = "alice"
if name == "Alice":
    print("Found Alice")
else:
    print("Not Alice")
```

What prints? (Hint: case matters!)
- **Answer:** Not Alice

### Problem 4 — Intermediate
```python
age = 20
if age >= 18:
    print("Adult")
    if age >= 65:
        print("Senior")
else:
    print("Minor")
```

What prints?
- **Answer:** Adult (65 check is not printed)

### Problem 5 — Challenge
```python
score = 85
if score > 90:
    print("A")
elif score > 80:
    print("B")
elif score > 70:
    print("C")
else:
    print("F")
```

What prints?
- **Answer:** B

### Problem 6 — Challenge
```python
x = 5
y = 10
z = 3
if x > y and y > z:
    print("1")
elif x > z or y > x:
    print("2")
else:
    print("3")
```

What prints? (Trace step-by-step)
- x > y: 5 > 10? NO
- x > z or y > x: (5 > 3) or (10 > 5) = True or True = True
- **Answer:** 2

---

## Tracing Strategy

**5-Step Tracing Process:**

1. **Set up:** Write current values of all variables
2. **Evaluate condition:** Write out each part
3. **Determine True/False:** State the result
4. **Execute branch:** Write what code runs
5. **Next statement:** Move to next non-skipped line

---

## Common Tracing Mistakes

**Mistake 1:** Skipping evaluation steps
- Write out: Is 5 > 3? YES
- Don't just assume

**Mistake 2:** Executing wrong branch
- If condition is False, skip if block, check elif
- Don't execute both

**Mistake 3:** Forgetting that elif stops checking
- Once elif is True, skip remaining elifs
- Don't check them all

**Mistake 4:** Forgetting variable changes
- If x = 10 in if block, x is now 10
- Remember updated values

**Mistake 5:** Incorrect operator precedence
- Evaluate from left to right (usually)
- Remember: and before or

---

## Challenge: Trace This

```python
items = 5
price = 10

if items > 0 and price < 15:
    total = items * price
    if total > 30:
        print(f"Total: {total}")
        if total < 75:
            print("Under budget")
    else:
        print("Cheap")
else:
    print("Invalid")
```

**Trace:**
1. items = 5, price = 10
2. Check: items > 0? YES and price < 15? YES → True and True = True
3. total = 5 * 10 = 50
4. Check: total > 30? 50 > 30? YES, True
5. Print "Total: 50"
6. Check: total < 75? 50 < 75? YES, True
7. Print "Under budget"

**Output:**
```
Total: 50
Under budget
```

---

## Key Takeaway

Tracing is the best way to understand conditional logic. Practice tracing code before running it—it builds mental models!
