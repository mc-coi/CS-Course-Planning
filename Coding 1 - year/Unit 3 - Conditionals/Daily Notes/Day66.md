# Day 66: Review — Vocabulary & Boolean Logic

**Learning Target:** I can recall and explain all Unit 3 vocabulary and Boolean logic concepts.

---

## Vocabulary Study Guide

### Core Terms

**Boolean:** Data type with two values: True or False
- Example: `is_student = True`
- Used in conditionals to make decisions

**Condition:** Expression that evaluates to True or False
- Example: `age >= 18` is a condition
- Determines which code block executes

**Comparison Operator:** Symbol that compares two values
- `==` equal to
- `!=` not equal to
- `<` less than
- `>` greater than
- `<=` less than or equal to
- `>=` greater than or equal to

**Logical Operator:** Combines Boolean expressions
- `and`: Both must be True
- `or`: At least one must be True
- `not`: Reverses Boolean value

**Compound Condition:** Multiple conditions combined with logical operators
- Example: `age >= 18 and has_license`

**Nested Conditional:** If statement inside another if statement
- Decision depends on previous decision
- Each level adds indentation

**Truthy/Falsy:** Non-Boolean values evaluated as True or False
- Falsy: 0, "", [], None, False
- Truthy: non-zero, non-empty, True

**Short-Circuit Evaluation:** Stopping evaluation when result is determined
- `and`: Stops at first False
- `or`: Stops at first True

**Input Validation:** Checking that input meets requirements
- Type checking (is it a number?)
- Range checking (is it in valid range?)
- Format checking (does it match pattern?)

**Flag Variable:** Boolean variable tracking program state
- Example: `is_logged_in = True`
- Named: `is_*`, `has_*`, `can_*`

---

## Boolean Logic Truth Tables

### AND Truth Table
```
and | T | F
----|---|--
T   | T | F
F   | F | F
```
**Both must be True**

### OR Truth Table
```
or | T | F
---|---|--
T  | T | T
F  | T | F
```
**At least one must be True**

### NOT Truth Table
```
Input | not Input
------|----------
T     | F
F     | T
```
**Reverses the value**

---

## Key Syntax

### if Statement
```python
if condition:
    # Code runs if True
```

### if/else
```python
if condition:
    # Runs if True
else:
    # Runs if False
```

### if/elif/else
```python
if condition1:
    # First option
elif condition2:
    # Second option
elif condition3:
    # Third option
else:
    # All else cases
```

### Nested if
```python
if condition1:
    if condition2:
        # Code if both True
```

### Logical Operators
```python
condition1 and condition2  # Both True
condition1 or condition2   # At least one True
not condition              # Reversed
```

### Chained Comparison
```python
1 <= x <= 10  # x between 1 and 10
```

---

## Common Patterns

### Pattern 1: Range Checking
```python
if 0 <= score <= 100:
    print("Valid")
```

### Pattern 2: Multiple Options
```python
if color == "red" or color == "blue" or color == "green":
    print("Primary color")

# Better with in
if color in ["red", "blue", "green"]:
    print("Primary color")
```

### Pattern 3: Validation
```python
if password and len(password) >= 8:
    print("Valid password")
```

### Pattern 4: Default Values
```python
name = input("Name: ") or "Guest"
```

### Pattern 5: Exclusion
```python
if not (x == 1 or x == 2):
    # x is NOT 1 or 2
```

---

## Quiz Yourself

**Evaluate these expressions:**

1. `5 > 3`
   - Answer: True

2. `"apple" > "banana"`
   - Answer: False (a comes before b)

3. `5 > 3 and 2 < 1`
   - Answer: False (5>3 is True, 2<1 is False, True and False = False)

4. `5 > 3 or 2 < 1`
   - Answer: True (at least one is True)

5. `not (5 > 3)`
   - Answer: False (not True = False)

6. `1 <= 5 <= 10`
   - Answer: True (5 is between 1 and 10)

7. `"hello" in "hello world"`
   - Answer: True (substring exists)

8. `[] or "Guest"`
   - Answer: "Guest" (empty list is falsy, so returns second value)

---

## Practice Problems

### Beginner

1. What does `==` do?
   - Compares two values for equality, returns Boolean

2. Write an if statement that prints "Adult" if age >= 18
   ```python
   if age >= 18:
       print("Adult")
   ```

3. What's wrong? `if x = 5:`
   - Should be `==` not `=` (== compares, = assigns)

### Intermediate

4. Evaluate: `age >= 18 and has_license`
   - Depends on values, but requires BOTH to be True

5. When does short-circuit evaluation help?
   - Prevents errors: `if data and data[0] > 5:` won't error on empty list

6. What's truthy? `bool("")`, `bool(0)`, `bool([])`
   - All are False (empty values are falsy)

### Challenge

7. Explain DeMorgan's Law
   - `not (A and B)` = `(not A) or (not B)`
   - `not (A or B)` = `(not A) and (not B)`

8. When should you use nested vs. logical operators?
   - Nested: hierarchical decisions
   - Operators: independent conditions that are simpler to read

---

## Study Tips

**For the Assessment:**
- Review truth tables daily
- Practice evaluating expressions
- Write out complex conditions step-by-step
- Test your code (don't just read it)
- Trace through programs line-by-line

**Memorize:**
- Truth tables for and/or/not
- Comparison operators (all 6)
- Truthy/falsy values
- When to use each conditional type

---

## Key Takeaway

Boolean logic is the foundation of all conditionals. Understand it thoroughly—it underlies everything in programming!
